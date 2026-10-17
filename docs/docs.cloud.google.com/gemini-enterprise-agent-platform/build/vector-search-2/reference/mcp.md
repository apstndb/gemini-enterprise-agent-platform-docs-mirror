---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp
title: 'MCP Reference: vectorsearch.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

MCP server for Agent Retrieval (formerly Vector Search 2.0), providing tools to view and query collections, indexes, and perform searches.

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For product-specific setup instructions, see [Use the Agent Retrieval remote MCP server](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/use-agent-retrieval-mcp) . For general information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

The Agent Retrieval (Vector Search API) MCP server exposes a single MCP endpoint:

- `https://vectorsearch.googleapis.com/mcp`

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/docs/concepts/tools) is a function or executable capability that an MCP server exposes to an LLM or AI application to perform an action in the real world.

The Agent Retrieval MCP server currently exposes the following tools on the single `/mcp` endpoint. If you use the MCP 2026-07-28 stateless protocol, each `tools/call` request must also include an `Mcp-Name` HTTP header whose value equals `params.name` (and `Mcp-Param-Region` for direct regional routing; see [Header-based routing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/use-agent-retrieval-mcp#header-based-routing) ); don't send `Mcp-Name` with `tools/list` . Requests that use earlier MCP protocol versions, such as the `curl` samples on the tool pages (with an `Authorization: Bearer` header), are also accepted.

- [`list_collections`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections) – List Vector Search collections in a project and location.
- [`get_collection`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_collection) – Retrieve the schema and metadata of a specific collection.
- [`list_indexes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes) – List indexes defined on a collection.
- [`get_index`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_index) – Retrieve the configuration of a specific index.
- [`get_data_object`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object) – Retrieve a data object by ID from a collection.
- [`search_data_objects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects) – Run a vector, semantic, or text search against a collection.
- [`query_data_objects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/query_data_objects) – List data objects that match a filter expression.
- [`batch_search_data_objects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects) – Run multiple searches in parallel and fuse the results with Reciprocal Rank Fusion (RRF) or the Vertex Ranking API.
- [`aggregate_data_objects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/aggregate_data_objects) – Aggregate data objects that match a filter expression (for example, counts).

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The Vector Search API MCP server supports the [MCP 2026-07-28 stateless protocol](https://modelcontextprotocol.io/specification/2026-07-28) : each request is self-describing and includes the protocol version in both the `MCP-Protocol-Version` HTTP header and the `params._meta.io.modelcontextprotocol/protocolVersion` body field, an `Mcp-Method` header that matches the JSON-RPC `method` , and a `params._meta.io.modelcontextprotocol/clientCapabilities` object (an empty object is accepted). The following `curl` example lists all tools and their specifications.

**Curl Request**

```
curl -X POST 'https://vectorsearch.googleapis.com/mcp' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'MCP-Protocol-Version: 2026-07-28' \
  -H 'Mcp-Method: tools/list' \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/list",
    "params": {
      "_meta": {
        "io.modelcontextprotocol/protocolVersion": "2026-07-28",
        "io.modelcontextprotocol/clientCapabilities": {}
      }
    }
  }'
```
