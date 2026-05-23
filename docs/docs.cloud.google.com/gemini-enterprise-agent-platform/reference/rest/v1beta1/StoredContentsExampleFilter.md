---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/StoredContentsExampleFilter
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/StoredContentsExampleFilter
title: StoredContentsExampleFilter
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata filters that will be used to remove or fetch StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied.

Fields

`searchKeys[]` `string`

Optional. The search keys for filtering. Only examples with one of the specified search keys ( `  StoredContentsExample.search_key  ` ) are eligible to be returned.

`functionNames` ` object ( ExamplesArrayFilter  ` )

Optional. The function names for filtering.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchKeys&quot;: [string],&quot;functionNames&quot;: {object (ExamplesArrayFilter)}}</code></pre></td>
</tr>
</tbody>
</table>
