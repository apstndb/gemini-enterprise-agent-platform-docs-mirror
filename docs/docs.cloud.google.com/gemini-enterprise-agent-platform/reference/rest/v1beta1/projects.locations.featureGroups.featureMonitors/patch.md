---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/patch
title: 'Method: featureMonitors.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.featureMonitors.patch

Updates the parameters of a single FeatureMonitor.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{featureMonitor.name}`  

`PATCH https://{service-endpoint}/v1beta1/{featureMonitor.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureMonitor.name` `string`

Identifier. name of the FeatureMonitor. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Field mask is used to specify the fields to be overwritten in the FeatureMonitor resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the updateMask to `*` to override all fields.

Updatable fields:

  - `labels`
  - `description`
  - `scheduleConfig`
  - `featureSelectionConfig`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  FeatureMonitor  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
