---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/use-agent-retrieval-mcp
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/use-agent-retrieval-mcp
title: Use the Agent Retrieval remote MCP server to connect to AI and custom applications
description: Learn how to use the Agent Retrieval remote MCP server to inspect collections and indexes, and perform vector, semantic, hybrid, and text search over your data.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document shows you how to use the Gemini Enterprise Agent Platform remote Model Context Protocol (MCP) server to connect with AI applications including Gemini CLI, ChatGPT, Claude, and custom applications you are developing. The Agent Retrieval remote MCP server lets you access and run Agent Retrieval tools to inspect collections and indexes, and perform vector, semantic, hybrid, and text search over your data from your AI-enabled development environments and AI agent platforms. The Gemini Enterprise Agent Platform remote MCP server is enabled when you enable the Gemini Enterprise Agent Platform API.

[Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) standardizes how large language models (LLMs) and AI applications or agents connect to external data sources. MCP servers let you use their tools, resources, and prompts to take actions and get updated data from their backend service.

## What's the difference between local and remote MCP servers?

  - Local MCP servers  
    Typically run on your local machine and use the standard input and output streams (stdio) for communication between services on the same device.
  - Remote MCP servers  
    Run on the service's infrastructure and offer an HTTP endpoint to AI applications for communication between the AI MCP client and the MCP server. For more information about MCP architecture, see [MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture) .

## Stateless core

With [MCP version 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28) , MCP changes from a bidirectional, stateful protocol to a stateless protocol. Each MCP request is self-describing and can be routed using headers. There isn't a need for the `initialize` / `initialized` handshake or `Mcp-Session-Id` because each request includes all the information needed in HTTP headers or the `_meta` parameter. MCP servers can request additional information required by a tool through [multi-round-trip requests (MRTR)](https://modelcontextprotocol.io/specification/latest/basic/patterns/mrtr) .

