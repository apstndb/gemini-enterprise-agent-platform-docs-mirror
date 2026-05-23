---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/speech/speech-to-text
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/speech/speech-to-text
title: Convert speech to text
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page shows you how to use Gemini Enterprise Agent Platform Studio to convert speech to text.

To learn how to convert text to speech, see [Convert text to speech](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/speech/text-to-speech) .

## Convert speech to text

To convert speech to text, do the following:

1.  In the Agent Platform section of the Google Cloud console, go to the **Gemini Enterprise Agent Platform Studio** page.

2.  Click **Generate speech** .

3.  Select the **Speech-to-text** tab.

4.  In **Speech** , click **Browse** to select the audio file that you want to convert to text.

5.  In the **Language** selector box, select the language of the speech in the audio file.

6.  Click **Submit** .
    
    The converted text appears in **Text** .

## Limitations

  - Audio files can be a maximum 60 seconds or 10 MB (whichever is less).
  - Files are transcribed with the [Chirp](https://cloud.google.com/speech-to-text/v2/docs/usm/usm-model) model.
  - Only 16-bit linear PCM WAV files are supported.

You can use the [Speech-to-Text UI](https://docs.cloud.google.com/speech-to-text/docs/transcribe-console) directly to overcome these limitations.

## What's next

  - For more models, advanced features, and ability to transcribe files up to 8 hours, see [Speech-to-Text](https://docs.cloud.google.com/speech-to-text/docs/transcribe-console) .
