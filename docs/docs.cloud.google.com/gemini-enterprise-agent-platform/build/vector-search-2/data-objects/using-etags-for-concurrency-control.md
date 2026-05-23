---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/using-etags-for-concurrency-control
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/using-etags-for-concurrency-control
title: Use ETags for Data Object Concurrency Control
description: Learn how to use ETags for concurrency control of Data Objects in Vector Search 2.0.
data_source: docs.cloud.google.com
---

Vector Search 2.0 supports **Optimistic Concurrency Control (OCC)** using ETags (entity tags), which are opaque identifiers representing specific [Data Object](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) versions.

When multiple processes operate concurrently on the same dataset, such as real-time API updates and bulk import jobs there is a risk of them overwriting each other's changes (a *last-write-wins* scenario). ETags let you guarantee data integrity and ensure that another process hasn't modified a record since you last read it.

## How ETags work

1.  **Read** : When you [create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#creating_a_data_object) or [get](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#get_a_data_object) a Data Object, the server returns an ETag string representing the Data Object's exact version.

2.  **Modify** : You make your changes to the Data Object locally.

3.  **Write** : You send the [update](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#updating_a_data_object) or [delete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#delete_data_objects) request back to Vector Search 2.0, including the ETag you originally received.

4.  **Verify** : The server checks if the provided ETag matches the current ETag stored in the database.
    
      - If they **match** , the operation succeeds and the server returns a new ETag for the updated Data Object.
      - If they **do not match** , the operation is blocked and the server returns the `ABORTED` error (HTTP **409 Conflict** ).

> **Note:** If your request omits the ETag, Vector Search 2.0 overwrites the existing data without checking for conflicts.

## Retrieving ETags

Before you can use an ETag for concurrency control, you need to retrieve the latest version from the system.

ETags can be retrieved the following ways:

  - **Real-Time API Responses** : When you call read or write methods on the `DataObjectService` (such as `GetDataObject` , `ListDataObjects` , `CreateDataObject` , or `UpdateDataObject` ), the returned Data Object resource includes its current ETag.

  - **Import API Output** : When you call `ImportDataObjects` , you can specify a URI prefix to a Cloud Storage in the `GcsImportConfig` field `output-uri` . If the import job succeeds, [JSONL](https://jsonlines.org/) files are created with each line containing the IDs and ETags for imported Data Objects. This is in the following format:
    
    `{ "id": "movie-789", "etag": "a3b8c1d9-e4f2-4a1b-9c8d-0e6f7a8b9c0d"}`
    
    > **Note:** Any errors encountered during the import job are written to files at the URI prefix specified in the required field `error_uri` .

  - **Export API ( `ExportDataObjects` )** - When you export data from Vector Search 2.0 to Cloud Storage, the resulting canonical JSONL data files contain the ETags for all exported Data Objects.

## Creating Data Objects

When calling `CreateDataObject` or `BatchCreateDataObjects` , any ETag you provide in the request is ignored because the Data Object does not exist yet.

When the create request is successful, the server includes the newly generated ETag in the returned Data Object resource.

## Updating Data Objects

To safely update an existing record using `UpdateDataObject` or `BatchUpdateDataObjects` , include the ETag directly within the Data Object resource in your request.

    {
      "name": "projects/my-project/locations/us-central1/collections/my-collection/dataObjects/movie-789",
      "etag": "a3b8c1d9-e4f2-4a1b-9c8d-0e6f7a8b9c0d",
      "data": {
        "genre": ["science-fiction", "thriller", "action"]
      }
    }

## Deleting Data Objects

Because the `DeleteDataObject` and `BatchDeleteDataObjects` methods don't take a full Data Object resource as their payload, the ETag must be provided as a top-level field in the `DeleteDataObjectRequest` .

    {
      "name": "projects/my-project/locations/us-central1/collections/my-collection/dataObjects/movie-789",
      "etag": "a3b8c1d9-e4f2-4a1b-9c8d-0e6f7a8b9c0d"
    }

## Using ETags with bulk ingestion ( `ImportDataObjects` )

Using the `ImportDataObjects` API runs asynchronously and can potentially collide with real-time updates. Include the `etag` field in your [JSONL](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/using-etags-for-concurrency-control#jsonl) import files to enforce concurrency control during imports.

Vector Search automatically detects the conflict resolution mode on a per-record basis:

  - **With ETag (OCC)** : If an ETag is provided and does not match the server's current version, the specific record will fail to import. The failure is then logged to your specified error URI, but the rest of the import job continues.

  - **Without ETag** : If the ETag is omitted, the record is ingested, overriding any existing data. This maximizes throughput when concurrency control isn't necessary.

### JSONL format

Include the ETag at the root level of the JSON object in your import file as shown in the following example.

    { "id": "movie-789", "etag": "a3b8c1d9-e4f2-4a1b-9c8d-0e6f7a8b9c0d", "data":{ "genre": ["science-fiction", "thriller"] }, "vectors": { ... } }

> **Important:** ETags are only supported when using the **canonical Vector Search 2.0 JSONL format** . The legacy Vector Search 1.0 input format does not support the `etag` field.

## Handling Concurrency Errors

If an operation fails an ETag check, the API will return an `ABORTED` (HTTP **409 Conflict** ) error code.

**Recommended Error Handling** :

When you receive an `ABORTED` error, your application should:

1.  Re-fetch the latest version of the Data Object from the server.

2.  Resolve any business-logic conflicts between the newly fetched data and your intended updates.

3.  Retry the operation using the new ETag.

## What's next?

  - Learn about [Collection Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) .
  - See how to [query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) and [search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) for Data Objects.
