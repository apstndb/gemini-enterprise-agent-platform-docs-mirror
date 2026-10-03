---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models/list
title: 'Method: models.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : publishers.models.list

Lists publisher models in Model Garden.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /models`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the Publisher from which to list the PublisherModels. Format: `publishers/{publisher}`

### Query parameters

`filter` `string`

Optional. The standard list filter.

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via [`ListPublisherModelsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models/list#body.ListPublisherModelsResponse.FIELDS.next_page_token) of the previous [`ModelGardenService.ListPublisherModels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models/list#google.cloud.aiplatform.v1beta1.ModelGardenService.ListPublisherModels) call.

`view` `enum ( `[`PublisherModelView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelView)` )`

Optional. PublisherModel view specifying which fields to read.

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending.

`languageCode` `string`

Optional. The IETF BCP-47 language code representing the language in which the publisher models' text information should be written in. If not set, by default English (en).

`listAllVersions` `boolean`

Optional. List all publisher model versions if the flag is set to true.

### Request body

The request body must be empty.

### Response body

Response message for [`ModelGardenService.ListPublisherModels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models/list#google.cloud.aiplatform.v1beta1.ModelGardenService.ListPublisherModels) .

If successful, the response body contains data with the following structure:

Fields

`publisherModels[]` `object ( `[`PublisherModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models#PublisherModel)` )`

List of PublisherModels in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to \[models.list.page_token\]\[\] to obtain that page.

**JSON representation**

```
{
  "publisherModels": [
    {
      object (PublisherModel)
    }
  ],
  "nextPageToken": string
}
```
