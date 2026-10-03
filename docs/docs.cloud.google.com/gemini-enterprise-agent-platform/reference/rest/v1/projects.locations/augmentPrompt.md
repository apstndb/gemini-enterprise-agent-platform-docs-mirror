---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/augmentPrompt
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/augmentPrompt
title: 'Method: locations.augmentPrompt'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.augmentPrompt

Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent}:augmentPrompt`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`contents[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Optional. Input content to augment, only text format is supported for now.

`model` `object ( `[`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/augmentPrompt#Model)` )`

Optional. metadata of the backend deployed model.

`data_source` `Union type`

The data source for retrieving contexts. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vertexRagStore` `object ( `[`VertexRagStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.cachedContents#VertexRagStore)` )`

Optional. Retrieves contexts from the Vertex RagStore.

End of mutually exclusive fields.

### Response body

Response message for locations.augmentPrompt.

If successful, the response body contains data with the following structure:

Fields

`augmentedPrompt[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Augmented prompt, only text format is supported for now.

`facts[]` `object ( `[`Fact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Fact)` )`

Retrieved facts from RAG data sources.

**JSON representation**

```
{
  "augmentedPrompt": [
    {
      object (Content)
    }
  ],
  "facts": [
    {
      object (Fact)
    }
  ]
}
```

## Model

metadata of the backend deployed model.

Fields

`model` `string`

Optional. The model that the user will send the augmented prompt for content generation.

`modelVersion` `string`

Optional. The model version of the backend deployed model.

**JSON representation**

```
{
  "model": string,
  "modelVersion": string
}
```
