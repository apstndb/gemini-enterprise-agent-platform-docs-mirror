---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list
title: 'Method: slices.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.evaluations.slices.list

Lists ModelEvaluationSlices in a ModelEvaluation.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /slices`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`

### Query parameters

`filter` `string`

The standard list filter.

- `slice.dimension` - for =.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via [`ListModelEvaluationSlicesResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list#body.ListModelEvaluationSlicesResponse.FIELDS.next_page_token) of the previous [`ModelService.ListModelEvaluationSlices`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list#google.cloud.aiplatform.v1.ModelService.ListModelEvaluationSlices) call.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`ModelService.ListModelEvaluationSlices`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list#google.cloud.aiplatform.v1.ModelService.ListModelEvaluationSlices) .

If successful, the response body contains data with the following structure:

Fields

`modelEvaluationSlices[]` `object ( `[`ModelEvaluationSlice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices#ModelEvaluationSlice)` )`

List of ModelEvaluations in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to [`ListModelEvaluationSlicesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "modelEvaluationSlices": [
    {
      object (ModelEvaluationSlice)
    }
  ],
  "nextPageToken": string
}
```
