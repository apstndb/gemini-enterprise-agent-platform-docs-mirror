---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores
title: Search documents in a data store
description: Learn how to configure data stores with documents that can be searched using Agent Retrieval (formerly Vector Search 2.0).
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The managed ingestion pipeline imports document and video files from data stores into Agent Retrieval as [Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) and [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) you can search with text queries, and automatically handles parsing, segmentation, embedding, and indexing for you.

> To see examples of importing and searching documents and videos in a data store, run the following notebooks in the environment of your choice:
>
> - "Search Your Documents with SearchDocuments in Agent Retrieval":
>
>   [Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/embeddings/agent-retrieval-search-documents.ipynb) \| [Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fagent-retrieval-search-documents.ipynb) \| [Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fagent-retrieval-search-documents.ipynb) \| [View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/embeddings/agent-retrieval-search-documents.ipynb)
>
> - "Search Inside Videos with Managed Video Ingestion in Agent Retrieval":
>
>   [Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/embeddings/agent-retrieval-video-search.ipynb) \| [Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fagent-retrieval-video-search.ipynb) \| [Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fagent-retrieval-video-search.ipynb) \| [View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/embeddings/agent-retrieval-video-search.ipynb)

## Supported document formats

The following table lists the supported document file formats and file extensions.

| Document type                 | File extension                           |
|-------------------------------|------------------------------------------|
| HTML                          | `.html` , `.htm`                         |
| JSON                          | `.json`                                  |
| PDF                           | `.pdf`                                   |
| Plain-Text                    | `.txt`                                   |
| Markdown                      | `.md`                                    |
| Microsoft Excel               | `.xlsx`                                  |
| Microsoft Macro-enabled Excel | `.xlsm` (scripts and macros are ignored) |
| Microsoft PowerPoint          | `.pptx`                                  |
| Microsoft Word                | `.docx`                                  |
| XML                           | `.xml`                                   |

> **Note:** Managed ingestion requires documents have the correct file extension as shown in the table.  
>   
> There is no character set detection. All UTF-8 characters are valid. UTF-16 isn't supported. Other characters are decoded as Latin-1 where possible, and invalid bytes are replaced with spaces. UTF-8 BOM is kept in search results.

## Supported video formats and codecs

The following table lists the supported video file formats and file extensions.

| Video format                     | File extension  |
|----------------------------------|-----------------|
| AVI                              | `.avi`          |
| Matroska                         | `.mkv`          |
| MPEG and MPEG-2 transport stream | `.ts` , `.m2ts` |
| MPEG-4 Part 14                   | `.mp4`          |
| MXF (OP1A only)                  | `.mxf`          |
| QuickTime                        | `.mov`          |
| WebM                             | `.webm`         |
| Windows Media (ASF)              | `.wmv`          |

The following codecs are supported:

- DNxHD
- DV
- H.264, H.265
- MPEG-1, MPEG-2, MPEG-4 part 2
- ProRes
- Theora
- VC-1
- VP8, VP9
- XAVC
- XDCAM

