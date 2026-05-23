---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SamplingStrategy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SamplingStrategy
title: SamplingStrategy
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Sampling Strategy for logging, can be for both training and prediction dataset.

Fields

`randomSampleConfig` ` object ( RandomSampleConfig  ` )

Random sample config. Will support more sampling strategies later.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;randomSampleConfig&quot;: {object (RandomSampleConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RandomSampleConfig

Requests are randomly selected.

Fields

`sampleRate` `number`

Sample rate (0, 1\]

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
  &quot;sampleRate&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
