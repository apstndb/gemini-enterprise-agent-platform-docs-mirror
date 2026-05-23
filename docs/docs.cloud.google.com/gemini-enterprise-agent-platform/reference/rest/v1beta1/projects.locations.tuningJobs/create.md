---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/create
title: 'Method: tuningJobs.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tuningJobs.create

Creates a tuning job. A created tuning job will be subsequently executed to start the model tuning process.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /tuningJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the location to create the tuning job in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains an instance of `  TuningJob  ` .

### Response body

If successful, the response body contains a newly created instance of `  TuningJob  ` .
