---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/resources/supported-capabilities
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/supported-capabilities
title: Supported capabilities
description: 'Discover Gemini ML Processing capabilities: system instructions, structured output, function calling, code execution, and regional endpoints.'
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform provides a suite of advanced features for the Gemini model family. To help you meet specific regulatory and architectural needs, we distinguish between capabilities supported on standard regional endpoints and those supported on jurisdictional multi-region endpoints.

## Which models are supported?

Model and capability availability support depends on the endpoint you use:

  - **Standard regional endpoints** : Supported for all versions of the Gemini family.
  - **Jurisdictional multi-region endpoint** s: These are designed exclusively for the Gemini 3 family and future versions. Older models (like Gemini 2.5 and earlier) are not supported on these endpoints.
  - **Global endpoints** : Most models are supported on global endpoints. For the complete list of models available on global endpoint, see [Deployment and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

For more information on the different kinds of available endpoints, see [Deployment and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

## ML processing commitments

ML processing for Gemini models have the following per-capability commitments:

  - **Guaranteed support** : The capabilities listed in the following sections are guaranteed to have ML processing support within the specified regional or jurisdictional boundary.
  - **Non-Listed capabilities** : If a capability is not explicitly listed, ML processing is not guaranteed to occur in a specific location.

For more information about ML processing in Agent Platform, see [Data residency](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency) .

## Endpoint support

The following sections cover the endpoint support for the following model aspects:

  - [Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/supported-capabilities#model-availability)
  - [Capabilities, consumption options, and features](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/supported-capabilities#capabilities-and-features)
  - [Known constraints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/supported-capabilities#known-constraints)

### Model availability

Model availability covers whether or not a particular model can be used on a specific kind of endpoint. The following table covers which model families are supported for each type of endpoint. For per-model information, see [Locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

For workloads requiring strictly jurisdictional ML processing, you must use the Gemini 3.x family. Models older than Gemini 3 are not supported on jurisdictional multi-region endpoints and will continue to be served using standard regional endpoints.

| Model family               | Standard regional endpoints | Jurisdictional multi-region endpoints | Global endpoint |
| -------------------------- | --------------------------- | ------------------------------------- | --------------- |
| Gemini 3.x (Pro and Flash) |                             |                                       |                 |
| Gemini 2 (all versions)    |                             |                                       |                 |

### Capabilities, consumption options, and features

The following table covers the availability of different model capabilities across locational endpoints and jurisdictional multi-region endpoints for Gemini 3.x models and higher. If a capability or feature is not explicitly listed as supported, localized ML processing is not guaranteed.

Capability, feature, or consumption option

Standard regional endpoints

Jurisdictional multi-region endpoints

Global endpoint

Capabilities, tools, and features

[Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)

[Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)

[Controllable parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/adjust-parameter-values)

[Context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)

[Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/list-token)

[Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)

[Grounding with Agent Platform Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-vertex-ai-search)

[Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search)

[Model tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning)

[RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)

[Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)

[System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instructions)

[Thinking budget](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)

[Thought summaries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)

Consumption options

[Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/batch-prediction-api)

[Standard PayGo (without usage tiers)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

[Standard PayGo with Usage Tiers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

[Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

[Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

[Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

[Single Zone PT (SZPT)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/szpt)

Platform features

[Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls)

[Computer Use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use)

For instructions on disabling unsupported capabilities in Gemini Enterprise Agent Platform, see [organization policy constraints](https://docs.cloud.google.com/resource-manager/docs/organization-policy/overview) .

### Known constraints

The following features are either out of scope or involve global infrastructure that cannot be localized to a jurisdictional boundary:

  - **UI console (Agent Studio)** : Not supported
  - **Gemini Live API** : Not supported
  - **Evaluation service (SxS)** : No plan
  - **Priority PayGo and Flex PayGo** : No plan

## What's next

  - To improve model performance by customizing models, see [Tune models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models) .
  - To learn about regional data handling, see [Data residency](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency) .
  - To understand how to secure your generative AI applications, see [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) .
  - To discover and explore various models, see [Explore models in Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .
