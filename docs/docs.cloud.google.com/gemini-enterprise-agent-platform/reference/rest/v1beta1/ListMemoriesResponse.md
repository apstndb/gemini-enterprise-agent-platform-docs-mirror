---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ListMemoriesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ListMemoriesResponse
title: ListMemoriesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`MemoryBankService.ListMemories`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/list#google.cloud.aiplatform.v1beta1.MemoryBankService.ListMemories) .

Fields

`memories[]` `object ( `[`Memory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories#Memory)` )`

List of Memories in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListMemoriesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "memories": [
    {
      object (Memory)
    }
  ],
  "nextPageToken": string
}
```
