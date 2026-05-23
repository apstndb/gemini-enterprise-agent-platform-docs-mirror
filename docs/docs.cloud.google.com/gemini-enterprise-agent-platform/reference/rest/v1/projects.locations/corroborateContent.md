---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/corroborateContent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/corroborateContent
title: 'Method: locations.corroborateContent'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.corroborateContent

Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent}:corroborateContent`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`facts[]` ` object ( Fact  ` )

Optional. Facts used to generate the text can also be used to corroborate the text.

`parameters` ` object ( Parameters  ` )

Optional. Parameters that can be set to override default settings per request.

`content` ` object ( Content  ` )

Optional. Input content to corroborate, only text format is supported for now.

### Response body

Response message for locations.corroborateContent.

If successful, the response body contains data with the following structure:

Fields

`claims[]` ` object ( Claim  ` )

Claims that are extracted from the input content and facts that support the claims.

`corroborationScore` `number`

confidence score of corroborating content. value is \[0,1\] with 1 is the most confidence.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;claims&quot;: [{object (Claim)}],&quot;corroborationScore&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## Parameters

Parameters that can be overrided per request.

Fields

`citationThreshold` `number`

Optional. Only return claims with citation score larger than the threshold.

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
  &quot;citationThreshold&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## Claim

Claim that is extracted from the input text and facts that support it.

Fields

`factIndexes[]` `integer`

Indexes of the facts supporting this claim.

`startIndex` `integer`

Index in the input text where the claim starts (inclusive).

`endIndex` `integer`

Index in the input text where the claim ends (exclusive).

`score` `number`

confidence score of this corroboration.

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
  &quot;factIndexes&quot;: [
    integer
  ],
  &quot;startIndex&quot;: integer,
  &quot;endIndex&quot;: integer,
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
