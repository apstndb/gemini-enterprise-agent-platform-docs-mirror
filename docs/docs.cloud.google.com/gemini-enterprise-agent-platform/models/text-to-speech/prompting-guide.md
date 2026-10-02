---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/prompting-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/prompting-guide
title: Gemini TTS prompting guide
description: Learn how to direct style, pacing, emphasis, vocal sounds, and multi-speaker dialogue with the Gemini 3.8 TTS models on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

This page describes best practices for writing prompts when using [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) and [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) .

For request syntax and code samples, see the [Gemini TTS overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .

The Gemini 3.8 TTS models treat the `text` field as a verbatim transcript. Sustained, turn-level direction goes in `speech_metadata` , and point-in-time vocal events go inline in the transcript. The following request combines a turn-level `style` with inline vocal tags and pauses:

    {
      "contents": [{
        "role": "user",
        "parts": [{
          "text": "Wait... <short pause> did you hear that? <gasp> Someone's at the door.",
          "speechMetadata": {"style": "whispered, nervous"}
        }]
      }],
      "generationConfig": {
        "responseModalities": ["AUDIO"],
        "speechConfig": {"voiceConfig": {"voice": "Kore"}}
      }
    }

## Style field versus inline tags

Split your performance instructions by scope:

  - **Turn-level delivery ( `speech_metadata.style` )** : Put sustained delivery attributes, such as emotion, prosody, overall pace, or delivery style (like `"whispering"` , `"out of breath"` , `"muttering"` , or `"sarcastic"` ), into the `style` field of `speech_metadata` . To create a stable character and performance across turns, design the persona upfront in [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) and use `style` only for optional turn-level tweaks.
  - **Point-in-time events (inline tags)** : Put momentary non-speech vocal bursts, breaths, or pauses inline inside the transcript using angle brackets ( `<cough>` , `<breath>` , `<sigh>` , `<short pause>` ). Use angle brackets ( `<...>` ) for highest audio quality, and stick to human vocalizations rather than non-vocal sound effects.

| Scope                                         | Where to place               | Examples                                                                                 |
| :-------------------------------------------- | :--------------------------- | :--------------------------------------------------------------------------------------- |
| **Turn-level** (sustained across the turn)    | `speech_metadata.style`      | `"angry tone"` , `"speaking rapidly"` , `"out of breath"` , `"whispers"` , `"sarcastic"` |
| **Point-in-time** (occurs at a specific word) | Inline in `text` ( `<...>` ) | `"<cough> Thank you all for coming tonight! <throat-clearing> As I was saying..."`       |

## Pacing and pauses

You can control rhythm and silence at three levels:

  - **Punctuation and ellipses** : Use commas, dashes ( `--` ), and ellipses ( `...` ) for natural hesitation.
  - **Inline pause tags** : Insert `<short pause>` or `<long pause>` where the speaker should pause. For example: `"Hold on, let me think... <short pause> Alright, I've got it."`
  - **Turn-level pace** : Set `"style": "speaking rapidly"` or `"style": "speaking slowly"` in `speech_metadata` to control the speaking rate for the whole turn.

## Prosody and pitch

Use `speech_metadata.style` to control prosody, pitch, and inflection across a turn. For example, `"style": "high pitch, cheerful and excited inflection"` or `"style": "monotone and flat"` . If the emotion shifts mid-dialogue, split the script into separate turns, each with its own `style` .

## Emphasis

Capitalize words in the transcript, together with punctuation and inline tags, to stress them. For example: `"This is a VERY important point!"` or `"It was a VERY long day <sigh> ... nobody listens anymore."`

## Vocal bursts and non-speech sounds

Place non-speech human vocalizations inline in angle brackets ( `<...>` ) at the point where the sound should occur. Use human vocalizations rather than non-vocal sound effects such as applause. Recommended vocal tags include:

| Tag                      | Tag             | Tag                        | Tag                           |
| :----------------------- | :-------------- | :------------------------- | :---------------------------- |
| `<argh>`                 | `<breath>`      | `<heavy breath>`           | `<exhales>`                   |
| `<cackle>`               | `<cheer>`       | `<chuckle>` / `<chuckles>` | `<cough>`                     |
| `<cry>`                  | `<gasp>`        | `<giggle>`                 | `<groan>`                     |
| `<growl>`                | `<grunt>`       | `<grr>`                    | `<hiss>`                      |
| `<laugh>` / `<laughter>` | `<moan>`        | `<pant>`                   | `<pff>` / `<phew>`            |
| `<scream>`               | `<shout>`       | `<shriek>`                 | `<sigh>` / `<sighs>`          |
| `<sneeze>`               | `<snicker>`     | `<snort>`                  | `<sob>`                       |
| `<throat-clearing>`      | `<tsk>`         | `<whimper>`                | `<whispers>` / `<whispering>` |
| `<yawn>`                 | `<short pause>` | `<long pause>`             |                               |

> **Note:** If your transcript isn't in English, keep the inline tags in English for best results.

## Backchannels and overlapping speech

In multi-speaker dialogue, wrap listener reactions in pipe characters ( `|reaction|` ) inside the active speaker's turn. This creates natural backchannels or overlapping speech without a separate turn for each reaction.

  - **Short backchannels** : Layer brief listener reactions inside the active speaker's turn:
      - **Turn 1 (Speaker A)** : `"So the launch is Thursday |oh hmm| Are we actually ready?"`
      - **Turn 2 (Speaker B)** : `"Ready enough |oh really?| The last blocker cleared this morning."`
      - **Turn 3 (Speaker A)** : `"Then let's ship it |absolutely| and watch the dashboards."`
  - **Overlapping and interleaved speech** : Use multiple pipe segments to simulate simultaneous speech. This works best with `gemini-3.8-flash-tts` :
      - **Countdown or chorus** : `"Let's surprise him on three |ok| ready?"` followed by `"one. two. three. |happy| happy |birthday| birthday!"`
      - **Full overlap** : `"Hello |oh| there |my| it |goodness| must |gracious| be |would| almost |you| time |look| for |at that| dinner"`

## Consistency across generations and what to avoid

Follow these guidelines to keep vocal identity stable across turns:

  - **Design personas upfront in Voice design instead of long style blocks** : Long-form `"Audio Profile"` paragraphs and multi-bullet `"Director's Notes"` carried over from earlier models are the most common cause of voice drift. Use that same creative intuition upfront in [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) to generate a persistent custom `voice_...` persona, then carry that voice ID through your TTS calls.
  - **Rely on the voice reference for stability (omit meta-instructions)** : Gemini 3.8 TTS models are trained to anchor on the audio reference first. Don't include instructions telling the model to hold the voice steady (such as `"do not switch speaker identity"` or `"maintain identical timbre"` ). Extra prompt text increases drift. Drop unnecessary style instructions and let the model vary naturally around the stable point provided by the voice reference.
  - **Don't try to change immutable speaker traits in `style`** : Avoid putting age, gender, names, or permanent accent changes in `speech_metadata.style` . Instead, pick a regional voice from the [Extended Voice Library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#voice-library) or create one with [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) .

## Recommended workflow

1.  **Build the character once** : Create your character in [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) or select a regional voice from the [Extended Voice Library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#voice-library) that matches your target language and persona.
2.  **Write natural spoken transcripts with disfluencies** : For maximum naturalness, write the `text` as a real spoken transcript, including natural conversational disfluencies and hesitations (for example, `"Oh uh yeah I think... hm, so that's interesting"` ).
3.  **Test plain TTS first** : Synthesize your transcript with an empty `style` field first. Most requests need no `style` instruction at all.
4.  **Add short `style` prompts only for tweaks** : Add a concise `style` string (such as `"casual, friendly"` or `"muttering, then reassuring"` ) only for turns that need a specific delivery adjustment, and reuse that exact short string across turns when you want a consistent baseline.

## Multi-turn dialogue and voice agents

When you build a conversational voice agent or another multi-turn application:

  - Make one TTS request for each turn as the LLM text arrives.
  - Let the configured `voice` carry the speaker's identity across turns. Don't resend a long persona description on each turn.
  - Leave `style` empty, or send one short constant string for the whole conversation.
  - Split long agent responses into shorter turns rather than strengthening the `style` prompt.

## What's next

  - Create a consistent character with [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) .
  - Update prompts written for earlier models with the [migration guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/migration-guide) .
