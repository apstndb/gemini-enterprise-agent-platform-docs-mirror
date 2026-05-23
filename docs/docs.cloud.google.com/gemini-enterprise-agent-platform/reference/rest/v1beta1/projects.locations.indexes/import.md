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

`config` ` object ( ConnectorConfig  ` )

Required. Configuration for importing data from an external source.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## ConnectorConfig

Configuration for importing data from an external source.

Fields

`source` `Union type`

The source of the data to import. `source` can be only one of the following:

`bigQuerySourceConfig` ` object ( BigQuerySourceConfig  ` )

Configuration for importing data from a BigQuery table.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// source&quot;bigQuerySourceConfig&quot;: {object (BigQuerySourceConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## BigQuerySourceConfig

Configuration for importing data from a BigQuery table.

Fields

`tablePath` `string`

Required. The path to the BigQuery table containing the index data, in the format of `bq://<projectId>.<datasetId>.<table>` .

`datapointFieldMapping` ` object ( DatapointFieldMapping  ` )

Required. Mapping of datapoint fields to BigQuery column names.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tablePath&quot;: string,&quot;datapointFieldMapping&quot;: {object (DatapointFieldMapping)}}</code></pre></td>
</tr>
</tbody>
</table>

## DatapointFieldMapping

Mapping of datapoint fields to column names for columnar data sources.

Fields

`idColumn` `string`

Required. The column with unique identifiers for each data point.

`embeddingColumn` `string`

Required. The column with the vector embeddings for each data point.

`restricts[]` ` object ( Restrict  ` )

Optional. List of restricts for string values.

`numericRestricts[]` ` object ( NumericRestrict  ` )

Optional. List of restricts for numeric values.

`metadataColumns[]` `string`

Optional. List of columns containing metadata to be included in the index.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;idColumn&quot;: string,&quot;embeddingColumn&quot;: string,&quot;restricts&quot;: [{object (Restrict)}],&quot;numericRestricts&quot;: [{object (NumericRestrict)}],&quot;metadataColumns&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## Restrict

Restrictions on string values.

Fields

`namespace` `string`

Required. The namespace of the restrict in the index.

`allowColumn[]` `string`

Optional. The columns containing the allow values.

`denyColumn[]` `string`

Optional. The columns containing the deny values.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;namespace&quot;: string,
  &quot;allowColumn&quot;: [
    string
  ],
  &quot;denyColumn&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## NumericRestrict

Restrictions on numeric values.

Fields

`namespace` `string`

Required. The namespace of the restrict.

`valueColumn` `string`

Optional. The column containing the numeric value.

`valueType` ` enum ( ValueType  ` )

Required. Numeric type of the restrict. Must be consistent for all datapoints within the namespace.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;namespace&quot;: string,&quot;valueColumn&quot;: string,&quot;valueType&quot;: enum (ValueType)}</code></pre></td>
</tr>
</tbody>
</table>

## ValueType

The type of numeric value for the restrict.

Enums

`VALUE_TYPE_UNSPECIFIED`

Should not be used.

`INT`

Represents 64 bit integer.

`FLOAT`

Represents 32 bit float.

`DOUBLE`

Represents 64 bit float.
