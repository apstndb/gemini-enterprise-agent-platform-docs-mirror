---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/query
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/query
title: 'Method: extensions.query'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.extensions.query

Queries an extension with a default controller.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:query`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. name (identifier) of the extension; Format: `projects/{project}/locations/{location}/extensions/{extension}`

### Request body

The request body contains data with the following structure:

Fields

`contents[]` ` object ( Content  ` )

Required. The content of the current conversation with the model.

For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request.

### Response body

Response message for `  ExtensionExecutionService.QueryExtension  ` .

If successful, the response body contains data with the following structure:

Fields

`steps[]` ` object ( Content  ` )

Steps of extension or LLM interaction, can contain function call, function response, or text response. The last step contains the final response to the query.

`failureMessage` `string`

Failure message if any.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;steps&quot;: [{object (Content)}],&quot;failureMessage&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
