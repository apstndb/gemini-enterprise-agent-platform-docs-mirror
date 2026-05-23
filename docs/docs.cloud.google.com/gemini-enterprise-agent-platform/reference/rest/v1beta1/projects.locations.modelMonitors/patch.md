---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/patch
title: 'Method: modelMonitors.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.patch

Updates a ModelMonitor.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{modelMonitor.name}`  

`PATCH https://{service-endpoint}/v1beta1/{modelMonitor.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`modelMonitor.name` `string`

Immutable. Resource name of the ModelMonitor. Format: `projects/{project}/locations/{location}/modelMonitors/{modelMonitor}` .

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. Mask specifying which fields to update.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  ModelMonitor  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
