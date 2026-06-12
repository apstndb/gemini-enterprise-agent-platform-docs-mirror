---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage
title: Create and manage agents
description: Learn how to create and manage agents with the REST API, configure MCP tools, and attach skills in Managed Agents API on Agent Platform.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

> To see an example of creating and managing agents, run the "Introduction to Managed Agents in Python" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/managed-agents/intro_managed_agents_python.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fmanaged-agents%2Fintro_managed_agents_python.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fmanaged-agents%2Fintro_managed_agents_python.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/managed-agents/intro_managed_agents_python.ipynb)

This guide explains how to create, retrieve, list, update, and delete custom agent resources that use Managed Agents API on Agent Platform, and how to configure the agent environment, Model Context Protocol (MCP) server tools, and skills.

> **Note:** Model usage during the preview is billed at standard rates. For more information, see the [pricing page](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Prerequisites

Before configuring your agents, complete the following:

  - In the Google Google Cloud console, on the project selector page, select or create a Google Cloud project.

  - [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

  - Enable the Gemini Enterprise Agent Platform API ( `aiplatform.googleapis.com` ) on your project.

  - Ensure you have one of the following roles:
    
      - `aiplatform.user` : Provides permissions to interact with AI Platform resources.
      - `aiplatform.admin` : Provides full control over AI Platform resources, including administrative tasks.

  - If you plan to use Google Cloud Model Context Protocol (MCP) tools with your agent, grant the `mcp.toolUser` role to both your user account and the associated service account.

## Create an agent

To create a new custom agent, use the `CreateAgent` method. This is a [long-running operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage#get-details-of-lro) .

> **Note:** During the Preview period, provisioning the first agent in your project can take between two and three minutes. Subsequent agents typically provision within two to three seconds.

### The base agent

The `base_agent` is the core orchestration harness that provides the agent with reasoning capabilities and access to the execution environment. It can inject skills and libraries into the environment and has access to service-side tools for code execution, file system operations, and search with grounding.

When creating an agent, only one value is supported for `base_agent` : `antigravity-preview-05-2026` .

### Create a basic agent

To create a basic agent with default tools and a Google Cloud Storage mount target, send a `POST` request:

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.

  - LOCATION : The regional location for your agent. Only the `global` region is supported.

  - AGENT\_ID : The unique custom identifier for your new agent. Custom Agent IDs must adhere to the following constraints:
    
      - Must be 1 to 63 characters long.
      - Must contain only lowercase letters, numbers, and hyphens.
      - Must start with a letter and end with a letter or number.

  - BASE\_AGENT : The name of the base agent to extend. Use `antigravity-preview-05-2026` .

  - AGENT\_DESCRIPTION : A short summary of the agent's scope.

  - INSTRUCTIONS : System instructions or persona to set on the agent.

  - GCS\_BUCKET : The folder path segment of your mounted Google Cloud Storage bucket (for example, `gs://cymbal-bucket-name` ). Note: To mount a bucket from a different project, grant the project's service account `read` and `write` access to the bucket.

  - network : For security reasons, network access in the environment is turned off. You must specify an `allowlist` to enable access. Using `*` as a domain in the `allowlist` allows connections to all domains, providing unrestricted network access.

#### HTTP method and URL

    POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents

#### Request JSON body

    {
      "id": "AGENT_ID",
      "base_agent": "BASE_AGENT",
      "description": "AGENT_DESCRIPTION",
      "system_instruction": "INSTRUCTIONS",
      "tools": [
        {"type": "code_execution"},
        {"type": "filesystem"},
        {"type": "google_search"},
        {"type": "url_context"}
      ],
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "gcs",
            "source": "GCS_BUCKET",
            "target": "/.agent"
          }
        ],
        "network": {
          "allowlist": [
            { "domain": "*" }
          ]
        }
      }
    }

#### `curl` command

    curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "id": "AGENT_ID",
          "base_agent": "antigravity-preview-05-2026",
          "description": "AGENT_DESCRIPTION",
          "system_instruction": "INSTRUCTIONS",
          "tools": [
              {"type": "code_execution"},
              {"type": "filesystem"},
              {"type": "google_search"},
              {"type": "url_context"}
          ],
          "base_environment": {
              "type": "remote",
              "sources": [
                  {
                      "type": "gcs",
                      "source": "GCS_BUCKET",
                      "target": "/.agent"
                  }
              ],
              "network": {
                  "allowlist": [
                      { "domain": "*" }
                  ]
              }
          }
      }'

