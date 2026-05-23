---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-explanations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-explanations
title: Feature attributions for forecasting
description: Learn about feature attribution methods for forecasting in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

## Introduction

This page provides a brief conceptual overview of the feature attribution methods available with Agent Platform.

Global feature importance (model feature attributions) shows how each feature impacts a model. The values are a percentage for each feature: the higher the percentage, the more impact the feature had on model training. For example, after reviewing the global feature importance for your model, you may come to the following conclusion: "The model sees that the previous month's sales are usually the strongest predictor of the next month's sales. Factors such as customer count and promotions are important, but they are less important than the sales figures."

To view the global feature importance for your model, examine the [evaluation metrics](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/evaluate-model) .

Local feature attributions for time series models indicate how much each feature in a model contributed to an inference. They measure a feature's contribution to an inference relative to an input baseline. For numerical features such as sales, the baseline input is the median sales. For categorical features such as the product name, the baseline input is the most common product name. The sum of all attributions is **not** the inference. The sum indicates how much the inference differs from the baseline *inference* (that is, all inputs are baseline inputs).

Feature attributions are determined based on forecasts made for *counterfactuals* . An example forecast is as follows: *What is the forecast if the advertisement value of `TRUE` on `2020-11-21` was replaced with `FALSE` , the most common value?* The required number of counterfactuals scales with the number of columns and the number of paths (service generated). The resulting number of inferences may be orders of magnitude larger than in a normal inference task and the expected run time scales accordingly.

You can use [Forecasting with AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) or [Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting) to generate and query local feature attributions. Forecasting with AutoML supports [batch inferences](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/get-predictions) only. Tabular Workflow for Forecasting supports both [batch inferences](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting-batch-predictions) and [online inferences](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting-online-predictions) .

## Advantages

If you inspect specific instances, and also aggregate feature attributions across your training dataset, you can get deeper insight into how your model works. Consider the following advantages:

  - **Debugging models** : Feature attributions can help detect issues in the data that standard model evaluation techniques would usually miss.

  - **Optimizing models** : You can identify and remove features that are less important, which can result in more efficient models.

## Conceptual limitations

Consider the following limitations of feature attributions:

  - Feature attributions, including local feature importance for AutoML, are specific to individual inferences. Inspecting the feature attributions for an individual inference may provide good insight, but the insight may not be generalizable to the entire class for that individual instance, or the entire model.
    
    To get more generalizable insight for AutoML models, refer to the model feature importance. To get more generalizable insight for other models, aggregate attributions over subsets over your dataset, or the entire dataset.

  - Each attribution only shows how much the feature affected the inference for that particular example. A single attribution might not reflect the overall behavior of the model. To understand approximate model behavior on an entire dataset, aggregate attributions over the entire dataset.

  - Although feature attributions can help with model debugging, they don't always indicate clearly whether an issue arises from the model or from the data that the model is trained on. Use your best judgment, and diagnose common data issues to narrow the space of potential causes.

  - The attributions depend entirely on the model and data used to train the model. They can only reveal the patterns the model found in the data, and can't detect any fundamental relationships in the data. The presence or absence of a strong attribution to a certain feature doesn't mean there is or is not a relationship between that feature and the target. The attribution merely shows that the model is or is not using the feature in its inferences.

  - Attributions alone cannot tell if your model is fair, unbiased, or of sound quality. Carefully evaluate your training data and evaluation metrics in addition to the attributions.

For more information about limitations, see the \[AI Explanations Whitepaper\].

## Improving feature attributions

The following factors have the highest impact on feature attributions:

  - The attribution methods approximate the Shapley value. You can increase the precision of the approximation by increasing the number of paths for the sampled Shapley method. As a result, the attributions could change dramatically.
  - The attributions only express how much the feature affected the change in inference value, relative to the baseline value. Be sure to choose a meaningful baseline, relevant to the question you're asking of the model. Attribution values and their interpretation might change significantly as you switch baselines.

View the path count and the baselines in the Explanation Parameters and Metadata.

## View explanation metadata and parameters

The Explanation Parameters and Metadata contain the following:

  - **static\_value** : The *baselines* used to generate explanations.
  - **pathCount** : The number of *paths* , a factor in the amount of time it takes to generate feature attributions.
  - **historical\_values** , **prediction\_values** : Columns available at forecast.
  - **historical\_values** : Columns unavailable at forecast.

The model can be viewed using the Agent Platform REST API and includes the explanation spec.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where your model is stored
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - MODEL\_ID : The ID of the model resource

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID" | Select-Object -Expand Content

You should see output similar to the following for a trained AutoML model.

#### Response

    {
      "name": "projects/PROJECT/locations/LOCATION/models/MODEL_ID",
      "displayName": "MODEL_DISPLAYNAME",
      ...
      "explanationSpec": {
        "parameters": {
          "sampledShapleyAttribution": {
            "pathCount": 6
          },
          "topK": -1
        },
        "metadata": {
          "inputs": {
            "prediction_values": {
              "inputBaselines": [
                [
                  {
                    "date": "2016-11-17",
                    "advertisement": "0",
                    "holiday": "0"
                  }
                ]
              ]
            },
            "static_value": {
              "inputBaselines": [
                {
                  "product": "product_0",
                  "store": "store_0"
                }
              ]
            },
            "historical_values": {
              "inputBaselines": [
                [
                  {
                    "date": "2016-11-17",
                    "advertisement": "0",
                    "holiday": "0",
                    "sales": 371.03544292464909
                  }
                ]
              ]
            }
          },
          "outputs": {
            "value": {}
          },
          "featureAttributionsSchemaUri": "..."
        }
      }
    }

## Algorithm

Gemini Enterprise Agent Platform provides feature attributions using *Shapley Values* , a cooperative game theory algorithm that assigns credit to each player in a game for a particular outcome. Applied to machine learning models, this means that each model feature is treated as a "player" in the game and credit is assigned in proportion to the outcome of a particular inference. For structured data models, Agent Platform uses a sampling approximation of exact Shapley Values called *Sampled Shapley* .

For in-depth information about how the sampled Shapley method works, read the paper \[Bounding the Estimation Error of Sampling-based Shapley Value Approximation\]\[sampled-shapley-paper\].

## What's next

The following resources provide further useful educational material:

  - [Interpretable Machine Learning: Shapley values](https://christophm.github.io/interpretable-ml-book/shapley.html)
  - [Introduction to Shapley values](https://www.kaggle.com/dansbecker/shap-values#Introduction)
