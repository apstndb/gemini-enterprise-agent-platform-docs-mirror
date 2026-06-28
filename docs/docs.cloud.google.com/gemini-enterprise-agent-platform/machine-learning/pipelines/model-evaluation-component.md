---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component
title: Model evaluation components
description: Learn how to use model evaluation components in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

Model evaluation components take ground truth and [batch prediction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component) results as input and generate evaluation metrics. Ground truth data is "correctly labeled" data as determined by humans, and is usually provided as the target field in the test dataset you used to train the model. For more information, see [Model evaluation in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction) .

Agent Platform provides the following model evaluation components:

  - [`ModelEvaluationClassificationOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html#v1.model_evaluation.ModelEvaluationClassificationOp)
  - [`ModelEvaluationForecastingOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html#v1.model_evaluation.ModelEvaluationForecastingOp)
  - [`ModelEvaluationRegressionOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html#v1.model_evaluation.ModelEvaluationRegressionOp)

## Model type support

The following table shows supported model types for each model evaluation component:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Model evaluation component</th>
<th>Supported model types</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">ModelEvaluationClassificationOp</code></td>
<td>AutoML tabular or image
Custom tabular</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ModelEvaluationRegressionOp</code></td>
<td>AutoML tabular
Custom tabular</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ModelEvaluationForecastingOp</code></td>
<td>AutoML tabular</td>
</tr>
</tbody>
</table>

## Remove the target field

For some model types, the [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component) component requires you to exclude the target column (ground truth) from your dataset.

## Configure and format slices for your tabular dataset

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

A slice is a subset of tabular data with specified characteristics. Sliced metrics offers more granular evaluation metrics for AutoML tabular and custom training classification models.

For example, consider a pet adoption dataset where a model is trained to predict whether a pet will be adopted within a week. While it's useful to look at metrics for the whole dataset, you may be interested in metrics related to the pet's species and age. In other words, you're interested in the following subset of the dataset:

| Feature          | Values                                |
| ---------------- | ------------------------------------- |
| `age (in years)` | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 |
| `species`        | "dog", "cat", "rabbit"                |

This fine-grained analysis can be helpful in identifying where the model might be most error prone, or ensuring that the model performs well on critical subsets of the data.

### Configure slices

To configure a slice, create a JSON file with the following configuration:

    {
      "FEATURE": {
        "KIND": {
          CONFIG
        }
      }
    }

Where:

  - FEATURE is a feature for which you want to create a slice. For example, `age` .

  - KIND is one of the following:
    
      - `value`
        
        `value` creates a single slice on a single value of a feature. Specify CONFIG as a key-value pair where the key is `float_value` or `string_value` . For example, `"float_value": 1.0` .
        
        The following example configuration creates a single slice containing data with the `age` of `1` :
        
            {
              "age": {
                "value": {
                  "float_value": 1.0
                }
              }
            }
    
      - `range`
        
        `range` creates a single slice that includes data within a specified range. Specify CONFIG as two key-value pairs where the keys are `low` and `high` .
        
        The following example configuration creates a single slice containing data where the `age` is any value between `1` and `3` :
        
            {
              "age": {
                "range": {
                  "low": 1,
                  "high": 3
                }
              }
            }
    
      - `all_values`
        
        `all_values` creates a separate slice for each possible label for the feature. Specify CONFIG as `"value": true` .
        
        The following example configuration creates three slices—one each for `"dog"` , `"cat"` , and `"rabbit"` :
        
            {
              "species": {
                "all_values": {
                  "value": true
                }
              }
            }

You can also use multiple features to create one or more slices.

The following configuration creates a single slice containing data where the `age` is between `1` and `3` and the `species` is `"dog"` :

    {
      "age": {
        "range": {
          "low": 1,
          "high": 3
        }
      },
      "species": {
        "value": {
          "string_value": "dog"
        }
      }
    }

The following configuration creates multiple slices—one for each unique species in the dataset, where the `age` is `1` .

    {
      "species": {
        "all_values": {
          "value": true
        }
      },
      "age": {
        "value": {
          "float_value": 1.0
        }
      }
    }

The resulting slices contain the following data from the example dataset:

  - **Slice 1:** `age:1` and `species:"dog"`

  - **Slice 2:** `age:1` and `species:"cat"`

  - **Slice 3:** `age:1` and `species:"rabbit"`

### Format slices

To format slices for the `ModelEvaluationClassificationOp` component, do the following:

1.  Create a `slicing_spec` . For example:
    
        from google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice import SliceSpec
        from google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec import SliceConfig
        
        slicing_spec = SliceSpec(configs={ 'feature_a': SliceConfig(SliceSpec.Value(string_value='label_a') ) })

2.  Create a list to store the slice configurations. For example:
    
        slicing_specs = []

3.  Format each `slicing_spec` as JSON or a dictionary. For example:
    
        slicing_spec_json = json_format.MessageToJson(slicing_spec)
        
        slicing_spec_dict = json_format.MessageToDict(slicing_spec)

4.  Combine each `slicing_spec` into a list. For example:
    
        slicing_specs.append(slicing_spec_json)

5.  Pass `slicing_specs` as a parameter to the `ModelEvaluationClassificationOp` component. For example:
    
        ModelEvaluationClassificationOp(slicing_specs=slicing_specs)

### Format fairness metrics configuration slices

To evaluate your model for [fairness](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/intro-evaluation-fairness) , use the following components:

  - [`DetectDataBiasOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.0.0/api/preview/model_evaluation.html#preview.model_evaluation.DetectDataBiasOp) : returns [data bias metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/data-bias-metrics) for the slices you pass into the component.

  - [`DetectModelBiasOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.0.0/api/preview/model_evaluation.html#preview.model_evaluation.DetectModelBiasOp) : returns [model bias metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/model-bias-metrics) for the slices you pass into the component.

To format your slices for the `DetectDataBiasOp` and `DetectModelBiasOp` components, do the following:

1.  Create a `BiasConfig` . For example:
    
        from google.cloud.aiplatform_v1.types.ModelEvaluation import BiasConfig
        from google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice import SliceSpec
        from google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec import SliceConfig
        
        bias_config = BiasConfig(bias_slices=SliceSpec(configs={ 'feature_a': SliceConfig(SliceSpec.Value(string_value='label_a') ) }))

2.  Create a list to store the bias configurations. For example:
    
        bias_configs = []

3.  Format each `bias_config` as JSON or a dictionary. For example:
    
        bias_config_json = json_format.MessageToJson(bias_config)
        
        bias_config_dict = json_format.MessageToDict(bias_config)

4.  Combine each `bias_config` into a list. For example:
    
        bias_configs.append(bias_config_json)

5.  Pass `bias_configs` as a parameter to the `DetectDataBiasOp` or `DetectModelBiasOp` component. For example:
    
        DetectDataBiasOp(bias_configs=bias_configs)
        
        DetectModelBiasOp(bias_configs=bias_configs)

## Required input parameters

The required input parameters for model evaluation components vary based on the type of model you are evaluating.

### AutoML models

When training AutoML models, Gemini Enterprise Agent Platform uses default schemas. Some input parameters for the model evaluation components are only required if you used a non-default schema to train your model.

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

The following tabs show example batch prediction output files and required input parameters for each Tabular model type parameters:

### Classification

The default schema includes the following fields:

  - `scores` : array
  - `classes` : array

The following is an example of a batch prediction output file with the target column of `male` :

``` 
{
  "instance": {
    "male": "1",
    "age": "49",
    "heartRate": "67",
    "education": "medium_high",
    "totChol": "282",
    "diaBP": "79",
    "BPMeds": "0",
    "currentSmoker": "current_high",
    "cigsPerDay": "25",
    "prevalentStroke": "stroke_0",
    "prevalentHyp": "hyp_0",
    "TenYearCHD": "FALSE",
    "diabetes": "0",
    "sysBP": "134",
    "BMI": "26.87",
    "glucose": "78"
    },
  "prediction": {
      "scores": [0.3666940927505493, 0.6333059072494507],
      "classes": ["0", "1"]
    }
}
          
```

This table describes the required parameters for the `ModelEvaluationClassificationOp` component with a tabular model:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evaluation component parameter</th>
<th>Required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">target_field_name</code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">prediction_label_column</code></td>
<td>Not required for default schema.<br />
Use <code dir="ltr" translate="no">prediction.classes</code> for non-default schemas.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">prediction_score_column</code></td>
<td>Not required for default schema.<br />
Use <code dir="ltr" translate="no">prediction.scores</code> for non-default schemas.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">evaluation_class_labels</code></td>
<td>Not required for default schema.<br />
Use <code dir="ltr" translate="no">["0","1"]</code> for non-default schemas.</td>
</tr>
</tbody>
</table>

### Regression

The default schema includes the following fields:

  - `value` : float
  - `lower_bound` : float
  - `upper_bound` : float

The following is an example of a batch prediction output file with the target column of `age` :

``` 
{
  "instance": {
    "BPMeds": "0",
    "diabetes": "0",
    "diaBP": "65",
    "cigsPerDay": "45",
    "prevalentHyp": "hyp_0",
    "age": "46",
    "male": "1",
    "sysBP": "112.5",
    "glucose": "78",
    "BMI": "27.48",
    "TenYearCHD": "FALSE",
    "totChol": "209",
    "education": "high",
    "prevalentStroke": "stroke_0",
    "heartRate": "75",
    "currentSmoker": "current_high"
  },
  "prediction": {
    "value": 44.96103286743164,
    "lower_bound": 44.61349868774414,
    "upper_bound": 44.590206146240234
  }
}
          
```

This table describes the required parameters for the `ModelEvaluationRegressionOp` component with a tabular model:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evaluation component parameter</th>
<th>Required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">target_field_name</code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">prediction_label_column</code></td>
<td>Not required for regression models.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">prediction_score_column</code></td>
<td>Not required for default schema.<br />
Use <code dir="ltr" translate="no">prediction.value</code> for non-default schemas.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">evaluation_class_labels</code></td>
<td>Not required for regression models.</td>
</tr>
</tbody>
</table>

### Forecasting

For tabular forecasting models, the `BatchPredictionJob` component requires you to exclude the target column (ground truth) from your dataset.

The default schema includes the following fields:

  - `id` : string
  - `displayNames` : string
  - `type` : enum
  - `timeSegmentStart` : string
  - `timeSegmentEnd` : string
  - `confidence` : float

The following is an example CSV file with `sale_dollars` as the target column:

``` 
date,store_name,city,zip_code,county,sale_dollars
2020-03-17,Thriftway,,,,774.08999999999992
2020-03-10,Thriftway,,,,1160.67
2020-03-03,Thriftway,,,,2247.24
2020-06-08,New Star / Fort Dodge,,,,753.98
2020-06-01,New Star / Fort Dodge,,,,967.73
2020-01-10,Casey's General Store #1280 / Fort Dodge,,,,1040.92
2020-10-30,KUM & GO #76 / ADAIR,Adair,50002,ADAIR,1387.02
          
```

The `TargetFieldDataRemoverOp` component removes the target column before sending the file to the `BatchPredictionJob` component:

``` 
date,store_name,city,zip_code,county
2020-03-17,Thriftway,nan,nan,nan
2020-03-10,Thriftway,nan,nan,nan
2020-03-03,Thriftway,nan,nan,nan
2020-06-08,New Star / Fort Dodge,nan,nan,nan
2020-06-01,New Star / Fort Dodge,nan,nan,nan
2020-01-10,Casey's General Store #1280 / Fort Dodge,nan,nan,nan
2020-10-30,KUM & GO #76 / ADAIR,Adair,50002.0,ADAIR
          
```

The following is an example of a batch prediction output file without the target column of `sale_dollars` :

``` 
{
  "instance": {
    "content": "gs://kbn-us-central1-test/datasets/text/happy_11556.txt",
    "mimeType":"text/plain"
  },
  "prediction": {
    "ids":    ["7903916851837534208","3292230833410146304","986387824196452352","2139309328803299328","5598073842623840256","6750995347230687232","4559431178561519616"],
    "displayNames": ["affection","bonding","achievement","exercise","nature","enjoy_the_moment","leisure"],
    "confidences": [0.99483216,0.005162797,4.1117933E-6,3.9997E-7,2.4624453E-7,1.9969502E-7,1.16997434E-7]
  }
}
          
```

This table describes the required parameters for the `ModelEvaluationForecastingOp` component with a tabular model:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evaluation component parameter</th>
<th>Required</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">target_field_name</code></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">prediction_label_column</code></td>
<td>Not required for forecasting models.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">prediction_score_column</code></td>
<td>Not required for default schema.<br />
Use <code dir="ltr" translate="no">"prediction.value"</code> for non-default schemas.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">evaluation_class_labels</code></td>
<td>Not required for forecasting models.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ground_truth_gcs_source</code></td>
<td>Yes: the Cloud Storage link to the original dataset with the target column.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ground_truth_format</code></td>
<td>Yes: the format of the original dataset. For example, <code dir="ltr" translate="no">"jsonl"</code> , <code dir="ltr" translate="no">"csv"</code> , or <code dir="ltr" translate="no">"bigquery"</code> .</td>
</tr>
</tbody>
</table>

### Custom-trained models

For custom-trained models, the [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component) component requires you to exclude the target column (ground truth) from your dataset. You can use the [`TargetFieldDataRemoverOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/google_cloud_pipeline_components.experimental.evaluation.html#google_cloud_pipeline_components.experimental.evaluation.TargetFieldDataRemoverOp) component for a more efficient workflow.

The following example shows a batch prediction output file and required input parameters for a custom-trained tabular classification model:

### Classification

The typical schema includes the following fields:

  - `instance` : array of input data in the same order as the model training dataset columns.
  - `prediction` : array of input data in the same order as the model training dataset columns.

The following is an example CSV dataset with `species` as the target column:

``` 
petal_length,petal_width,sepal_length,sepal_width,species
6.4,2.8,5.6,2.2,2
5.0,2.3,3.3,1.0,1
4.9,2.5,4.5,1.7,2
4.9,3.1,1.5,0.1,0
          
```

The `TargetFieldDataRemoverOp` component removes the target column before sending the file to the batch prediction component:

``` 
petal_length,petal_width,sepal_length,sepal_width
6.4,2.8,5.6,2.2
5.0,2.3,3.3,1.0
4.9,2.5,4.5,1.7
4.9,3.1,1.5,0.1
          
```

The following is an example of a batch prediction output file without the target column of `species` :

``` 
{
  "instance": [5.6, 2.5, 3.9, 1.1],
  "prediction": [0.0005816521588712931, 0.9989032745361328, 0.0005150380893610418]
}
{
  "instance": [5.0, 3.6, 1.4, 0.2],
  "prediction": [0.999255359172821, 0.000527293945197016, 0.00021737271163146943]
}
{
  "instance": [6.0, 2.9, 4.5, 1.5],
  "prediction": [0.00025063654175028205, 0.9994204044342041, 0.00032893591560423374]
}
          
```

This table describes the required parameters for the `ModelEvaluationClassificationOp` component with a custom-trained model:

| Evaluation component parameter | Required                                                                                           |
| ------------------------------ | -------------------------------------------------------------------------------------------------- |
| `target_field_name`            | Yes                                                                                                |
| `prediction_label_column`      | Must be empty; this column doesn't exist in custom-trained models.                                 |
| `prediction_score_column`      | Not required for default schema; is set automatically for `JSONL` , `CSV` , or `BIGQUERY` formats. |
| `evaluation_class_labels`      | Yes. Must be the same length as the output prediction array.                                       |
| `ground_truth_gcs_source`      | Yes: the Cloud Storage link to the original dataset with the target column.                        |
| `ground_truth_format`          | Yes: the format of the original dataset. For example, `"jsonl"` , `"csv"` , or `"bigquery"` .      |

## Model evaluations without Agent Platform-generated batch predictions

You can use a model evaluation pipeline component with a batch prediction that you didn't generate in Agent Platform. However, note that the input for the model evaluation pipeline component must be a batch prediction directory containing files that match the following prefixes:

  - `prediction.results-`

  - `explanation.results-`

  - `predictions_`

## API reference

  - For component reference, see the [Google Cloud SDK reference page for Model evaluation components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html) .

  - For examples of how to use the Model Evaluation components, see the notebooks listed at [Create an evaluation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/using-model-evaluation#python) .

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .
