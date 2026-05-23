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

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Extension was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Extension was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`manifest` ` object ( ExtensionManifest  ` )

Required. Manifest of the Extension.

`extensionOperations[]` ` object ( ExtensionOperation  ` )

Output only. Supported operations.

`runtimeConfig` ` object ( RuntimeConfig  ` )

Optional. Runtime config controlling the runtime behavior of this Extension.

`toolUseExamples[]` ` object ( ToolUseExample  ` )

Optional. Examples to illustrate the usage of the extension as a tool.

`privateServiceConnectConfig` ` object ( ExtensionPrivateServiceConnectConfig  ` )

Optional. The PrivateServiceConnect config for the extension. If specified, the service endpoints associated with the Extension should be [registered with private network access in the provided service Directory](https://cloud.google.com/service-directory/docs/configuring-private-network-access) .

If the service contains more than one endpoint with a network, the service will arbitrarilty choose one of the endpoints to use for extension execution.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;manifest&quot;: {object (ExtensionManifest)},&quot;extensionOperations&quot;: [{object (ExtensionOperation)}],&quot;runtimeConfig&quot;: {object (RuntimeConfig)},&quot;toolUseExamples&quot;: [{object (ToolUseExample)}],&quot;privateServiceConnectConfig&quot;: {object (ExtensionPrivateServiceConnectConfig)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## ExtensionManifest

Manifest spec of an Extension needed for runtime execution.

Fields

`name` `string`

Required. Extension name shown to the LLM. The name can be up to 128 characters long.

`description` `string`

Required. The natural language description shown to the LLM. It should describe the usage of the extension, and is essential for the LLM to perform reasoning. e.g., if the extension is a data store, you can let the LLM know what data it contains.

`apiSpec` ` object ( ApiSpec  ` )

Required. Immutable. The API specification shown to the LLM.

`authConfig` ` object ( AuthConfig  ` )

Required. Immutable. type of auth supported by this extension.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;apiSpec&quot;: {object (ApiSpec)},&quot;authConfig&quot;: {object (AuthConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ApiSpec

The API specification shown to the LLM.

Fields

`api_spec` `Union type`

`api_spec` can be only one of the following:

`openApiYaml` `string`

The API spec in Open API standard and YAML format.

`openApiGcsUri` `string`

Cloud Storage URI pointing to the OpenAPI spec.

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

  // api_spec
  &quot;openApiYaml&quot;: string,
  &quot;openApiGcsUri&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## AuthConfig

Auth configuration to run the extension.

Fields

`authType` ` enum ( AuthType  ` )

type of auth scheme.

`auth_config` `Union type`

`auth_config` can be only one of the following:

`apiKeyConfig` ` object ( ApiKeyConfig  ` )

Config for API key auth.

`httpBasicAuthConfig` ` object ( HttpBasicAuthConfig  ` )

Config for HTTP Basic auth.

`googleServiceAccountConfig` ` object ( GoogleServiceAccountConfig  ` )

Config for Google service Account auth.

`oauthConfig` ` object ( OauthConfig  ` )

Config for user oauth.

`oidcConfig` ` object ( OidcConfig  ` )

Config for user OIDC auth.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;authType&quot;: enum (AuthType),// auth_config&quot;apiKeyConfig&quot;: {object (ApiKeyConfig)},&quot;httpBasicAuthConfig&quot;: {object (HttpBasicAuthConfig)},&quot;googleServiceAccountConfig&quot;: {object (GoogleServiceAccountConfig)},&quot;oauthConfig&quot;: {object (OauthConfig)},&quot;oidcConfig&quot;: {object (OidcConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ApiKeyConfig

Config for authentication with API key.

Fields

`name` `string`

Optional. The parameter name of the API key. E.g. If the API request is "https://example.com/act?apiKey= ", "apiKey" would be the parameter name.

`apiKeySecret` `string`

Optional. The name of the SecretManager secret version resource storing the API key. Format: `projects/{project}/secrets/{secrete}/versions/{version}`

  - If both `apiKeySecret` and `apiKeyString` are specified, this field takes precedence over `apiKeyString` .

  - If specified, the `secretmanager.versions.access` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the specified resource.

`httpElementLocation` ` enum ( HttpElementLocation  ` )

