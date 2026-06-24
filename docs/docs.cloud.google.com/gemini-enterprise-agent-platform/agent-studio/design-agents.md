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

Use the following steps to design and test an agent in Agent Studio:

1.  In the Google Cloud console, go to the **Agents** page.  

2.  Click **Create agent** to open the Agent Studio canvas for a new agent.

3.  Design your agent in the Agent Studio canvas. You can switch between the following tabs:
    
      - **Flow:** Create the main agent and subagents by using a visual representation of your agent's workflow and control logic.
        
        1.  Click an agent to open the **Details** panel for that agent. You can also click **Add a subagent** (+) to add subagents.
        
        2.  Configure your main agent and subagents in the **Details** panel:
            
            1.  **Name:** Add a name to help identify the agent.
            
            2.  **Description:** A summary of your agent's purpose.
            
            3.  **Instructions:** Add instructions to guide your agent.
            
            4.  **Model:** Select the model to power your agent.
            
            5.  **Tools:** Click **Add tools** (+) to add tools that let the agent complete tasks. For more information, see [Set up and add tools](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#set-up-tools) .
    
      - **Preview:** Test the agent's capabilities and response as you build your agent. Chat with your agent to test its capabilities. To preview a saved agent, Agent Studio verifies the agent's identity permissions. If any required permissions are missing, a permissions dialog is displayed. Unsaved agents don't have an identity yet, so the **Preview** and **Deploy** options are disabled until you save the agent. For more information, see [Grant permissions to agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#grant-permissions) .

4.  Click **Get code** to see your agent code. If you want to continue developing your agent elsewhere, you can copy the code and paste it to a code editor of your choice. See [ADK tutorials](https://google.github.io/adk-docs/get-started/python/) for more options to continue developing your agent.

Once your agent is complete, you can deploy it directly from Agent Studio. For more information, see [Deploy an Agent from Agent Studio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#deploy-agent) .

## Set up and add tools in Agent Studio

You can configure the following tools for your agent:

  - **Google Search:** Lets the agent perform web searches using Google Search. Toggled on by default.

  - **URL context:** Let the model analyze URLs from prompts sent to the agent. Toggled on by default.

  - **Agent Platform Search Data Store:** Click **Add** (+) to let your agent access information that has been indexed in your Agent Search data store.
    
      - **Project Number:** The Google Cloud project number associated with your Agent Search data store. [View your project number](https://console.cloud.google.com/welcome) .
    
      - **Location:** The [location](https://console.cloud.google.com/gen-app-builder/data-stores) of your data store.
    
      - **Data Store ID:** Firestore in Datastore mode (Datastore) ID of the data to include. [View a list of your data stores and IDs](https://console.cloud.google.com/gen-app-builder/data-stores) .
    
      - **Collection ID** : Collection ID of the data to include. [View a list of your data stores and collection IDs](https://console.cloud.google.com/gen-app-builder/data-stores) . If your data store doesn't have a Collection ID, enter `default_collection` .
    
    If you don't have an existing data store, see [Get started with custom search](https://docs.cloud.google.com/generative-ai-app-builder/docs/try-enterprise-search#create_a_data_store) to create one. Then grant service account access to Agent Platform Search:
    
    1.  In the Google Cloud console, go to the **IAM** page.  
    
    2.  Click **Grant access** .
    
    3.  In the **New principals** field, enter the following service account information: `service- PROJECT_NUMBER @gcp-sa-aiplatform-re.iam.gserviceaccount.com` .
    
    4.  Select **+ Add roles** . Search for and select **Discovery Engine User** . Click **Apply** and then **Save** .

  - **MCP Server:** Click **Add** (+) to add MCP tools by connecting to an MCP server.
    
    1.  **MCP display name:** Enter a name for your MCP server.
    
    2.  **Endpoint URL:** Enter an endpoint URL for the MCP server.
    
    3.  **Authentication:** Autofilled as **None** . Agent Studio only supports MCP servers that don't require authentication.
    
    Your agent can use all tools in your connected MCP server.

## Grant permissions to agent identity

> **Preview**
> 
> The permissions dialog and automatic role-granting features are in **Preview** and subject to change.

Each agent in Agent Studio has a unique SPIFFE identity, which acts as an IAM principal for accessing other Google Cloud resources.

The principal format is:

    principal://agents-nonprod.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/REASONING_ENGINE_ID

Replace the following:

  - `  ORGANIZATION_ID  ` : the numeric ID of your organization.
  - `  PROJECT_NUMBER  ` : the project number of your Google Cloud project.
  - `  LOCATION  ` : the region where your agent is deployed.
  - `  REASONING_ENGINE_ID  ` : the resource ID of your reasoning engine.

For more context on agent identities, see [Create an agent with agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity) and [Agent identity overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) .

### Permissions dialog behavior

When you click **Deploy** or open the **Preview** tab for a saved agent, Agent Studio automatically checks if the agent's identity has the required IAM roles based on the tools you have configured.

  - **Missing roles:** If required roles are missing, a dialog appears listing the detailed roles. Click **Grant All** in the dialog to automatically grant all necessary roles to the agent's identity in a single action.
  - **All roles granted:** If all required roles are already granted, the permissions dialog does not appear.
  - **Unsaved agents:** Unsaved agents do not have an identity yet. The permissions dialog does not appear, and the **Preview** tab and **Deploy** options are disabled until you save the agent.

### Required roles

The specific roles requested in the dialog depend on the agent's configuration:

  - `roles/storage.objectViewer` : Required if the agent uses uploaded or draft files. This role is granted on the specific Cloud Storage bucket for agent files (for example, `{projectNumber}_{location}_agent_studio_files` ).
  - `roles/mcp.toolUser` : Required if the agent utilizes a Model Context Protocol (MCP) tool, including tools from the Agent Registry.
  - `roles/agentregistry.viewer` : Potentially required for agents using an Agent Registry MCP tool. (Note: This role might be removed in the future.)
  - `roles/iamconnectors.user` : Required if an Agent Registry MCP tool specifies an `authProviderName` .

### Roles not automatically handled

The following role isn't automatically handled by this dialog:

  - `roles/discoveryengine.viewer` : The Vertex AI Search tool has been deprecated in favor of Agent Registry. To grant access to Vertex AI Search data stores, you must manually grant the **Discovery Engine User** role to the agent's service account. For details, see [Set up and add tools](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents#set-up-tools) .

## Deploy an Agent from Agent Studio

Once you create and preview an agent, you can deploy it to production. Use the following steps to deploy an agent from Agent Studio:

1.  From the **Agents** list page, click the agent you want to deploy. The Agent detail page appears for the selected agent.

2.  Click **Deploy** to open the **Deploy to an Agent Runtime instance** dialog.

3.  (Optional) Edit the **Display name** or **Description** for your agent.

4.  Select a deployment region from the list of available regions, then click **OK** .

5.  Click **Deploy** .

Deployment creates a new runtime instance and can take up to five minutes to complete. Upon success, a message appears on the **Flow** tab of the Agent Studio canvas. Your agent is now available in production and can integrate securely with your external apps.

## View a deployed agent

To view your deployed agent:

1.  In the Google Cloud console, go to the **Agent Platform** page.  

2.  Use the **Region** list to filter by deployment region.

3.  Deployed agents that are part of the selected project appear in the list.

4.  Click the name of the specified agent. The **Metrics** page for the agent opens.

For more information on available metrics for your agent, see [View metrics for your deployed agent](https://docs.cloud.google.com/agent-builder/agent-engine/manage/overview#view-metrics) .
