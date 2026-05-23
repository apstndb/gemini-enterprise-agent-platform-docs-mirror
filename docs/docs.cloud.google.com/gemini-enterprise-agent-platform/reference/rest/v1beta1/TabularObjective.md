---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective
title: TabularObjective
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Tabular monitoring objective.

Fields

`featureDriftSpec` ` object ( DataDriftSpec  ` )

Input feature distribution drift monitoring spec.

`predictionOutputDriftSpec` ` object ( DataDriftSpec  ` )

Prediction output distribution drift monitoring spec.

`featureAttributionSpec` ` object ( FeatureAttributionSpec  ` )

feature attribution monitoring spec.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureDriftSpec&quot;: {object (DataDriftSpec)},&quot;predictionOutputDriftSpec&quot;: {object (DataDriftSpec)},&quot;featureAttributionSpec&quot;: {object (FeatureAttributionSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## DataDriftSpec

data drift monitoring spec. data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.

Fields

`features[]` `string`

feature names / Prediction output names interested in monitoring. These should be a subset of the input feature names or prediction output names specified in the monitoring schema. If the field is not specified all features / prediction outputs outlied in the monitoring schema will be used.

`categoricalMetricType` `string`

Supported metrics type: \* l\_infinity \* jensen\_shannon\_divergence

`numericMetricType` `string`

Supported metrics type: \* jensen\_shannon\_divergence

`defaultCategoricalAlertCondition` ` object ( ModelMonitoringAlertCondition  ` )

Default alert condition for all the categorical features.

`defaultNumericAlertCondition` ` object ( ModelMonitoringAlertCondition  ` )

Default alert condition for all the numeric features.

`featureAlertConditions` ` map (key: string, value: object ( ModelMonitoringAlertCondition  ` ))

Per feature alert condition will override default alert condition.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;features&quot;: [string],&quot;categoricalMetricType&quot;: string,&quot;numericMetricType&quot;: string,&quot;defaultCategoricalAlertCondition&quot;: {object (ModelMonitoringAlertCondition)},&quot;defaultNumericAlertCondition&quot;: {object (ModelMonitoringAlertCondition)},&quot;featureAlertConditions&quot;: {string: {object (ModelMonitoringAlertCondition)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringAlertCondition

Monitoring alert triggered condition.

Fields

`condition` `Union type`

Alert triggered condition. `condition` can be only one of the following:

`threshold` `number`

A condition that compares a stats value against a threshold. Alert will be triggered if value above the threshold.

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

  // condition
  &quot;threshold&quot;: number
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureAttributionSpec

feature attribution monitoring spec.

Fields

`features[]` `string`

feature names interested in monitoring. These should be a subset of the input feature names specified in the monitoring schema. If the field is not specified all features outlied in the monitoring schema will be used.

`defaultAlertCondition` ` object ( ModelMonitoringAlertCondition  ` )

Default alert condition for all the features.

`featureAlertConditions` ` map (key: string, value: object ( ModelMonitoringAlertCondition  ` ))

Per feature alert condition will override default alert condition.

`batchExplanationDedicatedResources` ` object ( BatchDedicatedResources  ` )

The config of resources used by the Model Monitoring during the batch explanation for non-AutoML models. If not set, `n1-standard-2` machine type will be used by default.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;features&quot;: [string],&quot;defaultAlertCondition&quot;: {object (ModelMonitoringAlertCondition)},&quot;featureAlertConditions&quot;: {string: {object (ModelMonitoringAlertCondition)},...},&quot;batchExplanationDedicatedResources&quot;: {object (BatchDedicatedResources)}}</code></pre></td>
</tr>
</tbody>
</table>
