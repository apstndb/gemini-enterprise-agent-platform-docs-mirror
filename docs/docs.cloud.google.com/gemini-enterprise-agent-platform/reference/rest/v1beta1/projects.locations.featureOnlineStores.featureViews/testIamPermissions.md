---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/testIamPermissions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/testIamPermissions
title: 'Method: featureViews.testIamPermissions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.testIamPermissions

Returns permissions that a caller has on the specified resource. If the resource does not exist, this will return an empty set of permissions, not a `NOT_FOUND` error.

Note: This operation is designed to be used for building permission-aware UIs and command-line tools, not for authorization checking. This operation may "fail open" without warning.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{resource}:testIamPermissions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`resource` `string`

REQUIRED: The resource for which the policy detail is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

### Query parameters

`permissions[]` `string`

The set of permissions to check for the `resource` . Permissions with wildcards (such as `*` or `storage.*` ) are not allowed. For more information see [IAM Overview](https://cloud.google.com/iam/docs/overview#permissions) .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  TestIamPermissionsResponse  ` .
