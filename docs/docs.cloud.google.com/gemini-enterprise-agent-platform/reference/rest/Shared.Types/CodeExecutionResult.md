---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CodeExecutionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CodeExecutionResult
title: CodeExecutionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

result of executing the [`ExecutableCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content#ExecutableCode) .

Generated only when the `CodeExecution` tool is used.

Fields

`outcome` `enum ( `[`Outcome`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Outcome)` )`

Required. Outcome of the code execution.

`output` `string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

`id` `string`

Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.

**JSON representation**

```
{
  "outcome": enum (Outcome),
  "output": string,
  "id": string
}
```
