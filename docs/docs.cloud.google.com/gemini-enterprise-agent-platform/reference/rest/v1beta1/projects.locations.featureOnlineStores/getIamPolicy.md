---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/getIamPolicy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/getIamPolicy
title: 'Method: featureOnlineStores.getIamPolicy'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.getIamPolicy

Gets the access control policy for a resource. Returns an empty policy if the resource exists and does not have a policy set.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{resource}:getIamPolicy`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`resource` `string`

REQUIRED: The resource for which the policy is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

### Query parameters

`options` ` object ( GetPolicyOptions  ` )

OPTIONAL: A `GetPolicyOptions` object for specifying options to `featureOnlineStores.getIamPolicy` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Policy  ` .
