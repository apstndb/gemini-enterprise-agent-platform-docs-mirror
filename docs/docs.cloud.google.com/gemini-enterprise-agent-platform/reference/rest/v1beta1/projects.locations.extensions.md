---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions
title: 'REST Resource: projects.locations.extensions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Extension

extensions are tools for large language models to access external data, run computations, etc.

Fields

`name` `string`

Identifier. The resource name of the Extension.

`displayName` `string`

Required. The display name of the Extension. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

Optional. The description of the Extension.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Extension was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Extension was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`manifest` `object ( `[`ExtensionManifest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ExtensionManifest)` )`

Required. Manifest of the Extension.

`extensionOperations[]` `object ( `[`ExtensionOperation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ExtensionOperation)` )`

Output only. Supported operations.

`runtimeConfig` `object ( `[`RuntimeConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#RuntimeConfig)` )`

Optional. Runtime config controlling the runtime behavior of this Extension.

`toolUseExamples[]` `object ( `[`ToolUseExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ToolUseExample)` )`

Optional. Examples to illustrate the usage of the extension as a tool.

`privateServiceConnectConfig` `object ( `[`ExtensionPrivateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ExtensionPrivateServiceConnectConfig)` )`

Optional. The PrivateServiceConnect config for the extension. If specified, the service endpoints associated with the Extension should be [registered with private network access in the provided service Directory](https://cloud.google.com/service-directory/docs/configuring-private-network-access) .

If the service contains more than one endpoint with a network, the service will arbitrarilty choose one of the endpoints to use for extension execution.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "manifest": {
    object (ExtensionManifest)
  },
  "extensionOperations": [
    {
      object (ExtensionOperation)
    }
  ],
  "runtimeConfig": {
    object (RuntimeConfig)
  },
  "toolUseExamples": [
    {
      object (ToolUseExample)
    }
  ],
  "privateServiceConnectConfig": {
    object (ExtensionPrivateServiceConnectConfig)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

## ExtensionManifest

Manifest spec of an Extension needed for runtime execution.

Fields

`name` `string`

Required. Extension name shown to the LLM. The name can be up to 128 characters long.

`description` `string`

Required. The natural language description shown to the LLM. It should describe the usage of the extension, and is essential for the LLM to perform reasoning. e.g., if the extension is a data store, you can let the LLM know what data it contains.

`apiSpec` `object ( `[`ApiSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ApiSpec)` )`

Required. Immutable. The API specification shown to the LLM.

