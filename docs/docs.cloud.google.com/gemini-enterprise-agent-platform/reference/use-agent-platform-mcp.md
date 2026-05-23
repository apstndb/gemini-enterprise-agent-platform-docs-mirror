---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/use-agent-platform-mcp
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/use-agent-platform-mcp
title: Use the Agent Platform remote MCP server
description: Learn how to use the Gemini Enterprise Agent Platform remote MCP server to manage Agent Platform resources.
data_source: docs.cloud.google.com
---

This document shows you how to use the Gemini Enterprise Agent Platform remote Model Context Protocol (MCP) server to connect with AI applications including Gemini CLI, ChatGPT, Claude, and custom applications you are developing. The Agent Platform remote MCP server lets you manage Agent Platform resources from your AI application. The Gemini Enterprise Agent Platform remote MCP server is enabled when you enable the Gemini Enterprise Agent Platform API.

[Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) standardizes how large language models (LLMs) and AI applications or agents connect to external data sources. MCP servers let you use their tools, resources, and prompts to take actions and get updated data from their backend service.

## What's the difference between local and remote MCP servers?

  - Local MCP servers  
    Typically run on your local machine and use the standard input and output streams (stdio) for communication between services on the same device.
  - Remote MCP servers  
    Run on the service's infrastructure and offer an HTTP endpoint to AI applications for communication between the AI MCP client and the MCP server. For more information about MCP architecture, see [MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture) .

## Google and Google Cloud remote MCP servers

Google and Google Cloud remote MCP servers have the following features and benefits:

  - Simplified, centralized discovery
  - Managed global or regional HTTP endpoints
  - Fine-grained authorization
  - Optional prompt and response security with Model Armor protection
  - Centralized audit logging

For information about other MCP servers and information about security and governance controls available for Google Cloud MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

## Before you begin

### Required roles

