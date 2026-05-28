---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/snapshots
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/snapshots
title: Manage snapshots
description: Guide on how to use sandbox snapshots in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Sandbox snapshots in Gemini Enterprise Agent Platform let you save the current state of a sandbox and restore it later. This is useful for lifecycle management tasks such as restoring a known good state or exploring variation branches.

Snapshots provide several benefits for managing your agent workflows:

  - **State persistence** : Save the exact state of the sandbox, including installed libraries, file system changes, and memory state.
  - **Efficiency** : Instead of recreating a complex environment from scratch, you can restore it from a snapshot in seconds.
  - **Checkpointing** : Create checkpoints during a long-running agent task to allow recovery if something goes wrong.
  - **Branching** : Create multiple sandboxes from the same snapshot to explore different paths or test variations.

### Limitations

You cannot restore a sandbox snapshot to a new sandbox environment if any of the following conditions are true:

  - The new sandbox uses a different server architecture (for example, `amd64` versus `arm64` ).
  - The new sandbox uses a different sandbox runtime version (for example, after a GKE cluster upgrade).
  - The new sandbox uses a different container image URI.

## Create a snapshot

To create a snapshot of a sandbox, use the Python SDK:

    import vertexai
    
    client = vertexai.Client(project='PROJECT_ID', location='LOCATION')
    sandbox_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironments/SANDBOX_ID'
    
    snapshot_operation = client.agent_engines.sandboxes.snapshots.create(
        source_sandbox_environment_name=sandbox_name,
        config={
            "display_name": "DISPLAY_NAME",
            "ttl": "3600s",
        }
    )
    print(f"Snapshot creation initiated: {snapshot_operation.name}")

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your resource. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID.
  - `SANDBOX_ID` : The existing sandbox ID to create a snapshot for.
  - `DISPLAY_NAME` : A descriptive display name for your snapshot.

## Restore from a snapshot

You can restore a sandbox state by referencing a saved snapshot when creating a new sandbox environment:

    agent_instance_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID
    snapshot_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironments/SANDBOX_ID'
    
    # Restore from a snapshot
    new_sandbox_operation = client.agent_engines.sandboxes.create(
        name=agent_instance_name,
        config={
            "display_name": "restored-sandbox",
            "sandbox_environment_snapshot": snapshot_name,
        }
    )

## List snapshots

To list all sandbox snapshots associated with an Agent Platform instance:

    snapshots_response = client.agent_engines.sandboxes.snapshots.list(name=agent_instance_name)
    
    for snapshot in snapshots_response.sandbox_environment_snapshots:
        print(snapshot.name)

## View snapshot details

To view the configuration of a specific sandbox snapshot:

    snapshot = client.agent_engines.sandboxes.snapshots.get(name=snapshot_name)
    print(snapshot)

## Delete a snapshot

To explicitly delete a sandbox snapshot when they are no longer needed:

    client.agent_engines.sandboxes.snapshots.delete(name=snapshot_name)
    print("Snapshot deleted.")
