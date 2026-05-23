---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills/create
title: 'Method: skills.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.skills.create

Create a Skill.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /skills`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The location to create the Skill in. Format: `projects/{project}/locations/{location}`

### Query parameters

`skillId` `string`

Required. The id to use for the Skill, which will become the final component of the Skill's resource name.

If not provided, a system-generated id will be used.

This value must be 1-63 characters. Valid characters are lowercase letters, numbers, and hyphens. The first character must be a lowercase letter, and the last character must be a lowercase letter or a number. Specifically, the id must match the regular expression: `^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$` See [AIP-122](https://aip.dev/122#resource-id-segments) for more details.

### Request body

The request body contains an instance of `  Skill  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
