---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DestinationFeatureSetting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DestinationFeatureSetting
title: DestinationFeatureSetting
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`featureId` `string`

Required. The id of the feature to apply the setting to.

`destinationField` `string`

Specify the field name in the export destination. If not specified, feature id is used.

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
  &quot;featureId&quot;: string,
  &quot;destinationField&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
