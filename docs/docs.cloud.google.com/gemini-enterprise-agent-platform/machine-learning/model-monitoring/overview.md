---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview
title: Introduction to Model Monitoring
description: Run monitoring jobs as needed or on a regular schedule to track the quality of your tabular models.
data_source: docs.cloud.google.com
---

This page provides an overview of Model Monitoring.

## Monitoring overview

Model Monitoring lets you run monitoring jobs as needed or on a regular schedule to track the quality of your tabular models. If you've set alerts, Model Monitoring informs you when metrics surpass a specified threshold.

For example, assume that you have a model that predicts customer lifetime value. As customer habits change, the factors that predict customer spending also change. Consequently, the features and feature values that you used to train your model before might not be relevant for making inferences today. This deviation in the data is known as drift.

Model Monitoring can track and alert you when deviations exceed a specified threshold. You can then re-evaluate or retrain your model to ensure the model is behaving as intended.

For example, Model Monitoring can provide visualizations like in the following figure, which overlays two graphs from two datasets. This visualization lets you quickly compare and see deviations between the two sets of data.

![An example of a numerical distribution of a baseline and tartget datasets.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/drift-sample.png)

## Model Monitoring versions

Model Monitoring provides two offerings: v2 and v1.

Model Monitoring v2 is in [Preview](https://docs.cloud.google.com/products#product-launch-stages) and is the latest offering that associates all monitoring tasks with a model version. In contrast, Model Monitoring v1 is Generally Available and is configured on Agent Platform endpoints.

If you need production-level support and want to monitor a model that's deployed on an Agent Platform endpoint, use Model Monitoring v1. For all other use cases, use Model Monitoring v2, which provides all the capabilities of Model Monitoring v1 and more. For more information, see the overview for each version:

  - [Model Monitoring v2 overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview#v2)
  - [Model Monitoring v1 overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview#v1)

For existing Model Monitoring v1 users, Model Monitoring v1 is maintained as is. You aren't required to migrate to Model Monitoring v2. If you want to migrate, you can use both versions concurrently until you have fully migrated to Model Monitoring v2 to help you avoid monitoring gaps during your transition.

## Model Monitoring v2 overview

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Model Monitoring v2 lets you track metrics over time after you configure a model monitor and run monitoring jobs. You can run on-demand monitoring jobs or set up scheduled runs. By using scheduled runs, Model Monitoring automatically runs monitoring jobs based on a schedule that you define.

### Monitoring objectives

The metrics and thresholds you monitor are mapped to *monitoring objectives* . For each model version, you can specify one or more monitoring objectives. The following table details each objective:

Objective

Description

Feature data type

Supported metrics

Input feature data drift

Measures the distribution of input feature values compared to a baseline data distribution.

**Categorical** : boolean, string, categorical

  - L-Infinity
  - Jensen Shannon Divergence

**Numerical** : float, integer

Jensen Shannon Divergence

Output inference data drift

Measures the model's inferences data distribution compared to a baseline data distribution.

**Categorical** : boolean, string, categorical

  - L-Infinity
  - Jensen Shannon Divergence

**Numerical** : float, integer

Jensen Shannon Divergence

Feature attribution

Measures the change in contribution of features to a model's inference compared to a baseline. For example, you can track if a highly important feature suddenly drops in importance.

All data types

SHAP value (SHapley Additive exPlanations)

#### Input feature and output inference drift

After a model is deployed in production, the input data can deviate from the data that was used to train the model or the distribution of feature data in production could shift significantly over time. Model Monitoring v2 can monitor changes in the distribution of production data compared to the training data or to track the evolution of production data distribution over time.

Similarly, for inference data, Model Monitoring v2 can monitor changes in the distribution of predicted outcomes compared to the training data or production data distribution over time.

#### Feature attribution

Feature attributions indicate how much each feature in your model contributed to the inferences for each given instance. Attribution scores are proportional to the contribution of the feature to a model's inference. They are typically signed, indicating whether a feature helps push the inference up or down. Attributions across all features must add up to the model's inference score.

By monitoring feature attributions, Model Monitoring v2 tracks changes in a feature's contributions to a model's inferences over time. A change in a key feature's attribution score often signals that the feature has changed in a way that can impact the accuracy of the model's inferences.

For more information about feature attributions and metrics, see [Feature-based explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/explainable-ai/overview#feature-attribution-methods) and [Sampled Shapley method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/explainable-ai/overview#sampled-shapley) .

### How to set up Model Monitoring v2

You must first register your models in Model Registry. If you are serving models outside of Agent Platform, you don't need to upload the model artifact. You then create a model monitor, which you associate with a model version, and define your model schema. For some models, such as AutoML models, the schema is provided for you.

In the model monitor, you can optionally specify default configurations such as monitoring objectives, a training dataset, monitoring output location, and notification settings. For more information, see [Set up model monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/set-up-model-monitoring) .

After you create a model monitor, you can run a monitoring job on demand or schedule regular jobs for continuous monitoring. When you run a job, Model Monitoring uses the default configuration set in the model monitor unless you provide a different monitoring configuration. For example, if you provide different monitoring objectives or a different comparison dataset, Model Monitoring uses the job's configurations instead of the default configuration from the model monitor. For more information, see [Run a monitoring job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/run-monitoring-job) .

### Pricing

You are not charged for Model Monitoring v2 during the [Preview](https://docs.cloud.google.com/products#product-launch-stages) . You are still charged for the usage of other services, such as Cloud Storage, BigQuery, Agent Platform batch inferences, Agent Platform Explainable AI, and Cloud Logging.

### Notebook tutorials

The following tutorials demonstrate how to use the Agent Platform SDK for Python to set up Model Monitoring v2 for your model.

#### Model Monitoring v2: Custom model batch inference job

> To learn more, run the "Model Monitoring for Custom Model Batch Prediction Job" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_batch_prediction_job.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring_v2%2Fmodel_monitoring_for_custom_model_batch_prediction_job.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring_v2%2Fmodel_monitoring_for_custom_model_batch_prediction_job.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_batch_prediction_job.ipynb)

#### Model Monitoring v2: Custom model online inference

> To learn more, run the "Model Monitoring for custom model online prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring_v2%2Fmodel_monitoring_for_custom_model_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring_v2%2Fmodel_monitoring_for_custom_model_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_online_prediction.ipynb)

#### Model Monitoring v2: Models outside Gemini Enterprise Agent Platform

> To learn more, run the "Model Monitoring for Models Outside " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_model_outside_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring_v2%2Fmodel_monitoring_for_model_outside_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring_v2%2Fmodel_monitoring_for_model_outside_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_model_outside_vertex.ipynb)

## Model Monitoring v1 overview

To help you maintain a model's performance, Model Monitoring v1 monitors the model's inference input data for feature *skew* and *drift* :

  - *Training-serving skew* occurs when the feature data distribution in production deviates from the feature data distribution used to train the model. If the original training data is available, you can enable skew detection to monitor your models for training-serving skew.

  - *Inference drift* occurs when feature data distribution in production changes significantly over time. If the original training data isn't available, you can enable drift detection to monitor the input data for changes over time.

You can enable both skew and drift detection.

Model Monitoring v1 supports feature skew and drift detection for *categorical* and *numerical* features:

  - *Categorical* features are data limited by number of possible values, typically grouped by qualitative properties. For example, categories such as product type, country, or customer type.

  - *Numerical* features are data that can be any numeric value. For example, weight and height.

Once the skew or drift for a model's feature exceeds an alerting threshold that you set, Model Monitoring v1 sends you an email alert. You can also view the distributions for each feature over time to evaluate whether you need to retrain your model.

### Calculate drift

To detect drift for v1, Model Monitoring uses [TensorFlow Data Validation (TFDV)](https://github.com/tensorflow/data-validation/blob/master/g3doc/anomalies.md) to calculate the distributions and *distance scores* .

1.  Calculate the *baseline* statistical distribution:
    
      - For skew detection, the baseline is the statistical distribution of the feature's values in the training data.
    
      - For drift detection, the baseline is the statistical distribution of the feature's values seen in production in the past.
    
    The distributions for categorical and numerical features are calculated as follows:
    
      - For categorical features, the computed distribution is the number or percentage of instances of each possible value of the feature.
    
      - For numerical features, Model Monitoring divides the range of possible feature values into equal intervals and computes the number or percentage of feature values that falls in each interval.
    
    The baseline is calculated when you [create a Model Monitoring job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/using-model-monitoring) , and is only recalculated if you update the training dataset for the job.

2.  Calculate the statistical distribution of the latest feature values seen in production.

3.  Compare the distribution of the latest feature values in production against the baseline distribution by calculating a *distance score* :
    
      - For categorical features, the distance score is calculated using the [L-infinity distance](https://en.wikipedia.org/wiki/Chebyshev_distance) .
    
      - For numerical features, the distance score is calculated using the [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen%E2%80%93Shannon_divergence) .

4.  When the distance score between two statistical distributions exceeds the threshold you specify, Model Monitoringidentifies the anomaly as skew or drift.

The following example shows skew or drift between the baseline and latest distributions of a categorical feature:

### Baseline distribution

![An example feature distribution of baseline dataset.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/categorical_baseline_stats.png)

### Latest distribution

![An example feature distribution of latest dataset.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/categorical_current_stats.png)

The following example shows skew or drift between the baseline and latest distributions of a numerical feature:

### Baseline distribution

![An example feature distribution of baseline dataset.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/example_histogram.png)

### Latest distribution

![An example feature distribution of latest dataset.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/current_dataset_histogram.png)

### Considerations when using Model Monitoring

  - For cost efficiency, you can set a *inference request sampling rate* to monitor a subset of the production inputs to a model.

  - You can set a frequency at which a deployed model's recently logged inputs are monitored for skew or drift. Monitoring frequency determines the timespan, or monitoring window size, of logged data that is analyzed in each monitoring run.

  - You can specify alerting thresholds for each feature you want to monitor. An alert is logged when the statistical distance between the input feature distribution and its corresponding baseline exceeds the specified threshold. By default, every categorical and numerical feature is monitored, with threshold values of 0.3.

  - An online inference endpoint can host multiple models. When you enable skew or drift detection on an endpoint, the following configuration parameters are shared across all models hosted in that endpoint:
    
      - Type of detection
      - Monitoring frequency
      - Fraction of input requests monitored
    
    For the other [configuration parameters](https://docs.cloud.google.com/sdk/gcloud/reference/ai/model-monitoring-jobs/create) , you can set different values for each model.

## What's next

  - [Get started with Model Monitoring v2](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/set-up-model-monitoring)
  - [Provide schema to Model Monitoring v1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/schemas)
