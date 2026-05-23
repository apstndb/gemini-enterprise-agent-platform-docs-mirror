---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.annotationSpecs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.annotationSpecs
title: 'REST Resource: projects.locations.datasets.annotationSpecs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: AnnotationSpec

Identifies a concept with which DataItems may be annotated with.

Fields

`name` `string`

Output only. Resource name of the AnnotationSpec.

`displayName` `string`

Required. The user-defined name of the AnnotationSpec. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this AnnotationSpec was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when AnnotationSpec was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

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
  &quot;displayName&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;etag&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            get           `

Gets an AnnotationSpec.
