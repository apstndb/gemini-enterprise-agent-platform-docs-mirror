---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata
title: GenericOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Generic metadata shared by all operations.

Fields

`partialFailures[]` ` object ( Status  ` )

Output only. Partial failures encountered. E.g. single files that couldn't be read. This field should never exceed 20 entries. status details field will contain standard Google Cloud error details.

`createTime` ` string ( Timestamp  ` format)

Output only. time when the operation was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. time when the operation was updated for the last time. If the operation has finished (successfully or not), this is the finish time.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;partialFailures&quot;: [{object (Status)}],&quot;createTime&quot;: string,&quot;updateTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
