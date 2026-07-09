---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/ingest-events
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/ingest-events
title: Ingest events
description: Streaming and ingesting events for memory generation with Agent Platform Memory Bank
data_source: docs.cloud.google.com
---

The `IngestEvents` API decouples event ingestion from memory generation in Memory Bank. You can continuously stream content to Memory Bank, and generation will automatically run when your triggering criteria are satisfied.

To complete the steps demonstrated in this guide, you must first follow the steps in [Set up for Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup) .

The examples on this page use the `agentplatform` SDK, which provides the latest `IngestEvents` configuration options. Initialize the client with `agentplatform` :

    import agentplatform
    
    client = agentplatform.Client(
        project="PROJECT_ID",
        location="LOCATION",
    )

## Understanding event ingestion

With the `GenerateMemories` API, memory generation is triggered immediately. This method provides you with direct control over when memory generation occurs. `IngestEvents` offers a streaming pattern that decouples event ingestion from memory generation:

  - **Continuous ingestion** : You can continuously stream context to Memory Bank whenever new data is available.
  - **Deduplication** : Memory Bank automatically detects and ignores overlapping conversation history based on shared event IDs.
  - **Automated triggers** : Generation is automatically triggered only when specific conditions are met, like event count thresholds or idle time.
  - **Asynchronous generation** : Events are processed in the background. The API immediately returns a long-running operation (LRO), which you can poll or monitor until the trigger condition is met and memories are generated.

### Streams and long-running operations (LROs)

Streams act as isolated buffers that accumulate events across multiple requests. Each stream is uniquely defined by the combination of its `scope` and `stream_id` . If you don't provide a stream ID, Memory Bank uses `default` as the ID. Events are only staged and "flushed" together if they share the exact same scope and ID, ensuring strict isolation during memory generation.

Multiple ingestion calls to the same stream return the same LRO until memory generation is triggered and finished. After completion, this `IngestEvents` LRO contains the downstream LRO for the `GenerateMemories` API call. Any subsequent ingestion requests to the stream will return a new LRO.

## Triggering memory generation

If no trigger conditions are met, all pending events in a stream are automatically flushed out 24 hours after the last event is ingested. This limit ensures Memory Bank processes all events, including ones that have been abandoned.

The `generation_trigger_config` determines when the collected events are flushed and processed for memory generation. You can use one of the following trigger conditions:

  - **Event count** ( `event_count` ): Generation triggers once the number of unique events accumulated reaches the limit.
  - **Inactive time** ( `idle_duration` , in seconds with minute granularity, meaning you must specify a multiple of 60): Generation is triggered when the stream hasn't received new events after the specified duration (for example, `"300s"` ).
  - **Fixed interval** ( `fixed_interval` , in seconds with minute granularity, meaning you must specify a multiple of 60): Generation executes on a fixed rhythm, polling for delta events after every specified duration (for example, `"300s"` ).
  - **Force flush** ( `force_flush` ): Flush all the pending events immediately.

The API uses the `event_id` to deduplicate data automatically. By providing a unique ID for each event, only new events are added to the buffer.

### Carry over context between generation windows

By default, each generation window only processes the events that accumulated since the previous flush. To keep memories coherent across consecutive generation windows, you can carry context over from one window into the next by setting `overlap_event_count` in the `generation_rule` . This re-includes the last *N* already-processed events at the start of the next window.

Carried-over events don't count toward the trigger condition. The `overlap_event_count` value must be a positive integer that is less than `event_count` , and it requires either `event_count` or a time-based rule ( `idle_duration` or `fixed_interval` ).

## Data source

With `IngestEvents` , you provide content by submitting events directly within your application request using [direct\_contents\_source](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#direct-contents-source) in a direct payload.

The following examples showcase different triggers.

#### Example: Event count trigger

This example uses a custom stream and triggers generation when 10 unique events have been accumulated in the stream.

### Dictionary

    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source={
            "events": [
                {
                    "content": {
                        "role": "user",
                        "parts": [{"text": "My favorite color is blue."}]
                    },
                    "event_id": "event-1" # Optional, used for deduplication.
                }
            ]
        },
        generation_trigger_config={
            "generation_rule": {
                "event_count": 10
            }
        },
        scope={"user_id": "123"}
    )

