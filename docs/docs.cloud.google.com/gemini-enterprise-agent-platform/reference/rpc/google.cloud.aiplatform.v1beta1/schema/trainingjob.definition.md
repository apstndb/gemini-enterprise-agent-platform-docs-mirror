---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/trainingjob.definition
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/trainingjob.definition
title: Package google.cloud.aiplatform.v1beta1.schema.trainingjob.definition
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  AutoMlForecasting  ` (message)
  - `  AutoMlForecastingInputs  ` (message)
  - `  AutoMlForecastingInputs.Granularity  ` (message)
  - `  AutoMlForecastingInputs.Transformation  ` (message)
  - `  AutoMlForecastingInputs.Transformation.AutoTransformation  ` (message)
  - `  AutoMlForecastingInputs.Transformation.CategoricalTransformation  ` (message)
  - `  AutoMlForecastingInputs.Transformation.NumericTransformation  ` (message)
  - `  AutoMlForecastingInputs.Transformation.TextTransformation  ` (message)
  - `  AutoMlForecastingInputs.Transformation.TimestampTransformation  ` (message)
  - `  AutoMlForecastingMetadata  ` (message)
  - `  AutoMlImageClassification  ` (message)
  - `  AutoMlImageClassificationInputs  ` (message)
  - `  AutoMlImageClassificationInputs.ModelType  ` (enum)
  - `  AutoMlImageClassificationMetadata  ` (message)
  - `  AutoMlImageClassificationMetadata.SuccessfulStopReason  ` (enum)
  - `  AutoMlImageObjectDetection  ` (message)
  - `  AutoMlImageObjectDetectionInputs  ` (message)
  - `  AutoMlImageObjectDetectionInputs.ModelType  ` (enum)
  - `  AutoMlImageObjectDetectionMetadata  ` (message)
  - `  AutoMlImageObjectDetectionMetadata.SuccessfulStopReason  ` (enum)
  - `  AutoMlImageSegmentation  ` (message)
  - `  AutoMlImageSegmentationInputs  ` (message)
  - `  AutoMlImageSegmentationInputs.ModelType  ` (enum)
  - `  AutoMlImageSegmentationMetadata  ` (message)
  - `  AutoMlImageSegmentationMetadata.SuccessfulStopReason  ` (enum)
  - `  AutoMlTables  ` (message)
  - `  AutoMlTablesInputs  ` (message)
  - `  AutoMlTablesInputs.Transformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.AutoTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.CategoricalArrayTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.CategoricalTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.NumericArrayTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.NumericTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.TextArrayTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.TextTransformation  ` (message)
  - `  AutoMlTablesInputs.Transformation.TimestampTransformation  ` (message)
  - `  AutoMlTablesMetadata  ` (message)
  - `  CustomJobMetadata  ` (message)
  - `  CustomTask  ` (message)
  - `  ExportEvaluatedDataItemsConfig  ` (message)
  - `  HierarchyConfig  ` (message)
  - `  HyperparameterTuningJobMetadata  ` (message)
  - `  HyperparameterTuningJobSpec  ` (message)
  - `  HyperparameterTuningTask  ` (message)
  - `  Seq2SeqPlusForecasting  ` (message)
  - `  Seq2SeqPlusForecastingInputs  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Granularity  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Transformation  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Transformation.AutoTransformation  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Transformation.CategoricalTransformation  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Transformation.NumericTransformation  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Transformation.TextTransformation  ` (message)
  - `  Seq2SeqPlusForecastingInputs.Transformation.TimestampTransformation  ` (message)
  - `  Seq2SeqPlusForecastingMetadata  ` (message)
  - `  TftForecasting  ` (message)
  - `  TftForecastingInputs  ` (message)
  - `  TftForecastingInputs.Granularity  ` (message)
  - `  TftForecastingInputs.Transformation  ` (message)
  - `  TftForecastingInputs.Transformation.AutoTransformation  ` (message)
  - `  TftForecastingInputs.Transformation.CategoricalTransformation  ` (message)
  - `  TftForecastingInputs.Transformation.NumericTransformation  ` (message)
  - `  TftForecastingInputs.Transformation.TextTransformation  ` (message)
  - `  TftForecastingInputs.Transformation.TimestampTransformation  ` (message)
  - `  TftForecastingMetadata  ` (message)
  - `  WindowConfig  ` (message)

## AutoMlForecasting

A TrainingJob that trains and uploads an AutoML Forecasting Model.

Fields

`inputs`

`  AutoMlForecastingInputs  `

The input parameters of this TrainingJob.

`metadata`

`  AutoMlForecastingMetadata  `

The metadata information.

## AutoMlForecastingInputs

Fields

`target_column`

`string`

The name of the column that the Model is to predict values for. This column must be unavailable at forecast.

`time_series_identifier_column`

`string`

The name of the column that identifies the time series.

`time_column`

`string`

The name of the column that identifies time order in the time series. This column must be available at forecast.

`transformations[]`

`  Transformation  `

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter.

`optimization_objective`

`string`

Objective function the model is optimizing towards. The training process creates a model that optimizes the value of the objective function over the validation set.

The supported optimization objectives:

  - "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE).

  - "minimize-mae" - Minimize mean-absolute error (MAE).

  - "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE).

  - "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE).

  - "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE).

  - "minimize-quantile-loss" - Minimize the quantile loss at the quantiles defined in `quantiles` .

  - "minimize-mape" - Minimize the mean absolute percentage error.

`train_budget_milli_node_hours`

`int64`

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

`weight_column`

`string`

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

`time_series_attribute_columns[]`

`string`

Column names that should be used as attribute columns. The value of these columns does not vary as a function of time. For example, store ID or item color.

`unavailable_at_forecast_columns[]`

`string`

Names of columns that are unavailable when a forecast is requested. This column contains information for the given entity (identified by the time\_series\_identifier\_column) that is unknown before the forecast For example, actual weather on a given day.

`available_at_forecast_columns[]`

`string`

Names of columns that are available and provided when a forecast is requested. These columns contain information for the given entity (identified by the time\_series\_identifier\_column column) that is known at forecast. For example, predicted weather for a specific day.

`data_granularity`

`  Granularity  `

Expected difference in time granularity between rows in the data.

`forecast_horizon`

`int64`

The amount of time into the future for which forecasted values for the target are returned. Expressed in number of units defined by the `data_granularity` field.

`context_window`

`int64`

The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the `data_granularity` field.

`export_evaluated_data_items_config`

`  ExportEvaluatedDataItemsConfig  `

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

`quantiles[]`

`double`

Quantiles to use for minimize-quantile-loss `optimization_objective` , or for probabilistic inference. Up to 5 quantiles are allowed of values between 0 and 1, exclusive. Required if the value of optimization\_objective is minimize-quantile-loss. Represents the percent quantiles to use for that objective. Quantiles must be unique.

`hierarchy_config`

`  HierarchyConfig  `

Configuration that defines the hierarchical relationship of time series and parameters for hierarchical forecasting strategies.

`window_config`

`  WindowConfig  `

Config containing strategy for generating sliding windows.

`holiday_regions[]`

`string`

The geographical region based on which the holiday effect is applied in modeling by adding holiday categorical array feature that include all holidays matching the date. This option only allowed when data\_granularity is day. By default, holiday effect modeling is disabled. To turn it on, specify the holiday region using this option.

`enable_probabilistic_inference`

`bool`

If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss.

`validation_options`

`string`

Validation options for the data validation component. The available options are:

  - "fail-pipeline" - default, will validate against the validation and fail the pipeline if it fails.

  - "ignore-validation" - ignore the results of the validation and continue

`additional_experiments[]`

`string`

Additional experiment flags for the time series forcasting training.

## Granularity

A duration of time expressed in time granularity units.

Fields

`unit`

`string`

The time granularity unit of this time period. The supported units are:

  - "minute"

  - "hour"

  - "day"

  - "week"

  - "month"

  - "year"

`quantity`

`int64`

The number of granularity\_units between data points in the training data. If `granularity_unit` is `minute` , can be 1, 5, 10, 15, or 30. For all other values of `granularity_unit` , must be 1.

## Transformation

Fields

Union field `transformation_detail` . The transformation that the training pipeline will apply to the input columns. `transformation_detail` can be only one of the following:

`auto`

`  AutoTransformation  `

`numeric`

`  NumericTransformation  `

`categorical`

`  CategoricalTransformation  `

`timestamp`

`  TimestampTransformation  `

`text`

`  TextTransformation  `

## AutoTransformation

Training pipeline will infer the proper transformation based on the statistic of dataset.

Fields

`column_name`

`string`

## CategoricalTransformation

Training pipeline will perform following transformation functions.

  - The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

  - Convert the category name to a dictionary lookup index and generate an embedding for each index.

  - Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Fields

`column_name`

`string`

## NumericTransformation

Training pipeline will perform following transformation functions.

  - The value converted to float32.

  - The z\_score of the value.

  - log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

  - z\_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

  - A boolean value that indicates whether the value is valid.

Fields

`column_name`

`string`

## TextTransformation

Training pipeline will perform following transformation functions.

  - The text as is--no change to case, punctuation, spelling, tense, and so on.

  - Convert the category name to a dictionary lookup index and generate an embedding for each index.

Fields

`column_name`

`string`

## TimestampTransformation

Training pipeline will perform following transformation functions.

  - Apply the transformation functions for Numerical columns.

  - Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

  - Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

Fields

`column_name`

`string`

`time_format`

`string`

The format in which that time field is expressed. The time\_format must either be one of:

  - `unix-seconds`

  - `unix-milliseconds`

  - `unix-microseconds`

  - `unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch);

