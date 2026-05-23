---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/augmentPrompt
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/augmentPrompt
title: 'Method: locations.augmentPrompt'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.augmentPrompt

Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent}:augmentPrompt`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`contents[]` ` object ( Content  ` )

Optional. Input content to augment, only text format is supported for now.

`model` ` object ( Model  ` )

Optional. metadata of the backend deployed model.

`data_source` `Union type`

The data source for retrieving contexts. `data_source` can be only one of the following:

`vertexRagStore` ` object ( VertexRagStore  ` )

Optional. Retrieves contexts from the Vertex RagStore.

### Response body

Response message for locations.augmentPrompt.

If successful, the response body contains data with the following structure:

Fields

`augmentedPrompt[]` ` object ( Content  ` )

Augmented prompt, only text format is supported for now.

`facts[]` ` object ( Fact  ` )

Retrieved facts from RAG data sources.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;augmentedPrompt&quot;: [{object (Content)}],&quot;facts&quot;: [{object (Fact)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Model

metadata of the backend deployed model.

Fields

`model` `string`

Optional. The model that the user will send the augmented prompt for content generation.

`modelVersion` `string`

Optional. The model version of the backend deployed model.

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
  &quot;model&quot;: string,
  &quot;modelVersion&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
