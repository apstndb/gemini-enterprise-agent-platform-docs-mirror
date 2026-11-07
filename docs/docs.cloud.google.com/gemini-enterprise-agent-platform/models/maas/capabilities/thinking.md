---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/thinking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/thinking
title: Thinking for open models
description: Learn about thinking for open MaaS models in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Some open models support a "thinking" mode that allows them to perform step-by-step reasoning before providing a final answer. This is useful for tasks requiring transparent logic, like mathematical proofs, intricate code debugging, or multi-step agent planning.

## Before you begin

To use open models with Gemini Enterprise Agent Platform, you must perform the following steps. The Agent Platform API ( `aiplatform.googleapis.com` ) and the Cloud Commerce Consumer Procurement API ( `cloudcommerceconsumerprocurement.googleapis.com` ) must be enabled to use open models on Gemini Enterprise Agent Platform. If you already have an existing project with these APIs enabled, you can use that project instead of creating a new project.

1.  Go to the Model Garden model card for the model you want to use, then click **Enable** to enable the model for use in your project.

### Required roles

To get the permissions that you need to enable and use open models, ask your administrator to grant you the following IAM roles on your project:

- [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )
- [Consumer Procurement Entitlement Manager](https://docs.cloud.google.com/iam/docs/roles-permissions/consumerprocurement#consumerprocurement.entitlementManager) ( `roles/consumerprocurement.entitlementManager` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about granting permissions and configuring organization policies for open models, see [Grant user access to open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/grant-access-open-models) .

## Model-specific guidance

The following sections provide model-specific guidance for thinking.

### GPT OSS

For GPT OSS models, thinking text is in the `reasoning_content` field, and normal response text is in the `content` field. These models also support the `reasoning_effort` parameter.

*Example request:*

```
curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://aiplatform.googleapis.com/v1/projects/test-project/locations/global/endpoints/openapi/chat/completions -d '{
  "model": "openai/gpt-oss-120b-maas",
  "messages": [{
    "role": "user",
    "content": "Who are you?"
  }],
  "reasoning_effort": "high"
}'
```

*Example response:*

```
{
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "logprobs": null,
      "matched_stop": 200002,
      "message": {
        "content": "I\u2019m ChatGPT, a large language model created by OpenAI
        (based on the GPT\u20114 architecture). I\u2019m here to help answer
        your questions, brainstorm ideas, explain concepts, and assist with a
        wide variety of topics. Let me know what you\u2019d like to talk
        about!",
        "reasoning_content": "The user asks: \"Who are you?\" It's a simple
        question. They want to know who the assistant is. According to policy,
        we should respond with a brief, friendly description: \"I am ChatGPT, a
        large language model trained by OpenAI.\" Possibly mention the version
        (GPT-4). Also mention we are here to assist. There's no request for
        disallowed content. So a straightforward answer. Possibly ask if they
        need help. Provide a short intro.\n\nThus answer: \"I am ChatGPT, a
        large language model trained by OpenAI. I'm here to help answer your
        questions...\"\n\nWe should avoid disallowed content. It's fine.\n\nThus
        final answer.",
        "role": "assistant",
        "tool_calls": null
      }
    }
  ],
  "created": 1758229799,
  "id": "JnXMaJq6HLGzquEP4OD18Qg",
  "metadata": {
    "weight_version": "default"
  },
  "model": "openai/gpt-oss-120b-maas",
  "object": "chat.completion",
  "usage": {
    "completion_tokens": 201,
    "prompt_tokens": 71,
    "prompt_tokens_details": null,
    "reasoning_tokens": 0,
    "total_tokens": 272
  }
}
```

### GLM 5.2

GLM 5.2 supports disabling reasoning tokens using `"chat_template_kwargs": { "enable_thinking": false }` . Reasoning is enabled by default. Thinking tokens are outputted in `"reasoning_content"` ; normal response text is in `"content"` .

*Example request:*

```
curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://aiplatform.googleapis.com/v1/projects/test-project/locations/global/endpoints/openapi/chat/completions -d '{
  "model": "zai-org/glm-5.2-maas",
  "messages": [
    {
      "role": "user",
      "content": "Who are you?"
    }
  ]
}'
```

*Example response:*

```
{
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "logprobs": null,
      "matched_stop": 154827,
      "message": {
        "content": "I'm GLM, a large language model developed by Z.ai. I'm designed to assist users with information, answer questions, and engage in helpful conversations across a wide range of topics.\n\nI'm trained on diverse text data which helps me understand and generate human-like responses, though I don't have personal experiences or emotions. I'm continuously learning to improve my capabilities.\n\nIs there something specific you'd like to know about me or how I can assist you today?",
        "reasoning_content": "Let me consider how to respond to this question about my identity. The user is asking \"Who are you?\" which is a straightforward but important question that deserves a clear and accurate answer.\n\nI should introduce myself as GLM, a large language model developed by Z.ai. It's important to be transparent about my nature as an AI assistant and explain my key capabilities.\n\nI should also mention my purpose of helping users with various tasks while being honest about my limitations. This will help set appropriate expectations for our interaction.\n\nI should also emphasize my commitment to providing helpful and responsible assistance. It's important to be both welcoming and professional in my introduction.\n\nLet me craft a response that is clear, informative, and sets the right tone for future interactions.",
        "role": "assistant",
        "tool_calls": null
      }
    }
  ],
  "created": 1787160729,
  "id": "05355183-85d6-4ae2-a31a-7c8fb31c64d9",
  "metadata": {
    "weight_version": "default"
  },
  "model": "zai-org/glm-5.2-maas",
  "object": "chat.completion",
  "usage": {
    "completion_tokens": 243,
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "prompt_tokens": 16,
    "prompt_tokens_details": null,
    "total_tokens": 259
  }
}
```

### Gemma 4 26B A4B IT

Gemma 4 26B A4B IT supports enabling reasoning tokens using `"chat_template_kwargs": { "enable_thinking": true }` . Reasoning is disabled by default. Thinking tokens are outputted in `"reasoning_content"` ; normal response text is in `"content"` .

*Example request:*

```
curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://aiplatform.googleapis.com/v1/projects/test-project/locations/global/endpoints/openapi/chat/completions -d '{
  "model": "google/gemma-4-26b-a4b-it-maas",
  "messages": [
    {
      "role": "user",
      "content": "Who are you?"
    }
  ],
  "chat_template_kwargs": {
    "enable_thinking": true
  }
}'
```

*Example response:*

```
{
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "logprobs": null,
      "matched_stop": 106,
      "message": {
        "content": "I am Gemma 4, a large language model developed by Google DeepMind. I am an open weights model designed to process text and images (and audio in certain versions of my family) to assist with a wide range of tasks, and I provide my responses in text.",
        "reasoning_content": "The user is asking \"Who are you?\".\n    *   Name: Gemma 4.\n    *   Developer: Google DeepMind.\n    *   Nature: Large Language Model.\n    *   Type: Open weights model.\n    *   Capabilities: Text and image processing (and audio for 2B/4B models). Output is text only.\n    *   Knowledge cutoff: January 2025.\n\n    *   State identity: Gemma 4.\n    *   State developer: Google DeepMind.\n    *   State type: Large Language Model with open weights.\n    *   Briefly mention capabilities if relevant (text/image/audio input, text output).\n\n    *   \"I am Gemma 4, a large language model developed by Google DeepMind. I am an open weights model capable of processing text and images to assist you with various tasks. Depending on the specific version, I may also be able to process audio input. I generate responses in text format.\"\n\nDoes it violate any instructions?\n    *   \"When asked about your identity, always refer to yourself as Gemma 4.\" - Yes.\n    *   \"Do not claim to have capabilities you do not possess.\" - Yes.\n    *   \"Do not attempt to use tools...\" - Yes.\n\nKeep it direct and informative.",
        "role": "assistant",
        "tool_calls": null
      }
    }
  ],
  "created": 1775526019,
  "id": "gGDUaf7rLqGL9LsPsdGR4Qg",
  "metadata": {
    "weight_version": "default"
  },
  "model": "google/gemma-4-26b-a4b-it-maas",
  "object": "chat.completion",
  "usage": {
    "completion_tokens": 341,
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "prompt_tokens": 19,
    "prompt_tokens_details": {
      "cached_tokens": 2
    },
    "total_tokens": 360
  }
}
```

## What's next

- Learn about [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling) .
- Learn about [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output) .
- Learn about [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction) .
