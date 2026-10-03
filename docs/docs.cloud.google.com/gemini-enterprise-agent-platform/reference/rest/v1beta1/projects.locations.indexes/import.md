---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import
title: 'Method: indexes.import'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexes.import

Imports an Index from an external source (e.g., BigQuery).

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:import`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Index resource to import data to. Format: `projects/{project}/locations/{location}/indexes/{index}`

### Request body

The request body contains data with the following structure:

Fields

`isCompleteOverwrite` `boolean`

Optional. If true, completely replace existing index data. Must be true for streaming update indexes.

`config` `object ( `[`ConnectorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import#ConnectorConfig)` )`

Required. Configuration for importing data from an external source.

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

## ConnectorConfig

Configuration for importing data from an external source.

Fields

`source` `Union type`

The source of the data to import. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bigQuerySourceConfig` `object ( `[`BigQuerySourceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import#BigQuerySourceConfig)` )`

Configuration for importing data from a BigQuery table.

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "bigQuerySourceConfig": {
    object (BigQuerySourceConfig)
  }
  // Union type
}
```

## BigQuerySourceConfig

Configuration for importing data from a BigQuery table.

Fields

`tablePath` `string`

Required. The path to the BigQuery table containing the index data, in the format of `bq://<projectId>.<datasetId>.<table>` .

`datapointFieldMapping` `object ( `[`DatapointFieldMapping`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import#DatapointFieldMapping)` )`

Required. Mapping of datapoint fields to BigQuery column names.

**JSON representation**

```
{
  "tablePath": string,
  "datapointFieldMapping": {
    object (DatapointFieldMapping)
  }
}
```

## DatapointFieldMapping

Mapping of datapoint fields to column names for columnar data sources.

Fields

`idColumn` `string`

Required. The column with unique identifiers for each data point.

`embeddingColumn` `string`

Required. The column with the vector embeddings for each data point.

`restricts[]` `object ( `[`Restrict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import#Restrict)` )`

Optional. List of restricts for string values.

`numericRestricts[]` `object ( `[`NumericRestrict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import#NumericRestrict)` )`

Optional. List of restricts for numeric values.

`metadataColumns[]` `string`

Optional. List of columns containing metadata to be included in the index.

**JSON representation**

```
{
  "idColumn": string,
  "embeddingColumn": string,
  "restricts": [
    {
      object (Restrict)
    }
  ],
  "numericRestricts": [
    {
      object (NumericRestrict)
    }
  ],
  "metadataColumns": [
    string
  ]
}
```

## Restrict

Restrictions on string values.

Fields

`namespace` `string`

Required. The namespace of the restrict in the index.

`allowColumn[]` `string`

Optional. The columns containing the allow values.

`denyColumn[]` `string`

Optional. The columns containing the deny values.

**JSON representation**

```
{
  "namespace": string,
  "allowColumn": [
    string
  ],
  "denyColumn": [
    string
  ]
}
```

## NumericRestrict

Restrictions on numeric values.

Fields

`namespace` `string`

Required. The namespace of the restrict.

`valueColumn` `string`

Optional. The column containing the numeric value.

`valueType` `enum ( `[`ValueType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/import#ValueType)` )`

Required. Numeric type of the restrict. Must be consistent for all datapoints within the namespace.

**JSON representation**

```
{
  "namespace": string,
  "valueColumn": string,
  "valueType": enum (ValueType)
}
```

## ValueType

The type of numeric value for the restrict.

| Enums                    |                            |
|--------------------------|----------------------------|
| `VALUE_TYPE_UNSPECIFIED` | Should not be used.        |
| `INT`                    | Represents 64 bit integer. |
| `FLOAT`                  | Represents 32 bit float.   |
| `DOUBLE`                 | Represents 64 bit float.   |