Optional. The location of the API key.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;apiKeySecret&quot;: string,&quot;httpElementLocation&quot;: enum (HttpElementLocation)}</code></pre></td>
</tr>
</tbody>
</table>

## HttpElementLocation

Enum of location an HTTP element can be.

Enums

`HTTP_IN_UNSPECIFIED`

`HTTP_IN_QUERY`

Element is in the HTTP request query.

`HTTP_IN_HEADER`

Element is in the HTTP request header.

`HTTP_IN_PATH`

Element is in the HTTP request path.

`HTTP_IN_BODY`

Element is in the HTTP request body.

`HTTP_IN_COOKIE`

Element is in the HTTP request cookie.

## HttpBasicAuthConfig

Config for HTTP Basic Authentication.

Fields

`credentialSecret` `string`

Required. The name of the SecretManager secret version resource storing the base64 encoded credentials. Format: `projects/{project}/secrets/{secrete}/versions/{version}`

  - If specified, the `secretmanager.versions.access` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the specified resource.

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
  &quot;credentialSecret&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleServiceAccountConfig

Config for Google service Account Authentication.

Fields

`serviceAccount` `string`

Optional. The service account that the extension execution service runs as.

  - If the service account is specified, the `iam.serviceAccounts.getAccessToken` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the specified service account.

  - If not specified, the Agent Platform Extension service Agent will be used to execute the Extension.

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
  &quot;serviceAccount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## OauthConfig

Config for user oauth.

Fields

`oauth_config` `Union type`

`oauth_config` can be only one of the following:

`accessToken` `string`

Access token for extension endpoint. Only used to propagate token from \[\[ExecuteExtensionRequest.runtime\_auth\_config\]\] at request time.

`serviceAccount` `string`

The service account used to generate access tokens for executing the Extension.

  - If the service account is specified, the `iam.serviceAccounts.getAccessToken` permission should be granted to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) on the provided service account.

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

  // oauth_config
  &quot;accessToken&quot;: string,
  &quot;serviceAccount&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## OidcConfig

Config for user OIDC auth.

Fields

`oidc_config` `Union type`

`oidc_config` can be only one of the following:

`idToken` `string`

OpenID Connect formatted id token for extension endpoint. Only used to propagate token from \[\[ExecuteExtensionRequest.runtime\_auth\_config\]\] at request time.

`serviceAccount` `string`

The service account used to generate an OpenID Connect (OIDC)-compatible JWT token signed by the Google OIDC Provider (accounts.google.com) for extension endpoint ( <https://cloud.google.com/iam/docs/create-short-lived-credentials-direct#sa-credentials-oidc)> .

  - The audience for the token will be set to the URL in the server url defined in the OpenApi spec.

  - If the service account is provided, the service account should grant `iam.serviceAccounts.getOpenIdToken` permission to Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents)> .

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

  // oidc_config
  &quot;idToken&quot;: string,
  &quot;serviceAccount&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## AuthType

type of Auth.

Enums

`AUTH_TYPE_UNSPECIFIED`

`NO_AUTH`

No Auth.

`API_KEY_AUTH`

API Key Auth.

`HTTP_BASIC_AUTH`

HTTP Basic Auth.

`GOOGLE_SERVICE_ACCOUNT_AUTH`

Google service Account Auth.

`OAUTH`

OAuth auth.

`OIDC_AUTH`

OpenID Connect (OIDC) Auth.

## ExtensionOperation

Operation of an extension.

Fields

`operationId` `string`

Operation id that uniquely identifies the operations among the extension. See: "Operation Object" in <https://swagger.io/specification/> .

This field is parsed from the OpenAPI spec. For HTTP extensions, if it does not exist in the spec, we will generate one from the HTTP method and path.

`functionDeclaration` ` object ( FunctionDeclaration  ` )

Output only. Structured representation of a function declaration as defined by the OpenAPI Spec.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;operationId&quot;: string,&quot;functionDeclaration&quot;: {object (FunctionDeclaration)}}</code></pre></td>
</tr>
</tbody>
</table>

## RuntimeConfig

Runtime configuration to run the extension.

Fields

`defaultParams` ` object ( Struct  ` format)

