---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TablesDatasetMetadata
title: TablesDatasetMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata of Datasets that contain tables data.

Fields

`inputConfig` ` object ( InputConfig  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputConfig&quot;: {object (InputConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## InputConfig

The tables Dataset's data source. The Dataset doesn't store the data directly, but only pointer(s) to its data.

Fields

`source` `Union type`

`source` can be only one of the following:

`gcsSource` ` object ( GcsSource  ` )

`bigquerySource` ` object ( BigQuerySource  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// source&quot;gcsSource&quot;: {object (GcsSource)},&quot;bigquerySource&quot;: {object (BigQuerySource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## GcsSource

Fields

`uri[]` `string`

Cloud Storage URI of one or more files. Only CSV files are supported. The first line of the CSV file is used as the header. If there are multiple files, the header is the first line of the lexicographically first file, the other files must either contain the exact same header or omit the header.

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
  &quot;uri&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## BigQuerySource

Fields

`uri` `string`

The URI of a BigQuery table. e.g. <bq://projectId.bqDatasetId.bqTableId>

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
  &quot;uri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
