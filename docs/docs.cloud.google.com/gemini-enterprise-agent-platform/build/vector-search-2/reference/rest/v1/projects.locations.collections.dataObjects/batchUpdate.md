---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchUpdate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchUpdate
title: 'Method: projects.locations.collections.dataObjects.batchUpdate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Updates dataObjects in a batch.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1/{parent}/dataObjects:batchUpdate`

### Path parameters

| Parameters |                                                                                                                                                                                                                                                   |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The resource name of the Collection to update the DataObjects in. Format: `projects/{project}/locations/{location}/collections/{collection}` . The parent field in the UpdateDataObjectRequest messages must match this field. |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "requests": [
    {
      object (UpdateDataObjectRequest)
    }
  ]
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `requests[]` | `object ( `[`UpdateDataObjectRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchUpdate#UpdateDataObjectRequest)` )` Required. The request message specifying the resources to update. A maximum of 1000 DataObjects can be updated in a batch. |

### Response body

If successful, the response body is empty.

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `vectorsearch.dataObjects.update`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## UpdateDataObjectRequest

Request message for [`DataObjectService.UpdateDataObject`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/patch#google.cloud.vectorsearch.v1.DataObjectService.UpdateDataObject) .

**JSON representation**

```
{
  "dataObject": {
    object (DataObject)
  },
  "updateMask": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataObject` | `object ( `[`DataObject`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects#DataObject)` )` Required. The DataObject which replaces the resource on the server.                                                                                                              |
| `updateMask` | `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)` Optional. The update mask applies to the resource. See [`google.protobuf.FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) . This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` . |
