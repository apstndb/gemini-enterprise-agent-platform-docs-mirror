---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/get
title: 'Method: featureMonitorJobs.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.featureMonitors.featureMonitorJobs.get

Get a feature monitor job.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the FeatureMonitorJob resource. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}/featureMonitorJobs/{featureMonitorJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  FeatureMonitorJob  ` .
