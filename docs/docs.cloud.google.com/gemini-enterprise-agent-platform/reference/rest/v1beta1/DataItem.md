---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DataItem
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DataItem
title: DataItem
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A piece of data in a Dataset. Could be an image, a video, a document or plain text.

Fields

`name` `string`

Output only. The resource name of the DataItem.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this DataItem was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this DataItem was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your DataItems.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one DataItem(System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`payload` ` value ( Value  ` format)

Required. The data that the DataItem represents (for example, an image or a text snippet). The schema of the payload is stored in the parent Dataset's `  metadata schema's  ` dataItemSchemaUri field.

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
  &quot;name&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;payload&quot;: value,
  &quot;etag&quot;: string,
  &quot;satisfiesPzs&quot;: boolean,
  &quot;satisfiesPzi&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
