---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/patch
title: 'Method: projects.locations.dataStores.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Updates the parameters of a single DataStore.

`dataStores.patch` , `dataStores.importDocuments` and `dataStores.purgeDocuments` run one at a time per DataStore. While one runs, one more can wait; any further request fails with `ABORTED` until the running operation finishes.

### HTTP request

`PATCH https://vectorsearch.googleapis.com/v1beta/{dataStore.name}`

### Path parameters

| Parameters       |                                                                                                                                                     |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataStore.name` | `string` Identifier. The fully qualified resource name of the DataStore. Format: `projects/{project}/locations/{location}/dataStores/{dataStoreId}` |

### Query parameters

| Parameters   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `updateMask` | `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)` Optional. Field mask is used to specify the fields to be overwritten in the DataStore resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. A path that names a message replaces the whole message: subfields omitted from the request are cleared and, under `processingConfig` , set back to their defaults. If the user does not provide a mask, every field that the request sets to a non-default value is overwritten. Messages sent empty (for example `layoutParsingConfig: {}` ) and fields set to their default value (for example `false` ) are not applied; name them in the mask instead. The following fields support update: `displayName` , `description` , `labels` , `processingConfig` and `documentMetadataSchema` . `documentMetadataSchema` must be updated as a whole (the mask path is `documentMetadataSchema` ), and only by adding properties: existing properties can't be removed or changed. If `*` is provided in the updateMask, full replacement will be performed. This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` . |
| `requestId`  | `string` Optional. An optional request ID to identify requests. Specify a unique request ID so that if you must retry your request, the server will know to ignore the request if it has already been completed. The server will guarantee that for at least 60 minutes since the first request. For example, consider a situation where you make an initial request and the request times out. If you make the request again with the same request ID, the server can check if original operation with the same request ID was received, and if so, will ignore the second request. This prevents clients from accidentally creating duplicate commitments. The request ID must be a valid UUID with the exception that zero UUID is not supported (00000000-0000-0000-0000-000000000000).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### Request body

The request body contains an instance of [`DataStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#DataStore) .

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
