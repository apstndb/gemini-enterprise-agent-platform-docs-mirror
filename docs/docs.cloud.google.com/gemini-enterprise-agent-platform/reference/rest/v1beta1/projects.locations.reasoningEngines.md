---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines
title: 'REST Resource: projects.locations.reasoningEngines'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ReasoningEngine

ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.

Fields

`name` `string`

Identifier. The resource name of the ReasoningEngine. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

`displayName` `string`

Required. The display name of the ReasoningEngine.

`description` `string`

Optional. The description of the ReasoningEngine.

`spec` ` object ( ReasoningEngineSpec  ` )

Optional. Configurations of the ReasoningEngine

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ReasoningEngine was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ReasoningEngine was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`contextSpec` ` object ( ReasoningEngineContextSpec  ` )

Optional. Configuration for how Agent Engine sub-resources should manage context.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a ReasoningEngine. If set, this ReasoningEngine and all sub-resources of this ReasoningEngine will be secured by this key.

`labels` `map (key: string, value: string)`

Labels for the ReasoningEngine.

`trafficConfig` ` object ( TrafficConfig  ` )

Optional. Traffic distribution configuration for the Reasoning Engine.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;spec&quot;: {object (ReasoningEngineSpec)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;contextSpec&quot;: {object (ReasoningEngineContextSpec)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;labels&quot;: {string: string,...},&quot;trafficConfig&quot;: {object (TrafficConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ReasoningEngineContextSpec

Configuration for how Agent Engine sub-resources should manage context.

Fields

`memoryBankConfig` ` object ( MemoryBankConfig  ` )

Optional. Specification for a Memory Bank, which manages memories for the Agent Engine.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;memoryBankConfig&quot;: {object (MemoryBankConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## MemoryBankConfig

Specification for a Memory Bank.

Fields

`generationConfig` ` object ( GenerationConfig  ` )

Optional. Configuration for how to generate memories for the Memory Bank.

`similaritySearchConfig` ` object ( SimilaritySearchConfig  ` )

Optional. Configuration for how to perform similarity search on memories. If not set, the Memory Bank will use the default embedding model `text-embedding-005` .

`ttlConfig` ` object ( TtlConfig  ` )

Optional. Configuration for automatic TTL ("time-to-live") of the memories in the Memory Bank. If not set, TTL will not be applied automatically. The TTL can be explicitly set by modifying the `expireTime` of each Memory resource.

`disableMemoryRevisions` `boolean`

If true, no memory revisions will be created for any requests to the Memory Bank.

`structuredMemoryConfigs[]` ` object ( StructuredMemoryConfig  ` )

Optional. Configuration for organizing structured memories for a particular scope.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;generationConfig&quot;: {object (GenerationConfig)},&quot;similaritySearchConfig&quot;: {object (SimilaritySearchConfig)},&quot;ttlConfig&quot;: {object (TtlConfig)},&quot;disableMemoryRevisions&quot;: boolean,&quot;structuredMemoryConfigs&quot;: [{object (StructuredMemoryConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

## GenerationConfig

Configuration for how to generate memories.

Fields

`model` `string`

Optional. The model used to generate memories. Format: `projects/{project}/locations/{location}/publishers/google/models/{model}` .

`generationTriggerConfig` ` object ( MemoryGenerationTriggerConfig  ` )

Optional. Specifies the default trigger configuration for generating memories using `IngestEvents` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;model&quot;: string,&quot;generationTriggerConfig&quot;: {object (MemoryGenerationTriggerConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## MemoryGenerationTriggerConfig

Represents configuration for triggering generation.

Fields

`generationRule` ` object ( GenerationTriggerRule  ` )

Optional. Represents the active rule that determines when to flush the buffer. If not set, then the stream will be force flushed immediately.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;generationRule&quot;: {object (GenerationTriggerRule)}}</code></pre></td>
</tr>
</tbody>
</table>

## GenerationTriggerRule

Represents the active rule that determines when to flush the buffer.

Fields

`eventCount` `integer`

Optional. Specifies to trigger generation when the event count reaches this limit.

`time_based_condition` `Union type`

Represents the time based condition that triggers generation. `time_based_condition` can be only one of the following:

`idleDuration` ` string ( Duration  ` format)

Optional. Specifies to trigger generation if the stream is inactive for the specified duration after the most recent event. The duration must have a minute-level granularity.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`fixedInterval` ` string ( Duration  ` format)

Optional. Specifies to trigger generation at a fixed interval. The duration must have a minute-level granularity.

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
  &quot;eventCount&quot;: integer,

  // time_based_condition
  &quot;idleDuration&quot;: string,
  &quot;fixedInterval&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## SimilaritySearchConfig

Configuration for how to perform similarity search on memories.

Fields

`embeddingModel` `string`

Required. The model used to generate embeddings to lookup similar memories. Format: `projects/{project}/locations/{location}/publishers/google/models/{model}` .

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
  &quot;embeddingModel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TtlConfig

Configuration for automatically setting the TTL ("time-to-live") of the memories in the Memory Bank.

Fields

`ttl` `Union type`

Configuration for automatically setting the TTL of the memories in the Memory Bank. `ttl` can be only one of the following:

`defaultTtl` ` string ( Duration  ` format)