#### Example Response

    {
      "name": "projects/1234567890/locations/global/agents/my-first-agent/operations/234567890123",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.CreateAgentOperationMetadata",
        "genericMetadata": {
          "createTime": "2026-05-12T23:50:16.933752Z",
          "updateTime": "2026-05-12T23:50:16.933752Z"
        }
      }
    }

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    agent = client.agents.create(
        id="AGENT_ID",
        base_agent="antigravity-preview-05-2026",
        description="AGENT_DESCRIPTION",
        system_instruction="INSTRUCTIONS",
        tools=[
            {"type": "code_execution"},
            {"type": "google_search"},
            {"type": "url_context"},
        ],
        base_environment={
            "type": "remote",
            "sources": [
                {
                    "type": "gcs",
                    "source": "GCS_BUCKET",
                    "target": "/.agent",
                }
            ],
            "network": {
                "allowlist": [{"domain": "*"}]
            },
        },
    )

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const agent = await client.agents.create({
        id: "AGENT_ID",
        base_agent: "antigravity-preview-05-2026",
        description: "AGENT_DESCRIPTION",
        system_instruction: "INSTRUCTIONS",
        tools: [
            { type: "code_execution" },
            { type: "google_search" },
            { type: "url_context" },
        ],
        base_environment: {
            type: "remote",
            sources: [
                {
                    type: "gcs",
                    source: "GCS_BUCKET",
                    target: "/.agent",
                },
            ],
            network: {
                allowlist: [{ domain: "*" }],
            },
        },
    });

### Create an agent with Google first-party tools

To create an agent with Google first-party tools (such as Grounding with Google Search and URL context), add these tools to the `tools` list in the agent configuration:

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.

  - LOCATION : The regional location for your agent. Only the `global` region is supported.

  - AGENT\_ID : The unique custom identifier for your new agent. Custom Agent IDs must adhere to the following constraints:
    
      - Must be 1 to 63 characters long.
      - Must contain only lowercase letters, numbers, and hyphens.
      - Must start with a letter and end with a letter or number.

  - AGENT\_DESCRIPTION : A short summary of the agent's scope.

#### Request JSON body

    {
      "id": "AGENT_ID",
      "base_agent": "antigravity-preview-05-2026",
      "description": "AGENT_DESCRIPTION",
      "tools": [
        {
          "type": "google_search"
        },
        {
          "type": "url_context"
        }
      ],
      "base_environment": {
        "type": "remote",
        "network": {
          "allowlist": [
            { "domain": "*" }
          ]
        }
      }
    }

#### `curl` command

    curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "id": "AGENT_ID",
          "base_agent": "antigravity-preview-05-2026",
          "description": "AGENT_DESCRIPTION",
          "tools": [
              {
                  "type": "google_search"
              },
              {
                  "type": "url_context"
              }
          ],
          "base_environment": {
              "type": "remote",
              "network": {
                  "allowlist": [
                      { "domain": "*" }
                  ]
              }
          }
      }'

### Create an agent with MCP configs

You can create an agent with preconfigured MCP server tools using the Managed Agents API on Agent Platform.

#### Before you begin

