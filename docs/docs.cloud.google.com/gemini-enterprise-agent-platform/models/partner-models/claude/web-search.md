---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search
title: Web search with Anthropic Claude models
description: Web search is a capability in Anthropic's Messages API that enables a Claude model to augment its knowledge with real-time data from the web
data_source: docs.cloud.google.com
---

Web search is a capability that enables a Claude model to augment its knowledge with real-time data from the web. The Claude models use a third-party search provider for the web search feature. The web search capability is particularly powerful for RAG (Retrieval-Augmented Generation) applications where you need to accurately cite sources.

The web search capability is well-suited for the following use cases:

  - **Retrieve the latest technical documentation** : Software developers can ask Claude about the latest API documentation or technical specifications, with Claude able to retrieve and synthesize information directly from source documentation.
  - **Gather business and market information** : Business analysts can gather current market data, company information, or industry news to support their decision-making processes
  - **Assist with research** : Knowledge workers can use Claude as a research assistant that can find, synthesize, and explain information from multiple web sources while maintaining accurate citations
  - **Support customers** : Customer service applications can access up-to-date product information, pricing, or support documentation from company websites

## Supported models

Gemini Enterprise Agent Platform supports web search for the following Anthropic Claude models:

  - [Claude Opus 4.8](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-8)
  - [Claude Opus 4.7](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-7)
  - [Claude Opus 4.6](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-6)
  - [Claude Sonnet 4.6](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4-6)
  - [Claude Opus 4.5](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-5)
  - [Claude Opus 4.1](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-1)
  - [Claude Opus 4](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4)
  - [Claude Sonnet 4.5](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4-5)
  - [Claude Sonnet 4](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4)
  - [Claude Haiku 4.5](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-haiku-4-5)

## Control access to web search

The web search feature requires public internet access. By default, web search is disabled by the organization policy constraint `constraints/vertexai.allowedPartnerModelFeatures` . To enable web search, you must configure this constraint to explicitly allow it.

Additionally, you can configure the organization policy constraint `constraints/vertexai.allowedModels` to restrict access to Claude models.

> **Important:** For the following model versions, the default denial for web search will not be enforced until July 2026:
> 
>   - Sonnet 4.0
>   - Sonnet 4.5
>   - Opus 4.0
>   - Opus 4.1
>   - Opus 4.5
>   - Haiku 4.5

To ensure continued access to web search for these specific model versions after June 2026, configure the `constraints/vertexai.allowedPartnerModelFeatures` organization policy to allow web search by the end of June 2026.

