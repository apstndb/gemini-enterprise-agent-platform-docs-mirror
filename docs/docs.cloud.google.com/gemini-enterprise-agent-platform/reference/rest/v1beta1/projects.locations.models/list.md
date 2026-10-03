---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/list
title: 'Method: models.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.list

Lists Models in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /models`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the Models from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

An expression for filtering the results of the request. For field names both snake_case and camelCase are supported.

- `model` supports = and !=. `model` represents the Model id, i.e. the last segment of the Model's [`resource name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.name) .
- `displayName` supports = and !=
- `labels` supports general map functions that is:
  - `labels.key=value` - key:value equality
  - \`labels.key:\* or labels:key - key existence
  - A key including a space must be quoted. `labels."a key"` .
- `base_model_name` only supports =

Some examples:

- `model=1234`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `baseModelName="text-bison"`

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via [`ListModelsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/list#body.ListModelsResponse.FIELDS.next_page_token) of the previous [`ModelService.ListModels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/list#google.cloud.aiplatform.v1beta1.ModelService.ListModels) call.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`ModelService.ListModels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/list#google.cloud.aiplatform.v1beta1.ModelService.ListModels)

If successful, the response body contains data with the following structure:

Fields

`models[]` `object ( `[`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model)` )`

List of Models in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to [`ListModelsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "models": [
    {
      object (Model)
    }
  ],
  "nextPageToken": string
}
```
