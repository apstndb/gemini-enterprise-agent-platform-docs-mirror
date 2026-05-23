---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenerateLossClustersResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenerateLossClustersResponse
title: GenerateLossClustersResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for EvaluationAnalyticsService.GenerateLossClusters.

Fields

`analysisTime` ` string ( Timestamp  ` format)

The timestamp when this analysis was completed.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`results[]` ` object ( LossAnalysisResult  ` )

The analysis results, one per config provided in the request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;analysisTime&quot;: string,&quot;results&quot;: [{object (LossAnalysisResult)}]}</code></pre></td>
</tr>
</tbody>
</table>

## LossAnalysisResult

The top-level result for loss analysis, stored within an EvalSet.

Fields

`config` ` object ( LossAnalysisConfig  ` )

The configuration used to generate this analysis.

`analysisTime` ` string ( Timestamp  ` format)

The timestamp when this analysis was performed.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`clusters[]` ` object ( LossCluster  ` )

The list of identified loss clusters.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;config&quot;: {object (LossAnalysisConfig)},&quot;analysisTime&quot;: string,&quot;clusters&quot;: [{object (LossCluster)}]}</code></pre></td>
</tr>
</tbody>
</table>

## LossCluster

Represents a semantic grouping of failures (e.g., "Hallucination of Action").

Fields

`clusterId` `string`

Unique identifier for the loss cluster within the scope of the analysis result.

`taxonomyEntry` ` object ( LossTaxonomyEntry  ` )

The structured definition of the loss taxonomy for this cluster.

`itemCount` `integer`

The total number of EvaluationItems falling into this cluster.

`examples[]` ` object ( LossExample  ` )

A list of examples that belong to this cluster. This links the cluster back to the specific EvaluationItems and Rubrics.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;clusterId&quot;: string,&quot;taxonomyEntry&quot;: {object (LossTaxonomyEntry)},&quot;itemCount&quot;: integer,&quot;examples&quot;: [{object (LossExample)}]}</code></pre></td>
</tr>
</tbody>
</table>

## LossTaxonomyEntry

Defines a specific entry in the loss pattern taxonomy.

Fields

`l1Category` `string`

The primary category of the loss (e.g., "Hallucination", "Tool Calling"). This field is typically required.

`l2Category` `string`

The secondary category of the loss (e.g., "Hallucination of Action", "Incorrect Tool Selection").

`description` `string`

A detailed description of this loss pattern. Example: "The agent verbally confirms an action without executing the tool."

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
  &quot;l1Category&quot;: string,
  &quot;l2Category&quot;: string,
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## LossExample

Represents a specific example of a loss pattern.

Fields

`failedRubrics[]` ` object ( FailedRubric  ` )

The specific rubric(s) that failed and caused this example to be classified here. An example might fail multiple rubrics, but only specific ones trigger this loss pattern.

`source` `Union type`

The source of this example. `source` can be only one of the following:

`evaluationItem` `string`

Reference to the persisted EvalItem resource name. Format: projects/.../locations/.../evaluationItems/{itemId} Used when analysis is run on an EvalSet.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;failedRubrics&quot;: [{object (FailedRubric)}],// source&quot;evaluationItem&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>
