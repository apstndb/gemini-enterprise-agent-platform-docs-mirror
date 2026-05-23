---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation
title: Annotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

Fields

`name` `string`

Output only. Resource name of the Annotation.

`payloadSchemaUri` `string`

Required. Google Cloud Storage URI points to a YAML file describing `  payload  ` . The schema is defined as an [OpenAPI 3.0.2 Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with the parent Dataset's `  metadata  ` .

`payload` ` value ( Value  ` format)

Required. The schema of the payload can be found in `  payload_schema  ` .

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Annotation was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Annotation was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`annotationSource` ` object ( UserActionReference  ` )

Output only. The source of the Annotation.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your Annotations.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Annotation(System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Annotation:

  - "aiplatform.googleapis.com/annotation\_set\_name": optional, name of the UI's annotation set this Annotation belongs to. If not set, the Annotation is not visible in the UI.

  - "aiplatform.googleapis.com/payload\_schema": output only, its value is the `  payload_schema's  ` title.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;payloadSchemaUri&quot;: string,&quot;payload&quot;: value,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;annotationSource&quot;: {object (UserActionReference)},&quot;labels&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>

## UserActionReference

References an API call. It contains more information about long running operation and Jobs that are triggered by the API call.

Fields

`method` `string`

The method name of the API RPC call. For example, "/google.cloud.aiplatform.{apiVersion}.DatasetService.CreateDataset"

`reference` `Union type`

`reference` can be only one of the following:

`operation` `string`

For API calls that return a long running operation. Resource name of the long running operation. Format: `projects/{project}/locations/{location}/operations/{operation}`

`dataLabelingJob` `string`

For API calls that start a LabelingJob. Resource name of the LabelingJob. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{dataLabelingJob}`

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
  &quot;method&quot;: string,

  // reference
  &quot;operation&quot;: string,
  &quot;dataLabelingJob&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>
