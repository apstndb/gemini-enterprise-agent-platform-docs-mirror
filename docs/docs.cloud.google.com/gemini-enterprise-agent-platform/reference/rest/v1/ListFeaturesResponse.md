---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ListFeaturesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ListFeaturesResponse
title: ListFeaturesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  FeaturestoreService.ListFeatures  ` . Response message for `  FeatureRegistryService.ListFeatures  ` .

Fields

`features[]` ` object ( Feature  ` )

The Features matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListFeaturesRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;features&quot;: [{object (Feature)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
