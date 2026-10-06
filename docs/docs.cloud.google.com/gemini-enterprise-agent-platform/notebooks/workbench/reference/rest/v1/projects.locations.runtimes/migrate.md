---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/migrate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/migrate
title: 'Method: projects.locations.runtimes.migrate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Migrate an existing Runtime to a new Workbench Instance.

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
<p>Required. Format: <code>projects/{projectId}/locations/{location}/runtimes/{runtimeId}</code></p>
<p>Authorization requires one or more of the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permissions on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.get</code></li>
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
  "network": string,
  "subnet": string,
  "serviceAccount": string,
  "requestId": string,
  "postStartupScriptOption": enum (PostStartupScriptOption)
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `network`                 | `string` Optional. Name of the VPC that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same VPC, and this field must be empty. Format: `projects/{projectId}/global/networks/{network_id}`                                                                                                                                                                                   |
| `subnet`                  | `string` Optional. Name of the subnet that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same subnet, and this field must be empty. Format: `projects/{projectId}/regions/{region}/subnetworks/{subnetwork_id}`                                                                                                                                                             |
| `serviceAccount`          | `string` Optional. The service account to be included in the Compute Engine instance of the new Workbench Instance when the Runtime uses "single user only" mode for permission. If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used. When the Runtime uses service account mode for permission, it will reuse the same service account, and this field must be empty. |
| `requestId`               | `string` Optional. Idempotent request UUID.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `postStartupScriptOption` | `enum ( `[`PostStartupScriptOption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/migrate#PostStartupScriptOption)` )` Optional. Specifies the behavior of post startup script during migration.                                                                                                                                                                                             |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

| Enums                                    |                                                                                          |
|------------------------------------------|------------------------------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED` | Post startup script option is not specified. Default is POST_STARTUP_SCRIPT_OPTION_SKIP. |
| `POST_STARTUP_SCRIPT_OPTION_SKIP`        | Not migrate the post startup script to the new Workbench Instance.                       |
| `POST_STARTUP_SCRIPT_OPTION_RERUN`       | Redownload and rerun the same post startup script as the Google-Managed Notebook.        |
