---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators/patch
title: 'Method: onlineEvaluators.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.onlineEvaluators.patch

Updates the fields of an OnlineEvaluator.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{onlineEvaluator.name}`  

`PATCH https://{service-endpoint}/v1beta1/{onlineEvaluator.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`onlineEvaluator.name` `string`

Identifier. The resource name of the OnlineEvaluator. Format: projects/{project}/locations/{location}/onlineEvaluators/{id}.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Field mask is used to control which fields get updated. If the mask is not present, all fields will be updated.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  OnlineEvaluator  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
