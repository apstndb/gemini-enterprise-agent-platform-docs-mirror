---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/list
title: 'Method: specialistPools.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.specialistPools.list

Lists SpecialistPools in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /specialistPools`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the SpecialistPool's parent resource. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained by [`ListSpecialistPoolsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/list#body.ListSpecialistPoolsResponse.FIELDS.next_page_token) of the previous [`SpecialistPoolService.ListSpecialistPools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/list#google.cloud.aiplatform.v1beta1.SpecialistPoolService.ListSpecialistPools) call. Return first page if empty.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read. FieldMask represents a set of

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`SpecialistPoolService.ListSpecialistPools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/list#google.cloud.aiplatform.v1beta1.SpecialistPoolService.ListSpecialistPools) .

If successful, the response body contains data with the following structure:

Fields

`specialistPools[]` `object ( `[`SpecialistPool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools#SpecialistPool)` )`

A list of SpecialistPools that matches the specified filter in the request.

`nextPageToken` `string`

The standard List next-page token.

**JSON representation**

```
{
  "specialistPools": [
    {
      object (SpecialistPool)
    }
  ],
  "nextPageToken": string
}
```
