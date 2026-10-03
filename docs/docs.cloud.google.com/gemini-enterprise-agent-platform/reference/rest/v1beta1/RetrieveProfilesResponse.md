---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveProfilesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveProfilesResponse
title: RetrieveProfilesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`MemoryBankService.RetrieveProfiles`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieveProfiles#google.cloud.aiplatform.v1beta1.MemoryBankService.RetrieveProfiles) .

Fields

`profiles` `map (key: string, value: object ( `[`MemoryProfile`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveProfilesResponse#MemoryProfile)` ))`

The retrieved structured profiles, which match the schemas under the requested scope. The key is the id of the schema that the profile is linked with, which corresponds to the `schemaId` defined inside the `SchemaConfig` , under `StructuredMemoryCustomizationConfig` .

**JSON representation**

```
{
  "profiles": {
    string: {
      object (MemoryProfile)
    },
    ...
  }
}
```

## MemoryProfile

A memory profile.

Fields

`schemaId` `string`

Represents the id of the schema. This id corresponds to the `schemaId` defined inside the SchemaConfig, under StructuredMemoryCustomizationConfig.

`profile` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Represents the profile data.

**JSON representation**

```
{
  "schemaId": string,
  "profile": {
    object
  }
}
```
