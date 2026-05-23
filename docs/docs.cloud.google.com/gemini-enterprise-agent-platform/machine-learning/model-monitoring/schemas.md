---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/schemas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/schemas
title: Provide schemas to Gemini Enterprise Agent Platform Model Monitoring
description: Describes how to provide schemas to Gemini Enterprise Agent Platform Model Monitoring.
data_source: docs.cloud.google.com
---

To start a monitoring job, Model Monitoring needs to know the schema of your tabular dataset in order to correctly parse the input payload.

  - For AutoML models, Model Monitoring automatically parses the schema because Gemini Enterprise Agent Platform already has access to your training data.

  - For custom-trained models:
    
      - Model Monitoring can automatically parse schemas for models that use a standard key-value input format.
    
      - For custom-trained models that don't use a key-value input format, you may need to provide a schema when [creating your monitoring job](https://docs.cloud.google.com/vertex-ai/docs/model-monitoring/using-model-monitoring) .
    
    Schema generation varies based on whether you are enabling Model Monitoring for an online inference endpoint or batch inferences.

## Schema parsing for online inference endpoints

For online inference endpoints, you can let Model Monitoring parse the schema automatically or upload a schema when you create a monitoring job.

### Automatic schema parsing

After you enable skew or drift detection for an online endpoint, Model Monitoring can usually automatically parse the input schema. For automatic schema parsing, Model Monitoring analyzes the first 1,000 input requests to determine the schema.

Automatic schema parsing works best when the input requests are formatted as key-value pairs, where `" key "` is the name of the feature and `" value "` is the value of the feature. For example:

    "key":"value"

    {"TenYearCHD":"0", "glucose":"5.4", "heartRate":"1", "age":"30",
    "prevalentStroke":"0", "gender":"f", "ethnicity":"latin american"}

If the inputs are not in `" key ":" value "` format, Model Monitoring tries to identify the data type of each feature, and automatically assigns a default feature name for each input.

### Custom instance schemas

You can provide your own input schema when you [create a Model Monitoring job](https://docs.cloud.google.com/vertex-ai/docs/model-monitoring/using-model-monitoring) to guarantee that Model Monitoring correctly parses your model's inputs.

This schema is called the *analysis instance schema* . The schema file specifies the format of the input payload, the names of each feature, and the type of each feature.

The schema must be written as a YAML file in the [Open API](https://swagger.io/specification/#schema) format. The following example is for an inference request with the `object` format:

    type: object
    properties:
      age:
        type: string
      BMI:
        type: number
      TenYearCHD:
        type: string
      cigsPerDay:
        type: array
        items:
          type: string
      BPMeds:
        type: string
    required:
    - age
    - BMI
    - TenYearCHD
    - cigsPerDay
    - BPMeds

  - `type` indicates whether your inference request is one of the following formats:
    
      - `object` : key-value pairs
      - `array` : array-like
      - `string` : csv-string

  - `properties` indicates the type of each individual feature.

  - If the request is in array or csv-string format, specify the order in which the features are listed in each request under the `required` field.

If your inference request is in array or csv-string format, represent any missing features as null values. For example, consider a inference request with five features:

`[feature_a, feature_b, feature_c, feature_d, feature_e]`

If `feature_c` allows missing values, a sample request missing `feature_c` would be: `{[1, 2, , 4, 6]}` . The list length is still 5, with one null value in the middle.

## Schema parsing for batch inferences

For batch inferences, you can let Model Monitoring parse the schema automatically or upload a schema when you create a monitoring job.

### Automatic schema parsing

If you don't provide a schema during monitoring job creation, Model Monitoring infers the data types of your features and generates your schema based on your training data.

Model Monitoring also needs to know which feature is the target column, which is the feature being predicted. The target column is excluded from the schema and feature skew metric. You can specify the target column while creating a monitoring job.

#### Target column specification

If you don't specify the target column while creating a monitoring job, Model Monitoring labels the last feature name in your training data as the target column.

For example, Model Monitoring labels `column_c` in this CSV training data as the target column because `column_c` is at the end of the first row:

    column_a, column_b, column_d, column_c
    1,"a", 2, "c"
    2,"b", 342, "d"

Similarly, Model Monitoring labels `column_c` in this JSONL file as the target column because `column_c` is at the end of the first row:

    {"column_a": 1, "column_b": "a", "column_d": 2, "column_c": "c" }
    {"column_a": 2, "column_b": "b", "column_c": "d",  "column_d": 342}

In both examples, the final schema only contains `column_a` , `column_b` , and `column_d` .

### Custom schemas

Your custom schema specifies the format of the input payload, the names of each feature, and the type of each feature.

The schema must be written as a YAML file with [Open API](https://swagger.io/docs/specification/data-models/data-types/#object) syntax. The following example is for an inference request with the `object` format:

    type: object
    properties:
      age:
        type: string
      BMI:
        type: number
      TenYearCHD:
        type: string
      cigsPerDay:
        type: array
        items:
          type: string
      BPMeds:
        type: string
    required:
    - age
    - BMI
    - TenYearCHD
    - cigsPerDay
    - BPMeds

Model Monitoring calculates feature skew based on the JSON Lines [batch inference output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions#input_data_requirements) . If your data type contains an array, the length of the array in the input data must be equal to the number of features specified in the yaml file. Otherwise Model Monitoring excludes the inference instance with the incorrect array length from feature skew calculation.

For example, the arrays in the following data types contain two features:

  - Array: `{[[1, 2]]}`

  - "Key"/"Value": `{"key": 0, "values": [[1, 2]]}`

The corresponding schema must also specify two features:

    type: object
    properties:
      name:
        type: string
      age:
        type: number
    required:
    - name
    - age

## What's next

  - [Enable skew and drift detection](https://docs.cloud.google.com/vertex-ai/docs/model-monitoring/using-model-monitoring) for your models.
  - Try the example notebook [in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) or [view it on GitHub](https://www.github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) .
