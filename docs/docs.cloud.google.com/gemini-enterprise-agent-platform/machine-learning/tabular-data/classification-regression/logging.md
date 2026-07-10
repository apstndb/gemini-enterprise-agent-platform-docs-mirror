---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging
title: View model architecture
description: Use Cloud Logging to view details about a Gemini Enterprise Agent Platform model.
data_source: docs.cloud.google.com
---

This page provides information about how to use Cloud Logging to view details about a Gemini Enterprise Agent Platform model. Using Logging, you see:

  - The hyperparameters of the final model as key-value pairs.
  - The hyperparameters and object values used during model training and tuning, as well as an objective value.

By default, logs are deleted after 30 days.

The following topics are covered:

1.  [Viewing training logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#training-logs) .
2.  [Log fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#log-fields) .

> **Note:** Model architecture logs are provided as part of the Cloud Logging service. For general information about Cloud Logging, see the [Cloud Logging](https://docs.cloud.google.com/logging/docs) documentation.

## Before you begin

Before you can view the hyperparameter logs for your model, you must [train it](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model) .

To perform this task, you must have the following [permissions](https://docs.cloud.google.com/iam/docs/overview#permissions) :

  - `logging.logServiceIndexes.list` on the project
  - `logging.logServices.list` on the project

## Viewing training logs

You can use the Google Cloud console to access the hyperparameter logs of the final model and the hyperparameter logs of the tuning trials.

1.  In the Google Cloud console, go to the Gemini Enterprise Agent Platform **Models** page.

2.  In the **Region** drop-down, select the region where your model is located.

3.  From the list of models, select your model.

4.  Select your model's version number.

5.  Open the **Version Details** tab.

6.  To see the hyperparameter log of the final model, go to the **Model hyperparameters** row and click **Model** .
    
    1.  There is just one log entry. Expand the payload as shown below. For details, see [Log fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#reading-logs) .
        
        ![Expanded Models logs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/images/model-logs-expanded.png)

7.  To see the hyperparameter log of the tuning trials, go to the **Model hyperparameters** row and click **Trials** .
    
    1.  There is one entry for each of the tuning trials. Expand the payload as shown below. For details, see [Log fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#reading-logs) .
        
        ![Expanded Trials logs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/images/trials-logs-expanded.png)

## Log fields

Activity logs are structured as described in the [LogEntry](https://docs.cloud.google.com/logging/docs/exported_logs#the_logentry_type) type documentation.

Gemini Enterprise Agent Platform model logs have, among other fields:

  - `labels` : The `log_type` field is set to `automl_tables` .
  - `jsonPayload` : The specific details of the log entry, provided in JSON object format. For details, see [Payload contents for the hyperparameter log of the final model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#final-payload) or [Payload contents for the hyperparameter log of a tuning trial](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#trial-payload) .
  - `timestamp` : The date and time when the model was created or the trial was run.

### Payload contents for the hyperparameter log of the final model

The `jsonPayload` field for the hyperparameter log of the final model contains a `modelParameters` field. This field contains one entry for each model that contributes to the final ensemble model. Each entry has a `hyperparameters` field, whose contents depend on the model type. For details, see [List of hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#hps) .

### Payload contents for the hyperparameter log of a tuning trial

The `jsonPayload` field for the hyperparameter log of a tuning trial contains the following fields:

| Field                    | Type | Description                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `modelStructure`         | JSON | A description of the Agent Platform model structure. This field contains a `modelParameters` field. The `modelParameters` field has a `hyperparameters` field, whose contents depend on the model type. For details, see [List of hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging#hps) . |
| `trainingObjectivePoint` | JSON | The optimization objective used for model training. This entry includes a timestamp and an objective value at the time the log entry was recorded.                                                                                                                                                                                                                                       |

### List of hyperparameters

The hyperparameter data provided in the logs differ for each type of model. The following sections describe the hyperparameters for each model type.

#### Gradient boosted decision tree models

  - Tree L1 regularization
  - Tree L2 regularization
  - Max tree depth
  - Model type: `GBDT`
  - Number of trees
  - Tree complexity

#### Feedforward neural network models

  - Dropout rate
  - Enable batchNorm ( `True` or `False` )
  - Enable embedding L1 ( `True` or `False` )
  - Enable embedding L2 ( `True` or `False` )
  - Enable L1 ( `True` or `False` )
  - Enable L2 ( `True` or `False` )
  - Enable layerNorm ( `True` or `False` )
  - Enable numerical embedding ( `True` or `False` )
  - Hidden layer size
  - Model type: `nn`
  - Normalize numerical column ( `True` or `False` )
  - Number of cross layers
  - Number of hidden layers
  - Skip connections type ( `dense` , `disable` , `concat` , or `slice_or_padding` )

## What's next

Once you're ready to make predictions with your classification or regression model, you have two options:

  - [Make online (real-time) predictions using your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions) .
  - [Get batch predictions directly from your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions) .

Additionally, you can:

  - [Evaluate your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model) .
  - [Review general information about Cloud Logging](https://docs.cloud.google.com/logging/docs) .
  - You can export your logs to BigQuery, Cloud Storage, or Pub/Sub. Read [Route logs to supported destinations](https://docs.cloud.google.com/logging/docs/export/configure_export_v2) in the Logging documentation to learn how to export activity logs.
