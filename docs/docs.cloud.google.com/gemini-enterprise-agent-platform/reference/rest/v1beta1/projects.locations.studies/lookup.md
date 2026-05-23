---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies/lookup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies/lookup
title: 'Method: studies.lookup'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.lookup

Looks a study up using the user-defined displayName field instead of the fully qualified resource name.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /studies:lookup`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to get the Study from. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`displayName` `string`

Required. The user-defined display name of the Study

### Response body

If successful, the response body contains an instance of `  Study  ` .
