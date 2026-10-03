---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/retrieveContexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/retrieveContexts
title: 'Method: locations.retrieveContexts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.retrieveContexts

Retrieves relevant contexts for a query.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent}:retrieveContexts`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`query` `object ( `[`RagQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagQuery)` )`

Required. Single RAG retrieve query.

`data_source` `Union type`

Data Source to retrieve contexts. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vertexRagStore` `object ( `[`VertexRagStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/retrieveContexts#VertexRagStore)` )`

The data source for Vertex RagStore.

End of mutually exclusive fields.

### Response body

Response message for [`VertexRagService.RetrieveContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/retrieveContexts#google.cloud.aiplatform.v1beta1.VertexRagService.RetrieveContexts) .

If successful, the response body contains data with the following structure:

Fields

`contexts` `object ( `[`RagContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagContexts)` )`

The contexts of the query.

**JSON representation**

```
{
  "contexts": {
    object (RagContexts)
  }
}
```

## VertexRagStore

The data source for Vertex RagStore.

Fields

`ragCorpora[] `**`(deprecated)`** `string`

> This item is deprecated!

Optional. Deprecated. Please use ragResources to specify the data source.

`ragResources[]` `object ( `[`RagResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/retrieveContexts#RagResource)` )`

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

`vectorDistanceThreshold `**`(deprecated)`** `number`

> This item is deprecated!

Optional. Only return contexts with vector distance smaller than the threshold.

**JSON representation**

```
{
  "ragCorpora": [
    string
  ],
  "ragResources": [
    {
      object (RagResource)
    }
  ],
  "vectorDistanceThreshold": number
}
```

## RagResource

The definition of the Rag resource.

Fields

`ragCorpus` `string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

`ragFileIds[]` `string`

Optional. ragFileId. The files should be in the same ragCorpus set in ragCorpus field.

**JSON representation**

```
{
  "ragCorpus": string,
  "ragFileIds": [
    string
  ]
}
```