Before you create an agent with preconfigured MCP server tools, do the following:

  - Grant the **MCP Tool User** ( `roles/mcp.toolUser` ) Identity and Access Management (IAM) role to both your user account and the associated service account.

  - Confirm that the MCP servers in your configuration communicate over standard `HTTP POST` for tool listings and execution. The Managed Agents API on Agent Platform requires remote MCP servers to be **Streamable HTTP servers** . The MCP servers must implement the [MCP Streamable HTTP transport](https://modelcontextprotocol.io/specification/2024-11-05/basic/transports) ), where `tools/list` and `tools/call` are sent as JSON-RPC over `HTTP POST` .
    
    The deprecated two-endpoint HTTP+SSE transport (a separate long-lived `GET /sse` stream) is not supported.

#### Authorize Google-hosted MCPs

If you are using a bearer token for authorization of Google-hosted MCP servers (such as BigQuery), complete the following steps:

1.  **Add OAuth Scopes:** Append the required [OAuth 2.0 scopes](https://developers.google.com/identity/protocols/oauth2/scopes) to your authentication token. For example, to use the BigQuery MCP, include the relevant BigQuery scopes in your request.
2.  **Validate Access:** Verify whether the MCP server is accessible with your newly configured scopes by testing the authorization flow in the [OAuth Playground](https://developers.google.com/oauthplayground/) .
3.  **Use Headers:** For Google MCPs like BigQuery, you must include the `X-Goog-User-Project` header set to your project name in the `headers` map.

For example, the request JSON body used to create an agent that uses the BigQuery MCP would look similar to the following:

    {
      "name": "projects/<projectname>/locations/global/agents/data-analyst",
      "id": "data-analyst",
      "system_instruction": "You are a data analyst. Use the provided tools and data to perform analysis.",
      "tools": [
        { "type": "code_execution" },
        { "type": "filesystem" },
        { "type": "google_search" },
        { "type": "url_context" },
        {
          "type": "mcp_server",
          "name": "bigquery-mcp",
          "url": "https://mcp-bigquery.googleapis.com/v1",
          "headers": {
            "Authorization": "Bearer ya29.a0AQyyyy",
            "X-Goog-User-Project": "project-nameyyyy"
          }
        }
      ],
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "gcs",
            "source": "gs://agents-1",
            "target": "/.agent/agents-1"
          }
        ],
        "network": {
          "allowlist": [ { "domain": "*" } ]
        }
      },
      "base_agent": "antigravity-preview-05-2026",
      "object": "agent"
    }

#### Create the agent

To create an agent with preconfigured MCP server tools, add details under the `tools` section:

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.

  - LOCATION : The regional location for your agent. Only the `global` region is supported.

  - AGENT\_ID : The unique custom identifier for your new agent. Custom Agent IDs must adhere to the following constraints:
    
      - Must be 1 to 63 characters long.
      - Must contain only lowercase letters, numbers, and hyphens.
      - Must start with a letter and end with a letter or number.

  - AGENT\_DESCRIPTION : A short summary of the agent's scope.

  - MCP\_SERVER\_NAME : A descriptive name for the MCP tool.

  - MCP\_SERVER\_URL : The remote HTTP gateway URL of the MCP server.

  - MCP\_HEADER\_KEY : Optional. The name of the header for authentication (for example, `Authorization` ).

  - MCP\_HEADER\_VALUE : Optional. The authentication bearer token (for example, `Bearer <token>` ).

#### Request JSON body

    {
      "id": "AGENT_ID",
      "base_agent": "antigravity-preview-05-2026",
      "description": "AGENT_DESCRIPTION",
      "tools": [
        {
          "type": "mcp_server",
          "name": "MCP_SERVER_NAME",
          "url": "MCP_SERVER_URL",
          "headers": {
            "MCP_HEADER_KEY": "MCP_HEADER_VALUE"
          }
        }
      ]
    }

#### `curl` command

    curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "id": "AGENT_ID",
          "base_agent": "antigravity-preview-05-2026",
          "description": "AGENT_DESCRIPTION",
          "tools": [
              {
                  "type": "mcp_server",
                  "name": "MCP_SERVER_NAME",
                  "url": "MCP_SERVER_URL",
                  "headers": {
                      "MCP_HEADER_KEY": "MCP_HEADER_VALUE"
                  }
              }
          ]
      }'

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    agent = client.agents.create(
        id="AGENT_ID",
        base_agent="antigravity-preview-05-2026",
        description="AGENT_DESCRIPTION",
        tools=[
            {
                "type": "mcp_server",
                "name": "MCP_SERVER_NAME",
                "url": "MCP_SERVER_URL",
                "headers": {
                    "MCP_HEADER_KEY": "MCP_HEADER_VALUE"
                },
            }
        ],
    )

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const agent = await client.agents.create({
        id: "AGENT_ID",
        base_agent: "antigravity-preview-05-2026",
        description: "AGENT_DESCRIPTION",
        tools: [
            {
                type: "mcp_server",
                name: "MCP_SERVER_NAME",
                url: "MCP_SERVER_URL",
                headers: {
                    "MCP_HEADER_KEY": "MCP_HEADER_VALUE",
                },
            },
        ],
    });

