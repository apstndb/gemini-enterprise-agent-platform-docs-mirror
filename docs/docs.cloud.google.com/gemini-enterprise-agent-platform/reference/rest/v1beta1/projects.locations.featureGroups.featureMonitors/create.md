---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/create
title: 'Method: featureMonitors.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.featureMonitors.create

Creates a new FeatureMonitor in a given project, location and FeatureGroup.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /featureMonitors`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of FeatureGroup to create FeatureMonitor. Format: `projects/{project}/locations/{location}/featureGroups/{featuregroup}`

### Query parameters

`featureMonitorId` `string`

Required. The id to use for this FeatureMonitor, which will become the final component of the FeatureGroup's resource name.

This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.

The value must be unique within the FeatureGroup.

### Request body

The request body contains an instance of `  FeatureMonitor  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
