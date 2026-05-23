---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/reportEvent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/reportEvent
title: 'Method: projects.locations.runtimes.reportEvent'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Reports and processes a runtime event.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{name}:reportEvent`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/runtimes/{runtimeId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `iam.permissions.none`

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;vmId&quot;: string,&quot;event&quot;: {object (Event)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`vmId`

`string`

Required. The VM hardware token for authenticating the VM. <https://cloud.google.com/compute/docs/instances/verifying-instance-identity>

`event`

` object ( Event  ` )

Required. The Event to be reported.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## Event

The definition of an Event for a managed / semi-managed notebook instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reportTime&quot;: string,&quot;type&quot;: enum (EventType),&quot;details&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reportTime`

` string ( Timestamp  ` format)

Event report time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`type`

` enum ( EventType  ` )

Event type.

`details`

`map (key: string, value: string)`

Optional. Event details. This field is used to pass event information.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

## EventType

The definition of the event types.

Enums

`EVENT_TYPE_UNSPECIFIED`

Event is not specified.

`IDLE`

The instance / runtime is idle

`HEARTBEAT`

The instance / runtime is available. This event indicates that instance / runtime underlying compute is operational.

`HEALTH`

The instance / runtime health is available. This event indicates that instance / runtime health information.

`MAINTENANCE`

The instance / runtime is available. This event allows instance / runtime to send Host maintenance information to Control Plane. <https://cloud.google.com/compute/docs/gpus/gpu-host-maintenance>
