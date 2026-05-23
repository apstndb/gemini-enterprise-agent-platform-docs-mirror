---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/directWrite
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/directWrite
title: 'Method: featureViews.directWrite'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.directWrite

Bidirectional streaming RPC to directly write to feature values in a feature view. Requests may not have a one-to-one mapping to responses and responses may be returned out-of-order to reduce latency.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{featureView}:directWrite`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView` `string`

FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Request body

The request body contains data with the following structure:

Fields

`dataKeyAndFeatureValues[]` ` object ( DataKeyAndFeatureValues  ` )

Required. The data keys and associated feature values.

### Response body

Response message for `  FeatureOnlineStoreService.FeatureViewDirectWrite  ` .

If successful, the response body contains data with the following structure:

Fields

`status` ` object ( Status  ` )

Response status for the keys listed in `  FeatureViewDirectWriteResponse.write_responses  ` .

The error only applies to the listed data keys - the stream will remain open for further \[FeatureOnlineStoreService.FeatureViewDirectWriteRequest\]\[\] requests.

Partial failures (e.g. if the first 10 keys of a request fail, but the rest succeed) from a single request may result in multiple responses - there will be one response for the successful request keys and one response for the failing request keys.

`writeResponses[]` ` object ( WriteResponse  ` )

Details about write for each key. If status is not OK, `  WriteResponse.data_key  ` will have the key with error, but `  WriteResponse.online_store_write_time  ` will not be present.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;status&quot;: {object (Status)},&quot;writeResponses&quot;: [{object (WriteResponse)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DataKeyAndFeatureValues

A data key and associated feature values to write to the feature view.

Fields

`dataKey` ` object ( FeatureViewDataKey  ` )

The data key.

`features[]` ` object ( Feature  ` )

List of features to write.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataKey&quot;: {object (FeatureViewDataKey)},&quot;features&quot;: [{object (Feature)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Feature

feature name & value pair.

Fields

`name` `string`

feature short name.

`data_oneof` `Union type`

Feature value data to write. `data_oneof` can be only one of the following:

`value` ` object ( FeatureValue  ` )

feature value. A user provided timestamp may be set in the `FeatureValue.metadata.generate_time` field.

`valueAndTimestamp` ` object ( FeatureValueAndTimestamp  ` )

feature value and timestamp.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,// data_oneof&quot;value&quot;: {object (FeatureValue)},&quot;valueAndTimestamp&quot;: {object (FeatureValueAndTimestamp)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureValueAndTimestamp

feature value and timestamp.

Fields

`value` ` object ( FeatureValue  ` )

The feature value.

`timestamp` ` string ( Timestamp  ` format)

The feature timestamp to store with this value. If not set, then the feature Store server will generate a timestamp when it receives the write request.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;value&quot;: {object (FeatureValue)},&quot;timestamp&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## WriteResponse

Details about the write for each key.

Fields

`dataKey` ` object ( FeatureViewDataKey  ` )

What key is this write response associated with.

`onlineStoreWriteTime` ` string ( Timestamp  ` format)

When the feature values were written to the online store. If `  FeatureViewDirectWriteResponse.status  ` is not OK, this field is not populated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataKey&quot;: {object (FeatureViewDataKey)},&quot;onlineStoreWriteTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
