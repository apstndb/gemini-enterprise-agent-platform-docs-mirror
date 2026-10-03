---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig
title: ModelMonitoringObjectiveConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

Fields

`trainingDataset` `object ( `[`TrainingDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig#TrainingDataset)` )`

Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified.

`trainingPredictionSkewDetectionConfig` `object ( `[`TrainingPredictionSkewDetectionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig#TrainingPredictionSkewDetectionConfig)` )`

The config for skew between training data and prediction data.

`predictionDriftDetectionConfig` `object ( `[`PredictionDriftDetectionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig#PredictionDriftDetectionConfig)` )`

The config for drift of prediction data.

`explanationConfig` `object ( `[`ExplanationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig#ExplanationConfig)` )`

The config for integrating with Vertex Explainable AI.

**JSON representation**

```
{
  "trainingDataset": {
    object (TrainingDataset)
  },
  "trainingPredictionSkewDetectionConfig": {
    object (TrainingPredictionSkewDetectionConfig)
  },
  "predictionDriftDetectionConfig": {
    object (PredictionDriftDetectionConfig)
  },
  "explanationConfig": {
    object (ExplanationConfig)
  }
}
```

## TrainingDataset

Training Dataset information.

Fields

`dataFormat` `string`

data format of the dataset, only applicable if the input is from Google Cloud Storage. The possible formats are:

"tf-record" The source file is a TFRecord file.

"csv" The source file is a CSV file. "jsonl" The source file is a JSONL file.

`targetField` `string`

The target field name the model is to predict. This field will be excluded when doing Predict and (or) Explain for the training data.

`loggingSamplingStrategy` `object ( `[`SamplingStrategy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SamplingStrategy)` )`

Strategy to sample data from Training Dataset. If not set, we process the whole dataset.

`data_source` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`dataset` `string`

The resource name of the Dataset used to train this Model.

`gcsSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GcsSource)` )`

The Google Cloud Storage uri of the unmanaged Dataset used to train this Model.

`bigquerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQuerySource)` )`

The BigQuery table of the unmanaged Dataset used to train this Model.

End of mutually exclusive fields.

**JSON representation**

```
{
  "dataFormat": string,
  "targetField": string,
  "loggingSamplingStrategy": {
    object (SamplingStrategy)
  },

  // data_source
  "dataset": string,
  "gcsSource": {
    object (GcsSource)
  },
  "bigquerySource": {
    object (BigQuerySource)
  }
  // Union type
}
```

## TrainingPredictionSkewDetectionConfig

The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

Fields

`skewThresholds` `map (key: string, value: object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` ))`

Key is the feature name and value is the threshold. If a feature needs to be monitored for skew, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between the training and prediction feature.

`attributionScoreSkewThresholds` `map (key: string, value: object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` ))`

Key is the feature name and value is the threshold. The threshold here is against attribution score distance between the training and prediction feature.

`defaultSkewThreshold` `object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` )`

Skew anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features.

**JSON representation**

```
{
  "skewThresholds": {
    string: {
      object (ThresholdConfig)
    },
    ...
  },
  "attributionScoreSkewThresholds": {
    string: {
      object (ThresholdConfig)
    },
    ...
  },
  "defaultSkewThreshold": {
    object (ThresholdConfig)
  }
}
```

## PredictionDriftDetectionConfig

The config for Prediction data drift detection.

Fields

`driftThresholds` `map (key: string, value: object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` ))`

Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws.

`attributionScoreDriftThresholds` `map (key: string, value: object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` ))`

Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows.

`defaultDriftThreshold` `object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` )`

Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features.

**JSON representation**

```
{
  "driftThresholds": {
    string: {
      object (ThresholdConfig)
    },
    ...
  },
  "attributionScoreDriftThresholds": {
    string: {
      object (ThresholdConfig)
    },
    ...
  },
  "defaultDriftThreshold": {
    object (ThresholdConfig)
  }
}
```

## ExplanationConfig

The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanationSpec populated.

Fields

`enableFeatureAttributes` `boolean`

If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Agent Platform will log the feature attributions from explain response and do the skew/drift detection for them.

`explanationBaseline` `object ( `[`ExplanationBaseline`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig#ExplanationBaseline)` )`

Predictions generated by the BatchPredictionJob using baseline dataset.

**JSON representation**

```
{
  "enableFeatureAttributes": boolean,
  "explanationBaseline": {
    object (ExplanationBaseline)
  }
}
```

## ExplanationBaseline

Output from [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob) for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

Fields

`predictionFormat` `enum ( `[`PredictionFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig#PredictionFormat)` )`

The storage format of the predictions generated BatchPrediction job.

`destination` `Union type`

The configuration specifying of BatchExplain job output. This can be used to generate the baseline of feature attribution scores. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcs` `object ( ``GcsDestination`` )`

Cloud Storage location for BatchExplain output.

`bigquery` `object ( `[`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQueryDestination)` )`

BigQuery location for BatchExplain output.

End of mutually exclusive fields.

**JSON representation**

```
{
  "predictionFormat": enum (PredictionFormat),

  // destination
  "gcs": {
    object (GcsDestination)
  },
  "bigquery": {
    object (BigQueryDestination)
  }
  // Union type
}
```

## PredictionFormat

The storage format of the predictions generated BatchPrediction job.

| Enums                           |                                 |
|---------------------------------|---------------------------------|
| `PREDICTION_FORMAT_UNSPECIFIED` | Should not be set.              |
| `JSONL`                         | Predictions are in JSONL files. |
| `BIGQUERY`                      | Predictions are in BigQuery.    |