or be written in `strftime` syntax.

If time\_format is not set, then the default format is RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z)

## AutoMlForecastingMetadata

Model metadata specific to AutoML Forecasting.

Fields

`train_cost_milli_node_hours`

`int64`

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

`evaluated_data_items_bigquery_uri`

`string`

BigQuery destination uri for exported evaluated examples.

## AutoMlImageClassification

A TrainingJob that trains and uploads an AutoML Image Classification Model.

Fields

`inputs`

`  AutoMlImageClassificationInputs  `

The input parameters of this TrainingJob.

`metadata`

`  AutoMlImageClassificationMetadata  `

The metadata information.

## AutoMlImageClassificationInputs

Fields

`model_type`

`  ModelType  `

`base_model_id`

`string`

The ID of the `base` model. If it is specified, the new model will be trained based on the `base` model. Otherwise, the new model will be trained from scratch. The `base` model must be in the same Project and Location as the new Model to train, and have the same modelType.

`budget_milli_node_hours`

`int64`

The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node\_hour = actual\_hour \* number\_of\_nodes\_involved. For modelType `cloud` (default), the budget must be between 8,000 and 800,000 milli node hours, inclusive. The default value is 192,000 which represents one day in wall time, considering 8 nodes are used. For model types `mobile-tf-low-latency-1` , `mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` , the training budget must be between 1,000 and 100,000 milli node hours, inclusive. The default value is 24,000 which represents one day in wall time on a single node that is used.

