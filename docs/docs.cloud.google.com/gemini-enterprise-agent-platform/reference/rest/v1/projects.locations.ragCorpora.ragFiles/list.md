---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list
title: 'Method: ragFiles.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragFiles.list

Lists RagFiles in a RagCorpus.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /ragFiles`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the RagCorpus from which to list the RagFiles. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size. The maximum value is 100. If not specified, a default value of 100 will be used.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via [`ListRagFilesResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list#body.ListRagFilesResponse.FIELDS.next_page_token) of the previous [`VertexRagDataService.ListRagFiles`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list#google.cloud.aiplatform.v1.VertexRagDataService.ListRagFiles) call.

### Request body

The request body must be empty.

### Response body

Response message for [`VertexRagDataService.ListRagFiles`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list#google.cloud.aiplatform.v1.VertexRagDataService.ListRagFiles) .

If successful, the response body contains data with the following structure:

Fields

`ragFiles[]` `object ( `[`RagFile`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles#RagFile)` )`

List of RagFiles in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListRagFilesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "ragFiles": [
    {
      object (RagFile)
    }
  ],
  "nextPageToken": string
}
```
