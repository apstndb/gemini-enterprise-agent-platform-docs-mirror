---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching
title: Prompt caching
description: Optimize Anthropic Claude model performance with prompt caching on Agent Platform. Reduce latency, control costs, configure TTL, and manage data processing.
data_source: docs.cloud.google.com
---

The Anthropic Claude models offer prompt caching to reduce latency and costs when reusing the same content in multiple requests. When you send a query, you can cache all or specific parts of your input so that subsequent queries can use the cached results from the previous request. This avoids additional compute and network costs. Caches are unique to your Google Cloud project and cannot be used by other projects.

For details about how to structure your prompts, see the Anthropic [Prompt caching](https://platform.claude.com/en/docs/build-with-claude/prompt-caching) documentation.

## Data processing

Anthropic explicit prompt caching is a feature of Anthropic Claude models. The Gemini Enterprise Agent Platform offering of these Anthropic models behaves as described in the [Anthropic documentation](https://platform.claude.com/en/docs/build-with-claude/prompt-caching) .

Prompt caching is an optional feature. Claude computes the hashes (fingerprints) of requests for caching keys. These hashes are only computed for requests that have caching enabled.

Although prompt caching is a feature implemented by the Claude models, from a data handling perspective, Google considers these hashes to be a type of "User Metadata". They are treated as customer "Service Data" under the [Google Cloud Privacy Notice](https://cloud.google.com/terms/cloud-privacy-notice) and not as "Customer Data" under the [Cloud Data Processing Addendum (Customers)](https://cloud.google.com/terms/data-processing-addendum) . In particular, additional protections for "Customer Data" don't apply to these hashes. Google does not use these hashes for any other purpose.

If you want to completely disable this prompt caching feature and make it unavailable in particular Google Cloud projects, you can request this by contacting [customer support](https://console.cloud.google.com/support/createcase/v2) and providing the relevant project numbers. After explicit caching is disabled for a project, requests from the project with prompt caching enabled are rejected.

## Use prompt caching

You can use the [Anthropic Claude SDK](https://pypi.org/project/anthropic/) or the Gemini Enterprise Agent Platform REST API to send requests to the Gemini Enterprise Agent Platform endpoint.

For more information, see [How prompt caching works](https://platform.claude.com/en/docs/build-with-claude/prompt-caching#how-prompt-caching-works) .

For additional examples, see the [Prompt caching examples](https://platform.claude.com/en/docs/build-with-claude/prompt-caching#prompt-caching-examples) in the Anthropic documentation.

Caching automatically occurs when subsequent requests contain the identical text, images, and `cache_control` parameter as the first request. All requests must also include the `cache_control` parameter in the same blocks.

By default, the cache has a five-minute lifetime or time to live (TTL). You can extend the TTL to one hour by setting `"ttl": "1h"` within the `cache_control` object. The cache lifetime is refreshed each time the cached content is accessed. For more information, see [1-hour cache duration](https://platform.claude.com/en/docs/build-with-claude/prompt-caching#1-hour-cache-duration) .

The one-hour TTL isn't supported for the following models: Claude 3.7 Sonnet, Claude 3.5 Sonnet v2, Claude 3.5 Sonnet, and Claude 3 Opus.

## Pricing

Prompt caching can affect billing costs. Note that:

  - Cache write tokens with a five-minute lifetime are 25% more expensive than base input tokens.
  - Cache write tokens with a one-hour lifetime are 100% more expensive than base input tokens.
  - Cache read tokens are 90% cheaper than base input tokens.
  - Regular input and output tokens are priced at standard rates.

For more information, see the [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#claude-models) page.
