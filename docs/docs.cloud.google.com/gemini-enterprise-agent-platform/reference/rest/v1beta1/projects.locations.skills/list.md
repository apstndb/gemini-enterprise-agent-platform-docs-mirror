---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/list
title: 'Method: skills.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.skills.list

List Skills.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /skills`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The location to list the Skills in. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

### Request body

The request body must be empty.

### Response body

Response message for `  SkillRegistryService.ListSkills  ` .

If successful, the response body contains data with the following structure:

Fields

`skills[]` ` object ( Skill  ` )

The Skills.

`nextPageToken` `string`

A token, which can be sent as `  ListSkillsRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;skills&quot;: [{object (Skill)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
