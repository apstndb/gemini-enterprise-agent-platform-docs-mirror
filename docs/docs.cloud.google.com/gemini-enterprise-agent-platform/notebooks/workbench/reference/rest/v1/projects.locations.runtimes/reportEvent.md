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

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{projectId}/locations/{location}/runtimes/{runtimeId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>iam.permissions.none</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "vmId": string,
  "event": {
    object (Event)
  }
}
```

| Fields  |                                                                                                                                                                                                                  |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `vmId`  | `string` Required. The VM hardware token for authenticating the VM. <https://cloud.google.com/compute/docs/instances/verifying-instance-identity>                                                                |
| `event` | `object ( `[`Event`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/reportEvent#Event)` )` Required. The Event to be reported. |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## Event

The definition of an Event for a managed / semi-managed notebook instance.

**JSON representation**

```
{
  "reportTime": string,
  "type": enum (EventType),
  "details": {
    string: string,
    ...
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reportTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Event report time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `type`       | `enum ( `[`EventType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/reportEvent#EventType)` )` Event type.                                                                                                                                                                                           |
| `details`    | `map (key: string, value: string)` Optional. Event details. This field is used to pass event information. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                          |

## EventType

The definition of the event types.

| Enums                    |                                                                                                                                                                                                    |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `EVENT_TYPE_UNSPECIFIED` | Event is not specified.                                                                                                                                                                            |
| `IDLE`                   | The instance / runtime is idle                                                                                                                                                                     |
| `HEARTBEAT`              | The instance / runtime is available. This event indicates that instance / runtime underlying compute is operational.                                                                               |
| `HEALTH`                 | The instance / runtime health is available. This event indicates that instance / runtime health information.                                                                                       |
| `MAINTENANCE`            | The instance / runtime is available. This event allows instance / runtime to send Host maintenance information to Control Plane. <https://cloud.google.com/compute/docs/gpus/gpu-host-maintenance> |
