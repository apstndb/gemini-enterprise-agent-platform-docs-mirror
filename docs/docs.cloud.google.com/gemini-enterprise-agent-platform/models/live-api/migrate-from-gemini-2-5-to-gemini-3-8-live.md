---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/migrate-from-gemini-2-5-to-gemini-3-8-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/migrate-from-gemini-2-5-to-gemini-3-8-live
title: Migrate from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live
description: Learn how to migrate from Gemini 2.5 Flash with Live API to Gemini 3.8 Live.
data_source: docs.cloud.google.com
---

This document describes changes required when migrating from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live.

## Function call changes

The Gemini 2.5 Flash Live API Native Audio server allows asynchronous tool calls. By contrast, Gemini 3.8 Live supports asynchronous function calling with the following behavior changes:

  - Gemini 3.8 Live supports blocking function calls when the function declaration declares `behavior=BLOCKING` in the setup. If a new input is received during the blocking function call's execution, then the Live API server cancels the current function call.

  - The `scheduling=interrupt` option to `FunctionResponse` changed behavior:
    
    | `FunctionResponse` scheduling | Who is speaking | Gemini 2.5 Flash Live API Native Audio                                    | Gemini 3.8 Live                                                           |
    | ----------------------------- | --------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
    | interrupt                     | model           | Stops the active model responding immediately; plays the tool's response. | Stops the active model responding immediately; plays the tool's response. |
    | interrupt                     | user            | Interrupts immediately; plays the tool's response over the user.          | Waits for the user to finish before playing the tool's response.          |
    

## Mitigating redundant sweeps and function-call retries

Gemini 3.8 Live sometimes makes redundant back-to-back function calls within a single turn when a tool returns no results. This can include repeating varied parameters, sweeping two to five times, before responding. The behavior increases time-to-first-audio (TTFA) and produces inaccurate fallback speech.

The redundant back-to-back function calls are caused by Gemini 3.8 Live attempting to resolve queries. When a tool returns an uninformative or empty response, such as `{"results": [], "total_available": 0}` or `None` , the model can't distinguish between "permanently exhausted", "query window too narrow" or "invalid argument". The model tries widening or varying the query in an attempt to improve results, and begins sweeping.

Apply the following complementary practices:

  - **Return informative function responses** : Every tool response must contain information about the error or results, to guide the Gemini 3.8 Live model for how to proceed.
    
    The following table describes the cases, how the model should respond, and required payload example to assist the model:
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Case</th>
    <th>What the Model Should Do</th>
    <th>Required Payload Content</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Valid query that returns no results. Retrying won't help.</td>
    <td>Stop searching, inform the user, and offer alternatives.</td>
    <td><code dir="ltr" translate="no">status: 'no_results'</code> ,<br />
    <code dir="ltr" translate="no">retryable: false</code> ,<br />
    and a clear explanatory natural-language message.</td>
    </tr>
    <tr class="even">
    <td>Invalid or non-existent argument (for example, "wrong provider").</td>
    <td>Stop searching, and ask user to clarify or confirm.</td>
    <td><code dir="ltr" translate="no">status: 'invalid_argument'</code> ,<br />
    <code dir="ltr" translate="no">reason_code</code> ,<br />
    <code dir="ltr" translate="no">retryable: false</code> , and<br />
    <code dir="ltr" translate="no">valid_options</code> list</td>
    </tr>
    <tr class="odd">
    <td>Valid query that has an empty window. A wider query genuinely helps.</td>
    <td>Perform one reasonable retry.</td>
    <td><code dir="ltr" translate="no">status: 'no_results_in_range'</code> ,<br />
    <code dir="ltr" translate="no">retryable: true</code> , and<br />
    <code dir="ltr" translate="no">retry_hint</code></td>
    </tr>
    </tbody>
    </table>
    
    The following example demonstrates a payload example where `search_appointment` is called but all of the potential dates are unavailable. The user expects to try on a vendor instead of sweeping the dates:
    
        def search_appointment(vendor: str, date: Datetime):
        
        # BEFORE (Invites Sweeping):
        {
          "results": [],
          "total_available": 0
        }
        
        # AFTER - Exhausted / Dead End (Stops Sweeping):
        {
          "results": [],
          "status": "no_availability",
          "retryable": false,
          "message": "No appointments are available for this provider for the foreseeable future. Searching other dates will not surface anything; openings only come from cancellations.",
          "suggested_next_step": "offer_waitlist_or_a_different_provider"
        }
        
        # AFTER - Invalid Argument (Prompts User Clarification):
        {
          "results": [],
          "status": "invalid_argument",
          "reason": "no_such_provider",
          "retryable": false,
          "message": "There is no provider named 'Mr. Johnson'. Ask the caller to confirm the name.",
          "valid_options": ["Dr. Johnson", "Dr. Chen"]
        }
    
    The following example demonstrates handling when `check_user_account` returns no exact matches. The expected result is to modify the search query or transfer control back to the user instead of retrying:
    
        def check_user_account(user_name: str, phone_suffix: str):...
        
        # Checked user account but not existing
        # BEFORE: insufficient error information
        {
         "found": false,
         "matches": []
        }
        
        # AFTER: providing sufficient information to the LiveAPI to avoid further retries because the retries have been exhausted.
        {
         "status": "EXHAUSTED",
         "retryable": false,
         "search_criteria": {
           "name": "Alex Rivera",
           "phone_suffix": "4921"
         },
         "search_scope": "Checked active orders, archived accounts, and guest checkouts across all regions.",
         "guidance": "Exhaustive search completed with 0 matches. Do NOT retry with parameter substrings or variations. Inform the user that no account was found matching those details, and ask if they have an Order ID or billing email."
        }

  - **System instructions retry policy** : Complement informative responses with an explicit constraint in the system instruction:
    
        "When a tool returns no results, tell the user the result before calling the
        tool again. If a call fails for a reason fundamental to the arguments (for
        example, the entity does not exist), do not silently retry with variations;
        ask the user to clarify or confirm. You may broaden a query once when a
        result set is simply empty. Do not run repeated searches with different
        parameters on your own initiative. Hard cap: Never issue more than two
        consecutive function calls without saying something back to the user."

