---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata
title: TablesDatasetMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata of Datasets that contain tables data.

Fields

`inputConfig` `object ( `[`InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata#InputConfig)` )`

**JSON representation**

```
{
  "inputConfig": {
    object (InputConfig)
  }
}
```

## InputConfig

The tables Dataset's data source. The Dataset doesn't store the data directly, but only pointer(s) to its data.

Fields

`source` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata#GcsSource)` )`

`bigquerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata#BigQuerySource)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "gcsSource": {
    object (GcsSource)
  },
  "bigquerySource": {
    object (BigQuerySource)
  }
  // Union type
}
```

## GcsSource

Fields

`uri[]` `string`

Cloud Storage URI of one or more files. Only CSV files are supported. The first line of the CSV file is used as the header. If there are multiple files, the header is the first line of the lexicographically first file, the other files must either contain the exact same header or omit the header.

**JSON representation**

```
{
  "uri": [
    string
  ]
}
```

## BigQuerySource

Fields

`uri` `string`

The URI of a BigQuery table. e.g. [bq://projectId.bqDatasetId.bqTableId](bq://projectId.bqDatasetId.bqTableId)

**JSON representation**

```
{
  "uri": string
}
```
