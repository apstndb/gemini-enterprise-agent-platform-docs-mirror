---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/overview
title: Lyria | AI Music Generator
description: Explore Lyria on Gemini Enterprise Agent Platform, a music generator that brings Google's music generation AI capabilities to application developers.
data_source: docs.cloud.google.com
---

> To see an example of Lyria Music Generation, run the "Lyria Music Generation with Python SDK" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/audio/music/getting-started/lyria3_music_generation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fmusic%2Fgetting-started%2Flyria3_music_generation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fmusic%2Fgetting-started%2Flyria3_music_generation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/music/getting-started/lyria3_music_generation.ipynb)

Lyria offers multiple models that let you generate audio. Lyria 3 lets you generate 30 second song clips. Lyria 3 Pro lets you generate 184 second audio tracks with a clear musical structure and vocals from prompts that you provide in the Google Cloud console or that you send in a Agent Platform API request.

## Lyria on Gemini Enterprise Agent Platform models

There are multiple Lyria music generation models that you can use. For more information, see [Lyria models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#lyria-models) .

## Locations

A location is a [region](https://docs.cloud.google.com/about/locations) you can specify in a request to control where data is stored at rest. For the list of available regions for Gemini Enterprise Agent Platform services, see [Generative AI on Gemini Enterprise Agent Platform locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

## Responsible AI

Lyria generates music from prompts. Lyria applies safety measures including content safety filters, recitation checking, and artist intent checks to prevent the input and generation of harmful or inappropriate content. SynthID watermarking is used on generated audio. Prompts that violate [responsible AI guidelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai) may be blocked.