### Class-based

    from google import genai
    from agentplatform import types
    
    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source=types.IngestionDirectContentsSource(
            events=[
                types.IngestionDirectContentsSourceEvent(
                    content=genai.types.Content(
                        role="user",
                        parts=[genai.types.Part.from_text(text="My favorite color is blue.")]
                    ),
                    event_id="event-1" # Optional, used for deduplication.
                )
            ]
        ),
        generation_trigger_config=types.MemoryGenerationTriggerConfig(
            generation_rule=types.MemoryGenerationTriggerConfigGenerationTriggerRule(
                event_count=10
            )
        ),
        scope={"user_id": "123"}
    )

#### Example: Time-based idle duration trigger

This example triggers generation when the stream has not received a new event for 5 minutes ( `300s` ). It also sets a custom `stream_id` .

### Dictionary

    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source={
            "events": [
                {
                    "content": {
                        "role": "user",
                        "parts": [{"text": "I will be back in a bit."}]
                    },
                    "event_id": "event-2" # Optional, used for deduplication.
                }
            ]
        },
        generation_trigger_config={
            "generation_rule": {
                "idle_duration": "300s"
            }
        },
        scope={"user_id": "123"}
    )

### Class-based

    from google import genai
    from agentplatform import types
    
    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source=types.IngestionDirectContentsSource(
            events=[
                types.IngestionDirectContentsSourceEvent(
                    content=genai.types.Content(
                        role="user",
                        parts=[genai.types.Part.from_text(text="I will be back in a bit.")]
                    ),
                    event_id="event-2" # Optional, used for deduplication.
                )
            ]
        ),
        generation_trigger_config=types.MemoryGenerationTriggerConfig(
            generation_rule=types.MemoryGenerationTriggerConfigGenerationTriggerRule(
                idle_duration="300s"
            )
        ),
        scope={"user_id": "123"}
    )

#### Example: Force flush events

This example unconditionally bypasses any trigger conditions and immediately forces all pending events in the stream to be flushed and processed.

### Dictionary

    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source={
            "events": [
                {
                    "content": {
                        "role": "user",
                        "parts": [{"text": "That's all for today!"}]
                    },
                }
            ]
        },
        config={
            "force_flush": True
        },
        scope={"user_id": "123"}
    )

### Class-based

    from google import genai
    from agentplatform import types
    
    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source=types.IngestionDirectContentsSource(
            events=[
                types.IngestionDirectContentsSourceEvent(
                    content=genai.types.Content(
                        role="user",
                        parts=[genai.types.Part.from_text(text="That's all for today!")]
                    ),
                )
            ]
        ),
        config=types.IngestEventsConfig(
            force_flush=True
        ),
        scope={"user_id": "123"}
    )

#### Example: Carry over context between windows

This example triggers generation every 10 unique events and re-includes the last 2 already-processed events in the next window so that memories stay coherent across windows.

### Dictionary

    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source={
            "events": [
                {
                    "content": {
                        "role": "user",
                        "parts": [{"text": "Let's continue where we left off."}]
                    },
                }
            ]
        },
        generation_trigger_config={
            "generation_rule": {
                "event_count": 10,
                "overlap_event_count": 2
            }
        },
        scope={"user_id": "123"}
    )

### Class-based

    from google import genai
    from agentplatform import types
    
    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source=types.IngestionDirectContentsSource(
            events=[
                types.IngestionDirectContentsSourceEvent(
                    content=genai.types.Content(
                        role="user",
                        parts=[genai.types.Part.from_text(text="Let's continue where we left off.")]
                    ),
                )
            ]
        ),
        generation_trigger_config=types.MemoryGenerationTriggerConfig(
            generation_rule=types.MemoryGenerationTriggerConfigGenerationTriggerRule(
                event_count=10,
                overlap_event_count=2
            )
        ),
        scope={"user_id": "123"}
    )

## Configure memory revisions