For detailed instructions on configuring organization policy constraints, see [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

## Use web search

> **Important:** The web search feature is invoked by using the `web_search_tool` . If [VPC-SC](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) is configured, any requests that use the `web_search_tool` are blocked.

Enable web search by providing a new Anthropic tool definition ( `web_search` ) in the API request.

For example, the following code snippet uses web search to retrieve real-time weather information:

    response = await client.messages.create(
        model="claude-4-sonnet-latest",
        max_tokens=1024,
        messages=[{
            "role": "user",
            "content": "What is the weather in San Francisco?"
        }],
        tools=[{
            "type": "web_search",
            "name": "web_search",
            "max_uses": 5
        }]
    )

You can also use optional fields to specify allowed and blocked domains. For example:

    tools=[{
      ...
      # Only one of allowed_domains and blocked_domains can be provided.
      # allowed_domains excludes everything except the specified domains
        "allowed_domains": ["example.com", "example.org"],
    
      # blocked_domains includes everything except the specified domains
      # Use the `NOT site:` search operator
        "blocked_domains": ["example.net"],
    }]

For more information on optional fields, see the [Claude web search tool documentation](https://docs.claude.com/en/docs/agents-and-tools/tool-use/web-search-tool#tool-definition)

When the model determines that web search is required, the API invokes the web search tool until no more tool calls are required. The response includes details about the intermediate searches, with the results encrypted.

The following code snippet is an example of a response with web search:

    {
      ...
      "role": "assistant",
      "content": [
        // Initial output from the model
        {
          "type": "text",
          "text": "I need to search the web to answer this question about the weather in San Francisco."
        },
        {
          "type": "server_tool_use",
          "id": "srvtoolu_9a90a390a",
          "name": "web_search",
          "input": {
            "query": "What is the weather in San Francisco?",
          }
        },
        // API sees an `</antml:function_calls>` stop sequence here, sees that
        // the tool use is for a server-side tool, and then runs that
        // tool. If there is a mix of client and server-side, the API would
        // need to return to the client and let it pass back client tool results
        // before continuing with server tools.
        {
          "type": "web_search_tool_result",
          // "name": "web_search", use this to determine what types of blocks are inside `content`
          "tool_use_id": "srvtoolu_9a90a390a",
          "content": [
            {
              "type": "web_search_result",
              "uri": "https://weather.com",
              "title": "National and Local Weather",
              "encrypted_content": "eyJlbmNyeXB0ZWRfa2V5Ijoic2VjcmV0LW...", // encrypted list of snippets from the web search provider
            },
            {
              "type": "web_search_result",
              "uri": "https://accuweather.com",
              "title": "San Francisco, CA Hourly Weather",
              "encrypted_content": "yaJlbmNyeXB0ZWRfa2V5Ijoic2VjcmV0LW...", // encrypted list of snippets from the web search provider
            },
          ],
        },
        // Server starts a new sampling run with the above content appended (unencrypted)
        // to the original request. Everything below is completion content from the
        // second sampling run.
        {
          "type": "text",
          "text": "The current weather in San Francisco, CA is 65 degrees Fahrenheit and partly cloudy."
        }
      ],
      // Server output is no longer 1-to-1 with a single sampling run. From the
      // user's perspective, there is just one "Message" with a single id
      "id": "msg_a930390d3",
      "usage": {
        "input_tokens": 3029,
        "output_tokens": 6039,
        "server_tool_use": {
          "web_search_requests": 2
        }
      },
      "stop_reason": "end_turn"
    }

## Streaming with web search

With streaming enabled, the model returns search events as part of the stream. For example:

    // Claude's decision to search
    
    event: content_block_start
    data: {"type": "content_block_start", "index": 1, "content_block": {"type": "server_tool_use", "id": "srvtoolu_xyz789", "name": "web_search"}}
    
    // Search query streamed
    event: content_block_delta
    data: {"type": "content_block_delta", "index": 1, "delta": {"type": "input_json_delta", "partial_json": "{\"query\":\"latest quantum computing breakthroughs 2025\"}"}}
    
    // Pause while search executes
    
    // Search results streamed
    event: content_block_start
    data: {"type": "content_block_start", "index": 2, "content_block": {"type": "web_search_tool_result", "tool_use_id": "srvtoolu_xyz789", "content": [{"type": "web_search_result", "title": "Quantum Computing Breakthroughs in 2025", "url": "https://example.com"}]}}

Usage is metered and included in `message_delta` messages, which includes a cumulative count of `web_search` items. For example:

    event: message_delta
    data: {"type":"message_delta","delta":{"stop_reason":"end_turn","stop_sequence":null},"usage":{"input_tokens":10682,"cache_creation_input_tokens":0,"cache_read_input_tokens":0,"output_tokens":510,"server_tool_use":{"web_search_requests":1}}}

## Data Governance for Requests enabling Web Search

The web search feature for Claude 4.0 and newer models is an optional feature of Anthropic's Claude models. You can enable it by providing the [web search tool](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/web-search-tool#how-to-use-web-search) in the requests. When you activate this feature, you are instructing Gemini Enterprise Agent Platform to enable the Claude models to send search queries derived from your request to a third-party search service provider selected by Anthropic. Google is not responsible for the data processing practices of this third-party provider. Once the search queries are transmitted, the handling of that data is governed by the third-party's own terms of service and privacy policy, not Google's.

Activating the web search feature has direct implications for your data governance and security posture. Gemini Enterprise Agent Platform additional commitments, such as Customer-Managed Encryption Keys (CMEK) and Data Residency, do not apply to the data while being processed by the third-party search provider. If your consumer project is under a VPC-SC perimeter, VertexAI will reject the requests with the following error message:

    {
      "error": {
        "code": 400,
        "message": "The requested model does not serve requests restricted by VPCSC",
        "status": "FAILED_PRECONDITION"
      }
    }

This feature is exclusively available for Claude 4.0 and subsequent models; it is not available for older Claude models on Gemini Enterprise Agent Platform. The list of third-party search services that Anthropic Web Search feature can call if the web search feature is used:

  - [Brave Search](https://search.brave.com/)

## Pricing

Web search is priced as an add-on to standard messages API usage, based on web request volume. Due to the additional sampling calls, users will also be charged for the additional input tokens.

For more information, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/pricing) .
