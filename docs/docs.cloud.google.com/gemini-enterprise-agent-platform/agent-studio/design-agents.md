---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents
title: Design agents in Agent Studio
description: Learn how to use the low-code visual designer in Agent Studio to build, configure, and test AI agents with integrated models and tools.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> The design agents feature in Agent Studio is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .
> 
> Relationship to Other Terms. The design agents feature in Agent Studio helps Customers design "AI Agents" as defined in the Service Specific Terms and thus the "Agentic AI Services" Service Specific Terms apply. When using Google Search as a tool in Agent Studio, the section entitled "Grounding with Google Search" in the Service Specific Terms also applies, except that the first reference to 'Gemini Enterprise or Agentspace' in subsection (iv) of the "Agentic AI Services" section is replaced with 'Gemini Enterprise Agent Platform'. Please ensure you review the terms of any other tools used in Agent Studio and verify that your agent is appropriate for deployment in Agent Runtime before utilizing that feature.

This page provides an overview of how to use [Agent Studio](https://console.cloud.google.com/agent-platform/studio/agent-designer/) in the Google Cloud console.

Agent Studio is a low-code visual designer within the Google Cloud console that simplifies agent development. You can visually map agent workflows, test responses in real time, and experiment with different configurations before deploying or transitioning to code.

This document provides an overview of Agent Studio and explains how to set up your environment, create and test agents, and deploy them directly to a production runtime.

## Set up your environment

Before using Agent Studio, get [set up with Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#project) .

### Get the required roles

To get the permissions that you need to use Agent Studio, ask your administrator to grant you the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an agent

> **Note:** All configuration files for created agents are stored in the `us-west1` region. If your organization has policies that prevent you from using this region, you might be unable to create an agent. For more information, see [Restrict resource locations](https://docs.cloud.google.com/organization-policy/restrict-locations) .

You can create an agent in Agent Studio using prompts or the flow builder.

### Create an agent using prompts

Use the following steps to create an agent using prompts:

1.  In the Google Cloud console, go to the **Agents** page.  

2.  Click **Create agent** to open the Agent Studio canvas for a new agent.

3.  In the chat box, enter a prompt that describes the purpose and intended behavior of your agent.

4.  Click send .

5.  Depending on your prompt, one of the following happens:
    
      - **Success** : The flow builder updates immediately to display the live preview of your agent, and the chat provides a summary of the modifications made. All changes are saved automatically.
    
      - **Clarification needed** : If your prompt is ambiguous, the assistant asks a clarifying question in the chat to better understand what you want to build.
    
      - **Error:** If the assistant cannot apply your prompt, an error message tells you to rephrase your request.

6.  You can continue to update the agent using prompts or the [flow builder](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#create-agent-flow-builder) .

7.  To save your agent, click **Save** in the canvas header and follow the prompts. For details, see [Save an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#save-agent) .

8.  To test the agent's capabilities and responses as you build your agent, click the **Preview** tab and chat with your agent.

#### Limitations

The following limitations apply when you create an agent using prompts:

| Capability | Limitation                                                                                                |
| ---------- | --------------------------------------------------------------------------------------------------------- |
| Knowledge  | Unable to add knowledge to an agent. You can use the flow builder interface to add knowledge to an agent. |

### Create an agent using the flow builder

Use the following steps to design and test an agent using the flow builder:

1.  In the Google Cloud console, go to the **Agents** page.  

2.  Click **Create agent** to open the Agent Studio canvas. for a new agent.

3.  Design and save your agent in the Agent Studio canvas. You can create a main agent and add subagents. The main agent is always a *local agent* . Subagents can be either *local agents* or *Agent Registry agents* :
    
      - **Local agent:** An agent whose instructions, model, and tools are authored and configured directly within the Agent Studio canvas.
      - **Agent Registry agent:** An agent that is registered and published in [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) . You can use these agents as remote subagents within your main agent's flow.
    
    When designing, you can switch between the following **Flow** and **Preview** tabs:
    
    ### Flow
    
    Create the main agent and subagents by using a visual representation of your agent's workflow and control logic.
    
    1.  Click an agent to open the **Details** panel for that agent. You can also click **Add a subagent** (+) to add subagents.
    
    2.  Configure your main agent and subagents in the **Details** panel:
        
        **For the main agent and local subagents:**
        
        1.  **Name:** Add a name to help identify the agent.
        2.  **Description:** A summary of your agent's purpose.
        3.  **Instructions:** Add instructions to guide your agent.
        4.  **Model:** Select the model to power your agent.
        5.  **Tools:** Click **Add tools** (+) to add tools that let the agent complete tasks. For more information, see [Set up and add tools](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#set-up-tools) .
        
        **For subagents (local or from Agent Registry):**
        
        1.  **Subagent source:** Select the source of the subagent:
            
              - **Local:** Author the subagent's instructions, model, and tools directly on the canvas.
              - **Agent Registry:** Select a registered agent from [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) as a remote subagent. This option is only available after you save the agent. For details, see [Save an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#save-agent) .
            
            When you select a registered agent, its name and description are imported from the registry and become read-only on the canvas. The parent agent routes tasks to this subagent based on its Agent Card.
            
            To run or deploy the parent agent, the parent agent's identity must have permissions to discover and invoke A2A subagents. The permissions dialog handles this action automatically. If you need to manage permissions manually, see [Grant access for Agent-to-Agent (A2A) delegation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#a2a-delegation) .
    
    3.  To save your agent, click **Save** in the canvas header and follow the prompts. For details, see [Save an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#save-agent) .
    
    ### Preview
    
    Chat with your agent in the preview pane to test its capabilities and responses.
    
      - To preview a saved agent, Agent Studio verifies the agent's identity permissions. If required roles are missing, a notification appears. Click **Manage** to open the [permissions dialog](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#permissions-dialog-behavior) and [manage agent identity permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#grant-permissions) .
      - You can inspect the events from each agent run to debug your agent's behavior. For more information, see [Inspect agent events](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#inspect-agent-events) .

4.  Click **Get code** to see your agent code. If you want to continue developing your agent elsewhere, you can copy the code and paste it to a code editor of your choice.
    
    If your agent uses a remote subagent from [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) , the generated Python code includes a call to `AgentRegistry.get_remote_a2a_agent` to dynamically resolve the subagent at runtime.

When your agent is complete, you can deploy it directly from Agent Studio. For more information, see [Deploy an Agent from Agent Studio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#deploy-agent) .

## Inspect agent events

Inspecting events helps you debug your agent's behavior, and troubleshoot and trace your agent's reasoning process and model requests.

You can debug agent execution by inspecting agent events in the **Preview** tab of Agent Studio. This action lets you diagnose issues in the individual events that the agent produces during a run.

To inspect agent events, follow these steps:

1.  Open your agent in the Agent Studio canvas and open the **Preview** tab.

2.  Start a chat with your agent in the preview pane to start a run.

3.  Select an event in the conversation to open its details. The available details depend on the event and can include the following:
    
      - **Author:** The agent or subagent that produced the event. Use the author to identify which subagent performed a step in a multi-agent workflow.
      - **Request and response:** The payload sent to the model and the response returned.
      - **Tool calls:** The arguments passed to tools during the agent's execution.
      - **Metadata:** Additional diagnostic information, such as the model name, token usage, and timestamp.

If the agent returns an error during preview, the error appears in the **Preview** tab so that you can diagnose the issue.

## Save an agent

You must save an agent before you can preview it, deploy it, or upload knowledge files, because an unsaved agent doesn't have an identity yet. This requirement also applies to [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) subagents.

To save an agent for the first time:

1.  In the Agent Studio canvas, click **Save** .

2.  In the **Save Agent** dialog, enter an **Agent name** .

3.  Click **Save** .

After the first save, Agent Studio automatically saves any further changes that you make. If you try to leave the canvas before you save a new agent, Agent Studio prompts you to save it first.

## Update an agent

Use the following steps to update an agent:

1.  In the Google Cloud console, go to the **Agents** page.  

2.  On the agent you want to update, click more\_vert , and then click **Edit** .

3.  Update the agent using prompts or the flow builder.

Agent Studio automatically saves your changes.

## Set up and add tools in Agent Studio

You can configure the following tools for your agent:

  - **Google Search:** Lets the agent perform web searches using Google Search. Toggled on by default.

  - **URL context:** Lets the model analyze URLs from prompts sent to the agent. Toggled on by default.

  - **Agent Search Data Store:** Click **Add** (+) to let your agent access information that has been indexed in your Agent Search data store.
    
      - **Project Number:** The Google Cloud project number associated with your Agent Search data store. [View your project number](https://console.cloud.google.com/welcome) .
    
      - **Location:** The [location](https://console.cloud.google.com/gen-app-builder/data-stores) of your data store.
    
      - **Data Store ID:** Firestore in Datastore mode (Datastore) ID of the data to include. [View a list of your data stores and IDs](https://console.cloud.google.com/gen-app-builder/data-stores) .
    
      - **Collection ID** : Collection ID of the data to include. [View a list of your data stores and collection IDs](https://console.cloud.google.com/gen-app-builder/data-stores) . If your data store doesn't have a Collection ID, enter `default_collection` .
    
    If you don't have an existing data store, see [Get started with custom search](https://docs.cloud.google.com/generative-ai-app-builder/docs/try-enterprise-search#create_a_data_store) to create one. Then grant service account access to Agent Search:
    
    1.  In the Google Cloud console, go to the **IAM** page.  
    
    2.  Click **Grant access** .
    
    3.  In the **New principals** field, enter the following service account information:
        
        `service- PROJECT_NUMBER @gcp-sa-aiplatform-re.iam.gserviceaccount.com` .
    
    4.  Select **+ Add roles** . Search for and select **Discovery Engine User** . Click **Apply** and then **Save** .

  - **MCP Server:** Connect a Model Context Protocol (MCP) server directly.
    
    1.  To add MCP tools by connecting to an MCP server, click **Add** (+) next to **MCP Server** .
    2.  **MCP display name:** Enter a name for your MCP server.
    3.  **Endpoint URL:** Enter an endpoint URL for the MCP server.
    4.  **Authentication:** Autofilled as **None** . Agent Studio only supports MCP servers that don't require authentication.
    
    Your agent can use all tools in your connected MCP server.

## Ground agents with knowledge files

Upload static reference documents to ground your agent's responses in Agent Studio:

1.  Select the parent agent node on the canvas where you want to attach reference files. Note that you can't attach knowledge files to subagents.

2.  In the node's **Details** panel, locate the **Knowledge** section. The **Knowledge** section appears only after you save the agent for the first time. For details, see [Save an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#save-agent) .

3.  Click the file upload component and browse to select your reference file. You can attach up to 10 files per agent. The file size must not exceed 2 megabytes (2 MB). The upload canvas supports the following file types:
    
      - PDF
      - Plain text

4.  In the canvas header, click **Save** to store files in a dedicated Cloud Storage bucket under a path prefix matching the parent agent's `AGENT_ID` .
    
    > **Caution:** Uploaded knowledge files are stored in a Cloud Storage bucket in your Google Cloud project. Anyone with access to the project or that bucket can view these files. Don't upload files that contain information you don't want shared with all principals who have access to the project.
    
    The permission dialog grants the Storage Object Viewer role ( `roles/storage.objectViewer` ) to the agent's identity on the bucket.

5.  Navigate to the **Preview** tab and submit a test query to verify that the agent grounds its response using the file's contents without hallucinating.

6.  Optional: You can click **Get code** to copy the generated Python code ( `agent.py` ) and inspect the grounding file configuration. You can skip this step.

## Manage agent identity permissions

Each agent in Agent Studio has a unique identity, which acts as an IAM principal to access other Google Cloud resources.

The principal format is:

    principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/REASONING_ENGINE_ID

Replace the following:

  - `  ORGANIZATION_ID  ` : the numeric ID of your organization.
  - `  PROJECT_NUMBER  ` : the project number of your Google Cloud project.
  - `  LOCATION  ` : the region where your agent is deployed.
  - `  REASONING_ENGINE_ID  ` : the resource ID of your reasoning engine.

For more context on agent identities, see [Create an agent with agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity) and [Agent identity overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) .

### Permissions dialog behavior

When you click **Deploy** or open the **Preview** tab for a saved agent, Agent Studio automatically checks if the agent's identity has the set of IAM roles required to run successfully. Some missing permissions could cause your agent to fail if they aren't set up correctly. Granting these permissions to the agent's identity helps it work as expected.

If the system detects any permission issues, the permissions dialog displays an error message.

  - **Missing roles:** If required roles are missing, a dialog appears listing the detailed roles. Click **Grant All** in the dialog to automatically grant all necessary roles to the agent's identity in a single action. To preview or deploy the agent without granting the roles, click **Proceed anyway** .
  - **All roles granted:** If all required roles are already granted, the permissions dialog does not appear.
  - **Unsaved agents:** Unsaved agents do not have an identity yet. The permissions dialog does not appear, and the **Preview** tab and **Deploy** options are disabled until you save the agent.

#### Required roles

The permissions dialog automatically grants the following list of roles:

  - `roles/storage.objectViewer` : Required if the agent uses uploaded files. This role must be granted on the specific Cloud Storage bucket for agent files (for example, `{projectNumber}_{location}_agent_studio_files` ).
  - `roles/mcp.toolUser` : Required if the agent utilizes an Agent Registry MCP tool.
  - `roles/agentregistry.viewer` : Required if the agent uses an Agent Registry MCP tool or subagent.
  - `roles/iamconnectors.user` : Required if an Agent Registry MCP tool specifies an `authProviderName` .
  - `roles/aiplatform.viewer` : Required if the agent invokes remote subagents through Agent-to-Agent (A2A) delegation.

### Manage roles manually in the Google Cloud console

The permissions dialog automatically grants required roles. However, if you prefer to manage roles manually or need to troubleshoot permission issues, follow these steps:

1.  Copy the agent's unique identity principal. In the Agent Studio canvas header, click the drop-down menu next to the agent name, and copy the principal string.
    
    The principal format looks like the following example:
    
    ` principal://agents.global.org- ORG_ID .system.id.goog/resources/aiplatform/projects/ PROJECT_NUMBER /locations/ LOCATION /reasoningEngines/ REASONING_ENGINE_ID  `

2.  In the Google Cloud console, go to **IAM** :

3.  Search for the agent identity principal in the principal list. You can search using the specific `  REASONING_ENGINE_ID  ` from the end of the principal string. To get the agent identity principal, you have one of the following options:
    
      - If the agent identity principal is already listed, click edit **Edit principal** next to the agent identity.
      - If the agent identity principal is not listed, click **Grant access** to add it as a new principal.

4.  Add or modify the required roles for your configuration, such as `roles/storage.objectViewer` or `roles/mcp.toolUser` .

5.  Click **Save** .

Depending on your configuration, you might need to manually grant additional roles that the permissions dialog doesn't automatically handle. For example, if your registered MCP tool accesses other Google Cloud resources, such as querying data from BigQuery, you must manually grant the necessary roles, such as the BigQuery Data Viewer ( `roles/bigquery.dataViewer` ) role, to the agent's identity.

## Deploy an agent from Agent Studio

After you create and preview an agent, you can deploy it to production. Use the following steps to deploy an agent from Agent Studio:

1.  From the **Agents** list page, click the agent you want to deploy. The Agent detail page appears for the selected agent.

2.  Click **Deploy** to open the **Deploy to an Agent Runtime instance** dialog.
    
    If the agent's identity is missing required permissions, the [permissions dialog](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#permissions-dialog-behavior) appears and handles this action automatically. If you need to manage permissions manually, see [Manage agent identity permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#grant-permissions) and [Grant access for Agent-to-Agent (A2A) delegation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#a2a-delegation) .

3.  In the deployment configuration window, configure the following options:
    
      - **Display name** and **Description** : Edit the display name and, optionally, add a description for your agent.
      - **Deploy as A2A** : Select this checkbox to deploy the agent as an Agent-to-Agent (A2A) asset that other agents can reuse. For standalone applications, leave the checkbox unselected to package the agent as a standard ADK application.

4.  Select a deployment region from the list of available regions, then click **OK** .

5.  Click **Deploy** .

Deployment creates a new runtime instance and can take up to five minutes to complete. Upon success, a message appears on the **Flow** tab of the Agent Studio canvas. Your agent is now available in production and can integrate securely with your external apps.

## View a deployed agent

To view your deployed agent:

1.  In the Google Cloud console, go to the Agent Platform **Deployments** page.  

2.  Use the **Region** list to filter by deployment region.

3.  Deployed agents that are part of the selected project appear in the list.

4.  Click the name of the specified agent. The **Metrics** page for the agent opens.

5.  Select the **Playground** tab to test your agent.

6.  Enter a test query in the chat pane to verify that the agent runs successfully.

For more information on available metrics for your agent, see [View metrics for your deployed agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/monitoring#view-metrics) .