### Attach skills to an agent

To load a reusable skill directly when creating the agent, mount it inside `base_environment.sources` .

You can attach skills using either of the following methods:

  - **Skill Registry:** Attach a skill registered within your project in [Skill Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry) .

  - **Google Cloud Storage:** Attach custom skills directly from a Cloud Storage bucket.
    
    As a best practice, we recommend mounting skills under the `/.agent/skills` folder in the environment to make them more discoverable to the agent.

#### CLI Skills

Developers can also install specialized skills in their CLI of choice to programmatically manage agents and interactions:

  - [Agents API Skill](https://github.com/google/skills/blob/main/skills/cloud/gemini-agents-api/SKILL.md)
  - [Interaction API Skill](https://github.com/google/skills/blob/main/skills/cloud/gemini-interactions-api/SKILL.md)

#### Attach a skill from the Skill Registry

To load a reusable skill directly from the Skill Registry when creating the agent:

### REST

##### Request variables

Before calling the API, make the following replacements:

  - `  PROJECT_ID  ` : Your Google Cloud project ID.
  - `  LOCATION  ` : The regional location for your agent. Only the `global` region is supported.
  - `  AGENT_ID  ` : The unique custom identifier for your new agent. Custom Agent IDs must adhere to the following constraints:
      - Must be 1 to 63 characters long.
      - Must contain only lowercase letters, numbers, and hyphens.
      - Must start with a letter and end with a letter or number.
  - `  SKILL_RESOURCE_NAME  ` : The resource path of the skill or list of skills to mount. You can specify one of the following formats:
      - **Skill (default version):** `projects/{projectID}/locations/{location}/skills/{skillName}`
      - **Specific version:** `projects/{projectID}/locations/{location}/skills/{skillName}/skill_versions/{skill_version}`
      - **List of skills:** `projects/{projectID}/locations/{location}/skills` . This mounts up to 100 skills from the specified `project/location` into the sandbox environment.
    For more information, see [list skills](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry/create-manage#list-skills) .

##### Request JSON body

    {
      "id": "AGENT_ID",
      "base_agent": "antigravity-preview-05-2026",
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "skill_registry",
            "source": "SKILL_RESOURCE_NAME",
            "target": "/.agent/skills"
          }
        ],
        "network": {
          "allowlist": [
            { "domain": "*" }
          ]
        }
      }
    }

##### `curl` command

    curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "id": "AGENT_ID",
          "base_agent": "antigravity-preview-05-2026",
          "base_environment": {
              "type": "remote",
              "sources": [
                  {
                      "type": "skill_registry",
                      "source": "SKILL_RESOURCE_NAME",
                      "target": "/.agent/skills"
                  }
              ],
              "network": {
                  "allowlist": [
                      { "domain": "*" }
                  ]
              }
          }
      }'

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    agent = client.agents.create(
        id="AGENT_ID",
        base_agent="antigravity-preview-05-2026",
        base_environment={
            "type": "remote",
            "sources": [
                {
                    "type": "skill_registry",
                    "source": "SKILL_RESOURCE_NAME",
                    "target": "./skills",
                }
            ],
            "network": {
                "allowlist": [{"domain": "*"}]
            },
        },
    )

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const agent = await client.agents.create({
        id: "AGENT_ID",
        base_agent: "antigravity-preview-05-2026",
        base_environment: {
            type: "remote",
            sources: [
                {
                    type: "skill_registry",
                    source: "SKILL_RESOURCE_NAME",
                    target: "./skills",
                },
            ],
            network: {
                allowlist: [{ domain: "*" }],
            },
        },
    });

#### Attach a skill from Google Cloud Storage

Alternatively, you can attach custom skills directly from a Google Cloud Storage bucket when creating the agent.

