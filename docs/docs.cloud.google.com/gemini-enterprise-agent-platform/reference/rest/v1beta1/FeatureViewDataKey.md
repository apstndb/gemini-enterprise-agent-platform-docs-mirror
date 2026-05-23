---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureViewDataKey
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureViewDataKey
title: FeatureViewDataKey
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lookup key for a feature view.

Fields

`key_oneof` `Union type`

`key_oneof` can be only one of the following:

`key` `string`

String key to use for lookup.

`compositeKey` ` object ( CompositeKey  ` )

The actual Entity id will be composed from this struct. This should match with the way id is defined in the FeatureView spec.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// key_oneof&quot;key&quot;: string,&quot;compositeKey&quot;: {object (CompositeKey)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CompositeKey

id that is comprised from several parts (columns).

Fields

`parts[]` `string`

Parts to construct Entity id. Should match with the same id columns as defined in FeatureView in the same order.

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
  &quot;parts&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