`disable_early_stopping`

`bool`

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used.

`multi_label`

`bool`

If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable).

`uptrain_base_model_id`

`string`

The ID of `base` model for upTraining. If it is specified, the new model will be upTrained based on the `base` model for upTraining. Otherwise, the new model will be trained from scratch. The `base` model for upTraining must be in the same Project and Location as the new Model to train, and have the same modelType.

## ModelType

Enums

`MODEL_TYPE_UNSPECIFIED`

Should not be set.

`CLOUD`

A Model best tailored to be used within Google Cloud, and which cannot be exported. Default.

`CLOUD_1`

A model type best tailored to be used within Google Cloud, which cannot be exported externally. Compared to the CLOUD model above, it is expected to have higher prediction accuracy.

`MOBILE_TF_LOW_LATENCY_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

`MOBILE_TF_VERSATILE_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device with afterwards.

`MOBILE_TF_HIGH_ACCURACY_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

## AutoMlImageClassificationMetadata

Fields

`cost_milli_node_hours`

`int64`

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

`successful_stop_reason`

`  SuccessfulStopReason  `

For successful job completions, this is the reason why the job has finished.

## SuccessfulStopReason

Enums

`SUCCESSFUL_STOP_REASON_UNSPECIFIED`

Should not be set.

`BUDGET_REACHED`

The inputs.budgetMilliNodeHours had been reached.

`MODEL_CONVERGED`

Further training of the Model ceased to increase its quality, since it already has converged.

## AutoMlImageObjectDetection

A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

Fields

`inputs`

`  AutoMlImageObjectDetectionInputs  `

The input parameters of this TrainingJob.

`metadata`

`  AutoMlImageObjectDetectionMetadata  `

The metadata information

## AutoMlImageObjectDetectionInputs

Fields

`model_type`

`  ModelType  `

`budget_milli_node_hours`

`int64`

The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node\_hour = actual\_hour \* number\_of\_nodes\_involved. For modelType `cloud` (default), the budget must be between 20,000 and 900,000 milli node hours, inclusive. The default value is 216,000 which represents one day in wall time, considering 9 nodes are used. For model types `mobile-tf-low-latency-1` , `mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the training budget must be between 1,000 and 100,000 milli node hours, inclusive. The default value is 24,000 which represents one day in wall time on a single node that is used.

`disable_early_stopping`

`bool`

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used.

`uptrain_base_model_id`

`string`

The ID of `base` model for upTraining. If it is specified, the new model will be upTrained based on the `base` model for upTraining. Otherwise, the new model will be trained from scratch. The `base` model for upTraining must be in the same Project and Location as the new Model to train, and have the same modelType.

