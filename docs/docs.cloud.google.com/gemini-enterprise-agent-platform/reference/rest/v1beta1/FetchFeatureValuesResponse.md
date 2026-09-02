---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FetchFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FetchFeatureValuesResponse
title: FetchFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  FeatureOnlineStoreService.FetchFeatureValues  `

Fields

`dataKey` ` object ( FeatureViewDataKey  ` )

The data key associated with this response. Will only be populated for `  FeatureOnlineStoreService.StreamingFetchFeatureValues  ` RPCs.

`format` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`keyValues` ` object ( FeatureNameValuePairList  ` )

feature values in keyvalue format.

`protoStruct` ` object ( Struct  ` format)

feature values in proto Struct format.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataKey&quot;: {object (FeatureViewDataKey)},// format&quot;keyValues&quot;: {object (FeatureNameValuePairList)},&quot;protoStruct&quot;: {object}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureNameValuePairList

Response structure in the format of key (feature name) and (feature) value pair.

Fields

`features[]` ` object ( FeatureNameValuePair  ` )

List of feature names and values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;features&quot;: [{object (FeatureNameValuePair)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureNameValuePair

feature name & value pair.

Fields

`name` `string`

feature short name.

`data` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`value` ` object ( FeatureValue  ` )

feature value.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,// data&quot;value&quot;: {object (FeatureValue)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>
