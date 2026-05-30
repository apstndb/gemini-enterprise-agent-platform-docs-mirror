---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-sandboxes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-sandboxes
title: Manage sandboxes
description: Learn how to manage active agent sandboxes, including listing them, viewing their details, and deleting them.
data_source: docs.cloud.google.com
---

This page demonstrates how to manage the lifecycle of your active sandbox environments using the Python SDK. You can list existing sandboxes, view their details, or delete them when they are no longer needed.

## Before you begin

To manage sandboxes, you need the following roles on your project:

  - Agent Platform User ( `roles/aiplatform.user` )

## Manage sandboxes

You can list, view details for, and delete active sandbox environments associated with an Agent Platform instance. To change an existing sandbox's configuration, you must delete it and create a new one.

### List sandboxes

To list all sandboxes associated with an Agent Platform instance:

    import vertexai
    
    client = vertexai.Client(project='<var>PROJECT_ID</var>', location='<var>LOCATION</var>')
    instance_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID'
    
    sandboxes = client.agent_engines.sandboxes.list(name=instance_name)
    
    for sandbox in sandboxes:
        print(sandbox.name)

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID.

### View sandbox details

To view the configuration and status of a specific sandbox:

    sandbox_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironments/SANDBOX_ID'
    
    sandbox = client.agent_engines.sandboxes.get(name=sandbox_name)
    print(sandbox)

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID that contains your sandbox.
  - `SANDBOX_ID` : The existing sandbox ID.

The output includes details like creation time, state (e.g., `STATE_RUNNING` ), and the sandbox specification.

### Delete a sandbox

To explicitly delete a sandbox environment and free up resources:

    client.agent_engines.sandboxes.delete(name=sandbox_name)
    print("Sandbox deleted.")
