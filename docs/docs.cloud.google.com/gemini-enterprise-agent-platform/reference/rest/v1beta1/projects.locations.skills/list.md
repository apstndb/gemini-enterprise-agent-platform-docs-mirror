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

Response message for [`SkillRegistryService.ListSkills`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/list#google.cloud.aiplatform.v1beta1.SkillRegistryService.ListSkills) .

If successful, the response body contains data with the following structure:

Fields

`skills[]` `object ( `[`Skill`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills#Skill)` )`

The Skills.

`nextPageToken` `string`

A token, which can be sent as [`ListSkillsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/list#body.QUERY_PARAMETERS.page_token) to retrieve the next page. If this field is omitted, there are no subsequent pages.

**JSON representation**

```
{
  "skills": [
    {
      object (Skill)
    }
  ],
  "nextPageToken": string
}
```
