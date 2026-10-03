---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/list
title: 'Method: indexes.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexes.list

Lists Indexes in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /indexes`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the Indexes. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

The standard list filter.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via [`ListIndexesResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/list#body.ListIndexesResponse.FIELDS.next_page_token) of the previous [`IndexService.ListIndexes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/list#google.cloud.aiplatform.v1beta1.IndexService.ListIndexes) call.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`IndexService.ListIndexes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/list#google.cloud.aiplatform.v1beta1.IndexService.ListIndexes) .

If successful, the response body contains data with the following structure:

Fields

`indexes[]` `object ( `[`Index`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes#Index)` )`

List of indexes in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to [`ListIndexesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "indexes": [
    {
      object (Index)
    }
  ],
  "nextPageToken": string
}
```
