---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TestIamPermissionsRequest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TestIamPermissionsRequest
title: TestIamPermissionsRequest
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Request message for `featurestores.testIamPermissions` method.

Fields

`resource` `string`

REQUIRED: The resource for which the policy detail is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

`permissions[]` `string`

The set of permissions to check for the `resource` . Permissions with wildcards (such as `*` or `storage.*` ) are not allowed. For more information see [IAM Overview](https://cloud.google.com/iam/docs/overview#permissions) .

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
  &quot;resource&quot;: string,
  &quot;permissions&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
