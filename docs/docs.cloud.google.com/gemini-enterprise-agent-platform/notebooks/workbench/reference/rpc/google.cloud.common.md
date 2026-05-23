---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.common
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.common
title: Package google.cloud.common
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  OperationMetadata  ` (message)

## OperationMetadata

Represents the metadata of the long-running operation.

Fields

`create_time`

`  Timestamp  `

Output only. The time the operation was created.

`end_time`

`  Timestamp  `

Output only. The time the operation finished running.

`target`

`string`

Output only. Server-defined resource path for the target of the operation.

`verb`

`string`

Output only. Name of the verb executed by the operation.

`status_detail`

`string`

Output only. Human-readable status of the operation, if any.

`cancel_requested`

`bool`

Output only. Identifies whether the user has requested cancellation of the operation. Operations that have been cancelled successfully have `  google.longrunning.Operation.error  ` value with a `  google.rpc.Status.code  ` of `1` , corresponding to `Code.CANCELLED` .

`api_version`

`string`

Output only. API version used to start the operation.
