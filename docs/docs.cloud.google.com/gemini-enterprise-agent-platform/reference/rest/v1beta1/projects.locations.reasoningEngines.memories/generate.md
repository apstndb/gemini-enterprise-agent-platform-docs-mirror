---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/generate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/generate
title: 'Method: memories.generate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.generate

Generate memories.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /memories:generate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to generate memories for. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`disableConsolidation` `boolean`

Optional. If true, generated memories will not be consolidated with existing memories; all generated memories will be added as new memories regardless of whether they are duplicates of or contradictory to existing memories. By default, memory consolidation is enabled.

`scope` `map (key: string, value: string)`

Optional. The scope of the memories that should be generated. Memories will be consolidated across memories with the same scope. Must be provided unless the scope is defined in the source content. If `scope` is provided, it will override the scope defined in the source content. scope values cannot contain the wildcard character '\*'.

`source` `Union type`

Source content used to generate memories. `source` can be only one of the following:

`vertexSessionSource` ` object ( VertexSessionSource  ` )

Defines a Vertex Session as the source content from which to generate memories.

`directContentsSource` ` object ( DirectContentsSource  ` )

Defines a direct source of content as the source content from which to generate memories.

`directMemoriesSource` ` object ( DirectMemoriesSource  ` )

Defines a direct source of memories that should be uploaded to Memory Bank. This is similar to `memories.create` , but it allows for consolidation between these new memories and existing memories for the same scope.

`revision_expiration` `Union type`

The expiration of the Memory Revisions created as a result of this request. If not set, Memory Bank will defer to `MemoryBankConfig.memory_revision_default_ttl` or the global default, 365 days. `revision_expiration` can be only one of the following:

`revisionExpireTime` ` string ( Timestamp  ` format)

Optional. timestamp of when the revision is considered expired. If not set, the memory revision will be kept until manually deleted.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`revisionTtl` ` string ( Duration  ` format)

Optional. The TTL for the revision. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## VertexSessionSource

Defines an Agent Engine Session from which to generate the memories. If `scope` is not provided, the scope will be extracted from the Session (i.e. {"userId": sesison.user\_id}).

Fields

`session` `string`

Required. The resource name of the Session to generate memories for. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sessions/{session}`

`startTime` ` string ( Timestamp  ` format)

Optional. time range to define which session events should be used to generate memories. Start time (inclusive) of the time range. If not set, the start time is unbounded.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Optional. End time (exclusive) of the time range. If not set, the end time is unbounded.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;session&quot;: string,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## DirectContentsSource

Defines a direct source of content from which to generate the memories.

Fields

`events[]` ` object ( Event  ` )

Required. The source content (i.e. chat history) to generate memories from.

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

A single piece of conversation from which to generate memories.

Fields

`content` ` object ( Content  ` )

Required. A single piece of content from which to generate memories.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: {object (Content)}}</code></pre></td>
</tr>
</tbody>
</table>

## DirectMemoriesSource

Defines a direct source of memories that should be uploaded to Memory Bank with consolidation.

Fields

`directMemories[]` ` object ( DirectMemory  ` )

Required. The direct memories to upload to Memory Bank. At most 5 direct memories are allowed per request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;directMemories&quot;: [{object (DirectMemory)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DirectMemory

A direct memory to upload to Memory Bank.

Fields

`fact` `string`

Required. The fact to consolidate with existing memories.

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
  &quot;fact&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
