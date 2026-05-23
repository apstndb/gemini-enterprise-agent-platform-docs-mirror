---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments/list
title: 'Method: experiments.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.list

Lists TensorboardExperiments in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /experiments`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

### Query parameters

`filter` `string`

Lists the TensorboardExperiments that match the filter expression.

`pageSize` `integer`

The maximum number of TensorboardExperiments to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardExperiments are returned. The maximum value is 1000; values above 1000 are coerced to 1000.

`pageToken` `string`

A page token, received from a previous `  TensorboardService.ListTensorboardExperiments  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  TensorboardService.ListTensorboardExperiments  ` must match the call that provided the page token.

`orderBy` `string`

Field to use to sort the list.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.ListTensorboardExperiments  ` .

If successful, the response body contains data with the following structure:

Fields

`tensorboardExperiments[]` ` object ( TensorboardExperiment  ` )

The TensorboardExperiments mathching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListTensorboardExperimentsRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tensorboardExperiments&quot;: [{object (TensorboardExperiment)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
