---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list
title: 'Method: ragCorpora.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.list

Lists RagCorpora in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /ragCorpora`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the RagCorpora. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size. The maximum value is 100. If not specified, a default value of 100 will be used.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via [`ListRagCorporaResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list#body.ListRagCorporaResponse.FIELDS.next_page_token) of the previous [`VertexRagDataService.ListRagCorpora`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list#google.cloud.aiplatform.v1beta1.VertexRagDataService.ListRagCorpora) call.

### Request body

The request body must be empty.

### Response body

Response message for [`VertexRagDataService.ListRagCorpora`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list#google.cloud.aiplatform.v1beta1.VertexRagDataService.ListRagCorpora) .

If successful, the response body contains data with the following structure:

Fields

`ragCorpora[]` `object ( `[`RagCorpus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora#RagCorpus)` )`

List of RagCorpora in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListRagCorporaRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "ragCorpora": [
    {
      object (RagCorpus)
    }
  ],
  "nextPageToken": string
}
```
