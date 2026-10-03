---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/listOptimalTrials
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/listOptimalTrials
title: 'Method: trials.listOptimalTrials'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.listOptimalTrials

Lists the pareto-optimal Trials for multi-objective Study or the optimal Trials for single-objective Study. The definition of pareto-optimal can be checked in wiki page. <https://en.wikipedia.org/wiki/Pareto_efficiency>

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /trials:listOptimalTrials`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the Study that the optimal Trial belongs to.

### Request body

The request body must be empty.

### Response body

Response message for [`VizierService.ListOptimalTrials`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/listOptimalTrials#google.cloud.aiplatform.v1.VizierService.ListOptimalTrials) .

If successful, the response body contains data with the following structure:

Fields

`optimalTrials[]` `object ( `[`Trial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials#Trial)` )`

The pareto-optimal Trials for multiple objective Study or the optimal trial for single objective Study. The definition of pareto-optimal can be checked in wiki page. <https://en.wikipedia.org/wiki/Pareto_efficiency>

**JSON representation**

```
{
  "optimalTrials": [
    {
      object (Trial)
    }
  ]
}
```