To help route and process requests without parsing the request body, some MCP headers are required, including the following:

  - Headers that are required by the MCP specification such as the [protocol version header](https://modelcontextprotocol.io/specification/latest/basic/transports/streamable-http#protocol-version-header) and [standard request headers](https://modelcontextprotocol.io/specification/latest/basic/transports/streamable-http#standard-request-headers) .
  - [Custom headers](https://modelcontextprotocol.io/specification/latest/basic/transports/streamable-http#custom-headers-from-tool-parameters) that are defined by the MCP server. These headers are mirrored into HTTP headers from the tool's input schema using the `x-mcp-header` property. For example, an MCP server might define a custom header to specify the Google Cloud region or project ID.

For more information about MCP architecture, see the MCP version 2026-07-28 [specification](https://modelcontextprotocol.io/specification/2026-07-28) and [key changes](https://modelcontextprotocol.io/specification/2026-07-28/changelog) .

## Google and Google Cloud remote MCP servers

Google and Google Cloud remote MCP servers have the following features and benefits:

  - Simplified, centralized discovery
  - Managed global or regional HTTP endpoints
  - Fine-grained authorization
  - Optional prompt and response security with Model Armor protection
  - Centralized audit logging

For information about other MCP servers and information about security and governance controls available for Google Cloud MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

## Before you begin

1.  Enable the Agent Retrieval API, if it is not already enabled.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to use the Agent Retrieval MCP server, ask your administrator to grant you the following IAM roles on the project where you want to use the Agent Retrieval MCP server:

  - Make MCP tool calls: [MCP Tool User](https://docs.cloud.google.com/iam/docs/roles-permissions/mcp#mcp.toolUser) ( `roles/mcp.toolUser` )
  - Read Agent Retrieval resources: [Vector Search Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/vectorsearch#vectorsearch.viewer) ( `roles/vectorsearch.viewer` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to use the Agent Retrieval MCP server. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to use the Agent Retrieval MCP server:

  - Make MCP tool calls: `mcp.tools.call`
  - List and inspect collections and indexes: `vectorsearch.collections.list` , `vectorsearch.collections.get` , `vectorsearch.indexes.list` , `vectorsearch.indexes.get`
  - Read and search data objects: `vectorsearch.dataObjects.get` , `vectorsearch.dataObjects.query` , `vectorsearch.dataObjects.search`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

The Agent Retrieval MCP server exposes only read-only tools; no write permissions are required.

## Authentication and authorization

The Agent Retrieval MCP server uses the [OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) protocol with [IAM](https://docs.cloud.google.com/iam/docs/overview) for authentication and authorization. All [Google Cloud identities](https://docs.cloud.google.com/docs/authentication/identity-products) are supported for authentication to MCP servers.

We recommend that you create a separate identity for agents that are using MCP tools so that access to resources can be controlled and monitored. For more information about authentication, see [Authenticate to MCP servers](https://docs.cloud.google.com/mcp/authenticate-mcp) .

## Agent Retrieval MCP OAuth scopes

OAuth 2.0 uses scopes and credentials to determine if an authenticated principal is authorized to take a specific action on a resource. For more information about OAuth 2.0 scopes at Google, see [Using OAuth 2.0 to access Google APIs](https://developers.google.com/identity/protocols/oauth2) .

The Agent Retrieval MCP server accepts the following OAuth scope:

| Scope URI                                        | Description                                                                               |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| `https://www.googleapis.com/auth/cloud-platform` | Grants broad access to all Google Cloud services, including all Agent Retrieval features. |

## Configure an MCP client to use the Agent Retrieval MCP server

AI applications and agents, such as Claude or Antigravity, can instantiate an MCP client that connects to a single MCP server. An AI application can have multiple clients that connect to different MCP servers. If your application isn't listed in the [client-specific guidance](https://docs.cloud.google.com/mcp/configure-mcp-ai-application#client-specific-guidance) , then you can use the following information to connect from most applications.

In your AI application, look for a way to add or connect to a remote MCP server. For the Agent Retrieval MCP server, enter the following information as required:

  - **Server name** : Agent Retrieval MCP server

  - **Server URL** or **Endpoint** : `https://vectorsearch.googleapis.com/mcp`
    
    This single endpoint exposes all nine Agent Retrieval MCP tools. Tool calls are dispatched to the correct backend by [header-based routing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/use-agent-retrieval-mcp#header-based-routing) .

  - **Transport** : HTTP

  - **Authentication details** : your Google Cloud credentials, your OAuth Client ID and secret, or an agent identity and credentials. For more information about authentication, see [Authenticate to MCP servers](https://docs.cloud.google.com/mcp/authenticate-mcp) .

### Header-based routing and client protocol requirements

The Agent Retrieval MCP server dispatches every `tools/call` at the network edge based on two HTTP headers:

  - `Mcp-Name` — must equal the tool name in the request body ( `params.name` ).
  - `Mcp-Param-Region` — must equal the `location` component of the resource path in the request body (for example, `us-central1` for a Collection at `projects/PROJECT_ID/locations/us-central1/collections/COLLECTION_ID` ).

If either header is missing or does not match the body, the request is rejected with `HTTP 400 Bad Request` .

Your MCP client must emit these headers dynamically per `tools/call` . This behavior is standardized in MCP protocol version `2026-07-28` and later; make sure your MCP client library advertises at least this protocol version during the `initialize` handshake. Clients pinned to earlier protocol versions, or SDK versions that don't support dynamic header emission, cannot use the Agent Retrieval MCP server through the unified `/mcp` endpoint.

### Redirect URIs

For web-based applications, and some desktop applications, you must allowlist a redirect URI when you create a client ID and secret for authentication. Redirect URIs are used by the authorization server to send tokens to your application. Your application's documentation should specify the redirect URI that you must use. [Custom redirect URIs](https://developers.google.com/identity/protocols/oauth2/native-app#redirect-uri_custom-scheme) aren't supported.

For application-specific guidance about setting up and connecting to MCP server, see [Client-specific guidance](https://docs.cloud.google.com/mcp/configure-mcp-ai-application#client-specific-guidance) .

For more general guidance, see the following resources:

  - [Connect to remote MCP servers](https://modelcontextprotocol.io/docs/develop/connect-remote-servers) .
  - [Configure MCP in an AI application](https://docs.cloud.google.com/mcp/configure-mcp-ai-application) .

## Available tools

The Agent Retrieval MCP server exposes nine read-only tools:

| Tool                        | Description                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `list_collections`          | List Agent Retrieval collections in a project and location.                                                         |
| `get_collection`            | Retrieve the schema and metadata of a specific collection.                                                          |
| `list_indexes`              | List indexes defined on a collection.                                                                               |
| `get_index`                 | Retrieve the configuration of a specific index.                                                                     |
| `get_data_object`           | Retrieve a data object by ID from a collection.                                                                     |
| `search_data_objects`       | Run a vector, semantic, or text search against a collection.                                                        |
| `query_data_objects`        | List data objects that match a filter expression.                                                                   |
| `batch_search_data_objects` | Run multiple searches in parallel and fuse the results with Reciprocal Rank Fusion (RRF) or the Vertex Ranking API. |
| `aggregate_data_objects`    | Aggregate data objects that match a filter expression (for example, counts).                                        |

All tools are read-only; the MCP server does not expose any write, update, or delete operations on Agent Retrieval resources.

### List tools

Use the [MCP inspector](https://modelcontextprotocol.io/docs/tools/inspector) to list tools, or send a `tools/list` HTTP request directly to the Agent Retrieval MCP server. The `tools/list` method doesn't require authentication.

The Agent Retrieval MCP server uses the [MCP 2026-07-28 stateless protocol](https://modelcontextprotocol.io/specification/2026-07-28) , so each request is self-describing and must declare the protocol version in both the `MCP-Protocol-Version` HTTP header and the `_meta.io.modelcontextprotocol/protocolVersion` body field. The `Mcp-Method` HTTP header must also match the `method` in the body.

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
            "io.modelcontextprotocol/protocolVersion": "2026-07-28"
          }
        }
      }'

## Sample use cases

The following are sample use cases for the Agent Retrieval MCP server:

  - **Resource inspection** : list collections and indexes in a project, and inspect their schemas and metadata.
  - **Vector and semantic search** : run vector or semantic search against a collection to find the most relevant data objects for a query.
  - **Hybrid retrieval** : combine semantic, text, and vector searches in a single batch call and fuse the results with Reciprocal Rank Fusion (RRF) or the Vertex Ranking API.
  - **Data object retrieval** : retrieve individual data objects by ID, or query a collection by filter to inspect ingested records.

### Sample prompts

  - "List the Agent Retrieval collections in project `PROJECT_ID` in `REGION` ."
  - "Show the schema of collection `COLLECTION_ID` in region `REGION` ."
  - "Run a semantic search on collection `COLLECTION_ID` for `QUERY_TEXT` and return the top 5 nearest neighbors."
  - "Do a hybrid search on collection `COLLECTION_ID` for `QUERY_TEXT` that combines semantic and text search, then rerank the top 50 with `semantic-ranker-fast@latest` ."
  - "Get the data object with ID `DATA_OBJECT_ID` from collection `COLLECTION_ID` ."

In the prompts, replace the following:

  - `PROJECT_ID` : the Google Cloud project ID
  - `REGION` : the region of your collection (for example, `us-central1` )
  - `COLLECTION_ID` : the ID of the Agent Retrieval collection
  - `DATA_OBJECT_ID` : the ID of a data object in the collection
  - `QUERY_TEXT` : the natural-language text of the query

## Quotas and limits

The Agent Retrieval MCP server doesn't have its own quotas. There is no limit on the number of calls that can be made to the MCP server. You are still subject to the quotas enforced by the Agent Retrieval API, which the MCP server tools call on your behalf. For more information, see [Agent Retrieval quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/quotas) .

## What's next

  - Learn how to [create a Collection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections#creating_a_collection) .
  - Learn how to [search for data objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) .
  - Learn how to [rerank search results](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/reranking) .
  - Learn more about [Google Cloud MCP servers](https://docs.cloud.google.com/mcp/overview) .
