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

Required. The desired id of the operation to be executed in this extension as defined in [`ExtensionOperation.operation_id`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ExtensionOperation.FIELDS.operation_id) .

`operationParams` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Request parameters that will be used for executing this operation.

The struct should be in a form of map with param name as the key and actual param value as the value. E.g. If this operation requires a param "name" to be set to "abc". you can set this to something like {"name": "abc"}.

`runtimeAuthConfig` `object ( `[`AuthConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#AuthConfig)` )`

Optional. Auth config provided at runtime to override the default value in \[Extension.manifest.auth_config\]\[\]. The AuthConfig.auth_type should match the value in \[Extension.manifest.auth_config\]\[\].

### Response body

Response message for [`ExtensionExecutionService.ExecuteExtension`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/execute#google.cloud.aiplatform.v1beta1.ExtensionExecutionService.ExecuteExtension) .

If successful, the response body contains data with the following structure:

Fields

`content` `string`

Response content from the extension. The content should be conformant to the response.content schema in the extension's manifest/OpenAPI spec.

**JSON representation**

```
{
  "content": string
}
```
