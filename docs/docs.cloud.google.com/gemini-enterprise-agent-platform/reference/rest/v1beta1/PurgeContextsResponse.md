---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PurgeContextsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PurgeContextsResponse
title: PurgeContextsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`MetadataService.PurgeContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/purge#google.cloud.aiplatform.v1beta1.MetadataService.PurgeContexts) .

Fields

`purgeCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of Contexts that this request deleted (or, if `force` is false, the number of Contexts that will be deleted). This can be an estimate.

`purgeSample[]` `string`

A sample of the Context names that will be deleted. Only populated if `force` is set to false. The maximum number of samples is 100 (it is possible to return fewer).

**JSON representation**

```
{
  "purgeCount": string,
  "purgeSample": [
    string
  ]
}
```
