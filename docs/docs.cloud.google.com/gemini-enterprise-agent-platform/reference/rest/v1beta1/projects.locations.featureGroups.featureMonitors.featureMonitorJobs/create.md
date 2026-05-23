---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/create
title: 'Method: featureMonitorJobs.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.featureMonitors.featureMonitorJobs.create

Creates a new feature monitor job.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /featureMonitorJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of FeatureMonitor to create FeatureMonitorJob. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}`

### Query parameters

`featureMonitorJobId` `string ( int64 format)`

Optional. Output only. System-generated id for feature monitor job.

### Request body

The request body contains an instance of `  FeatureMonitorJob  ` .

### Response body

If successful, the response body contains a newly created instance of `  FeatureMonitorJob  ` .
