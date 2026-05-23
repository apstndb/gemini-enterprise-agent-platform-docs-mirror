---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringInput
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringInput
title: ModelMonitoringInput
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Model monitoring data input spec.

Fields

`dataset` `Union type`

Dataset source. `dataset` can be only one of the following:

`columnizedDataset` ` object ( ModelMonitoringDataset  ` )

Columnized dataset.

`batchPredictionOutput` ` object ( BatchPredictionOutput  ` )

Agent Platform Batch prediction Job.

`vertexEndpointLogs` ` object ( VertexEndpointLogs  ` )

Agent Platform Endpoint request & response logging.

`time_spec` `Union type`

Time specification for the dataset. `time_spec` can be only one of the following:

`timeInterval` ` object ( Interval  ` )

The time interval (pair of startTime and endTime) for which results should be returned.

`timeOffset` ` object ( TimeOffset  ` )

The time offset setting for which results should be returned.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// dataset&quot;columnizedDataset&quot;: {object (ModelMonitoringDataset)},&quot;batchPredictionOutput&quot;: {object (BatchPredictionOutput)},&quot;vertexEndpointLogs&quot;: {object (VertexEndpointLogs)}// Union type// time_spec&quot;timeInterval&quot;: {object (Interval)},&quot;timeOffset&quot;: {object (TimeOffset)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringDataset

Input dataset spec.

Fields

`timestampField` `string`

The timestamp field. Usually for serving data.

`data_location` `Union type`

Choose one of supported data location for columnized dataset. `data_location` can be only one of the following:

`vertexDataset` `string`

Resource name of the Agent Platform managed dataset.

`gcsSource` ` object ( ModelMonitoringGcsSource  ` )

Google Cloud Storage data source.

`bigquerySource` ` object ( ModelMonitoringBigQuerySource  ` )

BigQuery data source.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timestampField&quot;: string,// data_location&quot;vertexDataset&quot;: string,&quot;gcsSource&quot;: {object (ModelMonitoringGcsSource)},&quot;bigquerySource&quot;: {object (ModelMonitoringBigQuerySource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringGcsSource

Dataset spec for data stored in Google Cloud Storage.

Fields

`gcsUri` `string`

Google Cloud Storage URI to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> .

`format` ` enum ( DataFormat  ` )

data format of the dataset.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;gcsUri&quot;: string,&quot;format&quot;: enum (DataFormat)}</code></pre></td>
</tr>
</tbody>
</table>

## DataFormat

Supported data format.

Enums

`DATA_FORMAT_UNSPECIFIED`

data format unspecified, used when this field is unset.

`CSV`

CSV files.

`TF_RECORD`

TfRecord files

`JSONL`

JsonL files.

## ModelMonitoringBigQuerySource

Dataset spec for data sotred in BigQuery.

Fields

`connection` `Union type`

`connection` can be only one of the following:

`tableUri` `string`

BigQuery URI to a table, up to 2000 characters long. All the columns in the table will be selected. Accepted forms:

  - BigQuery path. For example: `bq://projectId.bqDatasetId.bqTableId` .

`query` `string`

Standard SQL to be used instead of the `tableUri` .

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

  // connection
  &quot;tableUri&quot;: string,
  &quot;query&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## BatchPredictionOutput

data from Agent Platform Batch prediction job output.

Fields

`batchPredictionJob` `string`

Agent Platform Batch prediction job resource name. The job must match the model version specified in \[ModelMonitor\].\[modelMonitoringTarget\].

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
  &quot;batchPredictionJob&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## VertexEndpointLogs

data from Agent Platform Endpoint request response logging.

Fields

`endpoints[]` `string`

List of endpoint resource names. The endpoints must enable the logging with the \[Endpoint\].\[requestResponseLoggingConfig\], and must contain the deployed model corresponding to the model version specified in \[ModelMonitor\].\[modelMonitoringTarget\].

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
  &quot;endpoints&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## TimeOffset

time offset setting.

Fields

`offset` `string`

\[offset\] is the time difference from the cut-off time. For scheduled jobs, the cut-off time is the scheduled time. For non-scheduled jobs, it's the time when the job was created. Currently we support the following format: 'w|W': Week, 'd|D': Day, 'h|H': Hour E.g. '1h' stands for 1 hour, '2d' stands for 2 days.

`window` `string`

\[window\] refers to the scope of data selected for analysis. It allows you to specify the quantity of data you wish to examine. Currently we support the following format: 'w|W': Week, 'd|D': Day, 'h|H': Hour E.g. '1h' stands for 1 hour, '2d' stands for 2 days.

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
  &quot;offset&quot;: string,
  &quot;window&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
