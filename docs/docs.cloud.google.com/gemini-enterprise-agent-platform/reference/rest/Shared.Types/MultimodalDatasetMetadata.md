---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MultimodalDatasetMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MultimodalDatasetMetadata
title: MultimodalDatasetMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata of Multimodal Datasets.

Fields

`inputConfig` ` object ( MultimodalDatasetInputConfig  ` )

Specifies the input source and configuration.

`geminiRequestReadConfig` ` object ( GeminiRequestReadConfig  ` )

The configuration for how to read Gemini requests from the dataset.

`keyColumnName` `string`

The name of the column in the BigQuery table that contains the keys of the rows.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputConfig&quot;: {object (MultimodalDatasetInputConfig)},&quot;geminiRequestReadConfig&quot;: {object (GeminiRequestReadConfig)},&quot;keyColumnName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## MultimodalDatasetInputConfig

Specifies the input source and configuration.

Fields

`source` `Union type`

The source of the input. We only support BigQuery as source for now. `source` can be only one of the following:

`bigquerySource` ` object ( BigQuerySource  ` )

BigQuery source table.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// source&quot;bigquerySource&quot;: {object (BigQuerySource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## BigQuerySource

Specifies the BigQuery source.

Fields

`uri` `string`

The URI of a BigQuery table. e.g. <bq://project.bqDataset.bqTable>

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
