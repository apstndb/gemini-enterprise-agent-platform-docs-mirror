---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NearestNeighborSearchOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NearestNeighborSearchOperationMetadata
title: NearestNeighborSearchOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation metadata with regard to Matching Engine Index.

Fields

`contentValidationStats[]` `object ( `[`ContentValidationStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NearestNeighborSearchOperationMetadata#ContentValidationStats)` )`

The validation stats of the content (per file) to be inserted or updated on the Matching Engine Index resource. Populated if contentsDeltaUri is provided as part of [`Index.metadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes#Index.FIELDS.metadata) . Please note that, currently for those files that are broken or has unsupported file format, we will not have the stats for those files.

`dataBytesCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The ingested data size in bytes.

**JSON representation**

```
{
  "contentValidationStats": [
    {
      object (ContentValidationStats)
    }
  ],
  "dataBytesCount": string
}
```

## ContentValidationStats

Fields

`sourceGcsUri` `string`

Cloud Storage URI pointing to the original file in user's bucket.

`validRecordCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of records in this file that were successfully processed.

`invalidRecordCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of records in this file we skipped due to validate errors.

`partialErrors[]` `object ( `[`RecordError`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NearestNeighborSearchOperationMetadata#RecordError)` )`

The detail information of the partial failures encountered for those invalid records that couldn't be parsed. Up to 50 partial errors will be reported.

`validSparseRecordCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of sparse records in this file that were successfully processed.

`invalidSparseRecordCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of sparse records in this file we skipped due to validate errors.

**JSON representation**

```
{
  "sourceGcsUri": string,
  "validRecordCount": string,
  "invalidRecordCount": string,
  "partialErrors": [
    {
      object (RecordError)
    }
  ],
  "validSparseRecordCount": string,
  "invalidSparseRecordCount": string
}
```

## RecordError

Fields

`errorType` `enum ( `[`RecordErrorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RecordErrorType)` )`

The error type of this record.

`errorMessage` `string`

A human-readable message that is shown to the user to help them fix the error. Note that this message may change from time to time, your code should check against errorType as the source of truth.

`sourceGcsUri` `string`

Cloud Storage URI pointing to the original file in user's bucket.

`embeddingId` `string`

Empty if the embedding id is failed to parse.

`rawRecord` `string`

The original content of this record.

**JSON representation**

```
{
  "errorType": enum (RecordErrorType),
  "errorMessage": string,
  "sourceGcsUri": string,
  "embeddingId": string,
  "rawRecord": string
}
```