Optional. Default parameters that will be set for all the execution of this extension. If specified, the parameter values can be overridden by values in \[\[ExecuteExtensionRequest.operation\_params\]\] at request time.

The struct should be in a form of map with param name as the key and actual param value as the value. E.g. If this operation requires a param "name" to be set to "abc". you can set this to something like {"name": "abc"}.

`GoogleFirstPartyExtensionConfig` `Union type`

Runtime configurations for Google first party extensions. `GoogleFirstPartyExtensionConfig` can be only one of the following:

`codeInterpreterRuntimeConfig` ` object ( CodeInterpreterRuntimeConfig  ` )

code execution runtime configurations for code interpreter extension.

`vertexAiSearchRuntimeConfig` ` object ( VertexAISearchRuntimeConfig  ` )

Runtime configuration for Agent Platform Search extension.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;defaultParams&quot;: {object},// GoogleFirstPartyExtensionConfig&quot;codeInterpreterRuntimeConfig&quot;: {object (CodeInterpreterRuntimeConfig)},&quot;vertexAiSearchRuntimeConfig&quot;: {object (VertexAISearchRuntimeConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CodeInterpreterRuntimeConfig

Fields

`fileInputGcsBucket` `string`

Optional. The Cloud Storage bucket for file input of this Extension. If specified, support input from the Cloud Storage bucket. Vertex Extension Custom code service Agent should be granted file reader to this bucket. If not specified, the extension will only accept file contents from request body and reject Cloud Storage file inputs.

`fileOutputGcsBucket` `string`

Optional. The Cloud Storage bucket for file output of this Extension. If specified, write all output files to the Cloud Storage bucket. Vertex Extension Custom code service Agent should be granted file writer to this bucket. If not specified, the file content will be output in response body.

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
  &quot;fileInputGcsBucket&quot;: string,
  &quot;fileOutputGcsBucket&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## VertexAISearchRuntimeConfig

Fields

`servingConfigName` `string`

Optional. Agent Platform Search serving config name. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{servingConfig}`

`engineId` `string`

Optional. Agent Platform Search engine id. This is used to construct the search request. By setting this engineId, API will construct the serving config using the default value to call search API for the user. The engineId and servingConfigName cannot both be empty at the same time.

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
  &quot;servingConfigName&quot;: string,
  &quot;engineId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolUseExample

A single example of the tool usage.

Fields

`displayName` `string`

Required. The display name for example.

`query` `string`

Required. Query that should be routed to this tool.

`requestParams` ` object ( Struct  ` format)

Request parameters used for executing this tool.

`responseParams` ` object ( Struct  ` format)

Response parameters generated by this tool.

`responseSummary` `string`

Summary of the tool response to the user query.

`Target` `Union type`

Target tool to use. `Target` can be only one of the following:

`extensionOperation` ` object ( ExtensionOperation  ` )

Extension operation to call.

`functionName` `string`

Function name to call.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;displayName&quot;: string,&quot;query&quot;: string,&quot;requestParams&quot;: {object},&quot;responseParams&quot;: {object},&quot;responseSummary&quot;: string,// Target&quot;extensionOperation&quot;: {object (ExtensionOperation)},&quot;functionName&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ExtensionOperation

Identifies one operation of the extension.

Fields

`extension` `string`

Resource name of the extension.

`operationId` `string`

Required. Operation id of the extension.

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
  &quot;extension&quot;: string,
  &quot;operationId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ExtensionPrivateServiceConnectConfig

PrivateExtensionConfig configuration for the extension.

Fields

`serviceDirectory` `string`

Required. The service Directory resource name in which the service endpoints associated to the extension are registered. Format: `projects/{projectId}/locations/{locationId}/namespaces/{namespaceId}/services/{serviceId}`

  - The Agent Platform Extension service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) should be granted `servicedirectory.viewer` and `servicedirectory.pscAuthorizedService` roles on the resource.

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
  &quot;serviceDirectory&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            delete           `

Deletes an Extension.

### `            execute           `

Executes the request against a given extension.

### `            get           `

Gets an Extension.

### `            import           `

Imports an Extension.

### `            list           `

Lists Extensions in a location.

### `            patch           `

Updates an Extension.

### `            query           `

Queries an extension with a default controller.