## ModelType

Enums

`MODEL_TYPE_UNSPECIFIED`

Should not be set.

`CLOUD_HIGH_ACCURACY_1`

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a higher latency, but should also have a higher prediction quality than other cloud models.

`CLOUD_LOW_LATENCY_1`

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a low latency, but may have lower prediction quality than other cloud models.

`CLOUD_1`

A model best tailored to be used within Google Cloud, and which cannot be exported. Compared to the CLOUD\_HIGH\_ACCURACY\_1 and CLOUD\_LOW\_LATENCY\_1 models above, it is expected to have higher prediction quality and lower latency.

`MOBILE_TF_LOW_LATENCY_1`

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

`MOBILE_TF_VERSATILE_1`

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards.

`MOBILE_TF_HIGH_ACCURACY_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

`CLOUD_STREAMING_1`

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to best support predictions in streaming with lower latency and lower prediction quality than other cloud models.

## AutoMlImageObjectDetectionMetadata

Fields

`cost_milli_node_hours`

`int64`

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

`successful_stop_reason`

`  SuccessfulStopReason  `

For successful job completions, this is the reason why the job has finished.

## SuccessfulStopReason

Enums

`SUCCESSFUL_STOP_REASON_UNSPECIFIED`

Should not be set.

`BUDGET_REACHED`

The inputs.budgetMilliNodeHours had been reached.

`MODEL_CONVERGED`

Further training of the Model ceased to increase its quality, since it already has converged.

## AutoMlImageSegmentation

A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

Fields

`inputs`

`  AutoMlImageSegmentationInputs  `

The input parameters of this TrainingJob.

`metadata`

`  AutoMlImageSegmentationMetadata  `

The metadata information.

## AutoMlImageSegmentationInputs

Fields

`model_type`

`  ModelType  `

`budget_milli_node_hours`

`int64`

The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node\_hour = actual\_hour \* number\_of\_nodes\_involved. Or actual\_wall\_clock\_hours = train\_budget\_milli\_node\_hours / (number\_of\_nodes\_involved \* 1000) For modelType `cloud-high-accuracy-1` (default), the budget must be between 20,000 and 2,000,000 milli node hours, inclusive. The default value is 192,000 which represents one day in wall time (1000 milli \* 24 hours \* 8 nodes).

`base_model_id`

`string`

The ID of the `base` model. If it is specified, the new model will be trained based on the `base` model. Otherwise, the new model will be trained from scratch. The `base` model must be in the same Project and Location as the new Model to train, and have the same modelType.

## ModelType

Enums

`MODEL_TYPE_UNSPECIFIED`

Should not be set.

`CLOUD_HIGH_ACCURACY_1`

A model to be used via prediction calls to uCAIP API. Expected to have a higher latency, but should also have a higher prediction quality than other models.

`CLOUD_LOW_ACCURACY_1`

A model to be used via prediction calls to uCAIP API. Expected to have a lower latency but relatively lower prediction quality.

`MOBILE_TF_LOW_LATENCY_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

## AutoMlImageSegmentationMetadata

Fields

`cost_milli_node_hours`

`int64`

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

`successful_stop_reason`

`  SuccessfulStopReason  `

For successful job completions, this is the reason why the job has finished.

## SuccessfulStopReason

Enums

`SUCCESSFUL_STOP_REASON_UNSPECIFIED`

Should not be set.

`BUDGET_REACHED`

The inputs.budgetMilliNodeHours had been reached.

`MODEL_CONVERGED`

Further training of the Model ceased to increase its quality, since it already has converged.

## AutoMlTables

A TrainingJob that trains and uploads an AutoML Tables Model.

Fields

`inputs`

`  AutoMlTablesInputs  `

The input parameters of this TrainingJob.

`metadata`

`  AutoMlTablesMetadata  `

The metadata information.

## AutoMlTablesInputs

Fields

`prediction_type`

`string`

The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings.

`target_column`

`string`

The column name of the target column that the model is to predict.

`transformations[]`

`  Transformation  `

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter.

`optimization_objective`

`string`

Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set.

The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used.

classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value.

classification (multi-class): "minimize-log-loss" (default) - Minimize log loss.

regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE).

`train_budget_milli_node_hours`

`int64`

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

`disable_early_stopping`

`bool`

Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used.

`weight_column_name`

`string`

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

`export_evaluated_data_items_config`

`  ExportEvaluatedDataItemsConfig  `

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

`additional_experiments[]`

`string`

Additional experiment flags for the Tables training pipeline.

