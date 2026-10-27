---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores
title: 'REST Resource: projects.locations.dataStores'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: DataStore

Message describing a DataStore object. A DataStore, owned directly by a Project, holds a set of related Documents that share a single, immutable DocumentType, together with the configuration used to process them. Imported Documents are split into segments, embedded, and stored in the DataStore's backing Collection (see `collectionName` ).

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "documentType": enum (DocumentType),
  "processingConfig": {
    object (ProcessingConfig)
  },
  "state": enum (State),
  "collectionName": string,
  "documentMetadataSchema": {
    object (DocumentMetadataSchema)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                   | `string` Identifier. The fully qualified resource name of the DataStore. Format: `projects/{project}/locations/{location}/dataStores/{dataStoreId}`                                                                                                                                                                                                                                                                                                                                                                                               |
| `displayName`            | `string` Optional. User-specified display name of the DataStore.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `description`            | `string` Optional. User-specified description of the DataStore.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `createTime`             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Create time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                              |
| `updateTime`             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Update time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                              |
| `labels`                 | `map (key: string, value: string)` Optional. Labels as key value pairs. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                                                                     |
| `documentType`           | `enum ( `[`DocumentType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#DocumentType)` )` Required. Immutable. The immutable content type of all Documents in this DataStore.                                                                                                                                                                                                                                                                          |
| `processingConfig`       | `object ( `[`ProcessingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#ProcessingConfig)` )` Optional. Configuration controlling how Documents in this DataStore are ingested (parsed, segmented and embedded). Can be changed with dataStores.patch. A change applies only to Documents processed after it: Documents already in the DataStore keep their existing segments, and re-importing a file that hasn't changed doesn't reprocess it. |
| `state`                  | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#State)` )` Output only. The state of the DataStore.                                                                                                                                                                                                                                                                                                                                   |
| `collectionName`         | `string` Output only. The resource name of the Collection backing this DataStore, in the form `projects/{project}/locations/{location}/collections/{collectionId}` . `collectionId` is `google-{dataStoreId}` , or `google-` followed by a hash of the DataStore ID when that would be longer than 63 characters. Populated once the backing Collection has been created.                                                                                                                                                                         |
| `documentMetadataSchema` | `object ( `[`DocumentMetadataSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#DocumentMetadataSchema)` )` Optional. Schema for user-defined metadata on Documents in this DataStore. The schema will be validated against [JSON Schema Draft 7](https://json-schema.org/draft-07/schema) . The schema can be extended later with dataStores.patch by adding properties; existing properties can't be removed or changed.                         |

## DocumentType

The content type of the Documents in a DataStore. All Documents in a DataStore share a single, immutable DocumentType.

| Enums                       |                                                                                              |
|-----------------------------|----------------------------------------------------------------------------------------------|
| `DOCUMENT_TYPE_UNSPECIFIED` | Default value, the document type is not specified.                                           |
| `UNSTRUCTURED`              | Text documents: PDF, plain text, Word, PowerPoint and Excel files, optionally with metadata. |
| `VIDEO`                     | Video documents, optionally with metadata.                                                   |

## ProcessingConfig

ProcessingConfig controls how Documents in a DataStore are parsed, segmented and embedded.

**JSON representation**

```
{
  "videoProcessingConfig": {
    object (VideoProcessingConfig)
  },
  "unstructuredProcessingConfig": {
    object (UnstructuredProcessingConfig)
  }
}
```

| Fields                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `videoProcessingConfig`        | `object ( `[`VideoProcessingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#VideoProcessingConfig)` )` Optional. Configuration for the video ingestion pipeline. Applies when the DataStore's `documentType` is `VIDEO` . If unset for a `VIDEO` DataStore, the pipeline defaults to fixed-window segmentation with a 30s window size, and audio disabled during per-segment embedding generation.                                               |
| `unstructuredProcessingConfig` | `object ( `[`UnstructuredProcessingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#UnstructuredProcessingConfig)` )` Optional. Configuration for the unstructured document ingestion pipeline. Applies when the DataStore's `documentType` is `UNSTRUCTURED` . If unset for an `UNSTRUCTURED` DataStore, the pipeline defaults to chunk segmentation with a `chunkSize` of 500, digital parsing, and text-only per-segment embedding generation. |

## VideoProcessingConfig

Configures the video ingestion pipeline applied to Documents ingested into this DataStore. Segmentation and embedding settings can evolve independently while remaining grouped in this message.

All sub-configurations are optional. Any omitted sub-configuration falls back to the platform default documented on that field.

**JSON representation**

```
{
  "segmentationConfig": {
    object (VideoSegmentationConfig)
  },
  "embeddingConfig": {
    object (VideoEmbeddingGenerationConfig)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `segmentationConfig` | `object ( `[`VideoSegmentationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#VideoSegmentationConfig)` )` Optional. Controls how videos are split into segments prior to embedding. If unset, defaults to fixed-window segmentation with a 30s window. If set, a segmentation mode such as `fixedWindowConfig` must be set; an empty config is rejected. |
| `embeddingConfig`    | `object ( `[`VideoEmbeddingGenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#VideoEmbeddingGenerationConfig)` )` Optional. Controls how the per-segment multimodal embedding is generated.                                                                                                                                                        |

## VideoSegmentationConfig

Configures how videos are broken down into segments prior to embedding.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "fixedWindowConfig": {
    object (FixedWindowConfig)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                             |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Required. Exactly one segmentation mode must be chosen. This isolates configuration so users cannot set fields that do not apply to their selected mode. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                             |
| `fixedWindowConfig`                                                                                                                                                                                                                                                 | `object ( `[`FixedWindowConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#FixedWindowConfig)` )` Fixed-window (deterministic) segmentation. |
| End of mutually exclusive fields.                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                             |

## FixedWindowConfig

Configures fixed-window segmentation. Segments are produced as deterministic, non-overlapping windows of `segmentDuration` each.

**JSON representation**

```
{
  "segmentDuration": string
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `segmentDuration` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. Specifies the fixed window size for each emitted segment. If unset, defaults to 30s. When explicitly set, must be greater than 5s and less than or equal to 80s. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |

## VideoEmbeddingGenerationConfig

Configures how per-segment multimodal embeddings are generated for the video modality.

**JSON representation**

```
{
  "audioMode": enum (AudioMode)
}
```

| Fields      |                                                                                                                                                                                                                                                                               |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `audioMode` | `enum ( `[`AudioMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#AudioMode)` )` Optional. Controls whether the audio track contributes to the embedding. Defaults to DISABLED. |

## AudioMode

Specifies how the audio track of the source video should be treated when generating per-segment embeddings.

This enum is frozen; new values are not expected.

| Enums                    |                                                                                                                                                                                                                                                                  |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `AUDIO_MODE_UNSPECIFIED` | Unspecified. Treated as DISABLED.                                                                                                                                                                                                                                |
| `ENABLED`                | Multiplexes the audio track into the multimodal embedding alongside video frames. Improves recall for queries that depend on spoken content or ambient sound (e.g. dialog-driven news, sports commentary), at the cost of a larger embedding-request token size. |
| `DISABLED`               | Drops the audio track and generates embeddings from visual frames only. Default.                                                                                                                                                                                 |

## UnstructuredProcessingConfig

Configuration for the unstructured document ingestion pipeline applied to Documents ingested into this DataStore. Segmentation and parsing settings can evolve independently while remaining grouped in this message.

All sub-configurations are optional; any omitted sub-configuration falls back to the platform default documented on that field.

**JSON representation**

```
{
  "segmentationConfig": {
    object (UnstructuredSegmentationConfig)
  },
  "parsingConfig": {
    object (UnstructuredParsingConfig)
  },
  "embeddingConfig": {
    object (UnstructuredEmbeddingConfig)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `segmentationConfig` | `object ( `[`UnstructuredSegmentationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#UnstructuredSegmentationConfig)` )` Optional. Controls how unstructured documents are split into segments prior to embedding. If unset, defaults to chunk segmentation with a `chunkSize` of 500. If set, exactly one of `chunkSegmentationConfig` or `pageSegmentationConfig` must be set; an empty config is rejected.                                                                                                                |
| `parsingConfig`      | `object ( `[`UnstructuredParsingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#UnstructuredParsingConfig)` )` Optional. The parsing config, applied to all file types for unstructured document parsing. Plain-text ( `.txt` ) files are always parsed digitally. If unset, defaults to digital (native text extraction) parsing, or to layout-aware parsing when `embeddingConfig.mode` is `MULTIMODAL` . If set, exactly one of `digitalParsingConfig` or `layoutParsingConfig` must be set; an empty config is rejected. |
| `embeddingConfig`    | `object ( `[`UnstructuredEmbeddingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#UnstructuredEmbeddingConfig)` )` Optional. Controls how the per-segment embedding is generated.                                                                                                                                                                                                                                                                                                                                            |

## UnstructuredSegmentationConfig

Configures how unstructured documents are broken down into segments prior to embedding.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "chunkSegmentationConfig": {
    object (ChunkSegmentationConfig)
  },
  "pageSegmentationConfig": {
    object (PageSegmentationConfig)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                        |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Required. Exactly one segmentation mode must be chosen. This isolates configuration so users cannot set fields that do not apply to their selected mode. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                        |
| `chunkSegmentationConfig`                                                                                                                                                                                                                                           | `object ( `[`ChunkSegmentationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#ChunkSegmentationConfig)` )` Chunk-level segmentation. |
| `pageSegmentationConfig`                                                                                                                                                                                                                                            | `object ( `[`PageSegmentationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#PageSegmentationConfig)` )` Page-level segmentation.    |
| End of mutually exclusive fields.                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                        |

## ChunkSegmentationConfig

The chunk segmentation configurations for unstructured documents. Segments are produced as semantic chunks (e.g. by paragraph).

**JSON representation**

```
{
  "chunkSize": integer,
  "includeAncestorHeadings": boolean
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                                                                         |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `chunkSize`               | `integer` Optional. The token size limit for each chunk. Supported values: 100-500 (inclusive). If unset, defaults to 500.                                                                                                                                                                                                                              |
| `includeAncestorHeadings` | `boolean` Optional. Whether each chunk also includes the headings of the sections it belongs to, so that a chunk taken from the middle of a section keeps its context. Headings are only detected by layout parsing ( `layoutParsingConfig` ). With digital parsing, and for plain-text files, this setting has no effect. If unset, defaults to false. |

## PageSegmentationConfig

This type has no fields.

The page segmentation configurations for unstructured documents. Segments are produced at the page level.

Use with digital parsing. With `layoutParsingConfig` , PDF files fail to import, and Word, PowerPoint and Excel files are split into chunks instead.

## UnstructuredParsingConfig

Related configurations applied to a specific type of unstructured document parser.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "digitalParsingConfig": {
    object (DigitalParsingConfig)
  },
  "layoutParsingConfig": {
    object (LayoutParsingConfig)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Required. Exactly one parsing mode must be chosen. This isolates configuration so users cannot set fields that do not apply to their selected mode. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                  |
| `digitalParsingConfig`                                                                                                                                                                                                                                         | `object ( `[`DigitalParsingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#DigitalParsingConfig)` )` Digital (native text extraction) parsing. |
| `layoutParsingConfig`                                                                                                                                                                                                                                          | `object ( `[`LayoutParsingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#LayoutParsingConfig)` )` Layout-aware parsing.                       |
| End of mutually exclusive fields.                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                  |

## DigitalParsingConfig

This type has no fields.

The digital parsing configurations for unstructured documents. Extracts the text stored in the file, without OCR or layout detection: text that appears only in images isn't extracted, and headings and tables aren't detected.

## LayoutParsingConfig

This type has no fields.

The layout parsing configurations for unstructured documents. Detects the document's structure, such as headings and tables, and runs OCR on PDF files. Required for `includeAncestorHeadings` to have an effect, and for `MULTIMODAL` embedding.

## UnstructuredEmbeddingConfig

Configures how per-segment embeddings are generated for the unstructured document modality.

**JSON representation**

```
{
  "mode": enum (EmbeddingMode)
}
```

| Fields |                                                                                                                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode` | `enum ( `[`EmbeddingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#EmbeddingMode)` )` Optional. Controls what a segment's embedding is computed from. Defaults to `TEXT` . |

## EmbeddingMode

What a segment's embedding is computed from.

| Enums                        |                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------|
| `EMBEDDING_MODE_UNSPECIFIED` | Unspecified. Treated as TEXT.                                                              |
| `TEXT`                       | Text only. Images extracted from the document do not contribute to the embedding. Default. |

## State

The state of the DataStore.

| Enums               |                                                                |
|---------------------|----------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The default value. This value is used if the state is omitted. |
| `CREATING`          | The DataStore is being created.                                |
| `ACTIVE`            | The DataStore is ready for use.                                |
| `DELETING`          | The DataStore is being deleted.                                |

## DocumentMetadataSchema

Schema for user-defined metadata on Documents in a DataStore.

**JSON representation**

```
{
  "schema": {
    object
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `schema` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The JSON schema for Document metadata. The schema will be validated against [JSON Schema Draft 7](https://json-schema.org/draft-07/schema) . Property names may contain only letters, digits, `_` and `-` , and must not start with `google` in any letter case; that prefix is reserved. The `additionalProperties` keyword is not supported within `properties` . |

| Methods                                                                                                                                                                       |                                                                          |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/create)                   | Creates a new DataStore in a given project and location.                 |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/delete)                   | Deletes a single DataStore.                                              |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/get)                         | Gets details of a single DataStore.                                      |
| [`importDocuments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/importDocuments) | Initiates a Long-Running Operation to import Documents into a DataStore. |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/list)                       | Lists DataStores in a given project and location.                        |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/patch)                     | Updates the parameters of a single DataStore.                            |
| [`purgeDocuments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/purgeDocuments)   | Initiates a Long-Running Operation to purge Documents from a DataStore.  |
