---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting-online-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting-online-predictions
title: Get online inferences for a forecast model
description: Project future values for a forecast model by using online inferences in Gemini Enterprise Agent Platform
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform provides two options for projecting future values using your trained forecast model: online inferences and batch inferences.

An online inference is a synchronous request. Use online inferences when you make requests in response to application input or in other situations where you require timely inference.

A batch inference request is an asynchronous request. Use batch inferences when you don't require an immediate response and want to process accumulated data by using a single request.

This page shows you how to project future values using online inferences. To learn how to project values using batch inferences, see [Get batch inferences for a forecast model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting-batch-predictions) .

You must deploy your model to an endpoint before you can use it for inferences. An endpoint is a set of physical resources.

You can request an explanation instead of an inference. The explanation's local feature importance values tell you how much each feature contributed to the inference result. For a conceptual overview, see [Feature attributions for forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-explanations) .

To learn about pricing for online inferences, see [Pricing for Tabular Workflows](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/pricing) .

## Before you begin

Before you can make an online inference request, first [train](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting-train) a model.

## Create or select an endpoint

Use the function [`aiplatform.Endpoint.create()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_create) to create an endpoint. If you already have an endpoint, use the function [`aiplatform.Endpoint()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint) to select it.

The following code provides an example:

    # Import required modules
    from google.cloud import aiplatform
    from google.cloud.aiplatform import models
    
    PROJECT_ID = "PROJECT_ID"
    REGION = "REGION"
    
    # Initialize the Vertex SDK for Python for your project.
    aiplatform.init(project=PROJECT_ID, location=REGION)
    endpoint = aiplatform.Endpoint.create(display_name='ENDPOINT_NAME')

Replace the following:

  - PROJECT\_ID : Your project ID.
  - REGION : The region where you use Gemini Enterprise Agent Platform.
  - ENDPOINT\_NAME : Display name for the endpoint.

## Select a trained model

Use the function [`aiplatform.Model()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model) to select a trained model:

    # Create reference to the model trained ahead of time.
    model_obj = models.Model("TRAINED_MODEL_PATH")

Replace the following:

  - TRAINED\_MODEL\_PATH : For example, `projects/ PROJECT_ID /locations/ REGION /models/[TRAINED_MODEL_ID]`

## Deploy the model to the endpoint

Use the function [`deploy()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_deploy) to deploy the model to the endpoint. The following code provides an example:

    deployed_model = endpoint.deploy(
        model_obj,
        machine_type='MACHINE_TYPE',
        traffic_percentage=100,
        min_replica_count='MIN_REPLICA_COUNT',
        max_replica_count='MAX_REPLICA_COUNT',
        sync=True,
        deployed_model_display_name='DEPLOYED_MODEL_NAME',
    )

