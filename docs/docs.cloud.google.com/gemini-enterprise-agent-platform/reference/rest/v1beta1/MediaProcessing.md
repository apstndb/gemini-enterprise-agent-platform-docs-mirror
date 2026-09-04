---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaProcessing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaProcessing
title: MediaProcessing
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`static` ` object ( StaticMediaProcessing  ` )

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;static&quot;: {object (StaticMediaProcessing)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## StaticMediaProcessing

Fields

`startOffset` ` string ( Duration  ` format)

Optional. Segment start time. Specified as a decimal number of seconds followed by an 's' suffix, e.g., "10.5s". Must be non-negative.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset` ` string ( Duration  ` format)

Optional. Segment end time. Specified as a decimal number of seconds followed by an 's' suffix, e.g., "30s". Must be non-negative and greater than `startOffset` if `startOffset` is set.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`fps` `number`

Optional. Video frame-rate sampling density.

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
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string,
  &quot;fps&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
