---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/upsertExamples
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/upsertExamples
title: 'Method: exampleStores.upsertExamples'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.exampleStores.upsertExamples

Create or update Examples in the Example Store.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{exampleStore}:upsertExamples`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`exampleStore` `string`

Required. The name of the ExampleStore resource that examples are added to or updated in. Format: `projects/{project}/locations/{location}/exampleStores/{exampleStore}`

### Request body

The request body contains data with the following structure:

Fields

`examples[]` `object ( `[`Example`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Example)` )`

Required. A list of examples to be created/updated.

`overwrite` `boolean`

Optional. A flag indicating whether an example can be overwritten if it already exists. If False (default) and the example already exists, the example will not be updated. This does not affect behavior if the example does not exist already.

### Response body

Response message for [`ExampleStoreService.UpsertExamples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/upsertExamples#google.cloud.aiplatform.v1beta1.ExampleStoreService.UpsertExamples) .

If successful, the response body contains data with the following structure:

Fields

`results[]` `object ( `[`UpsertResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/upsertExamples#UpsertResult)` )`

A list of results for creating/updating. It's either a successfully created/updated example or a status with an error message.

**JSON representation**

```
{
  "results": [
    {
      object (UpsertResult)
    }
  ]
}
```

## UpsertResult

The result for creating/updating a single example.

Fields

`result` `Union type`

The outcome of creating/updating a single example. It's either the example that was successfully created/updated or a status with an error message. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`example` `object ( `[`Example`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Example)` )`

The example created/updated successfully.

`status` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

The error message of the example that was not created/updated successfully.

End of mutually exclusive fields.

**JSON representation**

```
{

  // result
  "example": {
    object (Example)
  },
  "status": {
    object (Status)
  }
  // Union type
}
```
