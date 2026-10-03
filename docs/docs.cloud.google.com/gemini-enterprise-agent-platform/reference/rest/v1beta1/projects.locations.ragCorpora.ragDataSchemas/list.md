---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list
title: 'Method: ragDataSchemas.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragDataSchemas.list

Lists RagDataSchemas in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /ragDataSchemas`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the RagCorpus from which to list the RagDataSchemas. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size. The maximum value is 100. If not specified, a default value of 100 will be used.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via [`ListRagDataSchemasResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list#body.ListRagDataSchemasResponse.FIELDS.next_page_token) of the previous [`VertexRagDataService.ListRagDataSchemas`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list#google.cloud.aiplatform.v1beta1.VertexRagDataService.ListRagDataSchemas) call.

### Request body

The request body must be empty.

### Response body

Response message for [`VertexRagDataService.ListRagDataSchemas`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list#google.cloud.aiplatform.v1beta1.VertexRagDataService.ListRagDataSchemas) .

If successful, the response body contains data with the following structure:

Fields

`ragDataSchemas[]` `object ( `[`RagDataSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas#RagDataSchema)` )`

List of RagDataSchemas in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListRagDataSchemasRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "ragDataSchemas": [
    {
      object (RagDataSchema)
    }
  ],
  "nextPageToken": string
}
```
