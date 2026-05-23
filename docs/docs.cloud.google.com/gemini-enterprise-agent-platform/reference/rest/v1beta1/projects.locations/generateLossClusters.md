---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/generateLossClusters
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/generateLossClusters
title: 'Method: locations.generateLossClusters'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.generateLossClusters

Generates loss clusters from evaluation results. This is a statelss API method that would not modify the EvaluationSet resource.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{location}:generateLossClusters`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`location` `string`

Required. The resource name of the Location. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`configs[]` ` object ( LossAnalysisConfig  ` )

Required. Configuration for the analysis algorithm. Analysis for multiple metrics and multiple candidates could be specified.

`source` `Union type`

The source of evaluation data to analyze. `source` can be only one of the following:

`evaluationSet` `string`

Reference to a persisted EvaluationSet. The service will read items from this set.

`inlineResults` ` object ( EvaluationResultList  ` )

Inline evaluation results. Useful for ephemeral analysis in notebooks/SDKs where data isn't persisted.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## EvaluationResultList

This type has no fields.

A wrapper to allow providing a list of items inline.

## LossAnalysisConfig

Configuration for the loss analysis job.

Fields

`metric` `string`

Required. The metric to analyze (e.g., "tool\_use\_quality"). This filters the EvaluationItems in the EvalSet to only those where EvaluationResult.metric matches this value.

`candidate` `string`

Required. The candidate model/agent to analyze (e.g., "gemini-3.0-pro"). This targets the specific CandidateResult within the EvaluationResult.

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
  &quot;metric&quot;: string,
  &quot;candidate&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