Optional. The default TTL duration of the memories in the Memory Bank. This applies to all operations that create or update a memory.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`granularTtlConfig` ` object ( GranularTtlConfig  ` )

Optional. The granular TTL configuration of the memories in the Memory Bank.

`memory_revision_ttl` `Union type`

Configuration for automatically setting the TTL of the memory revisions in the Memory Bank. `memory_revision_ttl` can be only one of the following:

`memoryRevisionDefaultTtl` ` string ( Duration  ` format)

Optional. The default TTL duration of the memory revisions in the Memory Bank. This applies to all operations that create a memory revision. If not set, a default TTL of 365 days will be used.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// ttl&quot;defaultTtl&quot;: string,&quot;granularTtlConfig&quot;: {object (GranularTtlConfig)}// Union type// memory_revision_ttl&quot;memoryRevisionDefaultTtl&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## GranularTtlConfig

Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.

Fields

`createTtl` ` string ( Duration  ` format)

Optional. The TTL duration for memories uploaded via CreateMemory.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`generateCreatedTtl` ` string ( Duration  ` format)

Optional. The TTL duration for memories newly generated via GenerateMemories ( `GenerateMemoriesResponse.GeneratedMemory.Action.CREATED` ).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`generateUpdatedTtl` ` string ( Duration  ` format)

Optional. The TTL duration for memories updated via GenerateMemories ( `GenerateMemoriesResponse.GeneratedMemory.Action.UPDATED` ). In the case of an UPDATE action, the `expireTime` of the existing memory will be updated to the new value (now + TTL).

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
  &quot;createTtl&quot;: string,
  &quot;generateCreatedTtl&quot;: string,
  &quot;generateUpdatedTtl&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## StructuredMemoryConfig

Represents configuration for organizing structured memories for a particular scope.

Fields

`scopeKeys[]` `string`

Optional. Represents the scope keys (i.e. 'userId') for which to use this config. A request's scope must include all of the provided keys for the config to be used (order does not matter). If empty, then the config will be used for all requests that do not have a more specific config. Only one default config is allowed per Memory Bank.

`schemaConfigs[]` ` object ( SchemaConfig  ` )

Optional. Represents configuration of the structured memories' schemas.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;scopeKeys&quot;: [string],&quot;schemaConfigs&quot;: [{object (SchemaConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

## SchemaConfig

Schema configuration for structured memories.

Fields

`id` `string`

Required. Represents the id of the schema. Must be 1-63 characters, start with a lowercase letter, and consist of lowercase letters, numbers, and hyphens.

`schema` ` object ( Schema  ` )

Required. Represents the OpenAPI schema of the structured memories. The schema `type` cannot be `ARRAY` when `memoryType` is `STRUCTURED_PROFILE` .

`memoryType` ` enum ( MemoryType  ` )

Optional. Represents the type of the structured memories associated with the schema. If not set, then `STRUCTURED_PROFILE` will be used.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;schema&quot;: {object (Schema)},&quot;memoryType&quot;: enum (MemoryType)}</code></pre></td>
</tr>
</tbody>
</table>

## TrafficConfig

Traffic distribution configuration.

Fields

`traffic_split` `Union type`

Traffic distribution configuration. `traffic_split` can be only one of the following:

`trafficSplitManual` ` object ( TrafficSplitManual  ` )

Optional. Manual traffic distribution configuration, where the user specifies the Runtime Revision IDs and the percentage of traffic to send to each.

`trafficSplitAlwaysLatest` ` object ( TrafficSplitAlwaysLatest  ` )

Optional. Traffic distribution configuration, where all traffic is sent to the latest Runtime Revision.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// traffic_split&quot;trafficSplitManual&quot;: {object (TrafficSplitManual)},&quot;trafficSplitAlwaysLatest&quot;: {object (TrafficSplitAlwaysLatest)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TrafficSplitManual

Manual traffic distribution configuration, where the user specifies the Runtime Revision IDs and the percentage of traffic to send to each.

Fields

`targets[]` ` object ( Target  ` )

A list of traffic targets for the Runtimes Revisions. The sum of percentages must equal to 100.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;targets&quot;: [{object (Target)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Target

A single target for the traffic split, specifying a Runtime Revision and the percentage of traffic to send to it.

Fields

`runtimeRevisionName` `string`

Required. The Runtime Revision name to which to send this portion of traffic, if traffic allocation is by Runtime Revision.

`percent` `integer`

Required. Specifies percent of the traffic to this Runtime Revision.

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
  &quot;runtimeRevisionName&quot;: string,
  &quot;percent&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## TrafficSplitAlwaysLatest

This type has no fields.

Traffic distribution configuration, where all traffic is sent to the latest Runtime Revision.

## Methods

### `            asyncQuery           `

Async query using a reasoning engine.

### `            cancelAsyncQuery           `

Cancels an AsyncQueryReasoningEngine operation.

### `            create           `

Creates a reasoning engine.

### `            delete           `

Deletes a reasoning engine.

### `            get           `

Gets a reasoning engine.

### `            list           `

Lists reasoning engines in a location.

### `            patch           `

Updates a reasoning engine.

### `            query           `

Queries using a reasoning engine.

### `            streamQuery           `

Streams queries using a reasoning engine.
