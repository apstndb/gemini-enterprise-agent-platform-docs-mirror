---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/generateFetchAccessToken
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/generateFetchAccessToken
title: 'Method: featureViews.generateFetchAccessToken'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.generateFetchAccessToken

RPC to generate an access token for the given feature view. FeatureViews under the same FeatureOnlineStore share the same access token.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{featureView}:generateFetchAccessToken`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView` `string`

FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Request body

The request body must be empty.

### Response body

Response message for `  FeatureOnlineStoreService.GenerateFetchAccessToken  ` .

If successful, the response body contains data with the following structure:

Fields

`accessToken` `string`

The OAuth 2.0 access token.

`expireTime` ` string ( Timestamp  ` format)

token expiration time. This is always set

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
  &quot;accessToken&quot;: string,
  &quot;expireTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
