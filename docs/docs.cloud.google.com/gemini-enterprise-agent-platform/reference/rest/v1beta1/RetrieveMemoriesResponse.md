---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveMemoriesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveMemoriesResponse
title: RetrieveMemoriesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`MemoryBankService.RetrieveMemories`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieve#google.cloud.aiplatform.v1beta1.MemoryBankService.RetrieveMemories) .

Fields

`retrievedMemories[]` `object ( `[`RetrievedMemory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveMemoriesResponse#RetrievedMemory)` )`

The retrieved memories.

`nextPageToken` `string`

A token that can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages. This token is not set if similarity search was used for retrieval.

**JSON representation**

```
{
  "retrievedMemories": [
    {
      object (RetrievedMemory)
    }
  ],
  "nextPageToken": string
}
```

## RetrievedMemory

A retrieved memory.

Fields

`memory` `object ( `[`Memory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories#Memory)` )`

The retrieved Memory.

`distance` `number`

The distance between the query and the retrieved Memory. Smaller values indicate more similar memories. This is only set if similarity search was used for retrieval.

**JSON representation**

```
{
  "memory": {
    object (Memory)
  },
  "distance": number
}
```
