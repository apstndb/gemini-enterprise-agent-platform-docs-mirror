---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/list
title: 'Method: endpoints.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.list

Lists endpoints in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /endpoints`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the endpoints. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `endpoint` supports `=` and `!=` . `endpoint` represents the Endpoint id, i.e. the last segment of the Endpoint's `  resource name  ` .
  - `displayName` supports `=` and `!=` .
  - `labels` supports general map functions that is:
      - `labels.key=value` - key:value equality
      - `labels.key:*` or `labels:key` - key existence
      - A key including a space must be quoted. `labels."a key"` .
  - `base_model_name` only supports `=` .

Some examples:

  - `endpoint=1`
  - `displayName="myDisplayName"`
  - `labels.myKey="myValue"`
  - `baseModelName="text-bison"`

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListEndpointsResponse.next_page_token  ` of the previous `  EndpointService.ListEndpoints  ` call.

`readMask` ` string ( FieldMask  ` format)

Optional. Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`gdcZone` `string`

Optional. Configures the Google Distributed Cloud (GDC) environment for online prediction. Only set this field when the Endpoint is to be deployed in a GDC environment.

### Request body

The request body must be empty.

### Response body

Response message for `  EndpointService.ListEndpoints  ` .

If successful, the response body contains data with the following structure:

Fields

`endpoints[]` ` object ( Endpoint  ` )

List of endpoints in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListEndpointsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;endpoints&quot;: [{object (Endpoint)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
