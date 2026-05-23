---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/importDataObjects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/importDataObjects
title: 'Method: projects.locations.collections.importDataObjects'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Initiates a Long-Running Operation to import DataObjects into a Collection.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{name}:importDataObjects`

### Path parameters

Parameters

`name`

`string`

Required. The resource name of the Collection to import DataObjects into. Format: `projects/{project}/locations/{location}/collections/{collection}` .

### Request body

The request body contains data with the following structure:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field config can be only one of the following:&quot;gcsImport&quot;: {object (GcsImportConfig)}// End of list of possible types for union field config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `config` . The configuration for the import data and error results. `config` can be only one of the following:

`gcsImport`

` object ( GcsImportConfig  ` )

The Cloud Storage location of the input content.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.dataObjects.import`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## GcsImportConfig

Google Cloud Storage configuration for the import.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;contentsUri&quot;: string,
  &quot;errorUri&quot;: string,
  &quot;outputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`contentsUri`

`string`

Required. URI prefix of the Cloud Storage DataObjects to import.

`errorUri`

`string`

Required. URI prefix of the Cloud Storage location to write any errors encountered during the import.

`outputUri`

`string`

Optional. URI prefix of the Cloud Storage location to write DataObject `IDs` and `etags` of DataObjects that were successfully imported. The service will write the successfully imported DataObjects to sharded files under this prefix. If this field is empty, no output will be written.