## Session history exchange

In Gemini 2.5 Flash Live API Native Audio, `send_client_content` is used to set up history seeding prior to the first turn, and to add extra history during mid-session.

In Gemini 3.8 Live, if you want to use the `send_client_content` method to set up history seeding, in the `HistoryConfig` section of the setup message, set `initial_history_in_client_content=True` . After receiving `setup_complete` . You can then call `send_client_content` repeatedly to build history until the last message where `turn_complete=True` is set.

## Model behavior differences

The following table describes model behavior differences for audio, multimodel, and output between Gemini 2.5 Flash Live API Native Audio and Gemini 3.8 Live:

| Feature                     | Gemini 2.5 Flash Live API Native Audio                | Gemini 3.8 Live                                                                                       |
| --------------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Affective dialog            | Supported through the `enable_affective_dialog` flag. | Always enabled by default.                                                                            |
| Proactive audio             | Supported through the `proactivity` flag.             | Always enabled by default.                                                                            |
| Image or video frame tokens | Lower default per-frame budget.                       | `media_resolution` is always supported when passing image frames. Lets you balance cost and accuracy. |
| Transcription and content   | Stable baseline transcription.                        | You can add `custom_vocabulary` to provide biasing to your domain-specific words to improve accuracy. |

The following Python code demonstrates setting `media_resolution` and `custom_vocabulary` :

    # Example: Setting media_resolution for image frames in Gemini 3.8 Live
    from google import genai
    from google.genai import types
    
    client = genai.Client()
    
    config = types.LiveConnectConfig(
        response_modalities=["AUDIO"],
        media_resolution=types.MediaResolution.MEDIA_RESOLUTION_LOW,  # or MEDIA_RESOLUTION_LOW or MEDIA_RESOLUTION_MEDIUM
    )
    
    async with client.aio.live.connect(
        model="gemini-3.8-live",
        config=config,
    ) as session:
        # Send image frames with the configured resolution budget
        ...
    
    
    # Example: Setting custom_vocabulary for domain-specific word biasing in Gemini 3.8 Live
    from google import genai
    from google.genai import types
    
    client = genai.Client()
    
    config = types.LiveConnectConfig(
        response_modalities=["AUDIO"],
        input_audio_transcription=types.AudioTranscriptionConfig(
            custom_vocabulary=["Gemini", "MagicWord", "Lagrangian"],
        ),
    )
    
    async with client.aio.live.connect(
        model="gemini-3.8-live",
        config=config,
    ) as session:
        ...

## Third-party framework compatibility

The following sections describe how third-party frameworks work with Gemini 3.8 Live:

### LiveKit

LiveKit's Google plugin RealtimeModel supports Gemini 3.8 Live, but the following settings are not supported in LiveKit's Google plugin:

  - `thinking_level`
  - `enable_affective_dialog`
  - `proactivity`

We recommend that you use extra caution when using LiveKit's Google plugin, because it requires careful adaptation to work with Gemini 3.8 Live.

### Pipecat

Pipecat supports Gemini 3.8 Live, with the following changes:

  - Thinking Configuration: remove thinking level as it isn't supported by Gemini 3.8 Live.

  - Pipecat connects Agent Platform endpoints using the `GoogleVertexLLMService` over the `GeminiLiveLLMService` connector.

## Wire-level token usage telemetry

Every server turn returns a `usage_metadata` frame. This is consistent across Gemini 2.5 Flash Live API Native Audio and Gemini 3.8 Live. The usage metadata is more categorized, such as cached token, tool-use token, tokens in different modalities, and so forth.

## Known model limitations and mitigations

For information about known limitations and mitigations when developing applications with Gemini 3.8 Live, see [Known limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/troubleshooting#known-limitations) .

## Migration checklist

The following is a client migration checklist that you can use when migrating from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live:

  - Function calling:
    
      - **Informative tool responses** : Refactor all tool handlers to return explicit status codes, retryable flags, and natural-language explanations. Never return bare `None` or empty `{}` .
    
      - **System instruction policy** : Add explicit constraints prohibiting silent tool retries, requiring user confirmation on argument failures, and capping consecutive tool calls.
    
      - **Tool call ID matching** : Ensure `FunctionResponse` passes `id=fc.id` on every tool reply.
    
      - **Function scheduling behavior change** : When the user is speaking, the `scheduling=interrupt` downgrades to `scheduling=when_idle` to provide a smoother user experience.

  - **Session: restrict `send_client_content`** : Use `send_client_content` to set the initial history by providing a sensible `HistoryConfig` .

  - **Thinking: purge prompt-level thinking hacks** : To prevent dropped audio, remove all prompt text that attempts to enforce step-by-step thinking schemas or token limits.