`authConfig` `object ( `[`AuthConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#AuthConfig)` )`

Required. Immutable. type of auth supported by this extension.

**JSON representation**

```
{
  "name": string,
  "description": string,
  "apiSpec": {
    object (ApiSpec)
  },
  "authConfig": {
    object (AuthConfig)
  }
}
```

## ApiSpec

The API specification shown to the LLM.

Fields

`api_spec` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`openApiYaml` `string`

The API spec in Open API standard and YAML format.

`openApiGcsUri` `string`

Cloud Storage URI pointing to the OpenAPI spec.

End of mutually exclusive fields.

**JSON representation**

```
{

  // api_spec
  "openApiYaml": string,
  "openApiGcsUri": string
  // Union type
}
```

## AuthConfig

Auth configuration to run the extension.

Fields

`authType` `enum ( `[`AuthType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#AuthType)` )`

type of auth scheme.

`auth_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`apiKeyConfig` `object ( `[`ApiKeyConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ApiKeyConfig)` )`

Config for API key auth.

`httpBasicAuthConfig` `object ( `[`HttpBasicAuthConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#HttpBasicAuthConfig)` )`

Config for HTTP Basic auth.

`googleServiceAccountConfig` `object ( `[`GoogleServiceAccountConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#GoogleServiceAccountConfig)` )`

Config for Google service Account auth.

`oauthConfig` `object ( `[`OauthConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#OauthConfig)` )`

Config for user oauth.

`oidcConfig` `object ( `[`OidcConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#OidcConfig)` )`

Config for user OIDC auth.

End of mutually exclusive fields.

**JSON representation**

```
{
  "authType": enum (AuthType),

  // auth_config
  "apiKeyConfig": {
    object (ApiKeyConfig)
  },
  "httpBasicAuthConfig": {
    object (HttpBasicAuthConfig)
  },
  "googleServiceAccountConfig": {
    object (GoogleServiceAccountConfig)
  },
  "oauthConfig": {
    object (OauthConfig)
  },
  "oidcConfig": {
    object (OidcConfig)
  }
  // Union type
}
```

## ApiKeyConfig

Config for authentication with API key.

Fields

`name` `string`

Optional. The parameter name of the API key. E.g. If the API request is "https://example.com/act?apiKey= ", "apiKey" would be the parameter name.

`apiKeySecret` `string`

Optional. The name of the SecretManager secret version resource storing the API key. Format: `projects/{project}/secrets/{secrete}/versions/{version}`

- If both `apiKeySecret` and `apiKeyString` are specified, this field takes precedence over `apiKeyString` .

- If specified, the `secretmanager.versions.access` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the specified resource.

`httpElementLocation` `enum ( `[`HttpElementLocation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#HttpElementLocation)` )`

Optional. The location of the API key.

**JSON representation**

```
{
  "name": string,
  "apiKeySecret": string,
  "httpElementLocation": enum (HttpElementLocation)
}
```

## HttpElementLocation

Enum of location an HTTP element can be.

| Enums                 |                                        |
|-----------------------|----------------------------------------|
| `HTTP_IN_UNSPECIFIED` |                                        |
| `HTTP_IN_QUERY`       | Element is in the HTTP request query.  |
| `HTTP_IN_HEADER`      | Element is in the HTTP request header. |
| `HTTP_IN_PATH`        | Element is in the HTTP request path.   |
| `HTTP_IN_BODY`        | Element is in the HTTP request body.   |
| `HTTP_IN_COOKIE`      | Element is in the HTTP request cookie. |

## HttpBasicAuthConfig

Config for HTTP Basic Authentication.

Fields

`credentialSecret` `string`

Required. The name of the SecretManager secret version resource storing the base64 encoded credentials. Format: `projects/{project}/secrets/{secrete}/versions/{version}`

- If specified, the `secretmanager.versions.access` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the specified resource.

**JSON representation**

```
{
  "credentialSecret": string
}
```

## GoogleServiceAccountConfig

Config for Google service Account Authentication.

Fields

`serviceAccount` `string`

Optional. The service account that the extension execution service runs as.

- If the service account is specified, the `iam.serviceAccounts.getAccessToken` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the specified service account.

- If not specified, the Agent Platform Extension service Agent will be used to execute the Extension.

**JSON representation**

```
{
  "serviceAccount": string
}
```

## OauthConfig

Config for user oauth.

Fields

`oauth_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`accessToken` `string`

Access token for extension endpoint. Only used to propagate token from \[\[ExecuteExtensionRequest.runtime_auth_config\]\] at request time.

`serviceAccount` `string`

The service account used to generate access tokens for executing the Extension.

- If the service account is specified, the `iam.serviceAccounts.getAccessToken` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the provided service account.

End of mutually exclusive fields.

**JSON representation**

```
{

  // oauth_config
  "accessToken": string,
  "serviceAccount": string
  // Union type
}
```

## OidcConfig

Config for user OIDC auth.

Fields

`oidc_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`idToken` `string`

OpenID Connect formatted id token for extension endpoint. Only used to propagate token from \[\[ExecuteExtensionRequest.runtime_auth_config\]\] at request time.

`serviceAccount` `string`

The service account used to generate an OpenID Connect (OIDC)-compatible JWT token signed by the Google OIDC Provider (accounts.google.com) for extension endpoint ( <https://cloud.google.com/iam/docs/create-short-lived-credentials-direct#sa-credentials-oidc)> .

- The audience for the token will be set to the URL in the server url defined in the OpenApi spec.

- If the service account is provided, the service account should grant `iam.serviceAccounts.getOpenIdToken` permission to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents)> .

End of mutually exclusive fields.

**JSON representation**

```
{

  // oidc_config
  "idToken": string,
  "serviceAccount": string
  // Union type
}
```

## AuthType

type of Auth.

| Enums                         |                              |
|-------------------------------|------------------------------|
| `AUTH_TYPE_UNSPECIFIED`       |                              |
| `NO_AUTH`                     | No Auth.                     |
| `API_KEY_AUTH`                | API Key Auth.                |
| `HTTP_BASIC_AUTH`             | HTTP Basic Auth.             |
| `GOOGLE_SERVICE_ACCOUNT_AUTH` | Google service Account Auth. |
| `OAUTH`                       | OAuth auth.                  |
| `OIDC_AUTH`                   | OpenID Connect (OIDC) Auth.  |

## ExtensionOperation

Operation of an extension.

Fields

`operationId` `string`

Operation id that uniquely identifies the operations among the extension. See: "Operation Object" in <https://swagger.io/specification/> .

This field is parsed from the OpenAPI spec. For HTTP extensions, if it does not exist in the spec, we will generate one from the HTTP method and path.

`functionDeclaration` `object ( `[`FunctionDeclaration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionDeclaration)` )`

Output only. Structured representation of a function declaration as defined by the OpenAPI Spec.

**JSON representation**

```
{
  "operationId": string,
  "functionDeclaration": {
    object (FunctionDeclaration)
  }
}
```

## RuntimeConfig

Runtime configuration to run the extension.

Fields

`defaultParams` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Default parameters that will be set for all the execution of this extension. If specified, the parameter values can be overridden by values in \[\[ExecuteExtensionRequest.operation_params\]\] at request time.

The struct should be in a form of map with param name as the key and actual param value as the value. E.g. If this operation requires a param "name" to be set to "abc". you can set this to something like {"name": "abc"}.

`GoogleFirstPartyExtensionConfig` `Union type`

Runtime configurations for Google first party extensions. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`codeInterpreterRuntimeConfig` `object ( `[`CodeInterpreterRuntimeConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#CodeInterpreterRuntimeConfig)` )`

code execution runtime configurations for code interpreter extension.

`vertexAiSearchRuntimeConfig` `object ( `[`VertexAISearchRuntimeConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#VertexAISearchRuntimeConfig)` )`

Runtime configuration for Agent Platform Search extension.

End of mutually exclusive fields.

**JSON representation**

```
{
  "defaultParams": {
    object
  },

  // GoogleFirstPartyExtensionConfig
  "codeInterpreterRuntimeConfig": {
    object (CodeInterpreterRuntimeConfig)
  },
  "vertexAiSearchRuntimeConfig": {
    object (VertexAISearchRuntimeConfig)
  }
  // Union type
}
```

## CodeInterpreterRuntimeConfig

Fields

`fileInputGcsBucket` `string`

Optional. The Cloud Storage bucket for file input of this Extension. If specified, support input from the Cloud Storage bucket. Vertex Extension Custom code service Agent should be granted file reader to this bucket. If not specified, the extension will only accept file contents from request body and reject Cloud Storage file inputs.

`fileOutputGcsBucket` `string`

Optional. The Cloud Storage bucket for file output of this Extension. If specified, write all output files to the Cloud Storage bucket. Vertex Extension Custom code service Agent should be granted file writer to this bucket. If not specified, the file content will be output in response body.

**JSON representation**

```
{
  "fileInputGcsBucket": string,
  "fileOutputGcsBucket": string
}
```

## VertexAISearchRuntimeConfig

Fields

`servingConfigName` `string`

Optional. Agent Platform Search serving config name. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{servingConfig}`

`engineId` `string`

Optional. Agent Platform Search engine id. This is used to construct the search request. By setting this engineId, API will construct the serving config using the default value to call search API for the user. The engineId and servingConfigName cannot both be empty at the same time.

**JSON representation**

```
{
  "servingConfigName": string,
  "engineId": string
}
```

## ToolUseExample

A single example of the tool usage.

Fields

`displayName` `string`

Required. The display name for example.

`query` `string`

Required. Query that should be routed to this tool.

`requestParams` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Request parameters used for executing this tool.

`responseParams` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Response parameters generated by this tool.

`responseSummary` `string`

Summary of the tool response to the user query.

`Target` `Union type`

Target tool to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`extensionOperation` `object ( `[`ExtensionOperation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions#ExtensionOperation_1)` )`

Extension operation to call.

`functionName` `string`

Function name to call.

End of mutually exclusive fields.

**JSON representation**

```
{
  "displayName": string,
  "query": string,
  "requestParams": {
    object
  },
  "responseParams": {
    object
  },
  "responseSummary": string,

  // Target
  "extensionOperation": {
    object (ExtensionOperation)
  },
  "functionName": string
  // Union type
}
```

## ExtensionOperation

Identifies one operation of the extension.

Fields

`extension` `string`

Resource name of the extension.

`operationId` `string`

Required. Operation id of the extension.

**JSON representation**

```
{
  "extension": string,
  "operationId": string
}
```

## ExtensionPrivateServiceConnectConfig

PrivateExtensionConfig configuration for the extension.

Fields

`serviceDirectory` `string`

Required. The service Directory resource name in which the service endpoints associated to the extension are registered. Format: `projects/{projectId}/locations/{locationId}/namespaces/{namespaceId}/services/{serviceId}`

- The Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) should be granted `servicedirectory.viewer` and `servicedirectory.pscAuthorizedService` roles on the resource.

**JSON representation**

```
{
  "serviceDirectory": string
}
```

| Methods                                                                                                                                  |                                                 |
|------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/delete)   | Deletes an Extension.                           |
| [`execute`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/execute) | Executes the request against a given extension. |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/get)         | Gets an Extension.                              |
| [`import`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/import)   | Imports an Extension.                           |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/list)       | Lists Extensions in a location.                 |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/patch)     | Updates an Extension.                           |
| [`query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/query)     | Queries an extension with a default controller. |