Note the following requirements when mounting skills from Cloud Storage:

  - **Upload requirements:** You must upload the entire skill folder to the bucket.
  - **No content validation:** The backend does not validate folder content before mounting; it behaves like a standard folder upload.
  - **Size limits:** All the attached files are subject to the sandbox environment memory limits (up to 4 GiB of RAM in total).
  - **Best practices:** For optimal skill quality, structure and prepare the files in your skill folder following the conventions described on [agentskills.io/home](https://agentskills.io/home) .

To attach a skill from Google Cloud Storage when creating the agent:

### REST

##### Request variables

Before calling the API, make the following replacements:

  - `  PROJECT_ID  ` : Your Google Cloud project ID.
  - `  LOCATION  ` : The regional location for your agent. Only the `global` region is supported.
  - `  AGENT_ID  ` : The unique custom identifier for your new agent. Custom Agent IDs must adhere to the following constraints:
      - Must be 1 to 63 characters long.
      - Must contain only lowercase letters, numbers, and hyphens.
      - Must start with a letter and end with a letter or number.
  - `  GCS_SOURCE_PATH  ` : The Google Cloud Storage bucket path containing your skill folder (for example, `gs://cymbal-bucket-name/my-skill-folder` ).

##### Request JSON body

    {
      "id": "AGENT_ID",
      "base_agent": "antigravity-preview-05-2026",
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "gcs",
            "source": "GCS_SOURCE_PATH",
            "target": "/.agent/skills"
          }
        ],
        "network": {
          "allowlist": [
            { "domain": "*" }
          ]
        }
      }
    }

##### `curl` command

    curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "id": "AGENT_ID",
          "base_agent": "antigravity-preview-05-2026",
          "base_environment": {
              "type": "remote",
              "sources": [
                  {
                      "type": "gcs",
                      "source": "GCS_SOURCE_PATH",
                      "target": "./skills"
                  }
              ],
              "network": {
                  "allowlist": [
                      { "domain": "*" }
                  ]
              }
          }
      }'

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    agent = client.agents.create(
        id="AGENT_ID",
        base_agent="antigravity-preview-05-2026",
        base_environment={
            "type": "remote",
            "sources": [
                {
                    "type": "gcs",
                    "source": "GCS_SOURCE_PATH",
                    "target": "./skills",
                }
            ],
            "network": {
                "allowlist": [{"domain": "*"}]
            },
        },
    )

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const agent = await client.agents.create({
        id: "AGENT_ID",
        base_agent: "antigravity-preview-05-2026",
        base_environment: {
            type: "remote",
            sources: [
                {
                    type: "gcs",
                    source: "GCS_SOURCE_PATH",
                    target: "./skills",
                },
            ],
            network: {
                allowlist: [{ domain: "*" }],
            },
        },
    });

## List agents

To list all saved agents in your project, send a `GET` request. You can use optional pagination to control the number of results per page.

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION : The regional location for listing agents. Only the `global` region is supported.
  - PAGE\_SIZE : Optional. The maximum number of agents to return per page. The default value is 10, and the maximum value is 100.
  - PAGE\_TOKEN : Optional. A page token, received from a previous `ListAgents` response. Provide this token to retrieve the subsequent page of results.

When the number of agents to return is larger than the `PAGE_SIZE` , the `ListAgents` response includes a `nextPageToken` field. To retrieve the next page of agents, pass the value of this `nextPageToken` as the `PAGE_TOKEN` parameter in your next `ListAgents` request. Repeat this process until the `nextPageToken` field is no longer returned in the response.

#### HTTP method and URL

    GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents?page_size=PAGE_SIZE&page_token=PAGE_TOKEN

#### `curl` command

    curl -X GET "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)"

#### Example Response

    {
      "agents": [
        {
          "name": "projects/1234567890/locations/global/agents/my-first-agent",
          "id": "my-first-agent",
          "created": "2026-05-12T23:50:16.933Z",
          "updated": "2026-05-12T23:50:21.159Z",
          "systemInstruction": "You are a helpful assistant to user."
        }
      ],
      "nextPageToken": "ABCDEFGHIJKLMNOPQRSTUVWXYZ=="
    }

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    response = client.agents.list()
    
    for agent in response.agents:
        print(agent)

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const response = await client.agents.list();
    
    if (response.agents) {
        for (const agent of response.agents) {
            console.log(agent);
        }
    }