Union field `additional_optimization_objective_config` . Additional optimization objective configuration. Required for `maximize-precision-at-recall` and `maximize-recall-at-precision` , otherwise unused. `additional_optimization_objective_config` can be only one of the following:

`optimization_objective_recall_value`

`float`

Required when optimization\_objective is "maximize-precision-at-recall". Must be between 0 and 1, inclusive.

`optimization_objective_precision_value`

`float`

Required when optimization\_objective is "maximize-recall-at-precision". Must be between 0 and 1, inclusive.

## Transformation

Fields

Union field `transformation_detail` . The transformation that the training pipeline will apply to the input columns. `transformation_detail` can be only one of the following:

`auto`

`  AutoTransformation  `

`numeric`

`  NumericTransformation  `

`categorical`

`  CategoricalTransformation  `

`timestamp`

`  TimestampTransformation  `

`text`

`  TextTransformation  `

`repeated_numeric`

`  NumericArrayTransformation  `

`repeated_categorical`

`  CategoricalArrayTransformation  `

`repeated_text`

`  TextArrayTransformation  `

## AutoTransformation

Training pipeline will infer the proper transformation based on the statistic of dataset.

Fields

`column_name`

`string`

## CategoricalArrayTransformation

Treats the column as categorical array and performs following transformation functions. \* For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean. \* Empty arrays treated as an embedding of zeroes.

Fields

`column_name`

`string`

## CategoricalTransformation

Training pipeline will perform following transformation functions. \* The categorical string as is--no change to case, punctuation, spelling, tense, and so on. \* Convert the category name to a dictionary lookup index and generate an embedding for each index. \* Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Fields

`column_name`

`string`

## NumericArrayTransformation

Treats the column as numerical array and performs following transformation functions. \* All transformations for Numerical types applied to the average of the all elements. \* The average of empty arrays is treated as zero.

Fields

`column_name`

`string`

`invalid_values_allowed`

`bool`

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

## NumericTransformation

Training pipeline will perform following transformation functions. \* The value converted to float32. \* The z\_score of the value. \* log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value. \* z\_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value. \* A boolean value that indicates whether the value is valid.

Fields

`column_name`

`string`

`invalid_values_allowed`

`bool`

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

## TextArrayTransformation

Treats the column as text array and performs following transformation functions. \* Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns. \* Empty arrays treated as an empty text.

Fields

`column_name`

`string`

## TextTransformation

Training pipeline will perform following transformation functions. \* The text as is--no change to case, punctuation, spelling, tense, and so on. \* Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean. \* Tokenization is based on unicode script boundaries. \* Missing values get their own lookup index and resulting embedding. \* Stop-words receive no special treatment and are not removed.

Fields

`column_name`

`string`

## TimestampTransformation

Training pipeline will perform following transformation functions. \* Apply the transformation functions for Numerical columns. \* Determine the year, month, day,and weekday. Treat each value from the \* timestamp as a Categorical column. \* Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

Fields

`column_name`

`string`

`time_format`

`string`

The format in which that time field is expressed. The time\_format must either be one of: \* `unix-seconds` \* `unix-milliseconds` \* `unix-microseconds` \* `unix-nanoseconds` (for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch); or be written in `strftime` syntax. If time\_format is not set, then the default format is RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z)

`invalid_values_allowed`

`bool`

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

## AutoMlTablesMetadata

Model metadata specific to AutoML Tables.

Fields

`train_cost_milli_node_hours`

`int64`

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

`evaluated_data_items_bigquery_uri`

`string`

BigQuery destination uri for exported evaluated examples.

## CustomJobMetadata

Fields

`backing_custom_job`

`string`

The resource name of the CustomJob that has been created to carry out this custom task.

## CustomTask

A TrainingJob that trains a custom code Model.

Fields

`inputs`

`  CustomJobSpec  `

The input parameters of this CustomTask.

`metadata`

`  CustomJobMetadata  `

The metadata information.

## ExportEvaluatedDataItemsConfig

Configuration for exporting test set predictions to a BigQuery table.

Fields

`destination_bigquery_uri`

`string`

URI of desired destination BigQuery table. Expected format: `bq://{project_id}:{dataset_id}:{table}`

If not specified, then results are exported to the following auto-created BigQuery table: `{project_id}:export_evaluated_examples_{model_name}_{yyyy_MM_dd'T'HH_mm_ss_SSS'Z'}.evaluated_examples`

`override_existing_table`

`bool`

If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails.

## HierarchyConfig

Configuration that defines the hierarchical relationship of time series and parameters for hierarchical forecasting strategies.

Fields

`group_columns[]`

`string`

