---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/directPredict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/directPredict
title: 'Method: endpoints.directPredict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.directPredict

Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:directPredict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`inputs[]` ` object ( Tensor  ` )

The prediction input.

`parameters` ` object ( Tensor  ` )

The parameters that govern the prediction.

### Response body

Response message for `  PredictionService.DirectPredict  ` .

If successful, the response body contains data with the following structure:

Fields

`outputs[]` ` object ( Tensor  ` )

The prediction output.

`parameters` ` object ( Tensor  ` )

The parameters that govern the prediction.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outputs&quot;: [{object (Tensor)}],&quot;parameters&quot;: {object (Tensor)}}</code></pre></td>
</tr>
</tbody>
</table>
