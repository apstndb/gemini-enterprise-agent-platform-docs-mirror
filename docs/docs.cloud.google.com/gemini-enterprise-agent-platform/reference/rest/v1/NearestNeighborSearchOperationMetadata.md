---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NearestNeighborSearchOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NearestNeighborSearchOperationMetadata
title: NearestNeighborSearchOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation metadata with regard to Matching Engine Index.

Fields

`contentValidationStats[]` ` object ( ContentValidationStats  ` )

The validation stats of the content (per file) to be inserted or updated on the Matching Engine Index resource. Populated if contentsDeltaUri is provided as part of `  Index.metadata  ` . Please note that, currently for those files that are broken or has unsupported file format, we will not have the stats for those files.

`dataBytesCount` `string ( int64 format)`

The ingested data size in bytes.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contentValidationStats&quot;: [{object (ContentValidationStats)}],&quot;dataBytesCount&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ContentValidationStats

Fields

`sourceGcsUri` `string`

Cloud Storage URI pointing to the original file in user's bucket.

`validRecordCount` `string ( int64 format)`

Number of records in this file that were successfully processed.

`invalidRecordCount` `string ( int64 format)`

Number of records in this file we skipped due to validate errors.

`partialErrors[]` ` object ( RecordError  ` )

The detail information of the partial failures encountered for those invalid records that couldn't be parsed. Up to 50 partial errors will be reported.

`validSparseRecordCount` `string ( int64 format)`

Number of sparse records in this file that were successfully processed.

`invalidSparseRecordCount` `string ( int64 format)`

Number of sparse records in this file we skipped due to validate errors.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceGcsUri&quot;: string,&quot;validRecordCount&quot;: string,&quot;invalidRecordCount&quot;: string,&quot;partialErrors&quot;: [{object (RecordError)}],&quot;validSparseRecordCount&quot;: string,&quot;invalidSparseRecordCount&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## RecordError

Fields

`errorType` ` enum ( RecordErrorType  ` )

The error type of this record.

`errorMessage` `string`

A human-readable message that is shown to the user to help them fix the error. Note that this message may change from time to time, your code should check against errorType as the source of truth.

`sourceGcsUri` `string`

Cloud Storage URI pointing to the original file in user's bucket.

`embeddingId` `string`

Empty if the embedding id is failed to parse.

`rawRecord` `string`

The original content of this record.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;errorType&quot;: enum (RecordErrorType),&quot;errorMessage&quot;: string,&quot;sourceGcsUri&quot;: string,&quot;embeddingId&quot;: string,&quot;rawRecord&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
