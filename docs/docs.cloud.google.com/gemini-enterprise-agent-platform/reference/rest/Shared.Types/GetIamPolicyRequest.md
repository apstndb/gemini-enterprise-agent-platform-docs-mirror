---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GetIamPolicyRequest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GetIamPolicyRequest
title: GetIamPolicyRequest
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Request message for `featurestores.getIamPolicy` method.

Fields

`resource` `string`

REQUIRED: The resource for which the policy is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

`options` `object ( `[`GetPolicyOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GetIamPolicyRequest#GetPolicyOptions)` )`

OPTIONAL: A `GetPolicyOptions` object for specifying options to `featurestores.getIamPolicy` .

**JSON representation**

```
{
  "resource": string,
  "options": {
    object (GetPolicyOptions)
  }
}
```

## GetPolicyOptions

Encapsulates settings provided to featurestores.getIamPolicy.

Fields

`requestedPolicyVersion` `integer`

Optional. The maximum policy version that will be used to format the policy.

Valid values are 0, 1, and 3. Requests specifying an invalid value will be rejected.

Requests for policies with any conditional role bindings must specify version 3. Policies with no conditional role bindings may specify any valid value or leave the field unset.

The policy in the response might use the policy version that you specified, or it might use a lower policy version. For example, if you specify version 3, but the policy has no conditional role bindings, the response uses version 1.

To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies) .

**JSON representation**

```
{
  "requestedPolicyVersion": integer
}
```
