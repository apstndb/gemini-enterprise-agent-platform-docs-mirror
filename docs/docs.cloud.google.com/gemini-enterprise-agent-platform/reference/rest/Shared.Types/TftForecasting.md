---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting
title: TftForecasting
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that trains and uploads an AutoML Forecasting Model.

Fields

`inputs` `object ( `[`TftForecastingInputs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#TftForecastingInputs)` )`

The input parameters of this TrainingJob.

`metadata` `object ( `[`TftForecastingMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#TftForecastingMetadata)` )`

The metadata information.

**JSON representation**

```
{
  "inputs": {
    object (TftForecastingInputs)
  },
  "metadata": {
    object (TftForecastingMetadata)
  }
}
```

## TftForecastingInputs

Fields

`targetColumn` `string`

The name of the column that the Model is to predict values for. This column must be unavailable at forecast.

`timeSeriesIdentifierColumn` `string`

The name of the column that identifies the time series.

`timeColumn` `string`

The name of the column that identifies time order in the time series. This column must be available at forecast.

`transformations[]` `object ( `[`Transformation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#Transformation)` )`

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter.

`optimizationObjective` `string`

Objective function the model is optimizing towards. The training process creates a model that optimizes the value of the objective function over the validation set.

The supported optimization objectives:

- "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE).

- "minimize-mae" - Minimize mean-absolute error (MAE).

- "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE).

- "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE).

- "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE).

- "minimize-quantile-loss" - Minimize the quantile loss at the quantiles defined in `quantiles` .

- "minimize-mape" - Minimize the mean absolute percentage error.

`trainBudgetMilliNodeHours` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

`weightColumn` `string`

column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. This column must be available at forecast.

`timeSeriesAttributeColumns[]` `string`

column names that should be used as attribute columns. The value of these columns does not vary as a function of time. For example, store id or item color.

`unavailableAtForecastColumns[]` `string`

Names of columns that are unavailable when a forecast is requested. This column contains information for the given entity (identified by the timeSeriesIdentifierColumn) that is unknown before the forecast For example, actual weather on a given day.

`availableAtForecastColumns[]` `string`

Names of columns that are available and provided when a forecast is requested. These columns contain information for the given entity (identified by the timeSeriesIdentifierColumn column) that is known at forecast. For example, predicted weather for a specific day.

`dataGranularity` `object ( `[`Granularity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#Granularity)` )`

Expected difference in time granularity between rows in the data.

`forecastHorizon` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The amount of time into the future for which forecasted values for the target are returned. Expressed in number of units defined by the `dataGranularity` field.

`contextWindow` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the `dataGranularity` field.

`holidayRegions[]` `string`

The geographical region based on which the holiday effect is applied in modeling by adding holiday categorical array feature that include all holidays matching the date. This option only allowed when dataGranularity is day. By default, holiday effect modeling is disabled. To turn it on, specify the holiday region using this option.

`exportEvaluatedDataItemsConfig` `object ( ``ExportEvaluatedDataItemsConfig`` )`

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

`windowConfig` `object ( ``WindowConfig`` )`

Config containing strategy for generating sliding windows.

`quantiles[]` `number`

Quantiles to use for minimize-quantile-loss `optimizationObjective` . Up to 5 quantiles are allowed of values between 0 and 1, exclusive. Required if the value of optimizationObjective is minimize-quantile-loss. Represents the percent quantiles to use for that objective. Quantiles must be unique.

`validationOptions` `string`

Validation options for the data validation component. The available options are:

- "fail-pipeline" - default, will validate against the validation and fail the pipeline if it fails.

- "ignore-validation" - ignore the results of the validation and continue

`additionalExperiments[]` `string`

Additional experiment flags for the time series forcasting training.

`hierarchyConfig` `object ( ``HierarchyConfig`` )`

Configuration that defines the hierarchical relationship of time series and parameters for hierarchical forecasting strategies.

**JSON representation**

```
{
  "targetColumn": string,
  "timeSeriesIdentifierColumn": string,
  "timeColumn": string,
  "transformations": [
    {
      object (Transformation)
    }
  ],
  "optimizationObjective": string,
  "trainBudgetMilliNodeHours": string,
  "weightColumn": string,
  "timeSeriesAttributeColumns": [
    string
  ],
  "unavailableAtForecastColumns": [
    string
  ],
  "availableAtForecastColumns": [
    string
  ],
  "dataGranularity": {
    object (Granularity)
  },
  "forecastHorizon": string,
  "contextWindow": string,
  "holidayRegions": [
    string
  ],
  "exportEvaluatedDataItemsConfig": {
    object (ExportEvaluatedDataItemsConfig)
  },
  "windowConfig": {
    object (WindowConfig)
  },
  "quantiles": [
    number
  ],
  "validationOptions": string,
  "additionalExperiments": [
    string
  ],
  "hierarchyConfig": {
    object (HierarchyConfig)
  }
}
```

## Transformation

Fields

`transformation_detail` `Union type`

The transformation that the training pipeline will apply to the input columns. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`auto` `object ( `[`AutoTransformation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#AutoTransformation)` )`

`numeric` `object ( `[`NumericTransformation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#NumericTransformation)` )`

`categorical` `object ( `[`CategoricalTransformation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#CategoricalTransformation)` )`

`timestamp` `object ( `[`TimestampTransformation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#TimestampTransformation)` )`

`text` `object ( `[`TextTransformation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftForecasting#TextTransformation)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // transformation_detail
  "auto": {
    object (AutoTransformation)
  },
  "numeric": {
    object (NumericTransformation)
  },
  "categorical": {
    object (CategoricalTransformation)
  },
  "timestamp": {
    object (TimestampTransformation)
  },
  "text": {
    object (TextTransformation)
  }
  // Union type
}
```

## AutoTransformation

Training pipeline will infer the proper transformation based on the statistic of dataset.

Fields

`columnName` `string`

**JSON representation**

```
{
  "columnName": string
}
```

## NumericTransformation

Training pipeline will perform following transformation functions.

- The value converted to float32.

- The z_score of the value.

- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

- z_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

Fields

`columnName` `string`

**JSON representation**

```
{
  "columnName": string
}
```

## CategoricalTransformation

Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

- Convert the category name to a dictionary lookup index and generate an embedding for each index.

- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Fields

`columnName` `string`

**JSON representation**

```
{
  "columnName": string
}
```

## TimestampTransformation

Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.

- Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

Fields

`columnName` `string`

`timeFormat` `string`

The format in which that time field is expressed. The timeFormat must either be one of:

- `unix-seconds`

- `unix-milliseconds`

- `unix-microseconds`

- `unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch);

or be written in `strftime` syntax.

If timeFormat is not set, then the default format is RFC 3339 `date-time` format, where `time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z)

**JSON representation**

```
{
  "columnName": string,
  "timeFormat": string
}
```

## TextTransformation

Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.

- Convert the category name to a dictionary lookup index and generate an embedding for each index.

Fields

`columnName` `string`

**JSON representation**

```
{
  "columnName": string
}
```

## Granularity

A duration of time expressed in time granularity units.

Fields

`unit` `string`

The time granularity unit of this time period. The supported units are:

- "minute"

- "hour"

- "day"

- "week"

- "month"

- "year"

`quantity` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of granularity_units between data points in the training data. If `granularity_unit` is `minute` , can be 1, 5, 10, 15, or 30. For all other values of `granularity_unit` , must be 1.

**JSON representation**

```
{
  "unit": string,
  "quantity": string
}
```

## TftForecastingMetadata

Model metadata specific to TFT Forecasting.

Fields

`trainCostMilliNodeHours` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

`evaluatedDataItemsBigqueryUri` `string`

BigQuery destination uri for exported evaluated examples.

**JSON representation**

```
{
  "trainCostMilliNodeHours": string,
  "evaluatedDataItemsBigqueryUri": string
}
```
