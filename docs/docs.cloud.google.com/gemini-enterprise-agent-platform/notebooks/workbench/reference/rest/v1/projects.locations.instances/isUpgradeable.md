---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/isUpgradeable
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/isUpgradeable
title: 'Method: projects.locations.instances.isUpgradeable'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Checks whether a notebook instance is upgradable.

### HTTP request

`GET https://notebooks.googleapis.com/v1/{notebookInstance}:isUpgradeable`

### Path parameters

Parameters

`notebookInstance`

`string`

Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `notebookInstance` :

  - `notebooks.instances.checkUpgradability`

### Query parameters

Parameters

`type`

` enum ( UpgradeType  ` )

Optional. The optional UpgradeType. Setting this field will search for additional compute images to upgrade this instance.

### Request body

The request body must be empty.

### Response body

Response for checking if a notebook instance is upgradeable.

If successful, the response body contains data with the following structure:

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
  &quot;upgradeable&quot;: boolean,
  &quot;upgradeVersion&quot;: string,
  &quot;upgradeInfo&quot;: string,
  &quot;upgradeImage&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`upgradeable`

`boolean`

If an instance is upgradeable.

`upgradeVersion`

`string`

The version this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.

`upgradeInfo`

`string`

Additional information about upgrade.

`upgradeImage`

`string`

The new image self link this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
