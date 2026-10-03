---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/exportDataObjects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/exportDataObjects
title: 'Method: projects.locations.collections.exportDataObjects'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Initiates a Long-Running Operation to export DataObjects from a Collection.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1/{name}:exportDataObjects`

### Path parameters

| Parameters |                                                                                                                                                                                |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` Required. The resource name of the Collection from which we want to export Data Objects. Format: `projects/{project}/locations/{location}/collections/{collection}` . |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{

  // Union field destination can be only one of the following:
  "gcsDestination": {
    object (GcsExportDestination)
  }
  // End of list of possible types for union field destination.
}
```

| Fields                                                                                                             |                                                                                                                                                                                                                                                                                           |
|--------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `destination` . The configuration for the export data. `destination` can be only one of the following: |                                                                                                                                                                                                                                                                                           |
| `gcsDestination`                                                                                                   | `object ( `[`GcsExportDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/exportDataObjects#GcsExportDestination)` )` The Cloud Storage location where user wants to export Data Objects. |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `vectorsearch.dataObjects.export`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## GcsExportDestination

Google Cloud Storage configuration for the export.

**JSON representation**

```
{
  "exportUri": string,
  "format": enum (Format)
}
```

| Fields      |                                                                                                                                                                                                                                            |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `exportUri` | `string` Required. URI prefix of the Cloud Storage where to export Data Objects. The bucket is required to be in the same region as the collection.                                                                                        |
| `format`    | `enum ( `[`Format`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/exportDataObjects#Format)` )` Required. The format of the exported Data Objects. |

## Format

Options for the format of the exported Data Objects.

| Enums                |                                         |
|----------------------|-----------------------------------------|
| `FORMAT_UNSPECIFIED` | Unspecified format.                     |
| `JSONL`              | Exports Data Objects in `JSONL` format. |
