---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective
title: TabularObjective
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Tabular monitoring objective.

Fields

`featureDriftSpec` `object ( `[`DataDriftSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#DataDriftSpec)` )`

Input feature distribution drift monitoring spec.

`predictionOutputDriftSpec` `object ( `[`DataDriftSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#DataDriftSpec)` )`

Prediction output distribution drift monitoring spec.

`featureAttributionSpec` `object ( `[`FeatureAttributionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#FeatureAttributionSpec)` )`

feature attribution monitoring spec.

**JSON representation**

```
{
  "featureDriftSpec": {
    object (DataDriftSpec)
  },
  "predictionOutputDriftSpec": {
    object (DataDriftSpec)
  },
  "featureAttributionSpec": {
    object (FeatureAttributionSpec)
  }
}
```

## DataDriftSpec

data drift monitoring spec. data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.

Fields

`features[]` `string`

feature names / Prediction output names interested in monitoring. These should be a subset of the input feature names or prediction output names specified in the monitoring schema. If the field is not specified all features / prediction outputs outlied in the monitoring schema will be used.

`categoricalMetricType` `string`

Supported metrics type: \* l_infinity \* jensen_shannon_divergence

`numericMetricType` `string`

Supported metrics type: \* jensen_shannon_divergence

`defaultCategoricalAlertCondition` `object ( `[`ModelMonitoringAlertCondition`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#ModelMonitoringAlertCondition)` )`

Default alert condition for all the categorical features.

`defaultNumericAlertCondition` `object ( `[`ModelMonitoringAlertCondition`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#ModelMonitoringAlertCondition)` )`

Default alert condition for all the numeric features.

`featureAlertConditions` `map (key: string, value: object ( `[`ModelMonitoringAlertCondition`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#ModelMonitoringAlertCondition)` ))`

Per feature alert condition will override default alert condition.

**JSON representation**

```
{
  "features": [
    string
  ],
  "categoricalMetricType": string,
  "numericMetricType": string,
  "defaultCategoricalAlertCondition": {
    object (ModelMonitoringAlertCondition)
  },
  "defaultNumericAlertCondition": {
    object (ModelMonitoringAlertCondition)
  },
  "featureAlertConditions": {
    string: {
      object (ModelMonitoringAlertCondition)
    },
    ...
  }
}
```

## ModelMonitoringAlertCondition

Monitoring alert triggered condition.

Fields

`condition` `Union type`

Alert triggered condition. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`threshold` `number`

A condition that compares a stats value against a threshold. Alert will be triggered if value above the threshold.

End of mutually exclusive fields.

**JSON representation**

```
{

  // condition
  "threshold": number
  // Union type
}
```

## FeatureAttributionSpec

feature attribution monitoring spec.

Fields

`features[]` `string`

feature names interested in monitoring. These should be a subset of the input feature names specified in the monitoring schema. If the field is not specified all features outlied in the monitoring schema will be used.

`defaultAlertCondition` `object ( `[`ModelMonitoringAlertCondition`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#ModelMonitoringAlertCondition)` )`

Default alert condition for all the features.

`featureAlertConditions` `map (key: string, value: object ( `[`ModelMonitoringAlertCondition`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective#ModelMonitoringAlertCondition)` ))`

Per feature alert condition will override default alert condition.

`batchExplanationDedicatedResources` `object ( `[`BatchDedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources)` )`

The config of resources used by the Model Monitoring during the batch explanation for non-AutoML models. If not set, `n1-standard-2` machine type will be used by default.

**JSON representation**

```
{
  "features": [
    string
  ],
  "defaultAlertCondition": {
    object (ModelMonitoringAlertCondition)
  },
  "featureAlertConditions": {
    string: {
      object (ModelMonitoringAlertCondition)
    },
    ...
  },
  "batchExplanationDedicatedResources": {
    object (BatchDedicatedResources)
  }
}
```
