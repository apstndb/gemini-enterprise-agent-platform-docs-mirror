---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setIamPolicy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setIamPolicy
title: 'Method: projects.locations.instances.setIamPolicy'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Sets the access control policy on the specified resource. Replaces any existing policy.

Can return `NOT_FOUND` , `INVALID_ARGUMENT` , and `PERMISSION_DENIED` errors.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{resource}:setIamPolicy`

### Path parameters

Parameters

`resource`

`string`

REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;policy&quot;: {object (Policy)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`policy`

` object ( Policy  ` )

REQUIRED: The complete policy to be applied to the `resource` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them.

### Response body

If successful, the response body contains an instance of `  Policy  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