## Get an agent

To retrieve the complete configuration of a specified agent, use a `GET` request.

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.

  - LOCATION : The regional location for your agent. Only the `global` region is supported.

  - AGENT\_ID : The unique ID of the custom agent config you are requesting.

#### HTTP method and URL

    GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID

#### `curl` command

    curl -X GET "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)"

#### Example Response

    {
      "name": "projects/vertex-agent-fishfood/locations/global/agents/my-first-agent",
      "id": "my-first-agent",
      "created": "2026-05-12T23:50:16.933Z",
      "updated": "2026-05-12T23:50:21.159Z",
      "systemInstruction": "You are a helpful assistant to user.",
      "tools": [
        {"type": "code_execution"},
        {"type": "filesystem"},
        {"type": "google_search"},
        {"type": "url_context"}
      ],
      "description": "A demo agent showcasing Environment and Skills use case.",
      "baseEnvironment": {
        "type": "remote",
        "sources": [
          {
            "type": "gcs",
            "source": "gs://agents-api-sample-skills",
            "target": "/.agent"
          }
        ],
        "network": {
          "allowlist": [
            {"domain": "*"}
          ]
        }
      },
      "baseAgent": "antigravity-preview-05-2026",
      "object": "agent"
    }

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    agent = client.agents.get(id="AGENT_ID")
    print(agent)

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const agent = await client.agents.get("AGENT_ID");
    console.log(agent);

## Update an agent

To update an existing agent's configuration, send a `PATCH` request. While the agent's ID is immutable, you can modify parameters such as instructions, tools, and environment variables. Use the `update_mask` query parameter to specify exactly which fields to update. This ensures that only the fields you intend to change are affected, preserving other configurations.

### Update a basic agent

To update an agent's system instructions, send a `PATCH` request with `update_mask=system_instruction` :

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION : The regional location of the agent. Only the `global` region is supported.
  - AGENT\_ID : Target agent configuration to patch update.
  - NEW\_INSTRUCTIONS : The updated instructions structure or description to replace.

#### HTTP method and URL

    PATCH https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID?update_mask=system_instruction

#### Request JSON body

    {
      "name": "AGENT_ID",
      "system_instruction": "NEW_INSTRUCTIONS"
    }

#### `curl` command

    curl -X PATCH "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID?update_mask=system_instruction" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "name": "AGENT_ID",
          "system_instruction": "NEW_INSTRUCTIONS"
      }'

### Python

> **Note:** The `update` method is not yet available in the Python SDK. Use the REST API to update agents.

### JavaScript

> **Note:** The `update` method is not yet available in the JavaScript SDK. Use the REST API to update agents.

### Update an agent with Google first-party tools

To update an agent to enable Google first-party (1P) tools (such as Grounding with Google Search and URL context), send a `PATCH` request with `update_mask=tools` :

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION : The regional location of the agent. Only the `global` region is supported.
  - AGENT\_ID : Target agent ID.

#### Request JSON body

    {
      "name": "AGENT_ID",
      "tools": [
        {
          "type": "google_search"
        },
        {
          "type": "url_context"
        }
      ]
    }

#### `curl` command

    curl -X PATCH "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID?update_mask=tools" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "name": "AGENT_ID",
          "tools": [
              {
                  "type": "google_search"
              },
              {
                  "type": "url_context"
              }
          ]
      }'

### Update an agent with MCP configs

To modify the MCP tools attached to your agent, send a `PATCH` request with `update_mask=tools` :

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION : The regional location of the agent. Only the `global` region is supported.
  - AGENT\_ID : Target agent ID.
  - NEW\_MCP\_SERVER\_NAME : Updated label of your MCP tools.
  - NEW\_MCP\_SERVER\_URL : The new URL endpoint parameter of the server.
  - NEW\_MCP\_HEADER\_KEY : Optional. The name of the header for authentication (for example, `Authorization` ).
  - NEW\_MCP\_HEADER\_VALUE : Optional. The authentication bearer token (for example, `Bearer <token>` ).

