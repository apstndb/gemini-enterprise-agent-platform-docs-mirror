---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/execute
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/execute
title: 'Method: extensions.execute'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.extensions.execute

Executes the request against a given extension.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:execute`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. name (identifier) of the extension; Format: `projects/{project}/locations/{location}/extensions/{extension}`

### Request body

The request body contains data with the following structure:

Fields

`operationId` `string`

Required. The desired id of the operation to be executed in this extension as defined in `  ExtensionOperation.operation_id  ` .

`operationParams` ` object ( Struct  ` format)

Optional. Request parameters that will be used for executing this operation.

The struct should be in a form of map with param name as the key and actual param value as the value. E.g. If this operation requires a param "name" to be set to "abc". you can set this to something like {"name": "abc"}.

`runtimeAuthConfig` ` object ( AuthConfig  ` )

Optional. Auth config provided at runtime to override the default value in \[Extension.manifest.auth\_config\]\[\]. The AuthConfig.auth\_type should match the value in \[Extension.manifest.auth\_config\]\[\].

### Response body

Response message for `  ExtensionExecutionService.ExecuteExtension  ` .

If successful, the response body contains data with the following structure:

Fields

`content` `string`

Response content from the extension. The content should be conformant to the response.content schema in the extension's manifest/OpenAPI spec.

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
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
