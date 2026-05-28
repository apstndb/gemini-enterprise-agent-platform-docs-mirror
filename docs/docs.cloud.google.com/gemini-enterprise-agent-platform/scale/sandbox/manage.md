---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage
title: Manage sandboxes, templates, and snapshots
description: Learn how to manage agent sandboxes, sandbox templates, and sandbox snapshots, including listing, viewing details, and deleting.
data_source: docs.cloud.google.com
---

This page demonstrates how to manage the lifecycle of your sandbox environments, sandbox templates, and sandbox snapshots using the Python SDK. You can list existing resources, view their details, or delete them when they are no longer needed.

## Before you begin

To manage sandboxes and templates, you need the following roles on your project:

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
  - `SANDBOX_ID` : The existing sandbox ID to create a snapshot for.

The output includes details like creation time, state (e.g., `STATE_RUNNING` ), and the sandbox specification.

### Delete a sandbox

To explicitly delete a sandbox environment and free up resources:

    client.agent_engines.sandboxes.delete(name=sandbox_name)
    print("Sandbox deleted.")

## Manage sandbox templates

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Sandbox templates serve as blueprints for custom container sandboxes. You can list, view, and delete these templates.

To modify a template's configuration (such as changing the container image), delete the existing template and create a new one with the updated configuration.

### List templates

To list all sandbox templates associated with an Agent Platform instance:

    templates_response = client.agent_engines.sandboxes.templates.list(name=instance_name)
    
    for template in templates_response.sandbox_environment_templates:
        print(template.name)

### View template details

To view the configuration of a specific sandbox template:

    template_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/SandboxEnvironmentTemplate/TEMPLATE_ID'
    
    template = client.agent_engines.sandboxes.templates.get(name=template_name)
    print(template)

### Delete a template

To delete a sandbox template:

    client.agent_engines.sandboxes.templates.delete(name=template_name)
    print("Template deleted.")

> **Note:** Deactivating a template is done by deleting it. You cannot delete a template if a warm pool is actively using it (meaning the template is being created), or if sandboxes are being created from it.

## Manage snapshots

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Sandbox snapshots preserve the state of your sandbox environment. You can list all snapshots, view details of a specific snapshot, or delete them using the Python SDK.

### List snapshots

To list all sandbox snapshots associated with an Agent Platform instance:

    snapshots = client.agent_engines.sandboxes.snapshots.list(name=instance_name)
    
    print(f"Size of sandbox snapshot list: {len(snapshots)}")
    for snapshot in snapshots:
        print(snapshot)

### View snapshot details

To view details of a specific sandbox snapshot:

    snapshot_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironmentSnapshots/SNAPSHOT_ID'
    
    snapshot = client.agent_engines.sandboxes.snapshots.get(name=snapshot_name)
    print(snapshot)

Replace `SNAPSHOT_ID` with the ID of your specific sandbox snapshot.

### Delete a snapshot

To delete a sandbox snapshot that is no longer needed:

    snapshot_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironmentSnapshots/SNAPSHOT_ID'
    
    client.agent_engines.sandboxes.snapshots.delete(name=snapshot_name)
    print("Snapshot deleted.")
