---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction
title: Model evaluation in Agent Platform
description: Learn about model evaluation in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Note:** Agent Platform provides model evaluation metrics for both predictive AI and generative AI models. This page provides an overview of the evaluation service for predictive AI models. To evaluate a generative AI model, see [Generative AI evaluation service overview](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/evaluation-overview) .

The inference AI evaluation service lets you evaluate model performance across specific use cases. You might also refer to evaluation as observability into a model's performance. The model evaluation provided by Agent Platform can fit in the typical machine learning workflow in several ways:

  - After you train your model, review model evaluation metrics before you deploy your model. Compare evaluation metrics across multiple models to help you decide which model to deploy.

  - After your model is deployed to production, periodically evaluate your model with new incoming data. If the evaluation metrics show that your model performance is degrading, consider re-training your model. This process is called *continuous evaluation* .

How you interpret and use those metrics depends on your business need and the problem your model is trained to solve. For example, you might have a lower tolerance for false positives than for false negatives, or the other way around. These kinds of questions affect which metrics you would focus on as you iterate on your model.

Some key metrics provided by the predictive AI model evaluation service include the following:

  - [Precision](https://developers.google.com/machine-learning/glossary#precision)
  - [Recall](https://developers.google.com/machine-learning/glossary#recall)
  - [AuPRC](https://developers.google.com/machine-learning/glossary#pr-auc-area-under-the-pr-curve)
  - [Confusion matrix](https://developers.google.com/machine-learning/glossary#confusion-matrix)

> **Note:** The model evaluation service described on this page is separate from the [evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/evaluating-automl-models#evaluation_metrics_returned_by) that are automatically generated during the AutoML training process.

## Features

To evaluate a model with Agent Platform, you need a trained model, a batch inference output, and a ground truth dataset. The following is a typical model evaluation workflow using Agent Platform:

1.  Train a model. You can do this in Gemini Enterprise Agent Platform using AutoML or custom training.

2.  Run a batch inference job on the model to generate inference results.

3.  Prepare the *ground truth* data, which is the "correctly labeled" data as determined by humans. The ground truth is usually the test dataset you used during the model training process.

4.  Run an evaluation job on the model, which evaluates the accuracy of the batch inference results compared to the ground truth data.

5.  Analyze the metrics that result from the evaluation job.

6.  Iterate on your model to see if you can improve your model's accuracy. You can run multiple evaluation jobs, and compare the results of multiple jobs across models or model versions.

You can run model evaluation in Agent Platform in several ways:

  - Create evaluations through the Gemini Enterprise Agent Platform Model Registry in the Google Cloud console.

  - Use model evaluations from Agent Platform as a [pipeline component](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component) with Gemini Enterprise Agent Platform Pipelines. You can create pipeline runs and templates that include model evaluations as a part of your automated MLOps workflow.
    
    You can run the [model evaluation component by itself](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component#without-batch) , or with other pipeline components such as the [batch inference component](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component) .

Agent Platform supports evaluation of the following model types:

### Image

### Classification

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

  - **AuPRC** : The [area under the precision-recall (PR) curve](https://developers.google.com/machine-learning/glossary#pr-auc-area-under-the-pr-curve) , also referred to as average precision. This value ranges from zero to one, where a higher value indicates a higher-quality model.
  - **Log loss** : The cross-entropy between the model inferences and the target values. This ranges from zero to infinity, where a lower value indicates a higher-quality model.
  - **Confidence threshold** : A confidence score that determines which inferences to return. A model returns inferences that are at this value or higher. A higher confidence threshold increases precision but lowers recall. Agent Platform returns confidence metrics at different threshold values to show how the threshold affects [precision](https://developers.google.com/machine-learning/glossary#precision) and [recall](https://developers.google.com/machine-learning/glossary#recall) .
  - **Recall** : The fraction of inferences with this class that the model correctly predicted. Also called *true positive rate* .
  - **Precision** : The fraction of classification inferences produced by the model that were correct.
  - **Confusion matrix** : A [confusion matrix](https://developers.google.com/machine-learning/glossary#confusion-matrix) shows how often a model correctly predicted a result. For incorrectly predicted results, the matrix shows what the model predicted instead. The confusion matrix helps you understand where your model is "confusing" two results.

### Tabular

### Classification

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

  - **AuPRC** : The [area under the precision-recall (PR) curve](https://developers.google.com/machine-learning/glossary#pr-auc-area-under-the-pr-curve) , also referred to as average precision. This value ranges from zero to one, where a higher value indicates a higher-quality model.
  - **AuROC** : The [area under receiver operating characteristic curve](https://developers.google.com/machine-learning/glossary#auc-area-under-the-roc-curve) . This ranges from zero to one, where a higher value indicates a higher-quality model.
  - **Log loss** : The cross-entropy between the model inferences and the target values. This ranges from zero to infinity, where a lower value indicates a higher-quality model.
  - **Confidence threshold** : A confidence score that determines which inferences to return. A model returns inferences that are at this value or higher. A higher confidence threshold increases precision but lowers recall. Agent Platform returns confidence metrics at different threshold values to show how the threshold affects [precision](https://developers.google.com/machine-learning/glossary#precision) and [recall](https://developers.google.com/machine-learning/glossary#recall) .
  - **Recall** : The fraction of inferences with this class that the model correctly predicted. Also called *true positive rate* .
  - **Recall at 1** : The recall (true positive rate) when only considering the label that has the highest inference score and not below the confidence threshold for each example.
  - **Precision** : The fraction of classification inferences produced by the model that were correct.
  - **Precision at 1** : The precision when only considering the label that has the highest inference score and not below the confidence threshold for each example.
  - **F1 score** : The harmonic mean of precision and recall. F1 is a useful metric if you're looking for a balance between precision and recall and there's an uneven class distribution.
  - **F1 score at 1** : The harmonic mean of recall at 1 and precision at 1.
  - **Confusion matrix** : A [confusion matrix](https://developers.google.com/machine-learning/glossary#confusion-matrix) shows how often a model correctly predicted a result. For incorrectly predicted results, the matrix shows what the model predicted instead. The confusion matrix helps you understand where your model is "confusing" two results.
  - **True negative count** : The number of times a model correctly predicted a negative class.
  - **True positive count** : The number of times a model correctly predicted a positive class.
  - **False negative count** : The number of times a model mistakenly predicted a negative class.
  - **False positive count** : The number of times a model mistakenly predicted a positive class.
  - **False positive rate** : The fraction of incorrectly predicted results out of all predicted results.
  - **False positive rate at 1** : The false positive rate when only considering the label that has the highest inference score and not below the confidence threshold for each example.
  - **Model feature attributions:** Agent Platform shows you how much each feature impacts a model. The values are provided as a percentage for each feature: the higher the percentage, the more impact the feature had on model training. Review this information to ensure that all of the most important features make sense for your data and business problem.

### Regression

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

  - **MAE** : The mean absolute error (MAE) is the average absolute difference between the target values and the predicted values. This metric ranges from zero to infinity; a lower value indicates a higher quality model.
  - **RMSE** : The root-mean-squared error is the square root of the average squared difference between the target and predicted values. RMSE is more sensitive to outliers than MAE,so if you're concerned about large errors, then RMSE can be a more useful metric to evaluate. Similar to MAE, a smaller value indicates a higher quality model (0 represents a perfect predictor).
  - **RMSLE** : The root-mean-squared logarithmic error metric is similar to RMSE, except that it uses the natural logarithm of the predicted and actual values plus 1. RMSLE penalizes under-inference more heavily than over-inference. It can also be a good metric when you don't want to penalize differences for large inference values more heavily than for small inference values. This metric ranges from zero to infinity; a lower value indicates a higher quality model. The RMSLE evaluation metric is returned only if all label and predicted values are non-negative.
  - **r^2** : r squared (r^2) is the square of the Pearson correlation coefficient between the labels and predicted values. This metric ranges between zero and one. A higher value indicates a closer fit to the regression line.
  - **MAPE** : Mean absolute percentage error (MAPE) is the average absolute percentage difference between the labels and the predicted values. This metric ranges between zero and infinity; a lower value indicates a higher quality model.  
    MAPE is not shown if the target column contains any 0 values. In this case, MAPE is undefined.
  - **Model feature attributions:** Agent Platform shows you how much each feature impacts a model. The values are provided as a percentage for each feature: the higher the percentage, the more impact the feature had on model training. Review this information to ensure that all of the most important features make sense for your data and business problem.

### Forecasting

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

  - **MAE** : The mean absolute error (MAE) is the average absolute difference between the target values and the predicted values. This metric ranges from zero to infinity; a lower value indicates a higher quality model.
  - **RMSE** : The root-mean-squared error is the square root of the average squared difference between the target and predicted values. RMSE is more sensitive to outliers than MAE,so if you're concerned about large errors, then RMSE can be a more useful metric to evaluate. Similar to MAE, a smaller value indicates a higher quality model (0 represents a perfect predictor).
  - **RMSLE** : The root-mean-squared logarithmic error metric is similar to RMSE, except that it uses the natural logarithm of the predicted and actual values plus 1. RMSLE penalizes under-inference more heavily than over-inference. It can also be a good metric when you don't want to penalize differences for large inference values more heavily than for small inference values. This metric ranges from zero to infinity; a lower value indicates a higher quality model. The RMSLE evaluation metric is returned only if all label and predicted values are non-negative.
  - **r^2** : r squared (r^2) is the square of the Pearson correlation coefficient between the labels and predicted values. This metric ranges between zero and one. A higher value indicates a closer fit to the regression line.
  - **MAPE** : Mean absolute percentage error (MAPE) is the average absolute percentage difference between the labels and the predicted values. This metric ranges between zero and infinity; a lower value indicates a higher quality model.  
    MAPE is not shown if the target column contains any 0 values. In this case, MAPE is undefined.
  - **WAPE** : Weighted absolute percentage error (WAPE) is the overall difference between the value predicted by a model and the values observed over the values observed. Compared to RMSE, WAPE is weighted towards the overall differences rather than individual differences, which can be highly influenced by low or intermittent values. A lower value indicates a higher quality model.
  - **RMSPE** : Root mean squared percentage error (RMPSE) shows RMSE as a percentage of the actual values instead of an absolute number. A lower value indicates a higher quality model.
  - **Quantile** : The percent quantile, which indicates the probability that an observed value will be below the predicted value. For example, at the 0.5 quantile, the observed values are expected to be lower than the predicted values 50% of the time.
  - **Observed quantile** : Shows the percentage of true values that were less than the predicted value for a given quantile.
  - **Scaled pinball loss** : The scaled pinball loss at a particular quantile. A lower value indicates a higher quality model at the given quantile.

## Notebook tutorials

### AutoML: Tabular

> To learn more, run the following notebooks in the environment of your choice:
> 
>   - ": Evaluating batch prediction results from an AutoML Tabular classification model":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fautoml_tabular_classification_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fautoml_tabular_classification_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb)
> 
>   - " Pipelines: Evaluating batch prediction results from AutoML Tabular regression model":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fautoml_tabular_regression_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fautoml_tabular_regression_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb)

### Custom training: Tabular

> To learn more, run the following notebooks in the environment of your choice:
> 
>   - " Pipelines: Evaluating BatchPrediction results from a Custom Tabular classification model":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fcustom_tabular_classification_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fcustom_tabular_classification_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb)
> 
>   - " Pipelines: Evaluating batch prediction results from custom tabular regression model":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fcustom_tabular_regression_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fcustom_tabular_regression_model_evaluation.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb)

### Gemini Enterprise Agent Platform Model Registry

> To learn more, run the "Get started with importing a custom model evaluation to the " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/get_started_with_custom_model_evaluation_import.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fget_started_with_custom_model_evaluation_import.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fget_started_with_custom_model_evaluation_import.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/get_started_with_custom_model_evaluation_import.ipynb)

## What's next

  - Learn how to [perform model evaluation using Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/using-model-evaluation) .
