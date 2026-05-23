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

`modelMonitoringTarget` ` object ( ModelMonitoringTarget  ` )

The entity that is subject to analysis. Currently only models in Agent Platform Model Registry are supported. If you want to analyze the model which is outside the Agent Platform, you could register a model in Agent Platform Model Registry using just a display name.

`trainingDataset` ` object ( ModelMonitoringInput  ` )

Optional training dataset used to train the model. It can serve as a reference dataset to identify changes in production.

`notificationSpec` ` object ( ModelMonitoringNotificationSpec  ` )

Optional default notification spec, it can be overridden in the ModelMonitoringJob notification spec.

`outputSpec` ` object ( ModelMonitoringOutputSpec  ` )

Optional default monitoring metrics/logs export spec, it can be overridden in the ModelMonitoringJob output spec. If not specified, a default Google Cloud Storage bucket will be created under your project.

`explanationSpec` ` object ( ExplanationSpec  ` )

Optional model explanation spec. It is used for feature attribution monitoring.

`modelMonitoringSchema` ` object ( ModelMonitoringSchema  ` )

Monitoring Schema is to specify the model's features, prediction outputs and ground truth properties. It is used to extract pertinent data from the dataset and to process features based on their properties. Make sure that the schema aligns with your dataset, if it does not, we will be unable to extract data from the dataset. It is required for most models, but optional for Agent Platform AutoML Tables unless the schem information is not available.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a ModelMonitor. If set, this ModelMonitor and all sub-resources of this ModelMonitor will be secured by this key.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelMonitor was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelMonitor was updated most recently.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`default_objective` `Union type`

Optional default monitoring objective, it can be overridden in the ModelMonitoringJob objective spec. `default_objective` can be only one of the following:

`tabularObjective` ` object ( TabularObjective  ` )

Optional default tabular model monitoring objective.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;modelMonitoringTarget&quot;: {object (ModelMonitoringTarget)},&quot;trainingDataset&quot;: {object (ModelMonitoringInput)},&quot;notificationSpec&quot;: {object (ModelMonitoringNotificationSpec)},&quot;outputSpec&quot;: {object (ModelMonitoringOutputSpec)},&quot;explanationSpec&quot;: {object (ExplanationSpec)},&quot;modelMonitoringSchema&quot;: {object (ModelMonitoringSchema)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,// default_objective&quot;tabularObjective&quot;: {object (TabularObjective)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringTarget

The monitoring target refers to the entity that is subject to analysis. e.g. Agent Platform Model version.

Fields

`source` `Union type`

`source` can be only one of the following:

`vertexModel` ` object ( VertexModelSource  ` )

Model in Agent Platform Model Registry.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// source&quot;vertexModel&quot;: {object (VertexModelSource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## VertexModelSource

Model in Agent Platform Model Registry.

Fields

`model` `string`

Model resource name. Format: projects/{project}/locations/{location}/models/{model}.

`modelVersionId` `string`

Model version id.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;model&quot;: string,
  &quot;modelVersionId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringSchema

The Model Monitoring Schema definition.

Fields

`featureFields[]` ` object ( FieldSchema  ` )

feature names of the model. Agent Platform will try to match the features from your dataset as follows: \* For 'csv' files, the header names are required, and we will extract the corresponding feature values when the header names align with the feature names. \* For 'jsonl' files, we will extract the corresponding feature values if the key names match the feature names. Note: Nested features are not supported, so please ensure your features are flattened. Ensure the feature values are scalar or an array of scalars. \* For 'bigquery' dataset, we will extract the corresponding feature values if the column names match the feature names. Note: The column type can be a scalar or an array of scalars. STRUCT or JSON types are not supported. You may use SQL queries to select or aggregate the relevant features from your original table. However, ensure that the 'schema' of the query results meets our requirements. \* For the Agent Platform Endpoint Request Response Logging table or Agent Platform Batch Prediction Job results. If the `instanceType` is an array, ensure that the sequence in `  featureFields  ` matches the order of features in the prediction instance. We will match the feature with the array in the order specified in \[featureFields\].

`predictionFields[]` ` object ( FieldSchema  ` )

Prediction output names of the model. The requirements are the same as the `  featureFields  ` . For AutoML Tables, the prediction output name presented in schema will be: `predicted_{targetColumn}` , the `targetColumn` is the one you specified when you train the model. For Prediction output drift analysis: \* AutoML Classification, the distribution of the argmax label will be analyzed. \* AutoML Regression, the distribution of the value will be analyzed.

`groundTruthFields[]` ` object ( FieldSchema  ` )

Target /ground truth names of the model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureFields&quot;: [{object (FieldSchema)}],&quot;predictionFields&quot;: [{object (FieldSchema)}],&quot;groundTruthFields&quot;: [{object (FieldSchema)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FieldSchema

Schema field definition.

Fields

`name` `string`

Field name.

`dataType` `string`

Supported data types are: `float` `integer` `boolean` `string` `categorical`

`repeated` `boolean`

Describes if the schema field is an array of given data type.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;dataType&quot;: string,
  &quot;repeated&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a ModelMonitor.

### `            delete           `

Deletes a ModelMonitor.

### `            get           `

Gets a ModelMonitor.

### `            list           `

Lists ModelMonitors in a Location.

### `            patch           `

Updates a ModelMonitor.

### `            searchModelMonitoringAlerts           `

Returns the Model Monitoring alerts.

### `            searchModelMonitoringStats           `

Searches Model Monitoring Stats generated within a given time window.
