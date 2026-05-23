---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/fetchExamples
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/fetchExamples
title: 'Method: exampleStores.fetchExamples'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.exampleStores.fetchExamples

Get Examples from the Example Store.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{exampleStore}:fetchExamples`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`exampleStore` `string`

Required. The name of the ExampleStore resource that the examples should be fetched from. Format: `projects/{project}/locations/{location}/exampleStores/{exampleStore}`

### Request body

The request body contains data with the following structure:

Fields

`pageSize` `integer`

Optional. The maximum number of examples to return. The service may return fewer than this value. If unspecified, at most 100 examples will be returned.

`pageToken` `string`

Optional. The `  nextPageToken  ` value returned from a previous list \[ExampleStoreService.FetchExamplesResponse\]\[\] call.

`exampleIds[]` `string`

Optional. Example IDs to fetch. If both metadata filters and Example IDs are specified, then both id and metadata filtering will be applied.

`metadata_filter` `Union type`

The example type-specific filters to be applied to the fetch operation. `metadata_filter` can be only one of the following:

`storedContentsExampleFilter` ` object ( StoredContentsExampleFilter  ` )

The metadata filters for StoredContentsExamples.

### Response body

Response message for `  ExampleStoreService.FetchExamples  ` .

If successful, the response body contains data with the following structure:

Fields

`examples[]` ` object ( Example  ` )

The examples in the Example Store that satisfy the metadata filters.

`nextPageToken` `string`

A token, which can be sent as `  FetchExamplesRequest.page_token  ` to retrieve the next page. Absence of this field indicates there are no subsequent pages.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;examples&quot;: [{object (Example)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
