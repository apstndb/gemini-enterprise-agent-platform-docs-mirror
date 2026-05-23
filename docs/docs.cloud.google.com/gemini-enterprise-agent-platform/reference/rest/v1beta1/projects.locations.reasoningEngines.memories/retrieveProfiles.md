---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieveProfiles
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieveProfiles
title: 'Method: memories.retrieveProfiles'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.retrieveProfiles

Retrieves profiles.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /memories:retrieveProfiles`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to retrieve profiles from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`scope` `map (key: string, value: string)`

Required. The scope of the profiles to retrieve.

### Response body

Response message for `  MemoryBankService.RetrieveProfiles  ` .

If successful, the response body contains data with the following structure:

Fields

`profiles` ` map (key: string, value: object ( MemoryProfile  ` ))

The retrieved structured profiles, which match the schemas under the requested scope. The key is the id of the schema that the profile is linked with, which corresponds to the `schemaId` defined inside the `SchemaConfig` , under `StructuredMemoryCustomizationConfig` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;profiles&quot;: {string: {object (MemoryProfile)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## MemoryProfile

A memory profile.

Fields

`schemaId` `string`

Represents the id of the schema. This id corresponds to the `schemaId` defined inside the SchemaConfig, under StructuredMemoryCustomizationConfig.

`profile` ` object ( Struct  ` format)

Represents the profile data.

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
  &quot;schemaId&quot;: string,
  &quot;profile&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>
