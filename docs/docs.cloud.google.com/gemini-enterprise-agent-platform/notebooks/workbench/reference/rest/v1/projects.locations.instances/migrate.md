---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/migrate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/migrate
title: 'Method: projects.locations.instances.migrate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Migrates an existing User-Managed Notebook to Workbench Instances.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{name}:migrate`

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
<p>Authorization requires one or more of the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permissions on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.get</code></li>
<li><code>notebooks.instances.create</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "postStartupScriptOption": enum (PostStartupScriptOption)
}
```

| Fields                    |                                                                                                                                                                                                                                                                                       |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `postStartupScriptOption` | `enum ( `[`PostStartupScriptOption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/migrate#PostStartupScriptOption)` )` Optional. Specifies the behavior of post startup script during migration. |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

| Enums                                    |                                                                                          |
|------------------------------------------|------------------------------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED` | Post startup script option is not specified. Default is POST_STARTUP_SCRIPT_OPTION_SKIP. |
| `POST_STARTUP_SCRIPT_OPTION_SKIP`        | Not migrate the post startup script to the new Workbench Instance.                       |
| `POST_STARTUP_SCRIPT_OPTION_RERUN`       | Redownload and rerun the same post startup script as the User-Managed Notebook.          |
