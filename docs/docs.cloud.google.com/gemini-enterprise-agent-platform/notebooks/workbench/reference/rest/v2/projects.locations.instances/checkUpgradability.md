---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/checkUpgradability
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/checkUpgradability
title: 'Method: projects.locations.instances.checkUpgradability'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Checks whether a notebook instance is upgradable.

### HTTP request

`GET https://notebooks.googleapis.com/v2/{notebookInstance}:checkUpgradability`

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
<td><code>notebookInstance</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{projectId}/locations/{location}/instances/{instanceId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>notebookInstance</code> :</p>
<ul>
<li><code>notebooks.instances.checkUpgradability</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

Response for checking if a notebook instance is upgradeable.

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "upgradeable": boolean,
  "upgradeVersion": string,
  "upgradeInfo": string,
  "upgradeImage": string
}
```

| Fields           |                                                                                                                                                                     |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `upgradeable`    | `boolean` If an instance is upgradeable.                                                                                                                            |
| `upgradeVersion` | `string` The version this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.             |
| `upgradeInfo`    | `string` Additional information about upgrade.                                                                                                                      |
| `upgradeImage`   | `string` The new image self link this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
