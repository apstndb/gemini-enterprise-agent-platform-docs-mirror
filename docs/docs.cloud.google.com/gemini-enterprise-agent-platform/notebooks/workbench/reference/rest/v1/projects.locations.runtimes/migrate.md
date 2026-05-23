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

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/runtimes/{runtimeId}`

Authorization requires one or more of the following [IAM](https://cloud.google.com/iam/docs/) permissions on the specified resource `name` :

  - `notebooks.runtimes.get`
  - `notebooks.instances.create`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;network&quot;: string,&quot;subnet&quot;: string,&quot;serviceAccount&quot;: string,&quot;requestId&quot;: string,&quot;postStartupScriptOption&quot;: enum (PostStartupScriptOption)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`network`

`string`

Optional. Name of the VPC that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same VPC, and this field must be empty. Format: `projects/{projectId}/global/networks/{network_id}`

`subnet`

`string`

Optional. Name of the subnet that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same subnet, and this field must be empty. Format: `projects/{projectId}/regions/{region}/subnetworks/{subnetwork_id}`

`serviceAccount`

`string`

Optional. The service account to be included in the Compute Engine instance of the new Workbench Instance when the Runtime uses "single user only" mode for permission. If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used. When the Runtime uses service account mode for permission, it will reuse the same service account, and this field must be empty.

`requestId`

`string`

Optional. Idempotent request UUID.

`postStartupScriptOption`

` enum ( PostStartupScriptOption  ` )

Optional. Specifies the behavior of post startup script during migration.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

Enums

`POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED`

Post startup script option is not specified. Default is POST\_STARTUP\_SCRIPT\_OPTION\_SKIP.

`POST_STARTUP_SCRIPT_OPTION_SKIP`

Not migrate the post startup script to the new Workbench Instance.

`POST_STARTUP_SCRIPT_OPTION_RERUN`

Redownload and rerun the same post startup script as the Google-Managed Notebook.
