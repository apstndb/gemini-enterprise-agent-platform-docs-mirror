---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/streamingFetchFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/streamingFetchFeatureValues
title: 'Method: featureViews.streamingFetchFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.streamingFetchFeatureValues

Bidirectional streaming RPC to fetch feature values under a FeatureView. Requests may not have a one-to-one mapping to responses and responses may be returned out-of-order to reduce latency.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{featureView}:streamingFetchFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView` `string`

Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Request body

The request body contains data with the following structure:

Fields

`dataKeys[]` ` object ( FeatureViewDataKey  ` )

`dataFormat` ` enum ( FeatureViewDataFormat  ` )

Specify response data format. If not set, keyvalue format will be used.

### Response body

Response message for `  FeatureOnlineStoreService.StreamingFetchFeatureValues  ` .

If successful, the response body contains data with the following structure:

Fields

`status` ` object ( Status  ` )

Response status. If OK, then `  StreamingFetchFeatureValuesResponse.data  ` will be populated. Otherwise `  StreamingFetchFeatureValuesResponse.data_keys_with_error  ` will be populated with the appropriate data keys. The error only applies to the listed data keys - the stream will remain open for further \[FeatureOnlineStoreService.StreamingFetchFeatureValuesRequest\]\[\] requests.

`data[]` ` object ( FetchFeatureValuesResponse  ` )

`dataKeysWithError[]` ` object ( FeatureViewDataKey  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;status&quot;: {object (Status)},&quot;data&quot;: [{object (FetchFeatureValuesResponse)}],&quot;dataKeysWithError&quot;: [{object (FeatureViewDataKey)}]}</code></pre></td>
</tr>
</tbody>
</table>
