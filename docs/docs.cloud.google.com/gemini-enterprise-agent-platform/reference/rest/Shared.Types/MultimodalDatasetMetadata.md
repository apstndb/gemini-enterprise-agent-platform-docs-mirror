---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MultimodalDatasetMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MultimodalDatasetMetadata
title: MultimodalDatasetMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata of Multimodal Datasets.

Fields

`inputConfig` `object ( `[`MultimodalDatasetInputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MultimodalDatasetMetadata#MultimodalDatasetInputConfig)` )`

Specifies the input source and configuration.

`geminiRequestReadConfig` `object ( `[`GeminiRequestReadConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig)` )`

The configuration for how to read Gemini requests from the dataset.

`keyColumnName` `string`

The name of the column in the BigQuery table that contains the keys of the rows.

**JSON representation**

```
{
  "inputConfig": {
    object (MultimodalDatasetInputConfig)
  },
  "geminiRequestReadConfig": {
    object (GeminiRequestReadConfig)
  },
  "keyColumnName": string
}
```

## MultimodalDatasetInputConfig

Specifies the input source and configuration.

Fields

`source` `Union type`

The source of the input. We only support BigQuery as source for now. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bigquerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MultimodalDatasetMetadata#BigQuerySource)` )`

BigQuery source table.

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "bigquerySource": {
    object (BigQuerySource)
  }
  // Union type
}
```

## BigQuerySource

Specifies the BigQuery source.

Fields

`uri` `string`

The URI of a BigQuery table. e.g. [bq://project.bqDataset.bqTable](bq://project.bqDataset.bqTable)

**JSON representation**

```
{
  "uri": string
}
```
