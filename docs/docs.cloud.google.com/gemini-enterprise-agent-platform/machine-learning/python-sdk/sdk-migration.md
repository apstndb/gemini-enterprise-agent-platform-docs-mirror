---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration
title: 'Agent Platform SDK for Python: version 2.0.1 migration guide'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The `google-cloud-aiplatform` package includes both the AI Platform SDK for Python and the Gemini Enterprise Agent Platform Python client library. This page covers the following categories of changes in the `google-cloud-aiplatform` package:

> **Caution:** Don't install `google-cloud-aiplatform==2.0.0` . Instead, treat 2.0.1 as the version 2 boundary. If you stay on the `google-cloud-aiplatform` package, pin `google-cloud-aiplatform < 2.0.0` until you complete the migration to version 2.0.1.

  - **Generative AI modules move to the Google Gen AI SDK** : The following generative AI modules in the `vertexai` package are deprecated and migrated to the Google Gen AI SDK ( `google-genai` ):
    
      - `vertexai.generative_models`
      - `vertexai.language_models`
      - `vertexai.vision_models`
      - `vertexai.caching`
      - `vertexai.tuning`
    
    To learn how to migrate the deprecated modules to Google Gen AI SDK, see [Moving Generative AI modules to the Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#moving-generative-ai-modules-to-the-google-gen-ai-sdk) .

  - **Agent surface restructure:** The following changes were made to the `agentplatform` modules of `google-cloud-aiplatform` :
    
      - Renames
      - Promotions to top-level
      - Removal of the global initializer
    
    To learn how to migrate to the new SDK structure, see [Agent Platform SDK restructure](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#agent-platform-sdk-restructure) .

  - **Decoupling of `agentplatform`** : `google-cloud-agentplatform` is now a standalone lightweight distribution and the recommended install for agent workloads. If you only build agents, install `google-cloud-agentplatform` , which doesn't contain generative AI modules. `agentplatform` modules cover the common integrations such as `[adk]` , `[a2a]` , `[agent_engines]` , `[langchain]` , `[ag2]` , `[llama_index]` , `[evaluation]` , `[bigquery]` , `[live]` , and `[all]` .

### What's not affected

The classic machine learning surface (datasets, training, models, prediction, tracking, pipelines) is fully supported, unaffected by version 2.0.1 changes, and has no equivalent in the Google Gen AI SDK. You can still access evaluation, Agent Runtime, prompts, and skills by installing `google-cloud-aiplatform` . Both `google-cloud-aiplatform` and `google-genai` coexist in one environment, and `google-genai` is now a hard dependency of `google-cloud-aiplatform` :

    import agentplatform
    
    client = agentplatform.Client(project="my-project", location="global")
    # client.evals                  client.prompts
    # client.prompt_optimizer client.datasets           client.skills

`vertexai.batch_prediction` is not deprecated, but a Google Gen AI SDK equivalent exists and is the recommended tool.

## Moving Generative AI modules to the Google Gen AI SDK

If you use the generative AI modules in the `google-cloud-aiplatform` package, use the following recommendations to migrate to the Google Gen AI SDK ( `google-genai` ):

1.  Set `google-cloud-aiplatform < 2.0.0` so unrelated dependency bumps cannot remove the modules underneath you.

2.  Search for the deprecated modules in your code:
    
      - `vertexai.generative_models`
      - `vertexai.language_models`
      - `vertexai.vision_models`
      - `vertexai.caching`
      - `vertexai.tuning`
    
    If you import any of the affected Python modules, you receive the following deprecation warning:
    
        UserWarning: This feature is deprecated as of June 24, 2025 and will be removed on
        June 24, 2026. For details, see
        https://cloud.google.com/vertex-ai/generative-ai/docs/deprecations/genai-vertexai-sdk.
    
    Run your test suite with `-W error::UserWarning` to catch imports you missed.

3.  Replace `vertexai.init(...)` with an explicit `genai.Client(enterprise=True, project=..., location=...)` . Keep `vertexai.init()` if you also use the classic machine learning surface.
    
    ### Before
    
        # pip install google-cloud-aiplatform
        
        import vertexai
        from vertexai.generative_models import GenerativeModel
        
        vertexai.init(project="my-project", location="us-central1")
        
        # Model identity and config are bound at construction time.
        model = GenerativeModel("gemini-2.5-flash")
    
    ### After
    
        # pip install google-genai
        
        from google import genai
        from google.genai import types
        
        client = genai.Client(
            enterprise=True,
            project="my-project",
            location="global",
        )
    
    Or configure from the environment:
    
        export GOOGLE_GENAI_USE_ENTERPRISE=true
        export GOOGLE_CLOUD_PROJECT=my-project
        export GOOGLE_CLOUD_LOCATION=global
    
        from google import genai
        
        client = genai.Client()
    
    Key considerations:
    
      - Global state becomes an explicit client. `vertexai.init()` configured the whole process; `genai.Client()` is an object you pass around. With `genai.Client()` , you can use two projects or regions in one process.
      - `enterprise=True` is required. If you omit it, the client silently targets the Gemini Developer API, which then fails on application default credentials or demands an API key.
      - The model name moves from construction to every call. There is no bind-once model object. `model=` is a required keyword argument on each `client.models.*` call.
      - Authentication is unchanged. Application default credentials still apply, and `credentials=` accepts a `google.auth.credentials.Credentials` in both SDKs.
      - `vertexai.init()` also carried non-generative settings such as `staging_bucket` , `experiment` , `encryption_spec_key_name` , `service_account` , `network` . `genai.Client` has no equivalent for them.
      - The newer `enterprise=True` spelling is accepted as of `google-genai` 2.20.0, but the older version `vertexai=True` works on every release and is the safer choice.

4.  Audit your code for silent changes where behavior diverges without an error. These compile and run but change meaning.
    
    | Behavior                                       | Before                                   | After                                                              |
    | ---------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------ |
    | `response.text` on a blocked or empty response | Raises `ValueError`                      | Returns `None`                                                     |
    | `response.text` with multiple candidates       | Raises `ValueError`                      | Logs a warning, returns the first candidate                        |
    | Client targeting                               | `vertexai.init()` implied Agent Platform | Omitting `vertexai=True` silently targets the Gemini Developer API |
    | Embeddings `auto_truncate`                     | Defaults to `True`                       | Unset; server default applies                                      |
    | A Python function passed as a tool             | Not supported                            | Executed automatically by the SDK                                  |
    | `system_instruction`                           | Bound once on the model                  | Must be passed on every call                                       |
    

    The `response.text` change is the one to search for first. Every `try` / `except ValueError` wrapped around `.text` becomes dead code, and every unguarded `.text` can now yield `None` where a `str` was previously returned:
    
        if response.text is None:
            print(
                "blocked or empty:",
                response.prompt_feedback,
                response.candidates[0].finish_reason if response.candidates else None,
            )

5.  Keep `google-cloud-aiplatform` installed if you use evaluation, Agent Runtime, prompts, datasets, skills, and the whole classic machine learning surface.

6.  [Change calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#task-based-call-changes) to the new versions. Start with mechanical renames, then continue with `config=` consolidation.

### Task-based call changes

See the changed calls based on task:

  - [Text generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#text-generation)
  - [Streaming generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#streaming-generation)
  - [Asynchronous generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#asynchronous-generation)
  - [Chat sessions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#chat-sessions)
  - [Configuration, safety settings, and system instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#configuration-safety-settings-and-system-instructions)
  - [Multimodal input](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#multimodal-input)
  - [Function calling and grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#function-calling-and-grounding)
  - [Embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#embeddings)
  - [Token counting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#token-counting)
  - [Context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#context-caching)
  - [Batch prediction and tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/sdk-migration#batch-prediction-and-tuning)

#### Text generation

For text generation tasks, all arguments are keyword-only. Positional calls raise `TypeError` .

### Before

    model = GenerativeModel("gemini-2.5-flash")
    
    response = model.generate_content("Why is the sky blue?")
    print(response.text)

### After

    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents="Why is the sky blue?",
    )
    print(response.text)

#### Streaming generation

For streaming generation tasks, the `stream=True` flag is removed. Streaming is now a separate method returning `Iterator[types.GenerateContentResponse]` . Use `if chunk.text:` to check before accessing the text, because each chunk is a full response object and its `.text` attribute can sometimes be `None` .

### Before

    stream = model.generate_content("Tell me a story in 300 words.", stream=True)
    for chunk in stream:
        print(chunk.text, end="")

### After

    for chunk in client.models.generate_content_stream(
        model="gemini-3.5-flash",
        contents="Tell me a story in 300 words.",
    ):
        if chunk.text:
            print(chunk.text, end="")

#### Asynchronous generation

For asynchronous generation tasks, the `_async` method-name suffix was removed. Every asynchronous call lives under `client.aio.<module>` with the same method name as its synchronous counterpart. Close the client with `await client.aio.aclose()` , or use `async with genai.Client(...).aio as aclient:` .

### Before

    response = await model.generate_content_async("Why is the sky blue?")
    
    async_stream = await model.generate_content_async("Why is the sky blue?", stream=True)
    async for chunk in async_stream:
        print(chunk.text, end="")

### After

    response = await client.aio.models.generate_content(
        model="gemini-3.5-flash",
        contents="Why is the sky blue?",
    )
    
    # Note the `await` in front of the async iterator.
    async for chunk in await client.aio.models.generate_content_stream(
        model="gemini-3.5-flash",
        contents="Tell me a story in 300 words.",
    ):
        print(chunk.text, end="")

#### Chat sessions

Note the following changes for chat sessions tasks:

  - Chats are created from the client, not from a model object.

  - `chat.history` (property) becomes `chat.get_history()` (method). The new method takes `curated: bool = False` . Passing `True` returns only the kept turns, which has no old equivalent.

  - `client.aio.chats.create(...)` returns an `AsyncChat` directly. Only `send_message` and `send_message_stream` are awaited.

  - Per-turn options collapse into one argument: `send_message(message, config=types.GenerateContentConfig(...))` . The first parameter is also renamed from `content` to `message` .

  - `start_chat(response_validation=False)` is a new method with no equivalent in previous versions.

### Before

    model = GenerativeModel("gemini-2.5-flash")
    chat = model.start_chat()
    
    print(chat.send_message("Tell me a story").text)
    
    for content in chat.history:
        print(content.role, content.parts)

### After

    chat = client.chats.create(model="gemini-3.5-flash")
    
    print(chat.send_message("Tell me a story").text)
    
    for content in chat.get_history():
        print(content.role, content.parts)

#### Configuration, safety settings, and system instructions

Note the following changes for configuration, safety settings, and system instructions tasks:

  - The following arguments are collapsed into one `config=` as fields of `GenerateContentConfig` :
    
      - `generation_config`
      - `safety_settings`
      - `tools`
      - `tool_config`
      - `labels`
      - `system_instruction`
    
    A plain `dict` works anywhere a config type works.

  - `system_instruction` moves from the model constructor to per-call config. In the earlier SDK version, `system_instruction` was set once when building `GenerativeModel` . Now `system_instruction` must be passed on every call or included in `client.chats.create(config=...)` .

  - Safety settings change from a `dict` to a `list` . For example, `[types.SafetySetting(category=c, threshold=t) for c, t in old_dict.items()]` .

  - Enums are accepted as plain strings and coerced.

  - Scalar field names are otherwise unchanged: `temperature` , `top_p` , `top_k` , `candidate_count` , `max_output_tokens` , `stop_sequences` , `presence_penalty` , `frequency_penalty` , `seed` , `response_mime_type` , `response_schema` , `response_logprobs` , `logprobs` .

  - New fields with no old equivalent include `thinking_config` , `cached_content` , `automatic_function_calling` , `http_options` , `media_resolution` , and `speech_config` .

### Before

    from vertexai.generative_models import (
        GenerativeModel, GenerationConfig, HarmCategory, HarmBlockThreshold,
    )
    
    model = GenerativeModel(
        "gemini-2.5-flash",
        system_instruction=["Talk like a pirate.", "Don't use rude words."],
    )
    
    response = model.generate_content(
        contents="Why is the sky blue?",
        generation_config=GenerationConfig(temperature=0, top_p=0.95, max_output_tokens=100),
        safety_settings={
            HarmCategory.HARM_CATEGORY_HATE_SPEECH: HarmBlockThreshold.BLOCK_MEDIUM_AND_ABOVE,
            HarmCategory.HARM_CATEGORY_DANGEROUS_CONTENT: HarmBlockThreshold.BLOCK_ONLY_HIGH,
        },
    )

### After

    from google.genai import types
    
    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents="Why is the sky blue?",
        config=types.GenerateContentConfig(
          system_instruction="Talk like a pirate. Don't use rude words.",
          temperature=0,
          top_p=0.95,
          max_output_tokens=100,
          safety_settings=[
              types.SafetySetting(
                  category="HARM_CATEGORY_HATE_SPEECH",
                  threshold="BLOCK_MEDIUM_AND_ABOVE",
              ),
              types.SafetySetting(
                  category=types.HarmCategory.HARM_CATEGORY_DANGEROUS_CONTENT,
                  threshold=types.HarmBlockThreshold.BLOCK_ONLY_HIGH,
              ),
          ],
        ),
    )

#### Multimodal input

Note the following changes for multimodal input tasks:

| Old                                                  | New                                                                      |
| ---------------------------------------------------- | ------------------------------------------------------------------------ |
| `Part.from_uri(uri, mime_type)` , positional allowed | `Part.from_uri(file_uri=, mime_type=)` , keyword-only, parameter renamed |
| `Part.from_data(data, mime_type)`                    | `Part.from_bytes(data=, mime_type=)` , method renamed                    |
| `Part.from_text(text)`                               | `Part.from_text(text=)` , keyword-only                                   |
| `Image.load_from_file(path)`                         | No equivalent; open the file and use `Part.from_bytes`                   |

  - `mime_type` is optional in `types.Part.from_uri()` (inferred server-side), but remains required in `types.Part.from_bytes()` .

  - `client.files.upload(...)` is supported only on the Gemini Developer API. For Agent Platform workloads, continue passing Cloud Storage URIs using `from_uri` or inline bytes using `from_bytes` .

### Before

    from vertexai.generative_models import GenerativeModel, Part, Image
    
    image = Image.load_from_file("image.jpg")
    print(model.generate_content(["What is shown in this image?", image]).text)
    
    image_part = Part.from_uri(
        "gs://cloud-samples-data/generative-ai/image/scones.jpg",
        mime_type="image/jpeg",
    )

### After

    from google.genai import types
    
    # Image.load_from_file has no equivalent: read the bytes yourself.
    with open("image.jpg", "rb") as f:
        image = types.Part.from_bytes(data=f.read(), mime_type="image/jpeg")
    
    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents=["What is shown in this image?", image],
    )
    
    image_part = types.Part.from_uri(
        file_uri="gs://cloud-samples-data/generative-ai/image/scones.jpg",
        mime_type="image/jpeg",
    )

#### Function calling and grounding

Note the following changes for function calling and grounding tasks:

  - Tools move into `config=` . There is no `tools=` argument on the call or on a model object.

  - `Tool.from_google_search_retrieval(grounding.GoogleSearchRetrieval())` becomes `types.Tool(google_search=types.GoogleSearch())` . A factory method becomes a plain field. `types.Tool` also has a separate `google_search_retrieval` field.

  - `response.function_calls` is the idiomatic accessor and does not fail when part zero happens to be text. The old traversal still works.

  - Raw JSON Schema is specified in `parameters_json_schema` . A typed `types.Schema` is specified in `parameters` .

  - You can now pass a Python function as a tool, and automatic function calling is on by default when you pass the function. If you port a manual tool loop and pass a function object, the SDK starts executing your code. Disable the default automatic function calling with `automatic_function_calling=types.AutomaticFunctionCallingConfig(disable=True)` .

  - The following new tool types have no equivalent in previous versions: `code_execution` , `url_context` , `google_maps` , `computer_use` , `file_search` , `enterprise_web_search` , `mcp_servers` .

### Before

    from vertexai.generative_models import GenerativeModel, FunctionDeclaration, Tool, grounding
    
    weather_tool = Tool(function_declarations=[
        FunctionDeclaration(
            name="get_current_weather",
            description="Get the current weather in a given location",
            parameters={
                "type": "object",
                "properties": {"location": {"type": "string"}},
                "required": ["location"],
            },
        )
    ])
    
    model = GenerativeModel("gemini-2.5-flash", tools=[weather_tool])
    response = model.generate_content("What is the weather in Boston?")
    call = response.candidates[0].content.parts[0].function_call
    
    # Grounding
    search_tool = Tool.from_google_search_retrieval(grounding.GoogleSearchRetrieval())

### After

    from google.genai import types
    
    weather_tool = types.Tool(function_declarations=[
        types.FunctionDeclaration(
            name="get_current_weather",
            description="Get the current weather in a given location",
            parameters_json_schema={
                "type": "object",
                "properties": {"location": {"type": "string"}},
                "required": ["location"],
            },
        )
    ])
    
    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents="What is the weather in Boston?",
        config=types.GenerateContentConfig(tools=[weather_tool]),
    )
    call = response.function_calls[0]
    
    # Grounding
    search_tool = types.Tool(google_search=types.GoogleSearch())

#### Embeddings

Note the following changes for embedding tasks:

  - `TextEmbeddingInput` is removed. `task_type` and `title` are now per-request, so mixed-task batches must be split into multiple calls.

  - The return type changed from a direct list to a response object. `get_embeddings()` directly returned a `list[TextEmbedding]` , so callers indexed the list directly ( `embeddings[0].values` ). In the new version, `embed_content()` returns an `EmbedContentResponse` object containing an `.embeddings` list, requiring you to access `response.embeddings[0].values` . The individual embedding fields ( `.values` and `.statistics` ) retain their original names.

  - `auto_truncate` no longer defaults to `True` . The new field defaults to `unset` . If you rely on silent truncation of over-long inputs, set `auto_truncate` explicitly.

### Before

    from vertexai.language_models import TextEmbeddingModel, TextEmbeddingInput
    
    model = TextEmbeddingModel.from_pretrained("gemini-embedding-001")
    
    text_input = TextEmbeddingInput(
        text="How do I get a driver's license?",
        task_type="RETRIEVAL_DOCUMENT",   # per input
        title="Driver's License",         # per input
    )
    
    embeddings = model.get_embeddings([text_input], output_dimensionality=3072, auto_truncate=True)
    print(embeddings[0].values)

### After

    from google.genai import types
    
    response = client.models.embed_content(
        model="gemini-embedding-2",
        contents="How do I get a driver's license?",
        config=types.EmbedContentConfig(
            task_type="RETRIEVAL_DOCUMENT",   # now per request
            title="Driver's License",         # now per request
            output_dimensionality=3072,
            auto_truncate=True,
        ),
    )
    print(response.embeddings[0].values)

#### Token counting

Note the following changes for token counting tasks:

  - `total_billable_characters` is removed and has no replacement. Any cost estimation keyed on `total_billable_characters` must be reworked (for example against `total_tokens` or `response.usage_metadata` ) from a generation call.

  - `client.models.compute_tokens(...)` was added for token IDs and string pieces.

  - Offline counting was added through `google.genai.local_tokenizer.LocalTokenizer` .

### Before

    model = GenerativeModel("gemini-2.5-flash")
    
    response = model.count_tokens(["Why is the sky blue?"])
    print(response.total_tokens)
    print(response.total_billable_characters)

### After

    response = client.models.count_tokens(
        model="gemini-3.5-flash",
        contents=["Why is the sky blue?"],
    )
    print(response.total_tokens)
    print(response.cached_content_token_count)

#### Context caching

Note the following changes for context caching tasks:

  - `ttl` changes type from `datetime.timedelta` to a duration string such as `"86400s"` .

  - Resource-object methods become client-module calls.

  - `update` returns a new object rather than mutating in place.

### Before

    import datetime
    from vertexai.caching import CachedContent
    
    cache = CachedContent.create(
        model_name="gemini-2.5-flash",
        system_instruction="Please answer my question formally",
        contents=contents,
        ttl=datetime.timedelta(days=1),
    )
    cache.update(ttl=datetime.timedelta(days=2))
    cache.delete()

### After

    from google.genai import types
    
    cache = client.caches.create(
        model="gemini-3.5-flash",
        config=types.CreateCachedContentConfig(
            contents=contents,
            system_instruction="Please answer my question formally",
            ttl="86400s",
        ),
    )
    cache = client.caches.update(
        name=cache.name, config=types.UpdateCachedContentConfig(ttl="172800s")
    )
    client.caches.delete(name=cache.name)

#### Batch prediction and tuning

Note the following changes for batch prediction and tuning tasks:

  - Polling is rebind-based, not in-place. There is no `job.refresh()` and no `job.has_ended` . Fetch a new object from `client.batches.get(name=...)` and compare `job.state` against the `JOB_STATE_*` strings.

  - Batch renames: `source_model` to `model` , `input_dataset` to `src` , `output_uri_prefix` to `config.dest` , `job_display_name` to `config.display_name` .

  - Batch machine-shape controls are removed and have no equivalent in the new SDK version. `machine_type` , `accelerator_type` , `accelerator_count` , `starting_replica_count` , and `max_replica_count` are no longer fields of `CreateBatchJobConfig` .

  - The following methods were renamed:
    
      - `sft.train` to `client.tunings.tune`
      - `source_model` to `base_model`
      - `train_dataset` to `training_dataset`
      - `epochs` to `epoch_count`

  - Tuning datasets are wrapped. A bare `"gs://..."` string becomes `types.TuningDataset(gcs_uri=...)` .

  - `adapter_size` changes type from an `int` to an enum string such as `"ADAPTER_SIZE_FOUR"` .

### Before

    from vertexai.batch_prediction import BatchPredictionJob
    from vertexai.tuning import sft
    
    job = BatchPredictionJob.submit(
        source_model="gemini-2.5-flash",
        input_dataset="bq://my-project.my-dataset.my-table",
        output_uri_prefix="bq://my-project.my-dataset.output",
    )
    while not job.has_ended:
        job.refresh()
    
    tuning_job = sft.train(
        source_model="gemini-2.5-flash",
        train_dataset="gs://bucket/train.jsonl",
        epochs=1,
        adapter_size=4,
    )

### After

    from google.genai import types
    
    job = client.batches.create(
        model="gemini-3.5-flash",
        src="bq://my-project.my-dataset.my-table",
        config=types.CreateBatchJobConfig(dest="bq://my-project.my-dataset.output"),
    )
    completed = {"JOB_STATE_SUCCEEDED", "JOB_STATE_FAILED", "JOB_STATE_CANCELLED", "JOB_STATE_PAUSED"}
    while job.state not in completed:
        job = client.batches.get(name=job.name)
    
    tuning_job = client.tunings.tune(
        base_model="gemini-3.5-flash",
        training_dataset=types.TuningDataset(gcs_uri="gs://bucket/train.jsonl"),
        config=types.CreateTuningJobConfig(
            epoch_count=1,
            adapter_size="ADAPTER_SIZE_FOUR",
        ),
    )

## Agent Platform SDK restructure

If you use the `agentplatform` modules of `google-cloud-aiplatform` , use the following recommendations to migrate to the new SDK structure:

1.  `google-cloud-agentplatform` is now a standalone lightweight distribution and the recommended install for agent workloads. If you don't need the classic machine learning surface, switch your install from `pip install google-cloud-aiplatform` to `pip install google-cloud-agentplatform` .

2.  Use the following table to update imports and attribute paths:
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Previous</th>
    <th>New</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code dir="ltr" translate="no">client.agent_engines.create</code></td>
    <td><code dir="ltr" translate="no">client.runtimes.create</code> (Deploy an Agent Runtime on Gemini Enterprise Agent Platform instance, which provides built-in Sessions, Sandbox code execution, and context memory configuration)<br />
    <code dir="ltr" translate="no">client.memory_banks.create</code> (Create standalone Memory Bank resources for persisting, managing, and retrieving memories across interactions)</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">client.agent_engines.sandboxes</code></td>
    <td><code dir="ltr" translate="no">client.sandboxes</code></td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">client.agent_engines.sandboxes.snapshots</code></td>
    <td><code dir="ltr" translate="no">client.sandboxes.snapshots</code></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">client.agent_engines.sandboxes.templates</code></td>
    <td><code dir="ltr" translate="no">client.sandboxes.templates</code></td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">client.agent_engines.sessions</code></td>
    <td><code dir="ltr" translate="no">client.sessions</code></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">client.agent_engines.sessions.events</code></td>
    <td><code dir="ltr" translate="no">client.sessions.events</code></td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">client.agent_engines.runtimes.revisions</code></td>
    <td><code dir="ltr" translate="no">client.runtimes.revisions</code></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">client.agent_engines.memories</code></td>
    <td><code dir="ltr" translate="no">client.memory_banks.memories</code></td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">agentplatform.agent_engines.templates</code></td>
    <td><code dir="ltr" translate="no">agentplatform.frameworks</code></td>
    </tr>
    </tbody>
    </table>

3.  The global initializer is removed, and agent frameworks no longer read project and location from `aiplatform.init()` or `vertexai.init()` state. Replace initializer-derived configuration with environment variables for anything running inside an agent framework. Code that relies on the initializer to configure deployed agents breaks silently rather than raising an error.

4.  Update `evals.run_inference(agent=...)` call sites to pass `types.Runtime` , since the SDK no longer accepts `types.AgentEngine` .

5.  Make the following changes:
    
      - `vertexai.Client` to `agentplatform.Client`
      - `vertexai.rag` to `agentplatform.Client().rag`
    
    `vertexai.Client` emits a `FutureWarning` on first instantiation:
    
        The vertexai.Client class is deprecated. Please use agentplatform.Client instead.
    
    `vertexai.rag` emits a `UserWarning` at module import time, not on call. Migrate to the following:
    
        import agentplatform
        
        client = agentplatform.Client(project="your-project", location="global")
        client.rag.create_corpus(...)

6.  Update error handling around `AdkApp` and session calls. Synchronous session methods and streaming agent runs now surface the underlying API error. Callers catching a generic wrapped error no longer match. Replace catches for generic library wrapper exceptions with `google.api_core.exceptions.GoogleAPICallError` (or specific status errors like `ResourceExhausted` and `NotFound` ).

7.  Update client callers or middleware to include the user's OAuth access token on each request, as tokens are now ephemeral and not persisted with session state. Ensure token refresh is managed client-side.

8.  Note that the `a2a.tasks` module was removed without a replacement.
