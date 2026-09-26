---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/codestral-2
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/codestral-2
title: Codestral 2
description: Codestral 2 with Agent Platform Model Garden
data_source: docs.cloud.google.com
---

Codestral 2 is Mistral's code generation specialized model built specifically for high-precision fill-in-the-middle (FIM) completion. It helps developers write and interact with code through a shared instruction and completion API endpoint. As it masters code and can also converse in a variety of languages, it can be used to design advanced AI applications for software developers.

The latest release of Codestral 2 delivers measurable upgrades over prior version Codestral (25.01):

  - 30% increase in accepted completions.
  - 10% more retained code after suggestion.
  - 50% fewer runaway generations, improving confidence in longer edits.

Improved performance on academic benchmarks for short and long-context FIM completion.

  - Code generation: code completion, suggestions, translation.
  - Code understanding and documentation: code summarization and explanation.
  - Code quality: code review, refactoring, bug fixing and test case generation.
  - Code fill-in-the-middle: users can define the starting point of the code using a prompt, and the ending point of the code using an optional suffix and an optional stop. The Codestral model will then generate the code that fits in between, making it ideal for tasks that require a specific piece of code to be generated.

Codestral 2 is well-suited for tasks such as:

  - Code generation
  - Fill-in-the-middle completion
  - Software development applications

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/mistralai/model-garden/codestral-2)

Model ID

`codestral-2`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code
  - Outputs:
    Text

Usage types

Supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Versions

`codestral-2`

  - **Launch stage:** GA
  - **Release date:** October 16, 2025

Supported regions

Model availability

United States

  - `us-central1`

Europe

  - `europe-west4`

ML processing

United States

  - `Multi-region`

Europe

  - `Multi-region`

Quota limits

us-central1:

  - QPM: 1,100
  - Context length: 128,000 tokens

europe-west4:

  - QPM: 1,100
  - Context length: 128,000 tokens

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
