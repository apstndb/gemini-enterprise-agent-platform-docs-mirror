---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs
title: 'REST Resource: projects.locations.tensorboards.experiments.runs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: TensorboardRun

TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc

Fields

`name` `string`

Output only. name of the TensorboardRun. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`

`displayName` `string`

Required. user provided name of this TensorboardRun. This value must be unique among all TensorboardRuns belonging to the same parent TensorboardExperiment.

`description` `string`

description of this TensorboardRun.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this TensorboardRun was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this TensorboardRun was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your TensorboardRuns.

This field will be used to filter and visualize Runs in the Tensorboard UI. For example, a Agent Platform training job can set a label aiplatform.googleapis.com/trainingJobId=xxxxx to all the runs created within that job. An end user can set a label experimentId=xxxxx for all the runs produced in a Jupyter notebook. These runs can be grouped by a label value and visualized together in the Tensorboard UI.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one TensorboardRun (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`etag` `string`

Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

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
  &quot;etag&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            batchCreate           `

Batch create TensorboardRuns.

### `            create           `

Creates a TensorboardRun.

### `            delete           `

Deletes a TensorboardRun.

### `            get           `

Gets a TensorboardRun.

### `            list           `

Lists TensorboardRuns in a Location.

### `            patch           `

Updates a TensorboardRun.

### `            write           `

Write time series data points into multiple TensorboardTimeSeries under a TensorboardRun.
