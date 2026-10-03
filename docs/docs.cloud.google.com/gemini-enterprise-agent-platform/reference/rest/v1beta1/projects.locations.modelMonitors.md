---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors
title: 'REST Resource: projects.locations.modelMonitors'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ModelMonitor

Agent Platform Model Monitoring service serves as a central hub for the analysis and visualization of data quality and performance related to models. ModelMonitor stands as a top level resource for overseeing your model monitoring tasks.

Fields

`name` `string`

Immutable. Resource name of the ModelMonitor. Format: `projects/{project}/locations/{location}/modelMonitors/{modelMonitor}` .

`displayName` `string`

The display name of the ModelMonitor. The name can be up to 128 characters long and can consist of any UTF-8.

`modelMonitoringTarget` `object ( `[`ModelMonitoringTarget`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#ModelMonitoringTarget)` )`

The entity that is subject to analysis. Currently only models in Agent Platform Model Registry are supported. If you want to analyze the model which is outside the Agent Platform, you could register a model in Agent Platform Model Registry using just a display name.

`trainingDataset` `object ( `[`ModelMonitoringInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringInput)` )`

Optional training dataset used to train the model. It can serve as a reference dataset to identify changes in production.

`notificationSpec` `object ( `[`ModelMonitoringNotificationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec)` )`

Optional default notification spec, it can be overridden in the ModelMonitoringJob notification spec.

`outputSpec` `object ( `[`ModelMonitoringOutputSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringOutputSpec)` )`

Optional default monitoring metrics/logs export spec, it can be overridden in the ModelMonitoringJob output spec. If not specified, a default Google Cloud Storage bucket will be created under your project.

`explanationSpec` `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExplanationSpec)` )`

Optional model explanation spec. It is used for feature attribution monitoring.

`modelMonitoringSchema` `object ( `[`ModelMonitoringSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#ModelMonitoringSchema)` )`

Monitoring Schema is to specify the model's features, prediction outputs and ground truth properties. It is used to extract pertinent data from the dataset and to process features based on their properties. Make sure that the schema aligns with your dataset, if it does not, we will be unable to extract data from the dataset. It is required for most models, but optional for Agent Platform AutoML Tables unless the schem information is not available.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key spec for a ModelMonitor. If set, this ModelMonitor and all sub-resources of this ModelMonitor will be secured by this key.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ModelMonitor was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ModelMonitor was updated most recently.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`default_objective` `Union type`

Optional default monitoring objective, it can be overridden in the ModelMonitoringJob objective spec. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`tabularObjective` `object ( `[`TabularObjective`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective)` )`

Optional default tabular model monitoring objective.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "modelMonitoringTarget": {
    object (ModelMonitoringTarget)
  },
  "trainingDataset": {
    object (ModelMonitoringInput)
  },
  "notificationSpec": {
    object (ModelMonitoringNotificationSpec)
  },
  "outputSpec": {
    object (ModelMonitoringOutputSpec)
  },
  "explanationSpec": {
    object (ExplanationSpec)
  },
  "modelMonitoringSchema": {
    object (ModelMonitoringSchema)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "createTime": string,
  "updateTime": string,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,

  // default_objective
  "tabularObjective": {
    object (TabularObjective)
  }
  // Union type
}
```

## ModelMonitoringTarget

The monitoring target refers to the entity that is subject to analysis. e.g. Agent Platform Model version.

Fields

`source` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vertexModel` `object ( `[`VertexModelSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#VertexModelSource)` )`

Model in Agent Platform Model Registry.

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "vertexModel": {
    object (VertexModelSource)
  }
  // Union type
}
```

## VertexModelSource

Model in Agent Platform Model Registry.

Fields

`model` `string`

Model resource name. Format: projects/{project}/locations/{location}/models/{model}.

`modelVersionId` `string`

Model version id.

**JSON representation**

```
{
  "model": string,
  "modelVersionId": string
}
```

## ModelMonitoringSchema

The Model Monitoring Schema definition.

Fields

`featureFields[]` `object ( `[`FieldSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#FieldSchema)` )`

feature names of the model. Agent Platform will try to match the features from your dataset as follows: \* For 'csv' files, the header names are required, and we will extract the corresponding feature values when the header names align with the feature names. \* For 'jsonl' files, we will extract the corresponding feature values if the key names match the feature names. Note: Nested features are not supported, so please ensure your features are flattened. Ensure the feature values are scalar or an array of scalars. \* For 'bigquery' dataset, we will extract the corresponding feature values if the column names match the feature names. Note: The column type can be a scalar or an array of scalars. STRUCT or JSON types are not supported. You may use SQL queries to select or aggregate the relevant features from your original table. However, ensure that the 'schema' of the query results meets our requirements. \* For the Agent Platform Endpoint Request Response Logging table or Agent Platform Batch Prediction Job results. If the `instanceType` is an array, ensure that the sequence in [`featureFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#ModelMonitoringSchema.FIELDS.feature_fields) matches the order of features in the prediction instance. We will match the feature with the array in the order specified in \[featureFields\].

`predictionFields[]` `object ( `[`FieldSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#FieldSchema)` )`

Prediction output names of the model. The requirements are the same as the [`featureFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#ModelMonitoringSchema.FIELDS.feature_fields) . For AutoML Tables, the prediction output name presented in schema will be: `predicted_{targetColumn}` , the `targetColumn` is the one you specified when you train the model. For Prediction output drift analysis: \* AutoML Classification, the distribution of the argmax label will be analyzed. \* AutoML Regression, the distribution of the value will be analyzed.

`groundTruthFields[]` `object ( `[`FieldSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#FieldSchema)` )`

Target /ground truth names of the model.

**JSON representation**

```
{
  "featureFields": [
    {
      object (FieldSchema)
    }
  ],
  "predictionFields": [
    {
      object (FieldSchema)
    }
  ],
  "groundTruthFields": [
    {
      object (FieldSchema)
    }
  ]
}
```

## FieldSchema

Schema field definition.

Fields

`name` `string`

Field name.

`dataType` `string`

Supported data types are: `float` `integer` `boolean` `string` `categorical`

`repeated` `boolean`

Describes if the schema field is an array of given data type.

**JSON representation**

```
{
  "name": string,
  "dataType": string,
  "repeated": boolean
}
```

| Methods                                                                                                                                                                             |                                                                       |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/create)                                           | Creates a ModelMonitor.                                               |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/delete)                                           | Deletes a ModelMonitor.                                               |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/get)                                                 | Gets a ModelMonitor.                                                  |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/list)                                               | Lists ModelMonitors in a Location.                                    |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/patch)                                             | Updates a ModelMonitor.                                               |
| [`searchModelMonitoringAlerts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringAlerts) | Returns the Model Monitoring alerts.                                  |
| [`searchModelMonitoringStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats)   | Searches Model Monitoring Stats generated within a given time window. |
