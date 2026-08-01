---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/ingestEvents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/ingestEvents
title: 'Method: memories.ingestEvents'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.ingestEvents

Ingests events for a Memory Bank.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /memories:ingestEvents`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to ingest events to. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`streamId` `string`

Optional. The id of the stream to ingest events into. If not provided, a new one will be created.

`generationTriggerConfig` ` object ( MemoryGenerationTriggerConfig  ` )

Optional. Configuration for triggering memory generation from this ingestion. If not set, then the stream will be force flushed immediately.

`scope` `map (key: string, value: string)`

Required. The scope of the memories that should be generated from the stream. Memories will be consolidated across memories with the same scope. scope values cannot contain the wildcard character '\*'.

`forceFlush` `boolean`

Optional. Forces a flush of all pending events in the stream and triggers memory generation immediately bypassing any conditions configured in the `generationTriggerConfig` .

`source` `Union type`

Source of the events to ingest. `source` can be only one of the following:

`directContentsSource` ` object ( IngestionDirectContentsSource  ` )

Ingest events directly from the request.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
