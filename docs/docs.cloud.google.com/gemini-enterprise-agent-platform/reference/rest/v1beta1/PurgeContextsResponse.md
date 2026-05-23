---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PurgeContextsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PurgeContextsResponse
title: PurgeContextsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  MetadataService.PurgeContexts  ` .

Fields

`purgeCount` `string ( int64 format)`

The number of Contexts that this request deleted (or, if `force` is false, the number of Contexts that will be deleted). This can be an estimate.

`purgeSample[]` `string`

A sample of the Context names that will be deleted. Only populated if `force` is set to false. The maximum number of samples is 100 (it is possible to return fewer).

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
  &quot;purgeCount&quot;: string,
  &quot;purgeSample&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
