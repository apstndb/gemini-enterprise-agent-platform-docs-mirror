---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TimeSegment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TimeSegment
title: TimeSegment
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A time period inside of a DataItem that has a time dimension (e.g. video).

Fields

`startTimeOffset` ` string ( Duration  ` format)

Start of the time segment (inclusive), represented as the duration since the start of the DataItem.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endTimeOffset` ` string ( Duration  ` format)

End of the time segment (exclusive), represented as the duration since the start of the DataItem.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
  &quot;startTimeOffset&quot;: string,
  &quot;endTimeOffset&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