> **Note:** To ingest a video file, the video format must be supported and have the corresponding file extension, and the video codec must be supported. For an up-to-date list of supported video formats and video codecs, see [Supported input formats](https://docs.cloud.google.com/transcoder/docs/concepts/supported-input-and-output-formats) .

## Prerequisites

Before you begin, you need:

- A Google Cloud project. For information on how to create a Google Cloud project, see [Set up a project and a development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment) .

- A Cloud Storage [bucket](https://docs.cloud.google.com/storage/docs/buckets) containing the [document or video files](https://docs.cloud.google.com/storage/docs/objects) you want to search.

- The [`roles/vectorsearch.serviceAgent`](https://docs.cloud.google.com/iam/docs/roles-permissions/vectorsearch#vectorsearch.serviceAgent) permission granted to the service agent `service-<var>PROJECT_NUMBER</var>@gcp-sa-vectorsearch.iam.gserviceaccount.com` on the bucket's project.

## Examples

The examples on this page build off of the following sample files.

### curl

```
PROJECT=acme-prod
LOCATION=us-east4
BASE=https://vectorsearch.googleapis.com/v1alpha
INGEST=${BASE}/projects/${PROJECT}/locations/${LOCATION}
AUTH="Authorization: Bearer $(gcloud auth print-access-token)"
```

### Python

```
import time
import google.auth
from google.auth.transport.requests import AuthorizedSession

PROJECT = "acme-prod"          # Replace with your project ID
LOCATION = "us-east4"          # Replace with your region

credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
session = AuthorizedSession(credentials)

BASE = "https://vectorsearch.googleapis.com/v1alpha"
INGEST = BASE + "/projects/" + PROJECT + "/locations/" + LOCATION

def wait(operation, poll_seconds=10):
    """Poll a long-running operation until it finishes, then return it."""
    name = operation["name"]
    while True:
        op = session.get(BASE + "/" + name).json()
        if op.get("done"):
            if "error" in op:
                raise RuntimeError(op["error"])
            return op
        meta = op.get("metadata", {})
        print("in progress:", meta)
        time.sleep(poll_seconds)
```

## The managed ingestion pipeline

The managed ingestion pipeline imports documents and videos from your data store into Agent Retrieval and does most of the work setting up [Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) and [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) for you.

> **Note:** Only one type of file (document or video) is supported per data store.

All you need to do is:

1.  [Stage your document or video files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#stage) .

2.  [Create a data store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#create-data-store) .

3.  [Import your video or document files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#import) .

4.  [Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#search) your files with text queries.

## 1. Stage your document or video files

[Create a bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) and [add the document or video files](https://docs.cloud.google.com/storage/docs/uploading-objects) that you want to search. You don't need to create a manifest.

Document managed ingestion:

- Skips over document files larger than 200 MB.

- Imports up to 100,000 documents at a time.

- Ignores macros and scripts in Microsoft Macro-enabled Excel ( `.xlsm` ) document files.

Video managed ingestion:

- Skips over video files larger than 600 GB.

- Skips over video files longer than 15 hours. For streamable video formats, files are skipped if the estimated duration is greater than the limit or cannot be determined.

- Imports up to 100 videos at a time.

- Ignores video files without a video stream.

> **Note:** You can also stage [JSONL](https://jsonlines.org/) that define metadata for your document and video files. For more information, see [Add metadata for your files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#add-metadata) .

## 2. Create a data store

After you stage the files you want to search, you need to create a data store. The data store provides the source for the managed ingestion pipeline and the configuration specifying how your files are ingested.

Managed ingestion is only available for data stores located in the `us-east4` or `europe-west4` region.

To create a data store, make a `POST` request to the `dataStores` API and provide the following parameter:

- **`data_store_id`** : The ID for the data store being created. This must start with a lowercase letter, end with a lowercase letter or digit, contain only lowercase letters, digits and hyphens, and be from 1 to 63 characters in length.

The JSON payload contains the JSON configuration settings that managed ingestion uses to create the data store and process the files you staged.

The JSON payload must include the top-level property `document_type` . This specifies the types of files to import from the data store. Valid values are:

- `UNSTRUCTURED` : The data store contains document files. See [Supported document formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#document-formats-supported) for a list of supported formats.

- `VIDEO` : The data store contains video files. See [Supported video formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#video-formats-supported) for a list of supported formats and codecs.

The following properties are optional:

- `display_name` : ( `STRING` ) The data store's display name. The maximum size is 1024 bytes. The default is an empty string.

- `description` : ( `STRING` ) The data store's description. The maximum size is 1024 bytes. The default is an empty string.

- `labels` : ( `STRING` array) An array of key-value pairs. For more information, go to [Organize resources using labels](https://docs.cloud.google.com/compute/docs/labeling-resources) . The default is an empty array.

- `processing_config` : ( `OBJECT` ): The configuration for how managed ingestion processes the data in the data store. This can be [updated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#update-processing-config) with a `PATCH` request. For default settings if omitted, see [Optional settings for document data stores](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#optional-settings-document) .

- `document_metadata_schema` : ( `OBJECT` ): The metadata schema for metadata associated with the documents in the data store. For more information, see [Add a metadata schema](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#add-metadata) . The default value is an empty object (no metadata schema).

> **Note:** The embedding model that managed ingestion uses is fixed to [`gemini-embedding-2`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings#use-gemini) with 768 output dimensionality. This cannot be changed.

### Optional settings for document data stores

The following optional settings are available for document data stores:

- `processing_config.unstructured_processing_config.segmentation_config` : ( `OBJECT` ) The ingestion configuration for how to segment the document (search results are per segment, not per document). For more information, see [Document segmentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#document-segmentation) . An empty object causes the request to be rejected with the status `INVALID_ARGUMENT` . If provided, it must include *one* of the following:
  - `page_segmentation_config` : ( `OBJECT` ) This object has no properties.
  - `chunk_segmentation_config` : ( `OBJECT` ) Has the following properties:
    - `chunk_size` : ( `INTEGER` ) The maximum number of tokens in a segment. The minimum value is 300 and the maximum value is 500. The default is 500.
    - `include_ancestor_headings` : ( `BOOL` ) Prepends a chain of section headings to each chunk for context. The default value is `false` .

- `processing_config.unstructured_processing_config.parsing_config` : ( `OBJECT` ) The ingestion configuration for how to parse the document. An empty object causes the request to be rejected with the status `INVALID_ARGUMENT` . If provided, it must include *one* of the following:
  - `layout_parsing_config` : ( `OBJECT` ) Layout parsing will be used. This object has no properties.
  - `digital_parsing_config` : ( `OBJECT` ) Digital parsing will be used. This object has no properties.

- `processing_config.unstructured_processing_config.embedding_config.mode` : ( `STRING` ) The embedding mode to use. Can be:

  - `TEXT` : Only extracted text is embedded. Images are ignored. The default value is `TEXT` .

You can also add metadata to your data store. For more information, see [Add metadata for your files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#add-metadata) .

#### Examples

The following examples demonstrate how to create a document data store.

### curl

```
  curl -X POST -H "${AUTH}" -H "Content-Type: application/json" \
  "${INGEST}/dataStores?data_store_id=acme-financials" \
  -d '{
    "display_name": "Acme financial reports",
    "document_type": "UNSTRUCTURED",
    "processing_config": {
      "unstructured_processing_config": {
        "segmentation_config": {
          "chunk_segmentation_config": {
            "chunk_size": 300,
            "include_ancestor_headings": true
          }
        },
        "parsing_config": {
          "layout_parsing_config": {}
        }
      }
    }
  }'
```

### Python

```
  op = session.post(
    INGEST + "/dataStores",
    params={"data_store_id": "acme-financials"},
    json={
        "display_name": "Acme financial reports",
        "document_type": "UNSTRUCTURED",
        "processing_config": {
            "unstructured_processing_config": {
                "segmentation_config": {
                    "chunk_segmentation_config": {
                        "chunk_size": 300,
                        "include_ancestor_headings": True,
                    }
                },
                "parsing_config": {"layout_parsing_config": {}},
            }
        },
    },
).json()

wait(op)
```

**Sample response**

```
{
  "name": "projects/acme-prod/locations/us-east4/dataStores/acme-financials",
  "documentType": "UNSTRUCTURED",
  "state": "ACTIVE",
  "collectionName": "projects/acme-prod/locations/us-east4/collections/google-acme-financials"
}
```

### Optional settings for video data stores

The following optional settings are available for video data stores:

- `processing_config.video_processing_config.segmentation_config` : ( `OBJECT` ) The ingestion configuration for how to segment the video. An empty object causes the request to be rejected with the status `INVALID_ARGUMENT` . If provided, the ingestion configuration must include:
  - `fixed_window_config` : ( `OBJECT` ) Has the following properties:
    - `segment_duration` : ( `STRING` ) The maximum number of seconds in a segment. The minimum value is `5.01s` and the maximum value is `80s` . The default is `30s` .
- `processing_config.video_processing_config.embedding_config.audio_mode` : ( `STRING` ) The audio mode to use. Only supported when `document_type` is `VIDEO` . The default value is `DISABLED` if not specified. See [Video audio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#video-audio) for more information. Can be:
  - `ENABLED` : Multiplexes the first audio track into the embedding alongside the frames.
  - `DISABLED` : Uses frames only.
  - `AUDIO_MODE_UNSPECIFIED` : Same as `DISABLED` .

#### Examples

The following examples demonstrate how to create a video data store.

### curl

```
  curl -X POST -H "${AUTH}" -H "Content-Type: application/json" \
  "${INGEST}/dataStores?data_store_id=acme-training-video" \
  -d '{
    "display_name": "Acme training video",
    "document_type": "VIDEO",
    "processing_config": {
      "video_processing_config": {
        "segmentation_config": {
          "fixed_window_config": {
            "segment_duration": "20s"
          }
        },
        "embedding_config": {
          "audio_mode": "ENABLED"
        }
      }
    }
  }'
```

### Python

```
  op = session.post(
    INGEST + "/dataStores",
    params={"data_store_id": "acme-training-video"},
    json={
        "display_name": "Acme training video",
        "document_type": "VIDEO",
        "processing_config": {
            "video_processing_config": {
                "segmentation_config": {
                    "fixed_window_config": {"segment_duration": "20s"}
                },
                "embedding_config": {"audio_mode": "ENABLED"},
            }
        },
    },
  ).json()

  wait(op)
```

**Sample response**

```
{
  "name": "projects/acme-prod/locations/us-east4/dataStores/acme-training-video",
  "documentType": "VIDEO",
  "state": "ACTIVE",
  "collectionName": "projects/acme-prod/locations/us-east4/collections/google-acme-training-video"
}
```

### Add metadata for your files

You can define metadata properties for the files you want managed ingestion to import. These properties can be retrieved from the corresponding Data Objects created by the pipeline and are useful for [filtering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) search results.

To define metadata:

1.  Create a [JSONL](https://jsonlines.org/) file. The extension should be `json` or `jsonl` .

2.  Add a JSON object to a new line for every file you want imported and include the following properties:

    - **`name`** : The file's name in the data store. The last segment of the name is used as an ID for the Data Object created for the file.

    - **`content.gcsUri`** : The URI of the file in Cloud Storage.

    - **`metadata.value`** : The file's metadata. The metadata properties are defined in a schema that you specify when you create your data store. For more information, see [Add a metadata schema](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#add-metadata-schema) .

The following example demonstrates a metadata JSONL with `category` , `year` , `tags` , and `issuer` metadata properties.

```
{"name":"projects/acme-prod/locations/us-east4/dataStores/acme-financials/documents/q3-earnings","content":{"gcsUri":"gs://acme-docs/reports/2025-q3-earnings.pdf"},"metadata":{"value":{"category":"earnings","year":2025,"tags":["revenue"],"issuer":{"country":"US"}}}}
{"name":"projects/acme-prod/locations/us-east4/dataStores/acme-financials/documents/covenants","content":{"gcsUri":"gs://acme-docs/reports/covenant-summary.docx"},"metadata":{"value":{"category":"covenant","year":2024,"tags":["credit","debt"]}}}
```

The properties must match a schema you provide when you create the data store.

You will use the JSONL files you created as input URIs when you [import your files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#import) .

#### Add a metadata schema

You can provide a metadata schema in the top-level `document_metadata_schema` property in the data store's JSON configuration. This defines a contract for the metadata you can associate with your documents, which can be retrieved per file or used to [filter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) search results.

Metadata properties must match the schema you provide when you create the data store. The schema closely follows JSON Schema Draft 7. The following data types are supported:

- `string`
- `number`
- `integer`
- `boolean`
- `object` (including properties)
- `array`

Property names can use only letters, digits, underscores ( `_` ), and hyphens ( `-` ), and must not start with `google` (any case), which is a reserved prefix for properties the service writes.

You can add properties later with a `PATCH` request. Properties in the schema cannot be removed or have their data type changed. For more information, see [Update a processing config](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#update-processing-config) .

The following example defines a metadata schema with `category` , `year` , `tags` , and `issuer` metadata properties.

```
"document_metadata_schema": {
  "schema": {
    "type": "object",
    "properties": {
      "category": {"type": "string"},
      "year":     {"type": "integer"},
      "tags":     {"type": "array", "items": {"type": "string"}},
      "issuer":   {"type": "object", "properties": {"country": {"type": "string"}}}
    }
  }
}
```

Metadata is particularly useful for videos. The following example defines a metadata schema for a video with `series` , `language` , and `year` metadata properties.

```
"document_metadata_schema": {
  "schema": {
    "type": "object",
    "properties": {
      "series":     {"type": "string"},
      "language":   {"type": "string"},
      "year":       {"type": "integer"}
    }
  }
}
```

### Update a processing config

After your data store is created, you can can update the processing configuration ( `processing_config` ) with a `PATCH` request.

The following properties can be updated:

- `display_name`
- `description`
- `labels`
- `document_metadata_schema` (only additional properties can be added)

Properties that are being updated must be included in the `update_mask` query parameter.

> **Note:** Changes only affect files imported or modified after the update request.

The following examples demonstrate how to update the `display_name` and `document_metadata_schema` properties of a processing configuration.

### curl

```
curl -X PATCH -H "${AUTH}" -H "Content-Type: application/json" \
"${INGEST}/dataStores/acme-financials?update_mask=display_name,document_metadata_schema" \
-d '{"display_name": "Acme reports",
"document_metadata_schema": {"schema": {"type": "object", "properties": {
"category": {"type": "string"}, "year": {"type": "integer"},
"region": {"type": "string"}}}}}'
```

### Document file segmentation

When [creating your data store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#create-data-store) , you can specify how the managed ingestion pipeline should attempt to segment your document files:

- [Page segmentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#page-segmentation) ( `processing_config.segmentation_config.page_segmentation_config` ): The managed ingestion attempts to segment document files by page.

- [Chunk segmentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#chunk-segmentation) ( `processing_config.segmentation_config.chunk_segmentation_config` ): The managed ingestion segments document files into separate chunks.

If not specified, the default is chunk segmentation. If both are specified, the request fails.

#### Page segmentation

Specifying page segmentation ( `processing_config.segmentation_config.page_segmentation_config` ) instructs the managed ingestion pipeline to segment documents by page or range of pages. If a document doesn't contain page information, such as a text file, they are segmented into pages up to 2.5 MB in size.

Page segmentation is optimized for document retrieval, such as applications that return PDFs or Word documents with each search result. For more information, see [Chunk documents for RAG](https://docs.cloud.google.com/generative-ai-app-builder/docs/parse-chunk-documents#parse-chunk-rag) .

#### Chunk segmentation

Specifying chunk segmentation ( `processing_config.segmentation_config.chunk_segmentation_config` ) instructs the managed ingestion pipeline to segment documents into chunks of up to `processing_config.segmentation_config.chunk_segmentation_config.chunk_size` tokens. By default, the chunk size is 500 tokens (the maximum chunk size). The minimum chunk size is 300.

Large chunks:

- Carry more context.
- Produce fewer segments.
- Can cover several topics that don't match a query, potentially burying relevant information.

Small chunks:

- Carry narrower pieces of text.
- Are more likely to contain only the information matching a query.
- Carry less context, potentially splitting relevant information into multiple segments.

For most long form content, a chunk size of 500 tokens works well. Smaller chunk sizes are better for short, fact-based content or retrieving compact, precise passages of text.

### Video segmentation

A short segment duration ( `10s` to `20s` ) gives more precise timestamps and answers, and it is the right choice when a query maps to a specific moment: a demo step, a slide, a product shot.

A long segment duration ( `60s` to `80s` ) gives each embedding greater context and produces far fewer segments to store and search.

The default ( `30s` ) provides a balance between the two.

You cannot change segment duration after ingestion without re-importing, but you can `PATCH` the data store and re-import; each file's document ID is stable, so the re-import replaces the old segments rather than adding to them.

### Video audio

When `processing_config.video_processing_config.embedding_config.audio_mode` is set to `ENABLED` , managed ingestion uses the dialog audio content from the video for embedding generation. The first audio track is multiplexed into the same multimodal embedding as the video file it's contained in, and a search query matches the video if it matches either the dialog audio or the video content.

Only the first audio track is used. If a video has multiple audio tracks, the other tracks are ignored. If you need to use a different audio track, add it to a separate video file as the first audio track and re-import.

> **Note:** Audio is always transcoded if present. Setting `audio_mode` to `ENABLED` only affects embedding generation.

### Input URIs

The `gcs_source.input_uris` JSON property is a string array that specifies the inputs for a managed ingestion request, such as what files to import from your data store or what to purge from Agent Retrieval.

If `gcs_source.source_format` is unspecified or set to `SOURCE_FORMAT_UNSPECIFIED` (the default), the input URIs can be:

- One or more specific URIs.
- One or more [wildcard patterns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#wildcards) .
- One or more text files.
  - Document IDs are defined one per line. Empty lines are ignored and whitespace is trimmed from each line.

If the `gcs_source.source_format` is set to `SOURCE_FORMAT_DOCUMENT_JSON` , the input URIs are defined in JSONL format. See [Add metadata to documents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#add-metadata) for more details.

#### Wildcards

| Pattern                           | Matches                                                                            |
|-----------------------------------|------------------------------------------------------------------------------------|
| `gs://acme/files/hello_world.xyz` | The specified file.                                                                |
| `gs://acme/files/*`               | Every file matching the specified `document_type` directly in `gs://acme/files/` . |
| `gs://acme/files/*.xyz`           | Every file with the extension `.xyz` .                                             |

Wildcards are not recursive. For example, specifying `gs://acme/files/*` wouldn't import files under `gs://acme/files/2025/` . The wildcard `**` is interpreted the same as `*` . You can either flatten the hierarchy or pass one pattern per level to work around this.

If a pattern does not match, the request fails. For example, if you pass four URIs and one contains a typo, importing does not continue with the other three URIs. Ensure each URI is correct before making an import request.

## 3. Import your files

The next stage in the pipeline is to call `importDocuments` with the URIs of the files in your data store you want ingested.

> **Warning:** The `importDocuments` call is a [long-running operation](https://developers.google.com/workspace/drive/api/guides/long-running-operations) and returns immediately with the operation's name in the response. Wait for the operation to finish before calling `importDocuments` again. Otherwise, the call will fail with the status `409 ABORTED` ( `unable to queue the operation` ). See [Track import progress](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#tracking-import-progress) to learn how to monitor an import job's progress.

The following examples demonstrate how to import documents.

### curl

```
curl -X POST -H "${AUTH}" -H "Content-Type: application/json" \
  "${INGEST}/dataStores/acme-financials:importDocuments" \
  -d '{
    "gcs_source": {
      "input_uris": ["gs://acme-docs/reports/*"]
    },
    "import_output_config": {
      "error_gcs_prefix": "gs://acme-docs/import-errors/"
    }
  }'
```

### Python

```
op = session.post(
    INGEST + "/dataStores/acme-financials:importDocuments",
    json={
        "gcs_source": {"input_uris": ["gs://acme-docs/reports/*"]},
        "import_output_config": {
            "error_gcs_prefix": "gs://acme-docs/import-errors/"
        },
    },
).json()

result = wait(op)
print(result["metadata"]["successCount"], "imported")
# failureCount is not set on import metadata; check error files instead.
```

You can optionally import them with metadata. For more information, see [Add metadata to documents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#add-metadata) .

The following examples demonstrate how to import the metadata JSONL files.

### curl

```
gcloud storage cp docs.jsonl gs://acme-docs/manifests/docs.jsonl
curl -X POST -H "${AUTH}" -H "Content-Type: application/json" \
  "${INGEST}/dataStores/acme-financials:importDocuments" \
  -d '{
    "gcs_source": {
      "input_uris": ["gs://acme-docs/manifests/docs.jsonl"],
      "source_format": "SOURCE_FORMAT_DOCUMENT_JSON"
    },
    "import_output_config": {
      "error_gcs_prefix": "gs://acme-docs/import-errors-json/"
    }
  }'
```

### Python

```
op = session.post(
    INGEST + "/dataStores/acme-financials:importDocuments",
    json={
        "gcs_source": {
            "input_uris": ["gs://acme-docs/manifests/docs.jsonl"],
            "source_format": "SOURCE_FORMAT_DOCUMENT_JSON",
        },
        "import_output_config": {
            "error_gcs_prefix": "gs://acme-docs/import-errors-json/"
        },
    },
).json()

result = wait(op)
```

#### The Collection managed ingestion creates

When you create your data store, managed ingestion creates a Collection in Agent Retrieval using public Agent Retrieval APIs and can be used like any other Agent Retrieval Collection. The Collection is empty until the import operation completes.

For information on how to query the Collection, see [Search your files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#search) .

> **Warning:** Don't modify the Collection schema. The managed ingestion pipeline writes against it.

The following example shows how to get the Collection name from the data store.

### curl

```
curl -H "${AUTH}" "${INGEST}/dataStores/acme-financials"
```

### Python

```
data_store = session.get(INGEST + "/dataStores/acme-financials").json()
collection_name = data_store["collectionName"]
print(collection_name)
```

The following JSON example demonstrates a typical response.

```
{
  "name": "projects/acme-prod/locations/us-east4/dataStores/acme-financials",
  "documentType": "UNSTRUCTURED",
  "state": "ACTIVE",
  "collectionName": "projects/acme-prod/locations/us-east4/collections/google-acme-financials"
}
```

#### Tracking import progress

To track the progress of the import job, poll the operation instead of checking the status of the bucket. The `successCount` field in the response provides the number of files that have been successfully imported.

You can fix errors and make another import request to try again. For more information, see [Re-running an import operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#rerun-import) .

The following examples demonstrate how to poll the operation.

### curl

```
curl -H "${AUTH}" "${BASE}/{OPERATION_NAME}"
```

### Python

```
# To check once, without blocking, using the op returned by the import call:
status = session.get(BASE + "/" + op["name"]).json()
print(status.get("done"), status.get("metadata", {}))
```

The following example demonstrates how to get a list of the files that were imported once the import operation is complete.

### curl

```
curl -H "${AUTH}" "${INGEST}/dataStores/acme-financials/documents"
```

### Python

```
docs = session.get(INGEST + "/dataStores/acme-financials/documents").json()
print(len(docs.get("documents", [])))
```

> **Note:** Expect importing video files to take substantially longer than importing document files. Videos are transcoded and embedded segment by segment. Be aware that counts are by file, and a long video import may appear stalled while transcoding and embedding is in progress.

#### Re-running an import operation

Running additional import operations on the same bucket only processes files that have been modified or added. A file that has already been imported and is unchanged is skipped.

> **Note:** If a file has already been imported and is renamed or moved, it will be imported again. This can cause file contents to be returned in search results multiple times. To fix this, see [Purge files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#purge) .

## Search your files

The [Collection managed ingestion creates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#collection) for you is just like a regular Agent Retrieval Collection. You can [query it and filter the results](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) , [rerank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/reranking) , [index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) , and more.

> **Important:** Your request should specify `RETRIEVAL_QUERY` for the `task_type` . You don't specify an embedding model; the server reads it from the Collection and embeds your query text with the same model that embedded the segments. The embedding call runs with your credentials, so you need `roles/aiplatform.user` on the project; without it search fails with `403 PERMISSION_DENIED` on `aiplatform.endpoints.predict` .

### Examples

The following example demonstrate how to search the contents of files imported from a data store.

### curl

```
COLLECTION=projects/${PROJECT}/locations/${LOCATION}/collections/google-acme-financials

curl -X POST -H "${AUTH}" -H "Content-Type: application/json" \
  "https://vectorsearch.googleapis.com/v1/${COLLECTION}/dataObjects:search" \
  -d '{
    "semantic_search": {
      "search_text": "what is the total revenue?",
      "search_field": "multimodal_embedding",
      "task_type": "RETRIEVAL_QUERY",
      "top_k": 10,
      "output_fields": {
        "data_fields": ["google_document_id", "google_customer_uri", "google_unstructured_details.content_snippet"]
      }
    }
  }'
```

### Python

```
from google.cloud import vectorsearch_v1

# Create the client
search_client = vectorsearch_v1.DataObjectSearchServiceClient()

# Initialize request argument(s)
semantic_search = vectorsearch_v1.SemanticSearch(
    search_text="what is the total revenue?",
    search_field="multimodal_embedding",
    task_type=vectorsearch_v1.EmbeddingTaskType.RETRIEVAL_QUERY,
    top_k=10,
    output_fields=vectorsearch_v1.OutputFields(
        data_fields=["google_document_id", "google_customer_uri", "google_unstructured_details.content_snippet"],
    ),
)
request = vectorsearch_v1.SearchDataObjectsRequest(
    parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
    semantic_search=semantic_search,
)

# Make the request
response = search_client.search_data_objects(request=request)

# Handle the response
for hit in response.results:
    data = dict(hit.data_object.data)
    print(hit.distance, data["google_customer_uri"][0])
    print(data["google_unstructured_details"]["content_snippet"][:200])
```

The parent is the ID of the Collection, not the data store. Use the Collection name obtained in the [previous section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#collection) .

`search_field` must be `multimodal_embedding` whether the data store contains document or video files.

### Search results

You must specify `output_fields` in your search request to specify which properties you want returned. If you don't specify `output_fields` , only the `distance` and `data_object_id` are returned.

Search results can contain the following properties:

| Property                                                       | Type                    | Description                                                                                                                      |
|----------------------------------------------------------------|-------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| `google_document_id`                                           | string                  | The document the segment came from.                                                                                              |
| `google_customer_uri`                                          | string array            | Your original `gs://` URI for citation.                                                                                          |
| `google_modality`                                              | string                  | `UNSTRUCTURED` or `VIDEO` .                                                                                                      |
| `google_unstructured_details`                                  | object                  | Details for unstructured content. Empty if `google_modality` is `VIDEO` .                                                        |
| `google_unstructured_details.content_snippet`                  | string                  | The segment text.                                                                                                                |
| `google_unstructured_details.start_page` / `end_page`          | integer                 | Page span of the chunk. Populated only with page segmentation, which requires digital parsing; empty for chunk segmentation.     |
| `google_video_details`                                         | object                  | Details for video content. Empty if `google_modality` is `UNSTRUCTURED` .                                                        |
| `google_video_details.start_offset_nanos` / `end_offset_nanos` | integer                 | Time span of a video segment in nanoseconds.                                                                                     |
| `multimodal_embedding`                                         | Vector, dense, 768 dims | The chunk embedding from `gemini-embedding-2` .                                                                                  |
| `metadata`                                                     | object                  | Copied from the document onto each of its segments, unprefixed and nested as declared (such aS `category` or `issuer.country` ). |

For document files, `start_page` and `end_page` are only populated if [page segmentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#page-segmentation) was specified when the data store was [created](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#create-data-store) .

Offsets are in nanoseconds, and are relative to the source video. Divide by 1,000,000,000 for the seconds you need to build a deep link or a player seek.

The properties in `metadata` correspond to the JSON schema provided during [import](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#import-data-store) .

For video files, several consecutive segments from the same video often match one query. Group hits by `google_document_id` and keep the earliest `start_offset_nanos` in each run if you want one result per scene rather than one per segment.

## Purge files

To purge a file from a data store, upload one or more text files to Cloud Storage with each line containing the ID of a file you want to purged. Pass the URIs of the text files to a `purgeDocuments` .

The response doesn't indicate which files are purged. To verify a file has been purged, call `GetDocument` . The response will return the status `404` .

Set `force` to `false` to test the purge operation first. This will log the files that will be purged to the `error_gcs_prefix` you specify.

Once the files have been purged, you can [delete the data store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search-data-stores#delete-data-store) that contains the files that were purged.

The following examples demonstrate how to purge files.

### curl

```
curl -X POST -H "${AUTH}" -H "Content-Type: application/json" \
"${INGEST}/dataStores/acme:purgeDocuments" \
-d '{
  "gcs_source": {
    "input_uris": ["gs://acme/purge/purge-ids.txt"]
  },
  "purge_output_config": {
    "error_gcs_prefix": "gs://acme/purge-force-errors/"
  },
  "force": true
}'
```

### Python

```
op = session.post(
  INGEST + "/dataStores/acme:purgeDocuments",
  json={
      "gcs_source": {
            "input_uris": ["gs://acme/purge/purge-ids.txt"],
        },
        "purge_output_config": {
            "error_gcs_prefix": "gs://acme/purge-force-errors/",
        },
        "force": True,
    },
).json()

result = wait(op)
```

## Delete a data store

Send a `DELETE` request with the data store URI to delete the data store. If `force` is set to `true` and the data store still contains files, the request will fail with the status `FAILED_PRECONDITION` and the message `DataStore deletion is not allowed because it still contains documents. Set force=true to delete the DataStore and all its Documents.` .

Set `backing_collection_deleted` to `true` to delete the Collection and Data Objects created after importing the data store. If this is not done, the Collection and Data Objects remain and continues using quota, and any request to create a new data store with the same ID will fail with the message `FAILED_PRECONDITION (BACKING_COLLECTION_ALREADY_EXISTS)` .

When the delete request is running, a `get` request returns the status `DELETING` and a `404` error after it completes.

The following example demonstrates how to delete a data store.

### curl

```
curl -X DELETE -H "${AUTH}" \
  "${INGEST}/dataStores/acme-financials?force=true&backing_collection_deleted=true"
```

### Python

```
op = session.delete(
  INGEST + "/dataStores/acme-financials",
  params={"force": "true", "backing_collection_deleted": "true"},
).json()

result = wait(op)
```