#### Request JSON body

    {
      "name": "AGENT_ID",
      "tools": [
        {
          "type": "mcp_server",
          "name": "NEW_MCP_SERVER_NAME",
          "url": "NEW_MCP_SERVER_URL",
          "headers": {
            "NEW_MCP_HEADER_KEY": "NEW_MCP_HEADER_VALUE"
          }
        }
      ]
    }

#### `curl` command

    curl -X PATCH "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID?update_mask=tools" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "name": "AGENT_ID",
          "tools": [
              {
                  "type": "mcp_server",
                  "name": "NEW_MCP_SERVER_NAME",
                  "url": "NEW_MCP_SERVER_URL",
                  "headers": {
                      "NEW_MCP_HEADER_KEY": "NEW_MCP_HEADER_VALUE"
                  }
              }
          ]
      }'

### Python

> **Note:** The `update` method is not yet available in the Python SDK. Use the REST API to update agents.

### JavaScript

> **Note:** The `update` method is not yet available in the JavaScript SDK. Use the REST API to update agents.

### Attach skills to an agent

To attach or modify skills within `base_environment.sources` during an agent update, send a `PATCH` request using `update_mask=base_environment` .

You can attach skills using either of the following methods:

  - **Skill Registry:** Attach a skill registered within your project in [Skill Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry) .

  - **Google Cloud Storage:** Attach custom skills directly from a Cloud Storage bucket.

#### Attach a skill from the Skill Registry

To attach a skill registered in the Skill Registry:

### REST

##### Request variables

Before calling the API, make the following replacements:

  - `  PROJECT_ID  ` : Your Google Cloud project ID.
  - `  LOCATION  ` : The regional location of the agent. Only the `global` region is supported.
  - `  AGENT_ID  ` : Target agent ID.
  - `  NEW_SKILL_RESOURCE_NAME  ` : The resource path of the skill or list of skills to mount. You can specify one of the following formats:
      - **Skill (default version):** `projects/{projectID}/locations/{location}/skills/{skillName}`
      - **Skill version (Pin to a specific version):** `projects/{projectID}/locations/{location}/skills/{skillName}/skill_versions/{skill_version}`
      - **ListSkills (Mount all skills):** `projects/{projectID}/locations/{location}/skills` . This mounts up to 100 skills in the project/location into the sandbox environment.
    For more information about finding the `name` value for `NEW_SKILL_RESOURCE_NAME` , see [List skills](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry/create-manage#list-skills) .

##### Request JSON body

    {
      "name": "AGENT_ID",
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "skill_registry",
            "source": "NEW_SKILL_RESOURCE_NAME",
            "target": "/.agent/skills"
          }
        ],
        "network": {
          "allowlist": [
            { "domain": "*" }
          ]
        }
      }
    }

##### `curl` command

    curl -X PATCH "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID?update_mask=base_environment" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "name": "AGENT_ID",
          "base_environment": {
              "type": "remote",
              "sources": [
                  {
                      "type": "skill_registry",
                      "source": "NEW_SKILL_RESOURCE_NAME",
                      "target": "/.agent/skills"
                  }
              ],
              "network": {
                  "allowlist": [
                      { "domain": "*" }
                  ]
              }
          }
      }'

### Python

> **Note:** The `update` method is not yet available in the Python SDK. Use the REST API to update agent skills.

### JavaScript

> **Note:** The `update` method is not yet available in the JavaScript SDK. Use the REST API to update agent skills.

#### Attach a skill from Google Cloud Storage

Alternatively, you can attach custom skills directly from a Google Cloud Storage bucket when creating the agent.

Note the following requirements when mounting skills from Cloud Storage:

  - **Upload requirements:** You must upload the entire skill folder to the bucket.
  - **No content validation:** The backend does not validate folder content before mounting; it behaves like a standard folder upload.
  - **Size limits:** All the attached files are subject to the sandbox environment memory limits (up to 4 GiB of RAM in total).
  - **Best practices:** For optimal skill quality, structure and prepare the files in your skill folder following the conventions described on [agentskills.io/home](https://agentskills.io/home) .

To attach a skill from Google Cloud Storage:

### REST

##### Request variables

Before calling the API, make the following replacements:

  - `  PROJECT_ID  ` : Your Google Cloud project ID.
  - `  LOCATION  ` : The regional location of the agent. Only the `global` region is supported.
  - `  AGENT_ID  ` : Target agent ID.
  - `  NEW_GCS_SOURCE_PATH  ` : The Google Cloud Storage bucket path containing your skill folder (for example, `gs://cymbal-bucket-name/my-skill-folder` ).

##### Request JSON body

    {
      "name": "AGENT_ID",
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "gcs",
            "source": "NEW_GCS_SOURCE_PATH",
            "target": "/.agent/skills"
          }
        ],
        "network": {
          "allowlist": [
            { "domain": "*" }
          ]
        }
      }
    }