A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. 'region' for a hierarchy of stores or 'department' for a hierarchy of products. If multiple columns are specified, time series will be grouped by their combined values, ex. ('blue', 'large') for 'color' and 'size', up to 5 columns are accepted. If no group columns are specified, all time series are considered to be part of the same group.

`group_total_weight`

`double`

The weight of the loss for predictions aggregated over time series in the same group.

`temporal_total_weight`

`double`

The weight of the loss for predictions aggregated over the horizon for a single time series.

`group_temporal_total_weight`

`double`

The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group.

## HyperparameterTuningJobMetadata

Fields

`backing_hyperparameter_tuning_job`

`string`

The resource name of the HyperparameterTuningJob that has been created to carry out this HyperparameterTuning task.

`best_trial_backing_custom_job`

`string`

The resource name of the CustomJob that has been created to run the best Trial of this HyperparameterTuning task.

## HyperparameterTuningJobSpec

Fields

`study_spec`

`  StudySpec  `

Study configuration of the HyperparameterTuningJob.

`trial_job_spec`

`  CustomJobSpec  `

The spec of a trial job. The same spec applies to the CustomJobs created in all the trials.

`max_trial_count`

`int32`

The desired total number of Trials.

`parallel_trial_count`

`int32`

The desired number of Trials to run in parallel.

`max_failed_trial_count`

`int32`

The number of failed Trials that need to be seen before failing the HyperparameterTuningJob.

If set to 0, Agent Platform decides how many Trials must fail before the whole job fails.

## HyperparameterTuningTask

A TrainingJob that tunes Hypererparameters of a custom code Model.

Fields

`inputs`

`  HyperparameterTuningJobSpec  `

The input parameters of this HyperparameterTuningTask.

`metadata`

`  HyperparameterTuningJobMetadata  `

The metadata information.

## Seq2SeqPlusForecasting

A TrainingJob that trains and uploads an AutoML Forecasting Model.

Fields

`inputs`

`  Seq2SeqPlusForecastingInputs  `

The input parameters of this TrainingJob.

`metadata`

`  Seq2SeqPlusForecastingMetadata  `

The metadata information.

## Seq2SeqPlusForecastingInputs

Fields

`target_column`

`string`

The name of the column that the Model is to predict values for. This column must be unavailable at forecast.

`time_series_identifier_column`

`string`

The name of the column that identifies the time series.

`time_column`

`string`

The name of the column that identifies time order in the time series. This column must be available at forecast.

`transformations[]`

`  Transformation  `

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter.

`optimization_objective`

`string`

Objective function the model is optimizing towards. The training process creates a model that optimizes the value of the objective function over the validation set.

The supported optimization objectives:

  - "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE).

  - "minimize-mae" - Minimize mean-absolute error (MAE).

  - "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE).

  - "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE).

  - "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE).

  - "minimize-quantile-loss" - Minimize the quantile loss at the quantiles defined in `quantiles` .

  - "minimize-mape" - Minimize the mean absolute percentage error.

`train_budget_milli_node_hours`

`int64`

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

`weight_column`

`string`

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. This column must be available at forecast.

`time_series_attribute_columns[]`

`string`

Column names that should be used as attribute columns. The value of these columns does not vary as a function of time. For example, store ID or item color.

`unavailable_at_forecast_columns[]`

`string`

Names of columns that are unavailable when a forecast is requested. This column contains information for the given entity (identified by the time\_series\_identifier\_column) that is unknown before the forecast For example, actual weather on a given day.

`available_at_forecast_columns[]`

`string`

Names of columns that are available and provided when a forecast is requested. These columns contain information for the given entity (identified by the time\_series\_identifier\_column column) that is known at forecast. For example, predicted weather for a specific day.

`data_granularity`

`  Granularity  `

Expected difference in time granularity between rows in the data.

`forecast_horizon`

`int64`

The amount of time into the future for which forecasted values for the target are returned. Expressed in number of units defined by the `data_granularity` field.

`context_window`

`int64`

The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the `data_granularity` field.

`holiday_regions[]`

`string`

The geographical region based on which the holiday effect is applied in modeling by adding holiday categorical array feature that include all holidays matching the date. This option only allowed when data\_granularity is day. By default, holiday effect modeling is disabled. To turn it on, specify the holiday region using this option.

`export_evaluated_data_items_config`

`  ExportEvaluatedDataItemsConfig  `

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

`window_config`

`  WindowConfig  `

Config containing strategy for generating sliding windows.

`quantiles[]`

`double`

Quantiles to use for minimize-quantile-loss `optimization_objective` . Up to 5 quantiles are allowed of values between 0 and 1, exclusive. Required if the value of optimization\_objective is minimize-quantile-loss. Represents the percent quantiles to use for that objective. Quantiles must be unique.

