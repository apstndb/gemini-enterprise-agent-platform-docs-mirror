---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions/list
title: 'Method: revisions.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.skills.revisions.list

List Skill Revisions for a Skill.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /revisions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Skill to list revisions for. Format: `projects/{project}/locations/{location}/skills/{skill}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

`filter` `string`

Optional. The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

Supported fields (equality match only): \* `labels`

### Request body

The request body must be empty.

### Response body

Response message for `  SkillRegistryService.ListSkillRevisions  ` .

If successful, the response body contains data with the following structure:

Fields

`skillRevisions[]` ` object ( SkillRevision  ` )

The list of Skill Revisions in the request page.

`nextPageToken` `string`

A token, which can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;skillRevisions&quot;: [{object (SkillRevision)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