##### `curl` command

    curl -X PATCH "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID?update_mask=base_environment" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -d '{
          "name": "AGENT_ID",
          "base_environment": {
              "type": "remote",
              "sources": [
                  {
                      "type": "gcs",
                      "source": "NEW_GCS_SOURCE_PATH",
                      "target": "/.agent/skills"
                  }
              ],
              "network": {
                  "allowlist": [
                      { "domain": "*" }
                  ]
              }
          }
      }'

### Python

> **Note:** The `update` method is not yet available in the Python SDK. Use the REST API to update agent skills.

### JavaScript

> **Note:** The `update` method is not yet available in the JavaScript SDK. Use the REST API to update agent skills.

## Delete an agent

To delete a specific custom agent config, send a `DELETE` request. This is a [long-running operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage#get-details-of-lro) and deletes the configuration permanently.

When you delete an agent, provide all necessary information in the URL and don't include a JSON request body.

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION : The region of the agent. Only the `global` region is supported.
  - AGENT\_ID : The ID of the agent you are deleting.

#### HTTP method and URL

    DELETE https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID

#### `curl` command

    curl -X DELETE "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/agents/AGENT_ID" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)"

#### Example Response

    {
      "name": "projects/1234567890/locations/global/operations/234567890123",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2026-05-13T02:15:45.936287Z",
          "updateTime": "2026-05-13T02:15:45.936287Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

### Python

Before running this code, set the variables described in the REST tab.

    from google import genai
    
    client = genai.Client(
        vertexai=True,
        project="PROJECT_ID",
        location="global",
    )
    
    response = client.agents.delete(id="AGENT_ID")
    print(response)

### JavaScript

Before running this code, set the variables described in the REST tab.

    import { GoogleGenAI } from "@google/genai";
    
    const client = new GoogleGenAI({
        vertexai: true,
        project: "PROJECT_ID",
        location: "global",
    });
    
    const response = await client.agents.delete("AGENT_ID");
    console.log(response);

## Get details of a long-running operation

Operations like `CreateAgent` , `UpdateAgent` , and `DeleteAgent` are asynchronous. The initial API response returns a `name` field containing the operation ID. Use `GetOperation` on this ID to poll the progress.

### REST

#### Request variables

Before calling the API, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION : The regional location of the operation. Only the `global` region is supported.
  - OPERATION\_ID : The operation ID extracted from the `name` field in the initial LRO response.

#### HTTP method and URL

    GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/operations/OPERATION_ID

#### `curl` command

    curl -X GET "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/operations/OPERATION_ID" \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)"

### Python

> **Note:** When using the Python SDK, operations like `agents.create()` and `agents.delete()` return the final result directly. Use `client.agents.get(id="AGENT_ID")` to verify provisioning status.

### JavaScript

> **Note:** When using the JavaScript SDK, operations like `agents.create()` and `agents.delete()` return the final result directly. Use `client.agents.get("AGENT_ID")` to verify provisioning status.

## Configure network access

By default, the sandbox disables network access when you create agents using the Agents API. To allow unrestricted access, use `*` .

For example, using `*` in the `allowlist` as shown in the following code gives access to all domains:

    "base_environment": {
        "type": "remote",
        "sources": [
            {
                "type": "skill_registry",
                "source": "SKILL_RESOURCE_NAME",
                "target": "./skills"
            }
        ],
        "network": {
            "allowlist": [{"domain": "*"}]
        }
    }

## What's next

Guide

### [Interact with agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents)

Learn how to interact with agents at runtime, manage session state, and dynamically override configurations.
