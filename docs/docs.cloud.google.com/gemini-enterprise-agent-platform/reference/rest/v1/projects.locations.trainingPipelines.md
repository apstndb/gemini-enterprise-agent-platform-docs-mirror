---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines
title: 'REST Resource: projects.locations.trainingPipelines'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: TrainingPipeline

The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Agent Platform's Dataset which becomes the training input, `  upload  ` the Model to Agent Platform, and evaluate the Model.

Fields

`name` `string`

Output only. Resource name of the TrainingPipeline.

`displayName` `string`

Required. The user-defined name of this TrainingPipeline.

`inputDataConfig` ` object ( InputDataConfig  ` )

Specifies Agent Platform owned input data that may be used for training the Model. The TrainingPipeline's `  trainingTaskDefinition  ` should make clear whether this config is used and if there are any special requirements on how it should be filled. If nothing about this config is mentioned in the `  trainingTaskDefinition  ` , then it should be assumed that the TrainingPipeline does not depend on this configuration.

`trainingTaskDefinition` `string`

Required. A Google Cloud Storage path to the YAML file that defines the training task which is responsible for producing the model artifact, and may also include additional auxiliary work. The definition files that can be used here are found in gs://google-cloud-aiplatform/schema/trainingjob/definition/. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`trainingTaskInputs` ` value ( Value  ` format)

Required. The training task's parameter(s), as specified in the `  trainingTaskDefinition  ` 's `inputs` .

`trainingTaskMetadata` ` value ( Value  ` format)

Output only. The metadata information as specified in the `  trainingTaskDefinition  ` 's `metadata` . This metadata is an auxiliary runtime and final information about the training task. While the pipeline is running this information is populated only at a best effort basis. Only present if the pipeline's `  trainingTaskDefinition  ` contains `metadata` object.

`modelToUpload` ` object ( Model  ` )

Describes the Model that may be uploaded (via `  ModelService.UploadModel  ` ) by this TrainingPipeline. The TrainingPipeline's `  trainingTaskDefinition  ` should make clear whether this Model description should be populated, and if there are any special requirements regarding how it should be filled. If nothing is mentioned in the `  trainingTaskDefinition  ` , then it should be assumed that this field should not be filled and the training task either uploads the Model without a need of this information, or that training task does not support uploading a Model as part of the pipeline. When the Pipeline's state becomes `PIPELINE_STATE_SUCCEEDED` and the trained Model had been uploaded into Agent Platform, then the modelToUpload's resource `  name  ` is populated. The Model is always uploaded into the Project and Location in which this pipeline is.

`modelId` `string`

Optional. The id to use for the uploaded Model, which will become the final component of the model resource name.

This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number or hyphen.

`parentModel` `string`

Optional. When specify this field, the `modelToUpload` will not be uploaded as a new model, instead, it will become a new version of this `parentModel` .

`state` ` enum ( PipelineState  ` )

Output only. The detailed state of the pipeline.

`error` ` object ( Status  ` )

Output only. Only populated when the pipeline's state is `PIPELINE_STATE_FAILED` or `PIPELINE_STATE_CANCELLED` .

`createTime` ` string ( Timestamp  ` format)

