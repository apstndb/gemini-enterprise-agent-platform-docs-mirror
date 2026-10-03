---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/resume_notebook_execution_schedule
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/resume_notebook_execution_schedule
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `resume_notebook_execution_schedule`

Use this tool to resume a paused notebook execution schedule. Format: 'projects/{project_id}/locations/{region}/schedules/{schedule_id}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `resume_notebook_execution_schedule` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "resume_notebook_execution_schedule",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `ScheduleService.ResumeSchedule` .

### ResumeScheduleRequest

**JSON representation**

```
{
  "name": string,
  "catchUp": boolean
}
```

| Fields    |                                                                                                                                                                                                                                                                                      |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`    | `string` Required. The name of the Schedule resource to be resumed. Format: `projects/{project}/locations/{location}/schedules/{schedule}`                                                                                                                                           |
| `catchUp` | `boolean` Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update `Schedule.catch_up` field. Default to false. |

## Output Schema

A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance:

```
service Foo {
  rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty);
}
```

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ❌ \| Open World Hint: ❌
