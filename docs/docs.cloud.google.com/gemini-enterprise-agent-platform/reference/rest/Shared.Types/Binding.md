---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Binding
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Binding
title: Binding
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Associates `members` , or principals, with a `role` .

Fields

`role` `string`

role that is assigned to the list of `members` , or principals. For example, `roles/viewer` , `roles/editor` , or `roles/owner` .

For an overview of the IAM roles and permissions, see the [IAM documentation](https://cloud.google.com/iam/docs/roles-overview) . For a list of the available pre-defined roles, see [here](https://cloud.google.com/iam/docs/understanding-roles) .

`members[]` `string`

Specifies the principals requesting access for a Google Cloud resource. `members` can have the following values:

  - `allUsers` : A special identifier that represents anyone who is on the internet; with or without a Google account.

  - `allAuthenticatedUsers` : A special identifier that represents anyone who is authenticated with a Google account or a service account. Does not include identities that come from external identity providers (IdPs) through identity federation.

  - `user:{emailid}` : An email address that represents a specific Google account. For example, `alice@example.com` .

<!-- end list -->

  - `serviceAccount:{emailid}` : An email address that represents a Google service account. For example, `my-other-app@appspot.gserviceaccount.com` .

  - `serviceAccount:{projectid}.svc.id.goog[{namespace}/{kubernetes-sa}]` : An identifier for a [Kubernetes service account](https://cloud.google.com/kubernetes-engine/docs/how-to/kubernetes-service-accounts) . For example, `my-project.svc.id.goog[my-namespace/my-kubernetes-sa]` .

  - `group:{emailid}` : An email address that represents a Google group. For example, `admins@example.com` .

<!-- end list -->

  - `domain:{domain}` : The G Suite domain (primary) that represents all the users of that domain. For example, `google.com` or `example.com` .

<!-- end list -->

  - `principal://iam.googleapis.com/locations/global/workforcePools/{poolId}/subject/{subject_attribute_value}` : A single identity in a workforce identity pool.

  - `principalSet://iam.googleapis.com/locations/global/workforcePools/{poolId}/group/{groupId}` : All workforce identities in a group.

  - `principalSet://iam.googleapis.com/locations/global/workforcePools/{poolId}/attribute.{attribute_name}/{attributeValue}` : All workforce identities with a specific attribute value.

  - `principalSet://iam.googleapis.com/locations/global/workforcePools/{poolId}/*` : All identities in a workforce identity pool.

  - `principal://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{poolId}/subject/{subject_attribute_value}` : A single identity in a workload identity pool.

  - `principalSet://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{poolId}/group/{groupId}` : A workload identity pool group.

  - `principalSet://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{poolId}/attribute.{attribute_name}/{attributeValue}` : All identities in a workload identity pool with a certain attribute.

  - `principalSet://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{poolId}/*` : All identities in a workload identity pool.

  - `deleted:user:{emailid}?uid={uniqueid}` : An email address (plus unique identifier) representing a user that has been recently deleted. For example, `alice@example.com?uid=123456789012345678901` . If the user is recovered, this value reverts to `user:{emailid}` and the recovered user retains the role in the binding.

  - `deleted:serviceAccount:{emailid}?uid={uniqueid}` : An email address (plus unique identifier) representing a service account that has been recently deleted. For example, `my-other-app@appspot.gserviceaccount.com?uid=123456789012345678901` . If the service account is undeleted, this value reverts to `serviceAccount:{emailid}` and the undeleted service account retains the role in the binding.

  - `deleted:group:{emailid}?uid={uniqueid}` : An email address (plus unique identifier) representing a Google group that has been recently deleted. For example, `admins@example.com?uid=123456789012345678901` . If the group is recovered, this value reverts to `group:{emailid}` and the recovered group retains the role in the binding.

  - `deleted:principal://iam.googleapis.com/locations/global/workforcePools/{poolId}/subject/{subject_attribute_value}` : Deleted single identity in a workforce identity pool. For example, `deleted:principal://iam.googleapis.com/locations/global/workforcePools/my-pool-id/subject/my-subject-attribute-value` .

`condition` ` object ( Expr  ` )

The condition that is associated with this binding.

If the condition evaluates to `true` , then this binding applies to the current request.

If the condition evaluates to `false` , then this binding does not apply to the current request. However, a different role binding might grant the same role to one or more of the principals in this binding.

To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies) .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;role&quot;: string,&quot;members&quot;: [string],&quot;condition&quot;: {object (Expr)}}</code></pre></td>
</tr>
</tbody>
</table>

## Expr

Represents a textual expression in the Common Expression Language (CEL) syntax. CEL is a C-like expression language. The syntax and semantics of CEL are documented at <https://github.com/google/cel-spec> .

Example (Comparison):

    title: "Summary size limit"
    description: "Determines if a summary is less than 100 chars"
    expression: "document.summary.size() < 100"

Example (Equality):

    title: "Requestor is owner"
    description: "Determines if requestor is the document owner"
    expression: "document.owner == request.auth.claims.email"

Example (Logic):

    title: "Public documents"
    description: "Determine whether the document should be publicly visible"
    expression: "document.type != 'private' && document.type != 'internal'"

Example (data Manipulation):

    title: "Notification string"
    description: "Create a notification string with a timestamp."
    expression: "'New message received at ' + string(document.create_time)"

The exact variables and functions that may be referenced within an expression are determined by the service that evaluates it. See the service documentation for additional information.

Fields

`expression` `string`

Textual representation of an expression in Common Expression Language syntax.

`title` `string`

Optional. title for the expression, i.e. a short string describing its purpose. This can be used e.g. in UIs which allow to enter the expression.

`description` `string`

Optional. description of the expression. This is a longer text which describes the expression, e.g. when hovered over it in a UI.

`location` `string`

Optional. String indicating the location of the expression for error reporting, e.g. a file name and a position in the file.

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
  &quot;expression&quot;: string,
  &quot;title&quot;: string,
  &quot;description&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
