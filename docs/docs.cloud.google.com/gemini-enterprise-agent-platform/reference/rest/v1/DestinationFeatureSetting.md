---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DestinationFeatureSetting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DestinationFeatureSetting
title: DestinationFeatureSetting
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`featureId` `string`

Required. The id of the feature to apply the setting to.

`destinationField` `string`

Specify the field name in the export destination. If not specified, feature id is used.

**JSON representation**

```
{
  "featureId": string,
  "destinationField": string
}
```
