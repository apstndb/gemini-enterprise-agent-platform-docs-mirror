---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/cancel_tuning_job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/cancel_tuning_job
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `cancel_tuning_job`

Starts an asynchronous cancellation request for a running GenAI tuning job. The server makes a best effort to cancel the job, but success is not guaranteed. Cancellation does not delete the tuning job resource, but transitions its state to CANCELLED. Use this to stop a job that is no longer needed or was started with incorrect parameters. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. IMPORTANT: This parameter requires the 19-digit numeric ID. Request the full ID if a shorter one is given.

The following sample demonstrate how to use `curl` to invoke the `cancel_tuning_job` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "cancel_tuning_job",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `GenAiTuningService.CancelTuningJob` .

### CancelTuningJobRequest

**JSON representation**

```
{
  "name": string
}
```

| Fields |                                                                                                                                    |
|--------|------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The name of the tuning job to cancel. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}` |

## Output Schema

A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance:

```
service Foo {
  rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty);
}
```

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ❌ \| Open World Hint: ❌
