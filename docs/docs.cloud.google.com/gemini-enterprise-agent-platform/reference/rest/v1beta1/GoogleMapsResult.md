---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult
title: GoogleMapsResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The result of the Google Maps.

Fields

`places[]` ` object ( Places  ` )

The places that were found.

`widgetContextToken` `string`

Resource name of the Google Maps widget context token.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;places&quot;: [{object (Places)}],&quot;widgetContextToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## Places

Fields

`placeId` `string`

The id of the place, in `places/{placeId}` format.

`name` `string`

title of the place.

`url` `string`

URI reference of the place.

`reviewSnippets[]` ` object ( ReviewSnippet  ` )

Snippets of reviews that are used to generate answers about the features of a given place in Google Maps.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;placeId&quot;: string,&quot;name&quot;: string,&quot;url&quot;: string,&quot;reviewSnippets&quot;: [{object (ReviewSnippet)}]}</code></pre></td>
</tr>
</tbody>
</table>
