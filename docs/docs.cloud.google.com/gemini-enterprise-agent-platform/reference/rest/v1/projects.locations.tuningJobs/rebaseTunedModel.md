---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/rebaseTunedModel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/rebaseTunedModel
title: 'Method: tuningJobs.rebaseTunedModel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tuningJobs.rebaseTunedModel

Rebase a tuned model.

A rebase operation takes a model that was previously tuned on a base model version, and retunes it on a new base model version. The rebase operation creates a new tuning job and a new tuned model.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /tuningJobs:rebaseTunedModel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the location in which to rebase the Model. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`tunedModelRef` `object ( `[`TunedModelRef`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/rebaseTunedModel#TunedModelRef)` )`

Required. A reference to the tuned model to rebase.

`tuningJob` `object ( `[`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob)` )`

Optional. The tuning job to be updated. Users can use this field to overwrite tuning configs.

`artifactDestination` `object ( `[`GcsDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec#GcsDestination)` )`

Optional. The Google Cloud Storage location to write the artifacts to.

`deployToSameEndpoint` `boolean`

Optional. By default, rebasing a model creates a new endpoint for the new model. If this flag is set to true, the new model will be deployed to the same endpoint as the original model.

WARNING: If you deploy to the same endpoint, the original model will be un-deployed and replaced by the new model.

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

## TunedModelRef

TunedModel Reference for legacy model migration.

Fields

`tuned_model_ref` `Union type`

The Tuned Model Reference for the model. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`tunedModel` `string`

Support migration from model registry.

`tuningJob` `string`

Support migration from tuning job list page, from gemini-1.0-pro-002 to 1.5 and above.

`pipelineJob` `string`

Support migration from tuning job list page, from bison model to gemini model.

End of mutually exclusive fields.

**JSON representation**

```
{

  // tuned_model_ref
  "tunedModel": string,
  "tuningJob": string,
  "pipelineJob": string
  // Union type
}
```