Like `GenerateMemories` , `IngestEvents` creates [memory revisions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/revisions) for the memories that it generates. You can configure the revisions that result from an ingestion request by setting the following fields in the `config` :

  - **Revision labels** ( `revision_labels` ): Key-value pairs that are applied to the generated memory revisions. For example, you can label a revision with its data source and later [filter revisions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/revisions#list-memory-revisions) by that label.
  - **Revision expiration** ( `revision_expire_time` or `revision_ttl` ): Controls when the generated memory revisions [expire](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/revisions#revision-expiration) . If you don't set an expiration, Memory Bank uses the instance configuration or the default time to live (TTL) of 365 days.
  - **Disable revisions** ( `disable_memory_revisions` ): If `True` , Memory Bank [doesn't create revisions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/revisions#disable-memory-revisions) for the memories that are generated from this request.

The following example labels the generated revisions with a data source and keeps them for 30 days:

### Dictionary

    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source={
            "events": [
                {
                    "content": {
                        "role": "user",
                        "parts": [{"text": "My favorite color is blue."}]
                    },
                }
            ]
        },
        generation_trigger_config={
            "generation_rule": {
                "event_count": 10
            }
        },
        config={
            "revision_labels": {"data_source": "321"},
            # Persist memory revisions for 30 days after they're created.
            "revision_ttl": f"{30 * 60 * 60 * 24}s"
        },
        scope={"user_id": "123"}
    )

### Class-based

    from google import genai
    from agentplatform import types
    
    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source=types.IngestionDirectContentsSource(
            events=[
                types.IngestionDirectContentsSourceEvent(
                    content=genai.types.Content(
                        role="user",
                        parts=[genai.types.Part.from_text(text="My favorite color is blue.")]
                    ),
                )
            ]
        ),
        generation_trigger_config=types.MemoryGenerationTriggerConfig(
            generation_rule=types.MemoryGenerationTriggerConfigGenerationTriggerRule(
                event_count=10
            )
        ),
        config=types.IngestEventsConfig(
            revision_labels={"data_source": "321"},
            # Persist memory revisions for 30 days after they're created.
            revision_ttl=f"{30 * 60 * 60 * 24}s"
        ),
        scope={"user_id": "123"}
    )

## Attach metadata to generated memories

You can attach [metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#metadata) to the memories that are generated from ingested events. Metadata lets you store structured information (strings, doubles, booleans, or timestamps) alongside a memory fact, which is useful for [filtering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories#metadata-filter) or managing the lifecycles of your memories.

Use `metadata_merge_strategy` to control how the metadata interacts with existing memories during consolidation. You can set it to `OVERWRITE` (the default when unset), `MERGE` , or `REQUIRE_EXACT_MATCH` . For more information, see [Using metadata during consolidation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#metadata) .

### Dictionary

    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source={
            "events": [
                {
                    "content": {
                        "role": "user",
                        "parts": [{"text": "My favorite color is blue."}]
                    },
                }
            ]
        },
        generation_trigger_config={
            "generation_rule": {
                "event_count": 10
            }
        },
        config={
            "metadata": {
                "my_string_key": {"string_value": "my_string_value"},
                "my_boolean_key": {"bool_value": True}
            },
            "metadata_merge_strategy": "MERGE"
        },
        scope={"user_id": "123"}
    )

### Class-based

    from google import genai
    from agentplatform import types
    
    client.agent_engines.memories.ingest_events(
        name=memory_bank.api_resource.name,
        stream_id="my-custom-stream",
        direct_contents_source=types.IngestionDirectContentsSource(
            events=[
                types.IngestionDirectContentsSourceEvent(
                    content=genai.types.Content(
                        role="user",
                        parts=[genai.types.Part.from_text(text="My favorite color is blue.")]
                    ),
                )
            ]
        ),
        generation_trigger_config=types.MemoryGenerationTriggerConfig(
            generation_rule=types.MemoryGenerationTriggerConfigGenerationTriggerRule(
                event_count=10
            )
        ),
        config=types.IngestEventsConfig(
            metadata={
                "my_string_key": types.MemoryMetadataValue(string_value="my_string_value"),
                "my_boolean_key": types.MemoryMetadataValue(bool_value=True)
            },
            metadata_merge_strategy=types.MemoryMetadataMergeStrategy.MERGE
        ),
        scope={"user_id": "123"}
    )

## What's next

  - [Fetch generated memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories)
  - [Inspect memory revisions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/revisions)
