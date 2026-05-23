---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchKeyGenerationMethod
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchKeyGenerationMethod
title: SearchKeyGenerationMethod
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Options for generating the search key from the conversation history.

Fields

`method` `Union type`

The method for generating the search key. `method` can be only one of the following:

`lastEntry` ` object ( LastEntry  ` )

Use only the last entry of the conversation history ( `contentsExample.contents` ) as the search key.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// method&quot;lastEntry&quot;: {object (LastEntry)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## LastEntry

This type has no fields.

Configuration for using only the last entry of the conversation history as the search key.