Output only. time when the TrainingPipeline was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` ` string ( Timestamp  ` format)

Output only. time when the TrainingPipeline for the first time entered the `PIPELINE_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Output only. time when the TrainingPipeline entered any of the following states: `PIPELINE_STATE_SUCCEEDED` , `PIPELINE_STATE_FAILED` , `PIPELINE_STATE_CANCELLED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. time when the TrainingPipeline was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize TrainingPipelines.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a TrainingPipeline. If set, this TrainingPipeline will be secured by this key.

Note: Model trained by this TrainingPipeline is also secured by this key if `  modelToUpload  ` is not set separately.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;inputDataConfig&quot;: {object (InputDataConfig)},&quot;trainingTaskDefinition&quot;: string,&quot;trainingTaskInputs&quot;: value,&quot;trainingTaskMetadata&quot;: value,&quot;modelToUpload&quot;: {object (Model)},&quot;modelId&quot;: string,&quot;parentModel&quot;: string,&quot;state&quot;: enum (PipelineState),&quot;error&quot;: {object (Status)},&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;encryptionSpec&quot;: {object (EncryptionSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## InputDataConfig

Specifies Agent Platform owned input data to be used for training, and possibly evaluating, the Model.

Fields

`datasetId` `string`

Required. The id of the Dataset in the same Project and Location which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's `  trainingTaskDefinition  ` . For tabular Datasets, all their data is exported to training, to pick and choose from.

`annotationsFilter` `string`

Applicable only to Datasets that have DataItems and Annotations.

A filter on Annotations of the Dataset. Only Annotations that both match this filter and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on (for the auto-assigned that role is decided by Agent Platform). A filter with same syntax as the one used in `  ListAnnotations  ` may be used, but note here it filters across all Annotations of the Dataset, and not just within a single DataItem.

`annotationSchemaUri` `string`

Applicable only to custom training with Datasets that have DataItems and Annotations.

Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/ , note that the chosen schema must be consistent with `  metadata  ` of the Dataset specified by `  datasetId  ` .

Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on.

When used in conjunction with `  annotationsFilter  ` , the Annotations used for training are filtered by both `  annotationsFilter  ` and `  annotationSchemaUri  ` .

`savedQueryId` `string`

Only applicable to Datasets that have SavedQueries.

The id of a SavedQuery (annotation set) under the Dataset specified by `  datasetId  ` used for filtering Annotations for training.

Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with `  annotationsFilter  ` , the Annotations used for training are filtered by both `  savedQueryId  ` and `  annotationsFilter  ` .

Only one of `  savedQueryId  ` and `  annotationSchemaUri  ` should be specified as both of them represent the same thing: problem type.

`persistMlUseAssignment` `boolean`

Whether to persist the ML use assignment to data item system labels.

`split` `Union type`

The instructions how the input data should be split between the training, validation and test sets. If no split type is provided, the `  fraction_split  ` is used by default. `split` can be only one of the following:

`fractionSplit` ` object ( FractionSplit  ` )

Split based on fractions defining the size of each set.

`filterSplit` ` object ( FilterSplit  ` )

Split based on the provided filters for each set.

`predefinedSplit` ` object ( PredefinedSplit  ` )

Supported only for tabular Datasets.

Split based on a predefined key.

`timestampSplit` ` object ( TimestampSplit  ` )

Supported only for tabular Datasets.

Split based on the timestamp of the input data pieces.

`stratifiedSplit` ` object ( StratifiedSplit  ` )

Supported only for tabular Datasets.

Split based on the distribution of the specified column.

`destination` `Union type`

Only applicable to Custom and Hyperparameter Tuning TrainingPipelines.

The destination of the training data to be written to.

Supported destination file formats: \* For non-tabular data: "jsonl". \* For tabular data: "csv" and "bigquery".

The following Agent Platform environment variables are passed to containers or python modules of the training task when this field is set:

  - AIP\_DATA\_FORMAT : Exported data format.
  - AIP\_TRAINING\_DATA\_URI : Sharded exported training data uris.
  - AIP\_VALIDATION\_DATA\_URI : Sharded exported validation data uris.
  - AIP\_TEST\_DATA\_URI : Sharded exported test data uris. `destination` can be only one of the following:

`gcsDestination` ` object ( GcsDestination  ` )

The Cloud Storage location where the training data is to be written to. In the given directory a new directory is created with name: `dataset-<dataset-id>-<annotation-type>-<timestamp-of-training-call>` where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format. All training input data is written into that directory.

The Agent Platform environment variables representing Cloud Storage data URIs are represented in the Cloud Storage wildcard format to support sharded data. e.g.: "gs://.../training-\*.jsonl"

  - AIP\_DATA\_FORMAT = "jsonl" for non-tabular data, "csv" for tabular data

  - AIP\_TRAINING\_DATA\_URI = "gcsDestination/dataset- - - /training-\*.${AIP\_DATA\_FORMAT}"

  - AIP\_VALIDATION\_DATA\_URI = "gcsDestination/dataset- - - /validation-\*.${AIP\_DATA\_FORMAT}"

  - AIP\_TEST\_DATA\_URI = "gcsDestination/dataset- - - /test-\*.${AIP\_DATA\_FORMAT}"

`bigqueryDestination` ` object ( BigQueryDestination  ` )

Only applicable to custom training with tabular Dataset with BigQuery source.

The BigQuery project location where the training data is to be written to. In the given project a new dataset is created with name `dataset_<dataset-id>_<annotation-type>_<timestamp-of-training-call>` where timestamp is in YYYY\_MM\_DDThh\_mm\_ss\_sssZ format. All training input data is written into that dataset. In the dataset three tables are created, `training` , `validation` and `test` .

  - AIP\_DATA\_FORMAT = "bigquery".

  - AIP\_TRAINING\_DATA\_URI = "bigqueryDestination.dataset\_ \_ \_ .training"

  - AIP\_VALIDATION\_DATA\_URI = "bigqueryDestination.dataset\_ \_ \_ .validation"

  - AIP\_TEST\_DATA\_URI = "bigqueryDestination.dataset\_ \_ \_ .test"

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;datasetId&quot;: string,&quot;annotationsFilter&quot;: string,&quot;annotationSchemaUri&quot;: string,&quot;savedQueryId&quot;: string,&quot;persistMlUseAssignment&quot;: boolean,// split&quot;fractionSplit&quot;: {object (FractionSplit)},&quot;filterSplit&quot;: {object (FilterSplit)},&quot;predefinedSplit&quot;: {object (PredefinedSplit)},&quot;timestampSplit&quot;: {object (TimestampSplit)},&quot;stratifiedSplit&quot;: {object (StratifiedSplit)}// Union type// destination&quot;gcsDestination&quot;: {object (GcsDestination)},&quot;bigqueryDestination&quot;: {object (BigQueryDestination)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FractionSplit

Assigns the input data to training, validation, and test sets as per the given fractions. Any of `trainingFraction` , `validationFraction` and `testFraction` may optionally be provided, they must sum to up to 1. If the provided ones sum to less than 1, the remainder is assigned to sets as decided by Agent Platform. If none of the fractions are set, by default roughly 80% of data is used for training, 10% for validation, and 10% for test.

Fields

`trainingFraction` `number`

The fraction of the input data that is to be used to train the Model.

`validationFraction` `number`

The fraction of the input data that is to be used to validate the Model.

`testFraction` `number`

The fraction of the input data that is to be used to evaluate the Model.

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
  &quot;trainingFraction&quot;: number,
  &quot;validationFraction&quot;: number,
  &quot;testFraction&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## FilterSplit

Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.

Fields

`trainingFilter` `string`

Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in `  DatasetService.ListDataItems  ` may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order.

`validationFilter` `string`

Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in `  DatasetService.ListDataItems  ` may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order.

`testFilter` `string`

Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in `  DatasetService.ListDataItems  ` may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order.

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
  &quot;trainingFilter&quot;: string,
  &quot;validationFilter&quot;: string,
  &quot;testFilter&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## PredefinedSplit

Assigns input data to training, validation, and test sets based on the value of a provided key.

Supported only for tabular Datasets.

Fields

`key` `string`

Required. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { `training` , `validation` , `test` }, and it defines to which set the given piece of data is assigned. If for a piece of data the key is not present or has an invalid value, that piece is ignored by the pipeline.

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
  &quot;key&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TimestampSplit

Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

Fields

`trainingFraction` `number`

The fraction of the input data that is to be used to train the Model.

`validationFraction` `number`

The fraction of the input data that is to be used to validate the Model.

`testFraction` `number`

The fraction of the input data that is to be used to evaluate the Model.

`key` `string`

Required. The key is a name of one of the Dataset's data columns. The values of the key (the values in the column) must be in RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z). If for a piece of data the key is not present or has an invalid value, that piece is ignored by the pipeline.

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
  &quot;trainingFraction&quot;: number,
  &quot;validationFraction&quot;: number,
  &quot;testFraction&quot;: number,
  &quot;key&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## StratifiedSplit

Assigns input data to the training, validation, and test sets so that the distribution of values found in the categorical column (as specified by the `key` field) is mirrored within each split. The fraction values determine the relative sizes of the splits.

For example, if the specified column has three values, with 50% of the rows having value "A", 25% value "B", and 25% value "C", and the split fractions are specified as 80/10/10, then the training set will constitute 80% of the training data, with about 50% of the training set rows having the value "A" for the specified column, about 25% having the value "B", and about 25% having the value "C".

Only the top 500 occurring values are used; any values not in the top 500 values are randomly assigned to a split. If less than three rows contain a specific value, those rows are randomly assigned.

Supported only for tabular Datasets.

Fields

`trainingFraction` `number`

The fraction of the input data that is to be used to train the Model.

`validationFraction` `number`

The fraction of the input data that is to be used to validate the Model.

`testFraction` `number`

The fraction of the input data that is to be used to evaluate the Model.

`key` `string`

Required. The key is a name of one of the Dataset's data columns. The key provided must be for a categorical column.

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
  &quot;trainingFraction&quot;: number,
  &quot;validationFraction&quot;: number,
  &quot;testFraction&quot;: number,
  &quot;key&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            cancel           `

Cancels a TrainingPipeline.

### `            create           `

Creates a TrainingPipeline.

### `            delete           `

Deletes a TrainingPipeline.

### `            get           `

Gets a TrainingPipeline.

### `            list           `

Lists TrainingPipelines in a Location.
