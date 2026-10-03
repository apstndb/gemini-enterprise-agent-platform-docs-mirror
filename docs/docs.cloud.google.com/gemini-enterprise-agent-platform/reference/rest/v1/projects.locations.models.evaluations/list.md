---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list
title: 'Method: evaluations.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.evaluations.list

Lists ModelEvaluations in a Model.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /evaluations`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Model to list the ModelEvaluations from. Format: `projects/{project}/locations/{location}/models/{model}`

### Query parameters

`filter` `string`

The standard list filter.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via [`ListModelEvaluationsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list#body.ListModelEvaluationsResponse.FIELDS.next_page_token) of the previous [`ModelService.ListModelEvaluations`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list#google.cloud.aiplatform.v1.ModelService.ListModelEvaluations) call.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`ModelService.ListModelEvaluations`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list#google.cloud.aiplatform.v1.ModelService.ListModelEvaluations) .

If successful, the response body contains data with the following structure:

Fields

`modelEvaluations[]` `object ( `[`ModelEvaluation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations#ModelEvaluation)` )`

List of ModelEvaluations in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to [`ListModelEvaluationsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "modelEvaluations": [
    {
      object (ModelEvaluation)
    }
  ],
  "nextPageToken": string
}
```
