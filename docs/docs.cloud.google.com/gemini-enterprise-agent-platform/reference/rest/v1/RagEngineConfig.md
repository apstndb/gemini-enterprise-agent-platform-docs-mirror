---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig
title: RagEngineConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Config for RagEngine.

Fields

`name` `string`

Identifier. The name of the RagEngineConfig. Format: `projects/{project}/locations/{location}/ragEngineConfig`

`ragManagedDbConfig` `object ( `[`RagManagedDbConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig#RagManagedDbConfig)` )`

The config of the RagManagedDb used by RagEngine.

**JSON representation**

```
{
  "name": string,
  "ragManagedDbConfig": {
    object (RagManagedDbConfig)
  }
}
```

## RagManagedDbConfig

Configuration message for RagManagedDb used by RagEngine.

Fields

`tier` `Union type`

The tier of the RagManagedDb. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`scaled `**`(deprecated)`** `object ( `[`Scaled`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig#Scaled)` )`

> This item is deprecated!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Scaled tier.

`basic `**`(deprecated)`** `object ( `[`Basic`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig#Basic)` )`

> This item is deprecated!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Basic tier.

`unprovisioned `**`(deprecated)`** `object ( `[`Unprovisioned`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig#Unprovisioned)` )`

> This item is deprecated!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Unprovisioned tier.

End of mutually exclusive fields.

**JSON representation**

```
{

  // tier
  "scaled": {
    object (Scaled)
  },
  "basic": {
    object (Basic)
  },
  "unprovisioned": {
    object (Unprovisioned)
  }
  // Union type
}
```

## Scaled

This type has no fields.

Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

## Basic

This type has no fields.

Basic tier is a cost-effective and low compute tier suitable for the following cases: \* Experimenting with RagManagedDb. \* Small data size. \* Latency insensitive workload. \* Only using RAG Engine with external vector DBs.

NOTE: This is the default tier under Spanner mode if not explicitly chosen.

## Unprovisioned

This type has no fields.

Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.
