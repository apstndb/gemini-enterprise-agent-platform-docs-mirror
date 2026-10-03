---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQuerySource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQuerySource
title: BigQuerySource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The BigQuery location for the input content.

Fields

`inputUri` `string`

Required. BigQuery URI to a table, up to 2000 characters long. Accepted forms:

- BigQuery path. For example: `bq://projectId.bqDatasetId.bqTableId` .

**JSON representation**

```
{
  "inputUri": string
}
```
