---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/getInstanceHealth
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/getInstanceHealth
title: 'Method: projects.locations.instances.getInstanceHealth'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Checks whether a notebook instance is healthy.

### HTTP request

`GET https://notebooks.googleapis.com/v1/{name}:getInstanceHealth`

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
<p>Required. Format: <code>projects/{projectId}/locations/{location}/instances/{instanceId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.getHealth</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

Response for checking if a notebook instance is healthy.

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "healthState": enum (HealthState),
  "healthInfo": {
    string: string,
    ...
  }
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `healthState` | `enum ( `[`HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/getInstanceHealth#HealthState)` )` Output only. Runtime healthState.                                                                                                                                                                         |
| `healthInfo`  | `map (key: string, value: string)` Output only. Additional information about instance health. Example: healthInfo": { "docker_proxy_agent_status": "1", "docker_status": "1", "jupyterlab_api_status": "-1", "jupyterlab_status": "-1", "updated": "2020-10-18 09:40:03.573409" } An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## HealthState

If an instance is healthy or not.

| Enums                      |                                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | The instance substate is unknown.                                                                                          |
| `HEALTHY`                  | The instance is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.       |
| `UNHEALTHY`                | The instance is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state. |
| `AGENT_NOT_INSTALLED`      | The instance has not installed health monitoring agent. Applies to ACTIVE state.                                           |
| `AGENT_NOT_RUNNING`        | The instance health monitoring agent is not running. Applies to ACTIVE state.                                              |
