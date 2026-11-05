---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-sandboxes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-sandboxes
title: Manage sandboxes
description: Learn how to manage active agent sandboxes, including listing them, viewing their details, pausing, resuming, and deleting them.
data_source: docs.cloud.google.com
---

This page demonstrates how to manage the lifecycle of your sandbox environments using the Python SDK. You can list existing sandboxes, view their details, pause and resume them, or delete them when they are no longer needed.

## Before you begin

To manage sandboxes, you need the following roles on your project:

- Agent Platform User ( `roles/aiplatform.user` )

## Manage sandboxes

You can list, view details for, pause, resume, and delete sandbox environments associated with an Agent Platform instance. Pause and resume let you deschedule compute resources for idle sandboxes and bring them back online later without losing file system state or connection identity. To change an existing sandbox's configuration, you must delete it and create a new one.

### List sandboxes

To list all sandboxes associated with an Agent Platform instance:

```
import agentplatform

client = agentplatform.Client(project='PROJECT_ID', location='LOCATION')
instance_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID'

sandboxes = client.sandboxes.list(name=instance_name)

for sandbox in sandboxes:
    print(sandbox.name)
```

Replace the following:

- `PROJECT_ID` : Your Google Cloud project ID.
- `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
- `INSTANCE_ID` : The Agent Platform instance ID.

### View sandbox details

To view the configuration and status of a specific sandbox:

```
sandbox_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironments/SANDBOX_ID'

sandbox = client.sandboxes.get(name=sandbox_name)
print(sandbox)
```

Replace the following:

- `PROJECT_ID` : Your Google Cloud project ID.
- `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
- `INSTANCE_ID` : The Agent Platform instance ID that contains your sandbox.
- `SANDBOX_ID` : The existing sandbox ID.

The output includes details like creation time, state (for example, `STATE_RUNNING` ), and the sandbox specification.

### Pause a sandbox

Pausing a sandbox releases its compute resources while preserving disk state and connection metadata. Paused sandboxes cost significantly less than running ones and can be resumed in seconds. Use pause when a sandbox is idle for an extended period but you want to preserve session state and connection identity for later use.

Paused sandboxes have the following characteristics:

- Retain their sandbox ID, connection metadata, and any Private Service Connect endpoint.
- Retain all in-container file system state at the moment of pause.
- Transition to `STATE_PAUSED` . Requests to their data-plane endpoint return errors until you resume.

To pause a running sandbox, run the following code:

```
import agentplatform

client = agentplatform.Client(project='PROJECT_ID', location='LOCATION')
sandbox_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironments/SANDBOX_ID'

pause_operation = client.sandboxes.pause(
    name=sandbox_name,
    config={
        "wait_for_completion": True,  # Optional. Blocks until the sandbox reaches STATE_PAUSED.
    },
)
paused_sandbox = pause_operation.response
print(f"Sandbox {paused_sandbox.name} state: {paused_sandbox.state}")  # STATE_PAUSED
```

Replace the following:

- `PROJECT_ID` : Your Google Cloud project ID.
- `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
- `INSTANCE_ID` : The Agent Platform instance ID that contains your sandbox.
- `SANDBOX_ID` : The existing sandbox ID.

### Resume a sandbox

Resuming a paused sandbox brings its compute back online. The sandbox retains the same ID, connection endpoint (including any Private Service Connect service attachment), and file system state it had at the moment of pause. Data-plane requests can be made to the sandbox again as soon as the resume operation completes.

To resume a paused sandbox, run the following code:

```
sandbox_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/sandboxEnvironments/SANDBOX_ID'

resume_operation = client.sandboxes.resume(
    name=sandbox_name,
    config={
        "wait_for_completion": True,  # Optional. Blocks until the sandbox reaches STATE_RUNNING.
    },
)
resumed_sandbox = resume_operation.response
print(f"Sandbox {resumed_sandbox.name} state: {resumed_sandbox.state}")  # STATE_RUNNING
```

Replace the following:

- `PROJECT_ID` : Your Google Cloud project ID.
- `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
- `INSTANCE_ID` : The Agent Platform instance ID that contains your sandbox.
- `SANDBOX_ID` : The paused sandbox ID.

> **Note:** You can only resume sandboxes that are in `STATE_PAUSED` . Attempting to resume a running sandbox returns `FAILED_PRECONDITION` .

### Delete a sandbox

To explicitly delete a sandbox environment and free up resources:

```
client.sandboxes.delete(name=sandbox_name)
print("Sandbox deleted.")
```

> **Note:** Sandboxes are billed while they exist. You can set `config.ttl` when you create the sandbox so that the sandbox is removed automatically when the TTL expires, even if your process crashes before it can call `delete()` .

## Audit logging and monitoring

When you manage and execute commands in sandboxes, Agent Platform records API-level activity in [Cloud Audit Logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/audit-logging) under the `aiplatform.googleapis.com` service name and the `audited_resource` monitored resource type:

- **Admin Activity ( `ADMIN_WRITE` ) logs** : Recorded automatically for control-plane lifecycle mutations, including `CreateSandboxEnvironment` , `PauseSandboxEnvironment` , `ResumeSandboxEnvironment` , `SnapshotSandboxEnvironment` , and `DeleteSandboxEnvironment` (requiring `aiplatform.sandboxEnvironments.*` IAM permissions).
- **Data Access ( `ADMIN_READ` ) logs** : Recorded when enabled for metadata read operations, including `GetSandboxEnvironment` and `ListSandboxEnvironments` .
- **Data Access ( `DATA_WRITE` ) logs** : Recorded when enabled for data-plane command execution and access authorization calls, including `ExecuteSandboxEnvironment` , `BidiExecuteSandboxEnvironment` , `AuthorizeSandboxEnvironmentAccess` , and `ExecuteCode` . For resources protected by VPC Service Controls, request and response payloads are omitted from audit logs.

Keep the following observability and threat detection boundaries in mind:

- **In-container process and stream activity** : Cloud Audit Logs logs the API request that initiates command execution or authorizes a connection, but doesn't log individual child processes spawned inside the container, file system modifications, or subsequent interactive frames sent over an open WebSocket, Chrome DevTools Protocol (CDP), or PTY session.
- **Container `stdout` and `stderr` logging** : Automatic [Cloud Logging collection for Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/logging) (such as `reasoning_engine_stdout` and `reasoning_engine_stderr` ) applies only to the parent `ReasoningEngine` instance and doesn't automatically collect logs from sandbox child resources. Command output ( `stdout` , `stderr` , and exit codes) is returned in the execution response to your parent agent, where you can inspect and write structured entries to Cloud Logging.
- **Threat detection and network inspection** : Sandboxes enforce containment through gVisor kernel isolation and an unprivileged in-sandbox identity with no ambient Google Cloud credentials. To monitor for anomalous behavior or unauthorized network egress, combine `DATA_WRITE` audit logs with [Agent anomaly detection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/audit/agent-anomalies) on the parent agent and route sandbox egress through a [Private Service Connect interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-vpc-sc#control-egress) with VPC Flow Logs, Cloud Next Generation Firewall (Cloud NGFW) rule logging, and Secure Web Proxy inspection. For details, see [Security, identity, and observability boundaries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox#security-boundaries) .
