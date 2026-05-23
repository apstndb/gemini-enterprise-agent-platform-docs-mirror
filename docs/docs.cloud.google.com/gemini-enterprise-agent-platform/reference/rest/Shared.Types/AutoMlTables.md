---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlTables
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlTables
title: AutoMlTables
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that trains and uploads an AutoML Tables Model.

Fields

`inputs` ` object ( AutoMlTablesInputs  ` )

The input parameters of this TrainingJob.

`metadata` ` object ( AutoMlTablesMetadata  ` )

The metadata information.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {object (AutoMlTablesInputs)},&quot;metadata&quot;: {object (AutoMlTablesMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlTablesInputs

Fields

`predictionType` `string`

The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings.

`targetColumn` `string`

The column name of the target column that the model is to predict.

`transformations[]` ` object ( Transformation  ` )

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter.

`optimizationObjective` `string`

Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set.

The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used.

classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value.

classification (multi-class): "minimize-log-loss" (default) - Minimize log loss.

regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE).

`trainBudgetMilliNodeHours` `string ( int64 format)`

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

`disableEarlyStopping` `boolean`

Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used.

`weightColumnName` `string`

column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

`exportEvaluatedDataItemsConfig` ` object ( ExportEvaluatedDataItemsConfig  ` )

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

`additionalExperiments[]` `string`

Additional experiment flags for the Tables training pipeline.

`additional_optimization_objective_config` `Union type`

Additional optimization objective configuration. Required for `maximize-precision-at-recall` and `maximize-recall-at-precision` , otherwise unused. `additional_optimization_objective_config` can be only one of the following:

`optimizationObjectiveRecallValue` `number`

Required when optimizationObjective is "maximize-precision-at-recall". Must be between 0 and 1, inclusive.

`optimizationObjectivePrecisionValue` `number`

Required when optimizationObjective is "maximize-recall-at-precision". Must be between 0 and 1, inclusive.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictionType&quot;: string,&quot;targetColumn&quot;: string,&quot;transformations&quot;: [{object (Transformation)}],&quot;optimizationObjective&quot;: string,&quot;trainBudgetMilliNodeHours&quot;: string,&quot;disableEarlyStopping&quot;: boolean,&quot;weightColumnName&quot;: string,&quot;exportEvaluatedDataItemsConfig&quot;: {object (ExportEvaluatedDataItemsConfig)},&quot;additionalExperiments&quot;: [string],// additional_optimization_objective_config&quot;optimizationObjectiveRecallValue&quot;: number,&quot;optimizationObjectivePrecisionValue&quot;: number// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Transformation

Fields

`transformation_detail` `Union type`

The transformation that the training pipeline will apply to the input columns. `transformation_detail` can be only one of the following:

`auto` ` object ( AutoTransformation  ` )

`numeric` ` object ( NumericTransformation  ` )

`categorical` ` object ( CategoricalTransformation  ` )

`timestamp` ` object ( TimestampTransformation  ` )

`text` ` object ( TextTransformation  ` )

`repeatedNumeric` ` object ( NumericArrayTransformation  ` )

`repeatedCategorical` ` object ( CategoricalArrayTransformation  ` )

`repeatedText` ` object ( TextArrayTransformation  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// transformation_detail&quot;auto&quot;: {object (AutoTransformation)},&quot;numeric&quot;: {object (NumericTransformation)},&quot;categorical&quot;: {object (CategoricalTransformation)},&quot;timestamp&quot;: {object (TimestampTransformation)},&quot;text&quot;: {object (TextTransformation)},&quot;repeatedNumeric&quot;: {object (NumericArrayTransformation)},&quot;repeatedCategorical&quot;: {object (CategoricalArrayTransformation)},&quot;repeatedText&quot;: {object (TextArrayTransformation)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AutoTransformation

Training pipeline will infer the proper transformation based on the statistic of dataset.

Fields

`columnName` `string`

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
  &quot;columnName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## NumericTransformation

Training pipeline will perform following transformation functions. \* The value converted to float32. \* The z\_score of the value. \* log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value. \* z\_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value. \* A boolean value that indicates whether the value is valid.

Fields

`columnName` `string`

`invalidValuesAllowed` `boolean`

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

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
  &quot;columnName&quot;: string,
  &quot;invalidValuesAllowed&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## CategoricalTransformation

Training pipeline will perform following transformation functions. \* The categorical string as is--no change to case, punctuation, spelling, tense, and so on. \* Convert the category name to a dictionary lookup index and generate an embedding for each index. \* Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Fields

`columnName` `string`

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
  &quot;columnName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TimestampTransformation

Training pipeline will perform following transformation functions. \* Apply the transformation functions for Numerical columns. \* Determine the year, month, day,and weekday. Treat each value from the \* timestamp as a Categorical column. \* Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

Fields

`columnName` `string`

`timeFormat` `string`

The format in which that time field is expressed. The timeFormat must either be one of: \* `unix-seconds` \* `unix-milliseconds` \* `unix-microseconds` \* `unix-nanoseconds` (for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch); or be written in `strftime` syntax. If timeFormat is not set, then the default format is RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z)

`invalidValuesAllowed` `boolean`

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

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
  &quot;columnName&quot;: string,
  &quot;timeFormat&quot;: string,
  &quot;invalidValuesAllowed&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## TextTransformation

Training pipeline will perform following transformation functions. \* The text as is--no change to case, punctuation, spelling, tense, and so on. \* Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean. \* Tokenization is based on unicode script boundaries. \* Missing values get their own lookup index and resulting embedding. \* Stop-words receive no special treatment and are not removed.

Fields

`columnName` `string`

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
  &quot;columnName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## NumericArrayTransformation

Treats the column as numerical array and performs following transformation functions. \* All transformations for Numerical types applied to the average of the all elements. \* The average of empty arrays is treated as zero.

Fields

`columnName` `string`

`invalidValuesAllowed` `boolean`

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

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
  &quot;columnName&quot;: string,
  &quot;invalidValuesAllowed&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## CategoricalArrayTransformation

Treats the column as categorical array and performs following transformation functions. \* For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean. \* Empty arrays treated as an embedding of zeroes.

Fields

`columnName` `string`

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
  &quot;columnName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TextArrayTransformation

Treats the column as text array and performs following transformation functions. \* Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns. \* Empty arrays treated as an empty text.

Fields

`columnName` `string`

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
  &quot;columnName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlTablesMetadata

Model metadata specific to AutoML Tables.

Fields

`trainCostMilliNodeHours` `string ( int64 format)`

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

`evaluatedDataItemsBigqueryUri` `string`

BigQuery destination uri for exported evaluated examples.

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
  &quot;trainCostMilliNodeHours&quot;: string,
  &quot;evaluatedDataItemsBigqueryUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
