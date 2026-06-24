---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/evaluate-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/evaluate-model
title: Evaluate AutoML forecast models
description: Evaluate your AutoML forecast models using model evaluation metrics.
data_source: docs.cloud.google.com
---

This page shows you how to evaluate your AutoML forecast models using model evaluation metrics. These metrics provide quantitative measurements of how your model performed on the [test set](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/data-splits) . How you interpret and use these metrics depends on your business need and the problem your model is trained to solve. For example, you might have a lower tolerance for false positives than for false negatives or the other way around. These kinds of questions affect which metrics you focus on.

## Before you begin

Before you can evaluate a model, you must [train it](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model) and wait for the training to complete.

Use the console or the API to check the status of your training job.

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Training** page.

2.  If the status of your training job is "Training", continue to wait for the training job to finish. If the status of your training job is "Finished", you are ready to begin model evaluation.

### API

Select a tab that corresponds to your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where your model is stored.
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - TRAINING\_PIPELINE\_ID : ID of the training pipeline.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines/TRAINING_PIPELINE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines/TRAINING_PIPELINE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines/TRAINING_PIPELINE_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

``` 
  If the model is still being trained:

  {
    "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAINING_PIPELINE_ID",
    ...
    "modelToUpload": {
      "displayName": "MODEL_DISPLAY_NAME"
    },
    "state": "PIPELINE_STATE_RUNNING",
    ...
  }

  If the model training is complete:

  {
    "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAINING_PIPELINE_ID",
    ...
    "modelToUpload": {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/models/MODEL_ID",
      "displayName": "MODEL_DISPLAY_NAME",
      "versionID": "1"
    },
    "state": "PIPELINE_STATE_SUCCEEDED",
    ...
  }
```

## Get evaluation metrics

You can get an aggregate set of [evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/evaluate-model#metrics) for your model. The following content describes how to get these metrics using the Google Cloud console or API.

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  In the **Region** drop-down, select the region where your model is located.

3.  From the list of models, select your model.

4.  Select your model's version number.

5.  In the **Evaluate** tab, you can view your model's aggregate evaluation metrics.

### API

To view aggregate model evaluation metrics, use the [`projects.locations.models.evaluations.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations) method.

Select a tab that corresponds to your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where your model is stored.
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - MODEL\_ID : The ID of the model resource . The MODEL\_ID appears in the training pipeline after model training is successfully completed. Refer to the [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/evaluate-model#before-you-begin) section to get the MODEL\_ID .

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "modelEvaluations": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID",
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/forecasting_metrics_1.0.0.yaml",
          "metrics": {
            "rootMeanSquaredError": 719.0045,
            "meanAbsoluteError": 487.0792,
            "meanAbsolutePercentageError": "Infinity",
            "rSquared": 0.8837288,
            "rootMeanSquaredLogError": "NaN",
            "quantileMetrics": [
              {
                "quantile": 0.2,
                "scaledPinballLoss": 157.34422,
                "observedQuantile": 0.15918367346938775
              },
              {
                "quantile": 0.5,
                "scaledPinballLoss": 243.5396,
                "observedQuantile": 0.45551020408163267
              },
              {
                "quantile": 0.8,
                "scaledPinballLoss": 175.39418,
                "observedQuantile": 0.81183673469387752
              }
            ]
          },
          "createTime": "2021-04-13T01:00:54.091953Z"
        }
      ]
    }

## Model evaluation metrics

A schema file determines which evaluation metrics Agent Platform provides for each objective.

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

The evaluation metrics for forecasting models are:

  - **MAE** : The mean absolute error (MAE) is the average absolute difference between the target values and the predicted values. This metric ranges from zero to infinity; a lower value indicates a higher quality model.
  - **MAPE** : Mean absolute percentage error (MAPE) is the average absolute percentage difference between the labels and the predicted values. This metric ranges between zero and infinity; a lower value indicates a higher quality model.  
    MAPE is not shown if the target column contains any 0 values. In this case, MAPE is undefined.
  - **RMSE** : The root-mean-squared error is the square root of the average squared difference between the target and predicted values. RMSE is more sensitive to outliers than MAE,so if you're concerned about large errors, then RMSE can be a more useful metric to evaluate. Similar to MAE, a smaller value indicates a higher quality model (0 represents a perfect predictor).
  - **RMSLE** : The root-mean-squared logarithmic error metric is similar to RMSE, except that it uses the natural logarithm of the predicted and actual values plus 1. RMSLE penalizes under-inference more heavily than over-inference. It can also be a good metric when you don't want to penalize differences for large inference values more heavily than for small inference values. This metric ranges from zero to infinity; a lower value indicates a higher quality model. The RMSLE evaluation metric is returned only if all label and predicted values are non-negative.
  - **r^2** : r squared (r^2) is the square of the Pearson correlation coefficient between the labels and predicted values. This metric ranges between zero and one. A higher value indicates a closer fit to the regression line.
  - **Quantile** : The percent quantile, which indicates the probability that an observed value will be below the predicted value. For example, at the 0.2 quantile, the observed values are expected to be lower than the predicted values 20% of the time. Agent Platform provides this metric if you specify `minimize-quantile-loss` for the optimization objective.
  - **Observed quantile** : Shows the percentage of true values that were less than the predicted value for a given quantile. Agent Platform provides this metric if you specify `minimize-quantile-loss` for the optimization objective.
  - **Scaled pinball loss** : The scaled pinball loss at a particular quantile. A lower value indicates a higher quality model at the given quantile. Agent Platform provides this metric if you specify `minimize-quantile-loss` for the optimization objective.
  - **Model feature attributions** : Agent Platform shows you how much each feature impacts a model. The values are provided as a percentage for each feature: the higher the percentage, the more impact the feature had on model training. Review this information to ensure that all of the most important features make sense for your data and business problem. To learn more, see [Feature attributions for forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-explanations) .

## What's next

  - [Get inferences from your forecast model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/get-predictions) .
