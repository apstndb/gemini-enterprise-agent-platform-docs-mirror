---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UrlContextResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UrlContextResult
title: UrlContextResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The result of the URL context.

Fields

`url` `string`

The URL that was fetched.

`status` ` enum ( Status  ` )

The status of the URL retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;url&quot;: string,&quot;status&quot;: enum (Status)}</code></pre></td>
</tr>
</tbody>
</table>

## Status

The status of the URL retrieval.

Enums

`STATUS_UNSPECIFIED`

Unspecified status. This value should not be used.

`SUCCESS`

url retrieval is successful.

`ERROR`

url retrieval is failed due to error.

`PAYWALL`

url retrieval is failed because the content is behind paywall.

`UNSAFE`

url retrieval is failed because the content is unsafe.
