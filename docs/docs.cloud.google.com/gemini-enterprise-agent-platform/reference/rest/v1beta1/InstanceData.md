---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InstanceData
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InstanceData
title: InstanceData
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Instance data used to populate placeholders in a metric prompt template.

Fields

`data` `Union type`

Supported formats for instance data. `data` can be only one of the following:

`text` `string`

Text data.

`contents` ` object ( Contents  ` )

List of Gemini content data.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// data&quot;text&quot;: string,&quot;contents&quot;: {object (Contents)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Contents

List of standard Content messages from Gemini API.

Fields

`contents[]` ` object ( Content  ` )

Optional. Repeated contents.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contents&quot;: [{object (Content)}]}</code></pre></td>
</tr>
</tbody>
</table>
