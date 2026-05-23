---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/removeExamples
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/removeExamples
title: 'Method: exampleStores.removeExamples'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.exampleStores.removeExamples

Remove Examples from the Example Store.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{exampleStore}:removeExamples`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`exampleStore` `string`

Required. The name of the ExampleStore resource that the examples should be removed from. Format: `projects/{project}/locations/{location}/exampleStores/{exampleStore}`

### Request body

The request body contains data with the following structure:

Fields

`exampleIds[]` `string`

Optional. Example IDs to remove. If both metadata filters and Example IDs are specified, the metadata filters will be applied to the specified examples in order to identify which should be removed.

`metadata_filter` `Union type`

The metadata filters that will be used to select which examples should be removed. `metadata_filter` can be only one of the following:

`storedContentsExampleFilter` ` object ( StoredContentsExampleFilter  ` )

The metadata filters for StoredContentsExamples.

### Response body

Response message for `  ExampleStoreService.RemoveExamples  ` .

If successful, the response body contains data with the following structure:

Fields

`exampleIds[]` `string`

The IDs for the removed examples.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;exampleIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
