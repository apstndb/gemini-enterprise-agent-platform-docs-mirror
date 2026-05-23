---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/directRawPredict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/directRawPredict
title: 'Method: endpoints.directRawPredict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.directRawPredict

Perform an unary online prediction request to a gRPC model server for custom containers.

### Endpoint

post `https: / /{service-endpoint} /v1 /{endpoint}:directRawPredict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`methodName` `string`

Fully qualified name of the API method being invoked to perform predictions.

Format: `/namespace.Service/method/` Example: `/tensorflow.serving.PredictionService/endpoints.predict`

`input` `string ( bytes format)`

The prediction input.

A base64-encoded string.

### Response body

Response message for `  PredictionService.DirectRawPredict  ` .

If successful, the response body contains data with the following structure:

Fields

`output` `string ( bytes format)`

The prediction output.

A base64-encoded string.

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
  &quot;output&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
