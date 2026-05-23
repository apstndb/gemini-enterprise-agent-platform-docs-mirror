---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/list
title: 'Method: artifacts.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.artifacts.list

Lists Artifacts in the MetadataStore.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /artifacts`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The MetadataStore whose Artifacts should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`

### Query parameters

`pageSize` `integer`

The maximum number of Artifacts to return. The service may return fewer. Must be in range 1-100, inclusive. Defaults to 100.

`pageToken` `string`

A page token, received from a previous `  MetadataService.ListArtifacts  ` call. Provide this to retrieve the subsequent page.

When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID\_ARGUMENT error.)

`filter` `string`

Filter specifying the boolean condition for the Artifacts to satisfy in order to be part of the result set. The syntax to define filter query is based on <https://google.aip.dev/160> . The supported set of filters include the following:

  - **attribute filtering** : For example: `display_name = "test"` . Supported fields include: `name` , `display_name` , `uri` , `state` , `schema_title` , `create_time` , and `update_time` . time fields, such as `create_time` and `update_time` , require values specified in RFC-3339 format. For example: `create_time = "2020-11-19T11:30:00-04:00"`
  - **metadata field** : To filter on metadata fields use traversal operation as follows: `metadata.<fieldName>.<typeValue>` . For example: `metadata.field_1.number_value = 10.0` In case the field name contains special characters (such as colon), one can embed it inside double quote. For example: `metadata."field:1".number_value = 10.0`
  - **Context based filtering** : To filter Artifacts based on the contexts to which they belong, use the function operator with the full resource name `in_context(<context-name>)` . For example: `in_context("projects/<projectNumber>/locations/<location>/metadataStores/<metadatastore_name>/contexts/<context-id>")`

Each of the above supported filter types can be combined together using logical operators ( `AND` & `OR` ). Maximum nested expression depth allowed is 5.

For example: `display_name = "test" AND metadata.field1.bool_value = true` .

`orderBy` `string`

How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as foo.bar. see <https://google.aip.dev/132#ordering> for more details.

### Request body

The request body must be empty.

### Response body

Response message for `  MetadataService.ListArtifacts  ` .

If successful, the response body contains data with the following structure:

Fields

`artifacts[]` ` object ( Artifact  ` )

The Artifacts retrieved from the MetadataStore.

`nextPageToken` `string`

A token, which can be sent as `  ListArtifactsRequest.page_token  ` to retrieve the next page. If this field is not populated, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;artifacts&quot;: [{object (Artifact)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
