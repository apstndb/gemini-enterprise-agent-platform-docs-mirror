---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/cancel_tuning_job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/cancel_tuning_job
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `cancel_tuning_job`

Starts an asynchronous cancellation request for a running GenAI tuning job. The server makes a best effort to cancel the job, but success is not guaranteed. Cancellation does not delete the tuning job resource, but transitions its state to CANCELLED. Use this to stop a job that is no longer needed or was started with incorrect parameters. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. IMPORTANT: This parameter requires the 19-digit numeric ID. Request the full ID if a shorter one is given.

The following sample demonstrate how to use `curl` to invoke the `cancel_tuning_job` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;cancel_tuning_job&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `GenAiTuningService.CancelTuningJob` .

### CancelTuningJobRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the tuning job to cancel. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`

## Output Schema

A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance:

    service Foo {
      rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty);
    }

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ❌ | Open World Hint: ❌
