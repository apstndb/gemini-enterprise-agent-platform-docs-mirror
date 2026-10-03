---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue
title: FeatureValue
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

value for a feature.

Fields

`metadata` `object ( `[`Metadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#Metadata)` )`

metadata of feature value.

`value` `Union type`

Value for the feature. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`boolValue` `boolean`

Bool type feature value.

`doubleValue` `number`

Double type feature value.

`int64Value` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Int64 feature value.

`stringValue` `string`

String feature value.

`boolArrayValue` `object ( `[`BoolArray`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#BoolArray)` )`

A list of bool type feature value.

`doubleArrayValue` `object ( `[`DoubleArray`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#DoubleArray)` )`

A list of double type feature value.

`int64ArrayValue` `object ( `[`Int64Array`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#Int64Array)` )`

A list of int64 type feature value.

`stringArrayValue` `object ( `[`StringArray`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#StringArray)` )`

A list of string type feature value.

`bytesValue` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Bytes feature value.

A base64-encoded string.

`structValue` `object ( `[`StructValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#StructValue)` )`

A struct type feature value.

End of mutually exclusive fields.

**JSON representation**

```
{
  "metadata": {
    object (Metadata)
  },

  // value
  "boolValue": boolean,
  "doubleValue": number,
  "int64Value": string,
  "stringValue": string,
  "boolArrayValue": {
    object (BoolArray)
  },
  "doubleArrayValue": {
    object (DoubleArray)
  },
  "int64ArrayValue": {
    object (Int64Array)
  },
  "stringArrayValue": {
    object (StringArray)
  },
  "bytesValue": string,
  "structValue": {
    object (StructValue)
  }
  // Union type
}
```

## BoolArray

A list of boolean values.

Fields

`values[]` `boolean`

A list of bool values.

**JSON representation**

```
{
  "values": [
    boolean
  ]
}
```

## DoubleArray

A list of double values.

Fields

`values[]` `number`

A list of double values.

**JSON representation**

```
{
  "values": [
    number
  ]
}
```

## Int64Array

A list of int64 values.

Fields

`values[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

A list of int64 values.

**JSON representation**

```
{
  "values": [
    string
  ]
}
```

## StringArray

A list of string values.

Fields

`values[]` `string`

A list of string values.

**JSON representation**

```
{
  "values": [
    string
  ]
}
```

## StructValue

Struct (or object) type feature value.

Fields

`values[]` `object ( `[`StructFieldValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue#StructFieldValue)` )`

A list of field values.

**JSON representation**

```
{
  "values": [
    {
      object (StructFieldValue)
    }
  ]
}
```

## StructFieldValue

One field of a Struct (or object) type feature value.

Fields

`name` `string`

name of the field in the struct feature.

`value` `object ( `[`FeatureValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue)` )`

The value for this field.

**JSON representation**

```
{
  "name": string,
  "value": {
    object (FeatureValue)
  }
}
```

## Metadata

metadata of feature value.

Fields

`generateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

feature generation timestamp. Typically, it is provided by user at feature ingestion time. If not, feature store will use the system timestamp when the data is ingested into feature store.

Legacy feature Store: For streaming ingestion, the time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

**JSON representation**

```
{
  "generateTime": string
}
```
