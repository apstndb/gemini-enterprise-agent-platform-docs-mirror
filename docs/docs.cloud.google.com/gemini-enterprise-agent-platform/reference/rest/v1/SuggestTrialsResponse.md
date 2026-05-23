---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SuggestTrialsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SuggestTrialsResponse
title: SuggestTrialsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  VizierService.SuggestTrials  ` .

Fields

`trials[]` ` object ( Trial  ` )

A list of Trials.

`studyState` ` enum ( State  ` )

The state of the Study.

`startTime` ` string ( Timestamp  ` format)

The time at which the operation was started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

The time at which operation processing completed.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trials&quot;: [{object (Trial)}],&quot;studyState&quot;: enum (State),&quot;startTime&quot;: string,&quot;endTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
