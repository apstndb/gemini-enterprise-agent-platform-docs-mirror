---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/importDocuments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/importDocuments
title: 'Method: projects.locations.dataStores.importDocuments'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Initiates a Long-Running Operation to import Documents into a DataStore.

A file that was already imported successfully is skipped unless its Cloud Storage object has been overwritten since or, for `SOURCE_FORMAT_DOCUMENT_JSON` , its metadata has changed. Files that failed in an earlier import are processed again. Individual files that can't be imported are reported in the error report (see `ImportOutputConfig.error_gcs_prefix` ) rather than failing the whole import.

`dataStores.importDocuments` , `dataStores.purgeDocuments` and `dataStores.patch` run one at a time per DataStore. While one runs, one more can wait; any further request fails with `ABORTED` until the running operation finishes. To import many files, list them all in `inputUris` of one request rather than sending parallel requests.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{name}:importDocuments`

### Path parameters

| Parameters |                                                                                                                                                            |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` Required. The resource name of the DataStore to import Documents into. Format: `projects/{project}/locations/{location}/dataStores/{dataStore}` . |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "importOutputConfig": {
    object (ImportOutputConfig)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "gcsSource": {
    object (GcsSource)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `importOutputConfig`                                                                                                                          | `object ( `[`ImportOutputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/importDocuments#ImportOutputConfig)` )` Optional. Configuration of destination for import documents output: where to write the import's error report.                                                                                                                                                            |
| Required. The source of the input. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `gcsSource`                                                                                                                                   | `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/GcsSource)` )` Cloud Storage location for the input content. With the default `sourceFormat` , a URI can be a pattern such as `gs://my-bucket/folder/*` , which matches the objects directly in `folder` but not those in its subfolders. One import can include at most 100,000 files for an `UNSTRUCTURED` DataStore, or 100 for a `VIDEO` DataStore. |
| End of mutually exclusive fields.                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## ImportOutputConfig

Configuration of destination for import documents related output.

**JSON representation**

```
{
  "errorGcsPrefix": string
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                 |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `errorGcsPrefix` | `string` Optional. URI prefix of the Cloud Storage location to write any errors encountered during the import. The prefix must not contain any objects. Errors are written to sharded files under this prefix, one per line, as a JSON-encoded `google.rpc.Status` message. If this field is empty, no error report is written. |
