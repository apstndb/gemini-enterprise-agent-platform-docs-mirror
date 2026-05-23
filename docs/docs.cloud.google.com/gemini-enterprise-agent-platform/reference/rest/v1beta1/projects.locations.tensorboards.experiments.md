---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments
title: 'REST Resource: projects.locations.tensorboards.experiments'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: TensorboardExperiment

A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

Fields

`name` `string`

Output only. name of the TensorboardExperiment. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`

`displayName` `string`

user provided name of this TensorboardExperiment.

`description` `string`

description of this TensorboardExperiment.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this TensorboardExperiment was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this TensorboardExperiment was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your TensorboardExperiment.

label keys and values cannot be longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with `aiplatform.googleapis.com/` and are immutable. The following system labels exist for each Dataset:

  - `aiplatform.googleapis.com/dataset_metadata_schema` : output only. Its value is the `  metadataSchema's  ` title.

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`source` `string`

Immutable. Source of the TensorboardExperiment. Example: a custom training job.

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
  &quot;description&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;etag&quot;: string,
  &quot;source&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            batchCreate           `

Batch create TensorboardTimeSeries that belong to a TensorboardExperiment.

### `            create           `

Creates a TensorboardExperiment.

### `            delete           `

Deletes a TensorboardExperiment.

### `            get           `

Gets a TensorboardExperiment.

### `            list           `

Lists TensorboardExperiments in a Location.

### `            patch           `

Updates a TensorboardExperiment.

### `            write           `

Write time series data points of multiple TensorboardTimeSeries in multiple TensorboardRun's.
