---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-best-practices
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-best-practices
title: Gemini image generation best practices
description: Learn about best practices when using Gemini to generate images.
data_source: docs.cloud.google.com
---

To improve your image generation results, follow these best practices:

  - **Be specific:** More details give you more control. For example, instead of "fantasy armor," try "ornate elven plate armor, etched with silver leaf patterns, with a high collar and pauldrons shaped like falcon wings."

  - **Provide context and intent:** Explain the purpose of the image to help the model understand the context. For example, "Create a logo for a high-end, minimalist skincare brand" works better than "Create a logo."

  - **Iterate and refine:** Don't expect a perfect image on your first attempt. Use follow-up prompts to make small changes, for example, "Make the lighting warmer" or "Change the character's expression to be more serious."

  - **Use step-by-step instructions:** For complex scenes, split your request into steps. For example, "First, create a background of a serene, misty forest at dawn. Then, in the foreground, add a moss-covered ancient stone altar. Finally, place a single, glowing sword on top of the altar."

  - **Describe what you want, not what you don't:** Instead of saying "no cars", describe the scene positively by saying, "an empty, deserted street with no signs of traffic."

  - **Control the camera:** Guide the camera view. Use photographic and cinematic terms to describe the composition, for example, "wide-angle shot", "macro shot", or "low-angle perspective".

  - **Prompt for images:** Describe the intent by using phrases such as "create an image of" or "generate an image of". Otherwise, the multimodal model might respond with text instead of the image.

  - **Pass [Thought Signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thought-signatures) :** When using Gemini, we recommend that you pass thought signatures back to the model during multi-turn image creation and editing. This lets you preserve reasoning context across interactions. For code samples related to multi-turn image editing using Gemini, see [Example of multi-turn image editing using thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thought-signatures#multi-turn-image-editing) .

## What's next?

See the following links for more information about Gemini image generation:

  - [Generate images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation)

  - [Edit images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images)

  - [Gemini image generation limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-limitations)

  - [Gemini image generation and responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-responsible-ai)
