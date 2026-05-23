---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/setIamPolicy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/setIamPolicy
title: 'Method: featureViews.setIamPolicy'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.setIamPolicy

Sets the access control policy on the specified resource. Replaces any existing policy.

Can return `NOT_FOUND` , `INVALID_ARGUMENT` , and `PERMISSION_DENIED` errors.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{resource}:setIamPolicy`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`resource` `string`

REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

### Request body

The request body contains data with the following structure:

Fields

`policy` ` object ( Policy  ` )

REQUIRED: The complete policy to be applied to the `resource` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them.

### Response body

If successful, the response body contains an instance of `  Policy  ` .
