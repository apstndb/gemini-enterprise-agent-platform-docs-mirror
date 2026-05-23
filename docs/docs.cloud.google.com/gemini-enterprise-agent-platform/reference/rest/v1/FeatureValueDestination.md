---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValueDestination
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValueDestination
title: FeatureValueDestination
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A destination location for feature values and format.

Fields

`destination` `Union type`

`destination` can be only one of the following:

`bigqueryDestination` ` object ( BigQueryDestination  ` )

Output in BigQuery format. `  BigQueryDestination.output_uri  ` in `  FeatureValueDestination.bigquery_destination  ` must refer to a table.

`tfrecordDestination` ` object ( TFRecordDestination  ` )

Output in TFRecord format.

Below are the mapping from feature value type in Featurestore to feature value type in TFRecord:

    value type in Featurestore                 | value type in TFRecord
    DOUBLE, DOUBLE_ARRAY                       | FLOAT_LIST
    INT64, INT64_ARRAY                         | INT64_LIST
    STRING, STRING_ARRAY, BYTES                | BYTES_LIST
    true -> byte_string("true"), false -> byte_string("false")
    BOOL, BOOL_ARRAY (true, false)             | BYTES_LIST

`csvDestination` ` object ( CsvDestination  ` )

Output in CSV format. Array feature value types are not allowed in CSV format.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// destination&quot;bigqueryDestination&quot;: {object (BigQueryDestination)},&quot;tfrecordDestination&quot;: {object (TFRecordDestination)},&quot;csvDestination&quot;: {object (CsvDestination)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TFRecordDestination

The storage details for TFRecord output content.

Fields

`gcsDestination` ` object ( GcsDestination  ` )

Required. Google Cloud Storage location.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;gcsDestination&quot;: {object (GcsDestination)}}</code></pre></td>
</tr>
</tbody>
</table>

## CsvDestination

The storage details for CSV output content.

Fields

`gcsDestination` ` object ( GcsDestination  ` )

Required. Google Cloud Storage location.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;gcsDestination&quot;: {object (GcsDestination)}}</code></pre></td>
</tr>
</tbody>
</table>
