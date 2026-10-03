---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValueDestination
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValueDestination
title: FeatureValueDestination
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A destination location for feature values and format.

Fields

`destination` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bigqueryDestination` `object ( `[`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQueryDestination)` )`

Output in BigQuery format. [`BigQueryDestination.output_uri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQueryDestination#FIELDS.output_uri) in [`FeatureValueDestination.bigquery_destination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValueDestination#FIELDS.bigquery_destination) must refer to a table.

`tfrecordDestination` `object ( `[`TFRecordDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValueDestination#TFRecordDestination)` )`

Output in TFRecord format.

Below are the mapping from feature value type in Featurestore to feature value type in TFRecord:

```
value type in Featurestore                 | value type in TFRecord
DOUBLE, DOUBLE_ARRAY                       | FLOAT_LIST
INT64, INT64_ARRAY                         | INT64_LIST
STRING, STRING_ARRAY, BYTES                | BYTES_LIST
true -> byte_string("true"), false -> byte_string("false")
BOOL, BOOL_ARRAY (true, false)             | BYTES_LIST
```

`csvDestination` `object ( `[`CsvDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValueDestination#CsvDestination)` )`

Output in CSV format. Array feature value types are not allowed in CSV format.

End of mutually exclusive fields.

**JSON representation**

```
{

  // destination
  "bigqueryDestination": {
    object (BigQueryDestination)
  },
  "tfrecordDestination": {
    object (TFRecordDestination)
  },
  "csvDestination": {
    object (CsvDestination)
  }
  // Union type
}
```

## TFRecordDestination

The storage details for TFRecord output content.

Fields

`gcsDestination` `object ( ``GcsDestination`` )`

Required. Google Cloud Storage location.

**JSON representation**

```
{
  "gcsDestination": {
    object (GcsDestination)
  }
}
```

## CsvDestination

The storage details for CSV output content.

Fields

`gcsDestination` `object ( ``GcsDestination`` )`

Required. Google Cloud Storage location.

**JSON representation**

```
{
  "gcsDestination": {
    object (GcsDestination)
  }
}
```