Replace the following:

  - MACHINE\_TYPE : For example, `n1-standard-8` . [Learn more about machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. You can increase or decrease the node count as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes. This value must be greater than or equal to 1. If you don't set the `min_replica_count` variable, the value defaults to `1` .
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. You can increase or decrease the node count as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes. If you don't set the `max_replica_count` variable, the maximum number of nodes is set to the value of `min_replica_count` .
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.

Model deployment may take approximately ten minutes.

## Get online inferences

To get inferences, use the function [`predict()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_predict) and provide one or more input instances. The following code shows an example:

    predictions = endpoint.predict(instances=[{...}, {...}])

Each input instance is a Python dictionary with the same schema that the model was trained on. It must contain an *available at forecast* key-value pair that corresponds to the time column and an *unavailable at forecast* key-value pair that contains the historical values of the targeted inference column. Gemini Enterprise Agent Platform expects each input instance to belong to a single time series. The order of the key-value pairs in the instance is not important.

The input instance is subject to the following constraints:

  - The *available at forecast* key-value pairs must all have the same number of data points.
  - The *unavailable at forecast* key-value pairs must all have the same number of data points.
  - The *available at forecast* key-value pairs must have at least as many data points as the *unavailable at forecast* key-value pairs.

To learn more about the types of columns used in forecasting, see [Feature type and availability at forecast](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .

The following code demonstrates a set of two input instances. The `Category` column contains attribute data. The `Timestamp` column contains data that is available at forecast. Three points are *context* data and two points are *horizon* data. The `Sales` column contains data that is unavailable at forecast. All three points are *context* data. To learn how context and horizon are used in forecasting, see [Forecast horizon, context window, and forecast window](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) .

    instances=[
      {
        # Attribute
        "Category": "Electronics",
        # Available at forecast: three days of context, two days of horizon
        "Timestamp": ['2023-08-03', '2023-08-04', '2023-08-05', '2023-08-06', '2023-08-07'],
        # Unavailable at forecast: three days of context
        "Sales": [490.50, 325.25, 647.00],
      },
      {
        # Attribute
        "Category": "Food",
        # Available at forecast: three days of context, two days of horizon
        "Timestamp": ['2023-08-03', '2023-08-04', '2023-08-05', '2023-08-06', '2023-08-07'],
        # Unavailable at forecast: three days of context
        "Sales": [190.50, 395.25, 47.00],
      }
    ])

For each instance, Gemini Enterprise Agent Platform responds with two inferences for `Sales` , corresponding with the two *horizon* timestamps ("2023-08-06" and "2023-08-07").

For optimal performance, the number of *context* data points and the number of *horizon* data points in each input instance must match the context and horizon lengths that the model was trained with. If there is a mismatch, Gemini Enterprise Agent Platform pads or truncates the instance to match the model's size.

If the number of *context* data points in your input instance is less than or greater than the number of *context* data points used for model training, ensure that this number of points is consistent across all of the *available at forecasting* key-value pairs and all of the *unavailable at forecasting* key-value pairs.

For example, consider a model that was trained with four days of *context* data and two days of *horizon* data. You can make an inference request with just three days of *context* data. In this case, the *unavailable at forecast* key-value pairs contain three values. The *available at forecast* key-value pairs must contain five values.

## Output of online inference

Gemini Enterprise Agent Platform provides online inference output in the `value` field:

    {
      'value': [...]
    }

The length of the inference response depends on the horizon used in model training and on the horizon of the input instance. The length of the inference response is the smallest of these two values.

Consider the following examples:

  - You train a model with `context` = `15` and `horizon` = `50` . Your input instance has `context` = `15` and `horizon` = `20` . The inference response has a length of `20` .
  - You train a model with `context` = `15` and `horizon` = `50` . Your input instance has `context` = `15` and `horizon` = `100` . The inference response has a length of `50` .

### Online inferences output for TFT models

For models trained with [Temporal Fusion Transformer (TFT)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#training-methods) , Gemini Enterprise Agent Platform provides TFT interpretability `tft_feature_importance` in addition to inferences in the `value` field:

    {
      "tft_feature_importance": {
        "attribute_weights": [...],
        "attribute_columns": [...],
        "context_columns": [...],
        "context_weights": [...],
        "horizon_weights": [...],
        "horizon_columns": [...]
      },
      "value": [...]
    }

  - `attribute_columns` : Forecasting features which are [time-invariant](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .
  - `attribute_weights` : The weights associated with each of the `attribute_columns` .
  - `context_columns` : Forecasting features whose [context window](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) values serve as inputs to the TFT Long Short-Term Memory (LSTM) Encoder.
  - `context_weights` : The feature importance weights associated with each of the `context_columns` for the predicted instance.
  - `horizon_columns` : Forecasting features whose [forecast horizon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) values serve as inputs to the TFT Long Short-Term Memory (LSTM) Decoder.
  - `horizon_weights` : The feature importance weights associated with each of the `horizon_columns` for the predicted instance.

### Online inference output for models optimized for quantile loss

For models optimized for [quantile loss](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#optimization-objectives) , Gemini Enterprise Agent Platform provides the following online inference output:

    {
      "value": [...],
      "quantile_values": [...],
      "quantile_predictions": [...]
    }

  - `value` : If your set of quantiles includes the median, `value` is the inference value at the median. Otherwise, `value` is the inference value at the lowest quantile in the set. For example, if your set of quantiles is `[0.1, 0.5, 0.9]` , `value` is the inference for quantile `0.5` . If your set of quantiles is `[0.1, 0.9]` , `value` is the inference for quantile `0.1` .
  - `quantile_values` : The values of the quantiles, which are set during model training.
  - `quantile_predictions` : The inference values associated with quantile\_values.

Consider, for example, a model in which the target column is the sales value. Quantile values are defined as `[0.1, 0.5, 0.9]` . Gemini Enterprise Agent Platform returns the following quantile inferences: `[4484, 5615, 6853]` . Here, the set of quantiles includes the median, so `value` is the inference for quantile `0.5` ( `5615` ). You can interpret the quantile inferences as follows:

  - `P(sales value < 4484)` = 10%
  - `P(sales value < 5615)` = 50%
  - `P(sales value < 6853)` = 90%

### Online inference output for models with probabilistic inference

If your model uses probabilistic inference, the `value` field contains the minimizer of the optimization objective. For example, if your optimization objective is `minimize-rmse` , the `value` field contains the mean value. If it is `minimize-mae` , the `value` field contains the median value.

If your model uses probabilistic inference with quantiles, Gemini Enterprise Agent Platform provides quantile values and inferences in addition to the minimizer of the optimization objective. Quantile values are set during model training. Quantile inferences are the inference values associated with the quantile values.

## Get online explanations

To get explanations, use the function [`explain()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_explain) and provide one or more input instances. The following code shows an example:

    explanations = endpoint.explain(instances=[{...}, {...}])

The format of the input instances is the same for online inferences and online explanations. To learn more, see [Get online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting-online-predictions#get-inferences) .

For a conceptual overview of feature attributions, see [Feature attributions for forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-explanations) .

## Output of online explanation

The following code demonstrates how you can output the explanation results:

    # Import required modules
    import json
    from google.protobuf import json_format
    
    def explanation_to_dict(explanation):
      """Converts the explanation proto to a human-friendly json."""
      return json.loads(json_format.MessageToJson(explanation._pb))
    
    for response in explanations.explanations:
      print(explanation_to_dict(response))

The explanation results have the following format:

    {
      "attributions": [
        {
          "baselineOutputValue": 1.4194682836532593,
          "instanceOutputValue": 2.152980089187622,
          "featureAttributions": {
            ...
            "store_id": [
              0.007947325706481934
            ],
            ...
            "dept_id": [
              5.960464477539062e-08
            ],
            "item_id": [
              0.1100526452064514
            ],
            "date": [
              0.8525647521018982
            ],
            ...
            "sales": [
              0.0
            ]
          },
          "outputIndex": [
            2
          ],
          "approximationError": 0.01433318599207033,
          "outputName": "value"
        },
        ...
      ]
    }

The number of `attributions` elements depends on the horizon used in model training and on the horizon of the input instance. The number of elements is the smallest of these two values.

The `featureAttributions` field in an `attributions` element contains one value for each of the columns in the input dataset. Gemini Enterprise Agent Platform generates explanations for all types of features: *attribute* , *available at forecast* , and *unavailable at forecast* . To learn more about the fields of an `attributions` element, see [Attribution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#attribution) .

## Delete the endpoint

Use the functions [`undeploy_all()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_undeploy_all) and [`delete()`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_delete) to delete your endpoint. The following code shows an example:

    endpoint.undeploy_all()
    endpoint.delete()

## What's next

  - Learn about [pricing for online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/pricing) .
