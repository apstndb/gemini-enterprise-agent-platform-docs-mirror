---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list
title: 'Method: metadataStores.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.list

Lists MetadataStores for a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /metadataStores`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The Location whose MetadataStores should be listed. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

The maximum number of metadata Stores to return. The service may return fewer. Must be in range 1-100, inclusive. Defaults to 100.

`pageToken` `string`

A page token, received from a previous [`MetadataService.ListMetadataStores`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list#google.cloud.aiplatform.v1.MetadataService.ListMetadataStores) call. Provide this to retrieve the subsequent page.

When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.)

### Request body

The request body must be empty.

### Response body

Response message for [`MetadataService.ListMetadataStores`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list#google.cloud.aiplatform.v1.MetadataService.ListMetadataStores) .

If successful, the response body contains data with the following structure:

Fields

`metadataStores[]` `object ( `[`MetadataStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores#MetadataStore)` )`

The MetadataStores found for the Location.

`nextPageToken` `string`

A token, which can be sent as [`ListMetadataStoresRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list#body.QUERY_PARAMETERS.page_token) to retrieve the next page. If this field is not populated, there are no subsequent pages.

**JSON representation**

```
{
  "metadataStores": [
    {
      object (MetadataStore)
    }
  ],
  "nextPageToken": string
}
```
