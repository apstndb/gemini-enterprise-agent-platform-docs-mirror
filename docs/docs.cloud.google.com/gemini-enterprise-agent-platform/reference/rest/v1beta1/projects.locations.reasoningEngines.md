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

`spec` `object ( `[`ReasoningEngineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReasoningEngineSpec)` )`

Optional. Configurations of the ReasoningEngine

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ReasoningEngine was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ReasoningEngine was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`contextSpec` `object ( `[`ReasoningEngineContextSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#ReasoningEngineContextSpec)` )`

Optional. Configuration for how Agent Engine sub-resources should manage context.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key spec for a ReasoningEngine. If set, this ReasoningEngine and all sub-resources of this ReasoningEngine will be secured by this key.

`labels` `map (key: string, value: string)`

Labels for the ReasoningEngine.

`trafficConfig` `object ( `[`TrafficConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#TrafficConfig)` )`

Optional. Traffic distribution configuration for the Reasoning Engine.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "spec": {
    object (ReasoningEngineSpec)
  },
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "contextSpec": {
    object (ReasoningEngineContextSpec)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "labels": {
    string: string,
    ...
  },
  "trafficConfig": {
    object (TrafficConfig)
  }
}
```

## ReasoningEngineContextSpec

Configuration for how Agent Engine sub-resources should manage context.

Fields

`memoryBankConfig` `object ( `[`MemoryBankConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#MemoryBankConfig)` )`

Optional. Specification for a Memory Bank, which manages memories for the Agent Engine.

**JSON representation**

```
{
  "memoryBankConfig": {
    object (MemoryBankConfig)
  }
}
```

## MemoryBankConfig

Specification for a Memory Bank.

Fields

`generationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#GenerationConfig)` )`

Optional. Configuration for how to generate memories for the Memory Bank.

`similaritySearchConfig` `object ( `[`SimilaritySearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#SimilaritySearchConfig)` )`

Optional. Configuration for how to perform similarity search on memories. If not set, the Memory Bank will use the default embedding model `text-embedding-005` .

`ttlConfig` `object ( `[`TtlConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#TtlConfig)` )`

Optional. Configuration for automatic TTL ("time-to-live") of the memories in the Memory Bank. If not set, TTL will not be applied automatically. The TTL can be explicitly set by modifying the `expireTime` of each Memory resource.

`disableMemoryRevisions` `boolean`

If true, no memory revisions will be created for any requests to the Memory Bank.

`structuredMemoryConfigs[]` `object ( `[`StructuredMemoryConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#StructuredMemoryConfig)` )`

Optional. Configuration for organizing structured memories for a particular scope.

**JSON representation**

```
{
  "generationConfig": {
    object (GenerationConfig)
  },
  "similaritySearchConfig": {
    object (SimilaritySearchConfig)
  },
  "ttlConfig": {
    object (TtlConfig)
  },
  "disableMemoryRevisions": boolean,
  "structuredMemoryConfigs": [
    {
      object (StructuredMemoryConfig)
    }
  ]
}
```

## GenerationConfig

Configuration for how to generate memories.

Fields

`model` `string`

Optional. The model used to generate memories. Format: `projects/{project}/locations/{location}/publishers/google/models/{model}` .

`generationTriggerConfig` `object ( `[`MemoryGenerationTriggerConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#MemoryGenerationTriggerConfig)` )`

Optional. Specifies the default trigger configuration for generating memories using `IngestEvents` .

**JSON representation**

```
{
  "model": string,
  "generationTriggerConfig": {
    object (MemoryGenerationTriggerConfig)
  }
}
```

## MemoryGenerationTriggerConfig

Represents configuration for triggering generation.

Fields

`generationRule` `object ( `[`GenerationTriggerRule`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#GenerationTriggerRule)` )`

Optional. Represents the active rule that determines when to flush the buffer. If not set, then the stream will be force flushed immediately.

**JSON representation**

```
{
  "generationRule": {
    object (GenerationTriggerRule)
  }
}
```

## GenerationTriggerRule

Represents the active rule that determines when to flush the buffer.

Fields

`eventCount` `integer`

Optional. Specifies to trigger generation when the event count reaches this limit.

`time_based_condition` `Union type`

Represents the time based condition that triggers generation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`idleDuration` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Specifies to trigger generation if the stream is inactive for the specified duration after the most recent event. The duration must have a minute-level granularity.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`fixedInterval` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Specifies to trigger generation at a fixed interval. The duration must have a minute-level granularity.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

End of mutually exclusive fields.

`overlap_window` `Union type`

Specifies how much context to carry over from one generation window into the next, so that memories stay coherent across GenerateMemories calls. Carried-over events do not count toward the trigger rule. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`overlapEventCount` `integer`

Optional. Re-include the last N already-processed events in the next window.

End of mutually exclusive fields.

**JSON representation**

```
{
  "eventCount": integer,

  // time_based_condition
  "idleDuration": string,
  "fixedInterval": string
  // Union type

  // overlap_window
  "overlapEventCount": integer
  // Union type
}
```

## SimilaritySearchConfig

Configuration for how to perform similarity search on memories.

Fields

`embeddingModel` `string`

Required. The model used to generate embeddings to lookup similar memories. Format: `projects/{project}/locations/{location}/publishers/google/models/{model}` .

**JSON representation**

```
{
  "embeddingModel": string
}
```

## TtlConfig

Configuration for automatically setting the TTL ("time-to-live") of the memories in the Memory Bank.

Fields

`ttl` `Union type`

Configuration for automatically setting the TTL of the memories in the Memory Bank. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`defaultTtl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The default TTL duration of the memories in the Memory Bank. This applies to all operations that create or update a memory.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`granularTtlConfig` `object ( `[`GranularTtlConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#GranularTtlConfig)` )`

Optional. The granular TTL configuration of the memories in the Memory Bank.

End of mutually exclusive fields.

`memory_revision_ttl` `Union type`

Configuration for automatically setting the TTL of the memory revisions in the Memory Bank. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`memoryRevisionDefaultTtl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The default TTL duration of the memory revisions in the Memory Bank. This applies to all operations that create a memory revision. If not set, a default TTL of 365 days will be used.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

End of mutually exclusive fields.

**JSON representation**

```
{

  // ttl
  "defaultTtl": string,
  "granularTtlConfig": {
    object (GranularTtlConfig)
  }
  // Union type

  // memory_revision_ttl
  "memoryRevisionDefaultTtl": string
  // Union type
}
```

## GranularTtlConfig

Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.

Fields

`createTtl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The TTL duration for memories uploaded via CreateMemory.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`generateCreatedTtl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The TTL duration for memories newly generated via GenerateMemories ( `GenerateMemoriesResponse.GeneratedMemory.Action.CREATED` ).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`generateUpdatedTtl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The TTL duration for memories updated via GenerateMemories ( `GenerateMemoriesResponse.GeneratedMemory.Action.UPDATED` ). In the case of an UPDATE action, the `expireTime` of the existing memory will be updated to the new value (now + TTL).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

**JSON representation**

```
{
  "createTtl": string,
  "generateCreatedTtl": string,
  "generateUpdatedTtl": string
}
```

## StructuredMemoryConfig

Represents configuration for organizing structured memories for a particular scope.

Fields

`scopeKeys[]` `string`

Optional. Represents the scope keys (i.e. 'userId') for which to use this config. A request's scope must include all of the provided keys for the config to be used (order does not matter). If empty, then the config will be used for all requests that do not have a more specific config. Only one default config is allowed per Memory Bank.

`schemaConfigs[]` `object ( `[`SchemaConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#SchemaConfig)` )`

Optional. Represents configuration of the structured memories' schemas.

**JSON representation**

```
{
  "scopeKeys": [
    string
  ],
  "schemaConfigs": [
    {
      object (SchemaConfig)
    }
  ]
}
```

## SchemaConfig

Schema configuration for structured memories.

Fields

`id` `string`

Required. Represents the id of the schema. Must be 1-63 characters, start with a lowercase letter, and consist of lowercase letters, numbers, and hyphens.

`schema` `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Schema)` )`

Required. Represents the OpenAPI schema of the structured memories. The schema `type` cannot be `ARRAY` when `memoryType` is `STRUCTURED_PROFILE` .

`memoryType` `enum ( `[`MemoryType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MemoryType)` )`

Optional. Represents the type of the structured memories associated with the schema. If not set, then `STRUCTURED_PROFILE` will be used.

`jsonSchema` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Optional. Represents the JSON Schema of the structured memories.

**JSON representation**

```
{
  "id": string,
  "schema": {
    object (Schema)
  },
  "memoryType": enum (MemoryType),
  "jsonSchema": value
}
```

## TrafficConfig

Traffic distribution configuration.

Fields

`traffic_split` `Union type`

Traffic distribution configuration. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`trafficSplitManual` `object ( `[`TrafficSplitManual`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#TrafficSplitManual)` )`

Optional. Manual traffic distribution configuration, where the user specifies the Runtime Revision IDs and the percentage of traffic to send to each.

`trafficSplitAlwaysLatest` `object ( `[`TrafficSplitAlwaysLatest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#TrafficSplitAlwaysLatest)` )`

Optional. Traffic distribution configuration, where all traffic is sent to the latest Runtime Revision.

End of mutually exclusive fields.

**JSON representation**

```
{

  // traffic_split
  "trafficSplitManual": {
    object (TrafficSplitManual)
  },
  "trafficSplitAlwaysLatest": {
    object (TrafficSplitAlwaysLatest)
  }
  // Union type
}
```

## TrafficSplitManual

Manual traffic distribution configuration, where the user specifies the Runtime Revision IDs and the percentage of traffic to send to each.

Fields

`targets[]` `object ( `[`Target`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#Target)` )`

A list of traffic targets for the Runtimes Revisions. The sum of percentages must equal to 100.

**JSON representation**

```
{
  "targets": [
    {
      object (Target)
    }
  ]
}
```

## Target

A single target for the traffic split, specifying a Runtime Revision and the percentage of traffic to send to it.

Fields

`runtimeRevisionName` `string`

Required. The Runtime Revision name to which to send this portion of traffic, if traffic allocation is by Runtime Revision.

`percent` `integer`

Required. Specifies percent of the traffic to this Runtime Revision.

**JSON representation**

```
{
  "runtimeRevisionName": string,
  "percent": integer
}
```

## TrafficSplitAlwaysLatest

This type has no fields.

Traffic distribution configuration, where all traffic is sent to the latest Runtime Revision.

| Methods                                                                                                                                                              |                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`asyncQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/asyncQuery)                 | Async query using a reasoning engine.                            |
| [`cancelAsyncQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/cancelAsyncQuery)     | Cancels an AsyncQueryReasoningEngine operation.                  |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/create)                         | Creates a reasoning engine.                                      |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/delete)                         | Deletes a reasoning engine.                                      |
| [`executeCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/executeCode)               | Executes code statelessly.                                       |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/get)                               | Gets a reasoning engine.                                         |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/getIamPolicy)             | Gets the access control policy for a resource.                   |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/list)                             | Lists reasoning engines in a location.                           |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/patch)                           | Updates a reasoning engine.                                      |
| [`query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/query)                           | Queries using a reasoning engine.                                |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/setIamPolicy)             | Sets the access control policy on the specified resource.        |
| [`streamQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/streamQuery)               | Streams queries using a reasoning engine.                        |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/testIamPermissions) | Returns permissions that a caller has on the specified resource. |
