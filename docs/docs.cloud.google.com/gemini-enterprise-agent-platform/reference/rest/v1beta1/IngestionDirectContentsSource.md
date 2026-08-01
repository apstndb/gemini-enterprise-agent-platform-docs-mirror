---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/IngestionDirectContentsSource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/IngestionDirectContentsSource
title: IngestionDirectContentsSource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Ingest events directly from the request.

Fields

`events[]` ` object ( Event  ` )

Required. The events to ingest.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;events&quot;: [{object (Event)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Event

A single event to ingest.

Fields

`content` ` object ( Content  ` )

Required. The content of the event.

`eventId` `string`

Optional. A unique identifier for the event. If an event with the same eventId is ingested multiple times, it will be de-duplicated.

`eventTime` ` string ( Timestamp  ` format)

Optional. The time at which the event occurred. If provided, this timestamp will be used for ordering events within a stream. If not provided, the server-side ingestion time will be used.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: {object (Content)},&quot;eventId&quot;: string,&quot;eventTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