`validation_options`

`string`

Validation options for the data validation component. The available options are:

  - "fail-pipeline" - default, will validate against the validation and fail the pipeline if it fails.

  - "ignore-validation" - ignore the results of the validation and continue

`additional_experiments[]`

`string`

Additional experiment flags for the time series forcasting training.

`hierarchy_config`

`  HierarchyConfig  `

Configuration that defines the hierarchical relationship of time series and parameters for hierarchical forecasting strategies.

## Granularity

A duration of time expressed in time granularity units.

Fields

`unit`

`string`

The time granularity unit of this time period. The supported units are:

  - "minute"

  - "hour"

  - "day"

  - "week"

  - "month"

  - "year"

`quantity`

`int64`

The number of granularity\_units between data points in the training data. If `granularity_unit` is `minute` , can be 1, 5, 10, 15, or 30. For all other values of `granularity_unit` , must be 1.

## Transformation

Fields

Union field `transformation_detail` . The transformation that the training pipeline will apply to the input columns. `transformation_detail` can be only one of the following:

`auto`

`  AutoTransformation  `

`numeric`

`  NumericTransformation  `

`categorical`

`  CategoricalTransformation  `

`timestamp`

`  TimestampTransformation  `

`text`

`  TextTransformation  `

## AutoTransformation

Training pipeline will infer the proper transformation based on the statistic of dataset.

Fields

`column_name`

`string`

## CategoricalTransformation

Training pipeline will perform following transformation functions.

  - The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

  - Convert the category name to a dictionary lookup index and generate an embedding for each index.

  - Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Fields

`column_name`

`string`

## NumericTransformation

Training pipeline will perform following transformation functions.

  - The value converted to float32.

  - The z\_score of the value.

  - log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

  - z\_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

Fields

`column_name`

`string`

## TextTransformation

Training pipeline will perform following transformation functions.

  - The text as is--no change to case, punctuation, spelling, tense, and so on.

  - Convert the category name to a dictionary lookup index and generate an embedding for each index.

Fields

`column_name`

`string`

## TimestampTransformation

Training pipeline will perform following transformation functions.

  - Apply the transformation functions for Numerical columns.

  - Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

  - Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

Fields

`column_name`

`string`

`time_format`

`string`

