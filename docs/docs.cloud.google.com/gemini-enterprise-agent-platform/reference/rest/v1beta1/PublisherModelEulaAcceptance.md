---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelEulaAcceptance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelEulaAcceptance
title: PublisherModelEulaAcceptance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for \[ModelGardenService.UpdatePublisherModelEula\]\[\].

Fields

`projectNumber` `string ( int64 format)`

The project number requesting access for named model.

`publisherModel` `string`

The publisher model resource name.

`publisherModelEulaAcked` `boolean`

The EULA content acceptance status.

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
  &quot;projectNumber&quot;: string,
  &quot;publisherModel&quot;: string,
  &quot;publisherModelEulaAcked&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
