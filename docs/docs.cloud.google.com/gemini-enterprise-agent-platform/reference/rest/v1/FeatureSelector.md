---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureSelector
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureSelector
title: FeatureSelector
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Selector for Features of an EntityType.

Fields

`idMatcher` `object ( `[`IdMatcher`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureSelector#IdMatcher)` )`

Required. Matches Features based on id.

**JSON representation**

```
{
  "idMatcher": {
    object (IdMatcher)
  }
}
```

## IdMatcher

Matcher for Features of an EntityType by feature id.

Fields

`ids[]` `string`

Required. The following are accepted as `ids` :

- A single-element list containing only `*` , which selects all Features in the target EntityType, or
- A list containing only feature IDs, which selects only Features with those IDs in the target EntityType.

**JSON representation**

```
{
  "ids": [
    string
  ]
}
```