The format in which that time field is expressed. The time\_format must either be one of:

  - `unix-seconds`

  - `unix-milliseconds`

  - `unix-microseconds`

  - `unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch);

or be written in `strftime` syntax.

If time\_format is not set, then the default format is RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z)

## Seq2SeqPlusForecastingMetadata

Model metadata specific to Seq2Seq Plus Forecasting.

Fields

`train_cost_milli_node_hours`

`int64`

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

`evaluated_data_items_bigquery_uri`

`string`

BigQuery destination uri for exported evaluated examples.

## TftForecasting

A TrainingJob that trains and uploads an AutoML Forecasting Model.

Fields

`inputs`

`  TftForecastingInputs  `

The input parameters of this TrainingJob.

`metadata`

`  TftForecastingMetadata  `

The metadata information.

## TftForecastingInputs

Fields

`target_column`

`string`

The name of the column that the Model is to predict values for. This column must be unavailable at forecast.

`time_series_identifier_column`

`string`

The name of the column that identifies the time series.

`time_column`

`string`

The name of the column that identifies time order in the time series. This column must be available at forecast.

`transformations[]`

`  Transformation  `

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter.

`optimization_objective`

`string`

Objective function the model is optimizing towards. The training process creates a model that optimizes the value of the objective function over the validation set.

The supported optimization objectives:

  - "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE).

  - "minimize-mae" - Minimize mean-absolute error (MAE).

  - "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE).

  - "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE).

  - "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE).

  - "minimize-quantile-loss" - Minimize the quantile loss at the quantiles defined in `quantiles` .

  - "minimize-mape" - Minimize the mean absolute percentage error.

`train_budget_milli_node_hours`

`int64`

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

`weight_column`

`string`

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. This column must be available at forecast.

`time_series_attribute_columns[]`

`string`

Column names that should be used as attribute columns. The value of these columns does not vary as a function of time. For example, store ID or item color.

`unavailable_at_forecast_columns[]`

`string`

Names of columns that are unavailable when a forecast is requested. This column contains information for the given entity (identified by the time\_series\_identifier\_column) that is unknown before the forecast For example, actual weather on a given day.

`available_at_forecast_columns[]`

`string`

Names of columns that are available and provided when a forecast is requested. These columns contain information for the given entity (identified by the time\_series\_identifier\_column column) that is known at forecast. For example, predicted weather for a specific day.

`data_granularity`

`  Granularity  `

Expected difference in time granularity between rows in the data.

`forecast_horizon`

`int64`

The amount of time into the future for which forecasted values for the target are returned. Expressed in number of units defined by the `data_granularity` field.

`context_window`

`int64`

The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the `data_granularity` field.

`holiday_regions[]`

`string`

The geographical region based on which the holiday effect is applied in modeling by adding holiday categorical array feature that include all holidays matching the date. This option only allowed when data\_granularity is day. By default, holiday effect modeling is disabled. To turn it on, specify the holiday region using this option.

`export_evaluated_data_items_config`

`  ExportEvaluatedDataItemsConfig  `

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

`window_config`

`  WindowConfig  `

Config containing strategy for generating sliding windows.

`quantiles[]`

`double`

Quantiles to use for minimize-quantile-loss `optimization_objective` . Up to 5 quantiles are allowed of values between 0 and 1, exclusive. Required if the value of optimization\_objective is minimize-quantile-loss. Represents the percent quantiles to use for that objective. Quantiles must be unique.

`validation_options`

`string`

Validation options for the data validation component. The available options are:

  - "fail-pipeline" - default, will validate against the validation and fail the pipeline if it fails.

  - "ignore-validation" - ignore the results of the validation and continue

`additional_experiments[]`

`string`

Additional experiment flags for the time series forcasting training.

`hierarchy_config`

`  HierarchyConfig  `

Configuration that defines the hierarchical relationship of time series and parameters for hierarchical forecasting strategies.

## Granularity

A duration of time expressed in time granularity units.

Fields

`unit`

`string`

The time granularity unit of this time period. The supported units are:

  - "minute"

  - "hour"

  - "day"

  - "week"

  - "month"

  - "year"

`quantity`

`int64`

The number of granularity\_units between data points in the training data. If `granularity_unit` is `minute` , can be 1, 5, 10, 15, or 30. For all other values of `granularity_unit` , must be 1.

## Transformation

Fields

Union field `transformation_detail` . The transformation that the training pipeline will apply to the input columns. `transformation_detail` can be only one of the following:

`auto`

`  AutoTransformation  `

`numeric`

`  NumericTransformation  `

`categorical`

`  CategoricalTransformation  `

`timestamp`

`  TimestampTransformation  `

`text`

`  TextTransformation  `

## AutoTransformation

Training pipeline will infer the proper transformation based on the statistic of dataset.

Fields

`column_name`

`string`

## CategoricalTransformation

Training pipeline will perform following transformation functions.

  - The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

  - Convert the category name to a dictionary lookup index and generate an embedding for each index.

  - Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Fields

`column_name`

`string`

## NumericTransformation

Training pipeline will perform following transformation functions.

  - The value converted to float32.

  - The z\_score of the value.

  - log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

  - z\_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

Fields

`column_name`

`string`

## TextTransformation

Training pipeline will perform following transformation functions.

  - The text as is--no change to case, punctuation, spelling, tense, and so on.

  - Convert the category name to a dictionary lookup index and generate an embedding for each index.

Fields

`column_name`

`string`

## TimestampTransformation

Training pipeline will perform following transformation functions.

  - Apply the transformation functions for Numerical columns.

  - Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

  - Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

Fields

`column_name`

`string`

`time_format`

`string`

The format in which that time field is expressed. The time\_format must either be one of:

  - `unix-seconds`

  - `unix-milliseconds`

  - `unix-microseconds`

  - `unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch);

or be written in `strftime` syntax.

If time\_format is not set, then the default format is RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z)

## TftForecastingMetadata

Model metadata specific to TFT Forecasting.

Fields

`train_cost_milli_node_hours`

`int64`

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

`evaluated_data_items_bigquery_uri`

`string`

BigQuery destination uri for exported evaluated examples.

## WindowConfig

Config that contains the strategy used to generate sliding windows in time series training. A window is a series of rows that comprise the context up to the time of prediction, and the horizon following. The corresponding row for each window marks the start of the forecast horizon. Each window is used as an input example for training/evaluation.

Fields

Union field `strategy` .

`strategy` can be only one of the following:

`column`

`string`

Name of the column that should be used to generate sliding windows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window with the horizon starting at that row. The column will not be used as a feature in training.

`stride_length`

`int64`

Stride length used to generate input examples. Within one time series, every {$STRIDE\_LENGTH} rows will be used to generate a sliding window.

`max_count`

`int64`

Maximum number of windows that should be generated across all time series.