To get the permissions that you need to use the Gemini Enterprise Agent Platform MCP server, ask your administrator to grant you the following IAM roles on the project where you want to use the Gemini Enterprise Agent Platform MCP server:

  - Make MCP tool calls: [MCP Tool User](https://docs.cloud.google.com/iam/docs/roles-permissions/mcp#mcp.toolUser) ( `roles/mcp.toolUser` )
  - Manage Agent Platform resources: [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

> **Note:** Specific tasks in Agent Platform require that you use additional Google Cloud products in addition to Agent Platform. For example, when you create a custom training pipeline, often you must use Cloud Storage and Artifact Registry. You might need to perform additional setup tasks to use other Google Cloud products.

## Authentication and authorization

The Gemini Enterprise Agent Platform remote MCP server uses the [OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) protocol with [Identity and Access Management (IAM)](https://docs.cloud.google.com/iam/docs/overview) for authentication and authorization. All [Google Cloud identities](https://docs.cloud.google.com/docs/authentication/identity-products) are supported for authentication to MCP servers.

Agent Platform accepts API keys for authentication. You can use an API key with Agent Platform in [express mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/overview) for rapid prototyping, or use an [API key bound to a service account](https://docs.cloud.google.com/docs/authentication/api-keys#bound-keys) in a standard project. Standard API keys that are not bound to a service account aren't supported because they don't provide a principal for Identity and Access Management (IAM) control.

We recommend that you create a separate identity for agents that are using MCP tools so that access to resources can be controlled and monitored. For more information about authentication, see [Authenticate to MCP servers](https://docs.cloud.google.com/mcp/authenticate-mcp) .

## Agent Platform MCP OAuth scopes

OAuth 2.0 uses scopes and credentials to determine if an authenticated principal is authorized to take a specific action on a resource. For more information about OAuth 2.0 scopes at Google, read [Using OAuth 2.0 to access Google APIs](https://developers.google.com/identity/protocols/oauth2) .

Agent Platform requires OAuth scopes for authorized access to its resources. Use the following scopes depending on the level of access required:

| Scope URI                                        | Description                                                                                             |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| `https://www.googleapis.com/auth/aiplatform`     | Grants full control plane access to see, edit, configure, and delete Agent Platform resources and data. |
| `https://www.googleapis.com/auth/cloud-platform` | Grants broad access to all Google Cloud services, including all Agent Platform features.                |

Additional scopes might be required on the resources accessed during a tool call. To view a list of scopes required for Agent Platform, see [Gemini Enterprise Agent Platform API, v1](https://developers.google.com/identity/protocols/oauth2/scopes#aiplatform) .

## Configure an MCP client to use the Gemini Enterprise Agent Platform MCP server

AI applications and agents, such as Claude or Gemini CLI, can instantiate an MCP client that connects to a single MCP server. An AI application can have multiple clients that connect to different MCP servers. To connect to a remote MCP server, the MCP client must know the remote MCP server's URL.

In your AI application, look for a way to connect to a remote MCP server. You are prompted to enter details about the server, such as its name and URL.

For the Gemini Enterprise Agent Platform MCP server, enter the following as required:

  - **Server name** : Gemini Enterprise Agent Platform MCP server

  - **Server URL** or **Endpoint** : ` https://aiplatform.googleapis.com TOOLSET_ENDPOINT  `
    
    Replace TOOLSET\_ENDPOINT with the toolset endpoint, for example: `/mcp/generate` . See [Toolsets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp#toolsets) .

  - **Transport** : HTTP

  - **Authentication details** : Depending on how you want to authenticate, you can enter your Google Cloud credentials, your OAuth Client ID and secret, or an agent identity and credentials. For more information about authentication, see [Authenticate to MCP servers](https://docs.cloud.google.com/mcp/authenticate-mcp) .

  - **OAuth scope** : the [OAuth 2.0 scope](https://developers.google.com/identity/protocols/oauth2/scopes) that you want to use when connecting to the Gemini Enterprise Agent Platform MCP server.

For host-specific guidance about setting up and connecting to MCP server, see the following:

  - [Claude.ai](https://docs.cloud.google.com/mcp/configure-mcp-ai-application#claude-ai)
  - [Gemini CLI](https://docs.cloud.google.com/mcp/configure-mcp-ai-application#gemini-cli)

For more general guidance, see the following resources:

  - [Connect to remote MCP servers](https://modelcontextprotocol.io/docs/develop/connect-remote-servers) .
  - [Configure MCP in an AI application](https://docs.cloud.google.com/mcp/configure-mcp-ai-application) .

## Available tools

To view details of available MCP tools and their descriptions for the Gemini Enterprise Agent Platform MCP server, see the [Gemini Enterprise Agent Platform MCP reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp) .

### List tools

Use the [MCP inspector](https://modelcontextprotocol.io/docs/tools/inspector) to list tools, or send a `tools/list` HTTP request directly to the Agent Platform remote MCP server. The `tools/list` method doesn't require authentication.

    POST /mcp HTTP/1.1
    Host: aiplatform.googleapis.com
    Content-Type: application/json
    
    {
      "jsonrpc": "2.0",
      "method": "tools/list",
    }

## Optional security and safety configurations

MCP introduces new security risks and considerations due to the wide variety of actions that you can do with the MCP tools. To minimize and manage these risks, Google Cloud offers default settings and customizable policies to control the use of MCP tools in your Google Cloud organization or project.

For more information about MCP security and governance, see [AI security and safety](https://docs.cloud.google.com/mcp/ai-security-safety) .

### Use Model Armor

[Model Armor](https://docs.cloud.google.com/model-armor/overview) is a Google Cloud service designed to enhance the security and safety of your AI applications. It works by proactively screening LLM prompts and responses, protecting against various risks and supporting responsible AI practices. Whether you are deploying AI in your cloud environment, or on external cloud providers, Model Armor can help you prevent malicious input, verify content safety, protect sensitive data, maintain compliance, and enforce your AI safety and security policies consistently across your diverse AI landscape.

When Model Armor is enabled with [logging enabled](https://docs.cloud.google.com/model-armor/configure-logging) , Model Armor logs the entire payload. This might expose sensitive information in your logs.

> **Caution:** Model Armor is available in [certain regions](https://docs.cloud.google.com/model-armor/locations) . When Model Armor is enabled and you use an MCP server in a jurisdiction that Model Armor doesn't support, the routing behavior of the call might be different for different MCP servers. For more information about the behavior of individual MCP servers, see [Model Armor supported products](https://docs.cloud.google.com/mcp/model-armor-supported-products) .

#### Enable Model Armor

You must enable Model Armor APIs before you can use Model Armor.

### Console

1.  Enable the Model Armor API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

2.  Select the project where you want to activate Model Armor.

### gcloud

Before you begin, follow these steps using the Google Cloud CLI with the Model Armor API:

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Run the following command to set the API endpoint for the Model Armor service.
    
        gcloud config set api_endpoint_overrides/modelarmor "https://modelarmor.LOCATION.rep.googleapis.com/"
    
    Replace `  LOCATION  ` with the region where you want to use Model Armor.

#### Configure protection for Google and Google Cloud remote MCP servers

To help protect your MCP tool calls and responses you can use Model Armor floor settings. A floor setting defines the minimum security filters that apply across the project. This configuration applies a consistent set of filters to all MCP tool calls and responses within the project.

> **Tip:** Don't enable the prompt injection and jailbreak filter unless your MCP traffic carries natural language data.

Set up a Model Armor floor setting with MCP sanitization enabled. For more information, see [Configure Model Armor floor settings](https://docs.cloud.google.com/model-armor/configure-floor-settings) .

> **Note:** If the agent and the MCP server are in different projects, you can create floor settings in both projects (the client project and the resource project). In this case, Model Armor is invoked twice, once for each project.

See the following example command:

    gcloud model-armor floorsettings update \
    --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
    --enable-floor-setting-enforcement=TRUE \
    --add-integrated-services=GOOGLE_MCP_SERVER \
    --google-mcp-server-enforcement-type=INSPECT_AND_BLOCK \
    --enable-google-mcp-server-cloud-logging \
    --malicious-uri-filter-settings-enforcement=ENABLED \
    --add-rai-settings-filters='[{"confidenceLevel": "MEDIUM_AND_ABOVE", "filterType": "DANGEROUS"}]'

Replace `  PROJECT_ID  ` with your Google Cloud project ID.

Note the following settings:

  - `INSPECT_AND_BLOCK` : The enforcement type that inspects content for the Google MCP server and blocks prompts and responses that match the filters.
  - `ENABLED` : The setting that enables a filter or enforcement.
  - `MEDIUM_AND_ABOVE` : The confidence level for the Responsible AI - Dangerous filter settings. You can modify this setting, though lower values might result in more false positives. For more information, see [Model Armor confidence levels](https://docs.cloud.google.com/model-armor/overview#ma-confidence-levels) .

#### Disable scanning MCP traffic with Model Armor

To stop Model Armor from automatically scanning traffic to and from Google MCP servers based on the project's floor settings, run the following command:

    gcloud model-armor floorsettings update \
      --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
      --remove-integrated-services=GOOGLE_MCP_SERVER

Replace `  PROJECT_ID  ` with the Google Cloud project ID. Model Armor doesn't automatically apply the rules defined in this project's floor settings to any Google MCP server traffic.

Model Armor floor settings and general configuration can impact more than just MCP. Because Model Armor integrates with services like Vertex AI, any changes you make to floor settings can affect traffic scanning and safety behaviors across all integrated services, not just MCP.

### Control MCP use with IAM deny policies

[Identity and Access Management (IAM) deny policies](https://docs.cloud.google.com/iam/docs/deny-overview) help you secure Google Cloud remote MCP servers. Configure these policies to block unwanted MCP tool access.

For example, you can deny or allow access based on:

  - The principal
  - Tool properties like read-only
  - The application's OAuth client ID

For more information, see [Control MCP use with Identity and Access Management](https://docs.cloud.google.com/mcp/control-mcp-use-iam) .

## What's next

  - Read the [Gemini Enterprise Agent Platform MCP reference documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp) .
  - Learn more about [Google Cloud MCP servers](https://docs.cloud.google.com/mcp/overview) .
