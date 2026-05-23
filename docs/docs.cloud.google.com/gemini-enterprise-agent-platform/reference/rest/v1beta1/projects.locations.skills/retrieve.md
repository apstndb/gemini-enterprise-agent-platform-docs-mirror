---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/retrieve
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/retrieve
title: 'Method: skills.retrieve'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.skills.retrieve

Retrieves skills.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /skills:retrieve`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The location to retrieve the Skills in. Format: `projects/{project}/locations/{location}`

### Query parameters

`query` `string`

Optional. The query to find matching skills.

`topK` `integer`

Optional. The maximum number of skills to return. The service may return fewer than this value. If unspecified, at most 10 skills will be returned. The maximum value is 100.

### Request body

The request body must be empty.

### Response body

Response message for `  SkillRegistryService.RetrieveSkills  ` .

If successful, the response body contains data with the following structure:

Fields

`retrievedSkills[]` ` object ( RetrievedSkill  ` )

Skills ranked by similarity if applicable; otherwise, the order is undefined.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;retrievedSkills&quot;: [{object (RetrievedSkill)}]}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievedSkill

A retrieved skill.

Fields

`skillName` `string`

The skill resource name. Format: projects/{project}/locations/{location}/skills/{skill}

`description` `string`

The skill description.

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
  &quot;skillName&quot;: string,
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
