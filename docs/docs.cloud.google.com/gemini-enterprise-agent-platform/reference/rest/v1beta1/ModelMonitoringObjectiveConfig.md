---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig
title: ModelMonitoringObjectiveConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

Fields

`trainingDataset` ` object ( TrainingDataset  ` )

Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified.

`trainingPredictionSkewDetectionConfig` ` object ( TrainingPredictionSkewDetectionConfig  ` )

The config for skew between training data and prediction data.

`predictionDriftDetectionConfig` ` object ( PredictionDriftDetectionConfig  ` )

The config for drift of prediction data.

`explanationConfig` ` object ( ExplanationConfig  ` )

The config for integrating with Vertex Explainable AI.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDataset&quot;: {object (TrainingDataset)},&quot;trainingPredictionSkewDetectionConfig&quot;: {object (TrainingPredictionSkewDetectionConfig)},&quot;predictionDriftDetectionConfig&quot;: {object (PredictionDriftDetectionConfig)},&quot;explanationConfig&quot;: {object (ExplanationConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## TrainingDataset

Training Dataset information.

Fields

`dataFormat` `string`

data format of the dataset, only applicable if the input is from Google Cloud Storage. The possible formats are:

"tf-record" The source file is a TFRecord file.

"csv" The source file is a CSV file. "jsonl" The source file is a JSONL file.

`targetField` `string`

The target field name the model is to predict. This field will be excluded when doing Predict and (or) Explain for the training data.

`loggingSamplingStrategy` ` object ( SamplingStrategy  ` )

Strategy to sample data from Training Dataset. If not set, we process the whole dataset.

`data_source` `Union type`

`data_source` can be only one of the following:

`dataset` `string`

The resource name of the Dataset used to train this Model.

`gcsSource` ` object ( GcsSource  ` )

The Google Cloud Storage uri of the unmanaged Dataset used to train this Model.

`bigquerySource` ` object ( BigQuerySource  ` )

The BigQuery table of the unmanaged Dataset used to train this Model.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataFormat&quot;: string,&quot;targetField&quot;: string,&quot;loggingSamplingStrategy&quot;: {object (SamplingStrategy)},// data_source&quot;dataset&quot;: string,&quot;gcsSource&quot;: {object (GcsSource)},&quot;bigquerySource&quot;: {object (BigQuerySource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TrainingPredictionSkewDetectionConfig

The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

Fields

`skewThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. If a feature needs to be monitored for skew, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between the training and prediction feature.

`attributionScoreSkewThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. The threshold here is against attribution score distance between the training and prediction feature.

`defaultSkewThreshold` ` object ( ThresholdConfig  ` )

Skew anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;skewThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;attributionScoreSkewThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;defaultSkewThreshold&quot;: {object (ThresholdConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## PredictionDriftDetectionConfig

The config for Prediction data drift detection.

Fields

`driftThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws.

`attributionScoreDriftThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows.

`defaultDriftThreshold` ` object ( ThresholdConfig  ` )

Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;driftThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;attributionScoreDriftThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;defaultDriftThreshold&quot;: {object (ThresholdConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExplanationConfig

The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanationSpec populated.

Fields

`enableFeatureAttributes` `boolean`

If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Agent Platform will log the feature attributions from explain response and do the skew/drift detection for them.

`explanationBaseline` ` object ( ExplanationBaseline  ` )

Predictions generated by the BatchPredictionJob using baseline dataset.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enableFeatureAttributes&quot;: boolean,&quot;explanationBaseline&quot;: {object (ExplanationBaseline)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExplanationBaseline

Output from `  BatchPredictionJob  ` for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

Fields

`predictionFormat` ` enum ( PredictionFormat  ` )

The storage format of the predictions generated BatchPrediction job.

`destination` `Union type`

The configuration specifying of BatchExplain job output. This can be used to generate the baseline of feature attribution scores. `destination` can be only one of the following:

`gcs` `object ( GcsDestination` )

Cloud Storage location for BatchExplain output.

`bigquery` ` object ( BigQueryDestination  ` )

BigQuery location for BatchExplain output.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictionFormat&quot;: enum (PredictionFormat),// destination&quot;gcs&quot;: {object (GcsDestination)},&quot;bigquery&quot;: {object (BigQueryDestination)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PredictionFormat

The storage format of the predictions generated BatchPrediction job.

Enums

`PREDICTION_FORMAT_UNSPECIFIED`

Should not be set.

`JSONL`

Predictions are in JSONL files.

`BIGQUERY`

Predictions are in BigQuery.
