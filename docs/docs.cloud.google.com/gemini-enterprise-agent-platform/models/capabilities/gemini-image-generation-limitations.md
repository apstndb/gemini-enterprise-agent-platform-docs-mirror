---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-limitations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-limitations
title: Gemini image generation limitations
description: Learn about limitations when using Gemini to generate images.
data_source: docs.cloud.google.com
---

Gemini image generation is subject to the following limitations:

  - For best performance with Gemini 2.5 Flash Image, use the following languages: EN, es-MX, ja-JP, zh-CN, or hi-IN. For best performance with Gemini 3 Pro Image, use the following languages: ar-EG, de-DE, EN, es-MX, fr-FR, hi-IN, id-ID, it-IT, ja-JP, ko-KR, pt-BR, ru-RU, ua-UA, vi-VN, and zh-CN

  - Image generation doesn't support audio or video inputs.

  - The model might not create the exact number of images you ask for.

  - For best results using Gemini 2.5 Flash Image, include a maximum of three images in an input. For best results using Gemini 3 Pro Image, include a maximum of 14 images in an input.

  - When generating an image containing text, first generate the text and then generate an image with that text.

  - Image or text generation might not work as expected in these situations:
    
      - The model might only create text and no image if the prompt is ambiguous. If you want images, clearly ask for images in your request. For example, "provide images as you go along."
    
      - The model might create text as an image. To generate text, specifically ask for text output. For example, "generate narrative text along with illustrations."
    
      - The model might stop generating content even when it's not finished. If this occurs, try again or use a different prompt.
    
      - If a prompt is potentially unsafe, the model might not process the request and returns a response indicating that it can't create unsafe images. In this case, the [`FinishReason`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#FinishReason) is `STOP` .

## What's next?

See the following links for more information about Gemini image generation:

  - [Generate images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation)

  - [Edit images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images)

  - [Gemini image generation best practices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-best-practices)

  - [Gemini image generation and responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-responsible-ai)
