---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters
title: Training parameters for forecast models
description: Learn about the parameters used in forecast model training in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page provides detailed information about the parameters used in forecast model training. To learn how to train a forecast model, see [Train a forecast model](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/train-model) and [Train a model with Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting-train) .

## Model training methods

Choose between the following methods for training your model:

**Time series Dense Encoder (TiDE)** : Optimized dense [DNN](https://developers.google.com/machine-learning/glossary#deep-neural-network) -based encoder-decoder model. Great model quality with fast training and inference, especially for long contexts and horizons. [Learn more](https://arxiv.org/abs/2304.08424) .

**Temporal Fusion Transformer (TFT)** : Attention-based [DNN](https://developers.google.com/machine-learning/glossary#deep-neural-network) model designed to produce high accuracy and interpretability by aligning the model with the general multi-horizon forecasting task. [Learn more](https://ai.googleblog.com/2021/12/interpretable-deep-learning-for-time.html) .

**AutoML (L2L)** : A good choice for a wide range of use cases. [Learn more](https://ai.googleblog.com/2020/12/using-automl-for-time-series-forecasting.html) .

**Seq2Seq+** : A good choice for experimentation. The algorithm is likely to converge faster than AutoML because its architecture is simpler and it uses a smaller search space. Our experiments find that Seq2Seq+ performs well with a small time budget and on datasets smaller than 1 GB in size.

## Feature type and availability at forecast

Every column used for training a forecasting model must have a type: *attribute* or *covariate* . Covariates are further designated as available or unavailable at forecast time.

Series type

Available at forecast time

Description

Examples

API fields

Attribute

Available

An attribute is a static feature that does not change with time.

Item color, product description.

`time_series_attribute_columns`

Covariate

Available

An exogenous variable that is expected to change over time. A covariate available at forecast time is a leading indicator.

You must provide inference data for this column for each point in the forecast horizon.

Holidays, planned promotions or events.

`available_at_forecast_columns`

Covariate

Not available

A covariate *not* available at forecast time. You don't need to provide values for these features when creating a forecast.

Actual weather.

`unavailable_at_forecast_columns`

Learn more about the relationship between feature availability and the [forecast horizon, context window, and forecast window](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) .

## Forecast horizon, context window, and forecast window

Forecasting features are either static attributes or time-variant covariates. See [Feature type and availability at forecast](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .

When you train a forecasting model, you must specify which covariate training data is the most important to capture. This is expressed in the form of a **Forecast window** , which is a series of rows composed of the following:

  - The context or historical data, up to the time of inference.
  - The horizon or rows used for inference.

Taken together, the rows in the window define a time-series instance that serves as a model input: it is what Agent Platform trains on, evaluates on, and uses for inference. The row used to generate the window is the first row of the horizon and uniquely identifies the window in the time series.

The forecast horizon determines how far into the future the model forecasts the target value for each row of inference data.

The context window sets how far back the model looks during training (and for forecasts). In other words, for each training datapoint, the context window determines how far back the model looks for predictive patterns. [Learn best practices](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/bp-tabular#context-window) for finding a good value for the context window.

For example, if **Context window** = `14` and **Forecast horizon** = `7` , then each window example will have `14 + 7 = 21` rows.

### Availability at forecast

Forecasting covariates can be divided into those that are available at forecast time and those that are unavailable at forecast time.

When dealing with covariates that are *available* at forecast time, Agent Platform considers covariate values from both the context window and the forecast horizon for training, evaluation, and inference. When dealing with covariates that are *unavailable* at forecast time, Agent Platform considers covariate values from the context window but explicitly excludes covariate values from the forecast horizon.

### Rolling window strategies

Agent Platform generates **Forecast windows** from the input data using a rolling window strategy. The default strategy is **Count** .

  - **Count** . The number of windows generated by Agent Platform must not exceed a user-provided maximum. If the number of rows in the input dataset is less than the maximum number of windows, every row is used to generate a window. Otherwise, Agent Platform performs random sampling to select the rows. The default value for the maximum number of windows is `100,000,000` . The maximum number of windows cannot exceed `100,000,000` .
  - **Stride** . Agent Platform uses one out of every X input rows to generate a window, up to a maximum of 100,000,000 windows. This option is useful for seasonal or periodic inferences. For example, you can limit forecasting to a single day of the week by setting the stride length value to `7` . The value can be between `1` and `1000` .
  - **Column** . You can add a column to your input data where the values are either `True` or `False` . Agent Platform generates a window for every input row where the value of the column is `True` . The `True` and `False` values can be set in any order, as long as the total count of `True` rows is less than `100,000,000` . Boolean values are preferred, but string values are also accepted. String values are not case sensitive.

By generating fewer than the default `100,000,000` windows, you can reduce the time required for preprocessing and model evaluation. Furthermore, window downsampling gives you more control over the distribution of windows seen during training. If used correctly, this may lead to improved and more consistent results.

### How the context window and forecast horizon are used during training and forecasts

Suppose you have data that is collected monthly, with a context window of 5 months and forecasting horizon of 5 months. Training your model with 12 months of data would result in the following sets of inputs and forecasts:

  - `[1-5]:[6-10]`
  - `[2-6]:[7-11]`
  - `[3-7]:[8-12]`

After training, the model could be used to predict months 13 through 17:

  - `[8-12]:[13-17]`

The model uses only the data that falls into the context window to make the forecast. Any data you provide that falls outside of the context window is ignored.

After data is collected for month 13, it can be used to predict through month 18:

  - `[9-13]:[14-18]`

This can continue into the future, as long as you are getting good results. Eventually, you could retrain the model with the new data. For example, if you retrained the model after adding 6 more months of data, the training data would be used as follows:

  - `[2-6]:[7-11]`
  - `[3-7]:[8-12]`
  - `[4-8]:[9-13]`
  - `[5-9]:[10-14]`
  - `[6-10]:[11-15]`
  - `[7-11]:[12-16]`
  - `[8-12]:[13-17]`
  - `[9-13]:[14-18]`

You can then use the model to predict month 19 through 23:

  - `[14-18]:[19-23]`

## Optimization objectives for forecast models

When you train a model, Agent Platform selects a default optimization objective based on your model type and the data type used for your target column. The following table provides some details about problems forecast models are best suited for:

| Optimization objective | API value                | Use this objective if you want to...                                                                                                                                                                                          |
| ---------------------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RMSE                   | `minimize-rmse`          | Minimize root-mean-squared error (RMSE). Captures more extreme values accurately and is less biased when aggregating inferences. Default value.                                                                               |
| MAE                    | `minimize-mae`           | Minimize mean-absolute error (MAE). Views extreme values as outliers with less impact on model.                                                                                                                               |
| RMSLE                  | `minimize-rmsle`         | Minimize root-mean-squared log error (RMSLE). Penalizes error on relative size rather than absolute value. Useful when both predicted and actual values can be large.                                                         |
| RMSPE                  | `minimize-rmspe`         | Minimize root-mean-squared percentage error (RMSPE). Captures a large range of values accurately. Similar to RMSE, but relative to target magnitude. Useful when the range of values is large.                                |
| WAPE                   | `minimize-wape-mae`      | Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). Useful when the actual values are low.                                                                                   |
| Quantile loss          | `minimize-quantile-loss` | Minimize the scaled pinball loss of the defined quantiles to quantify uncertainty in estimates. Quantile inferences quantify the uncertainty of inferences. They measure the likelihood of an inference being within a range. |

## Holiday regions

For certain use cases, forecasting data can exhibit irregular behaviour on days that correspond to regional holidays. If you want your model to take this effect into account, select the geographical region or regions that correspond to your input data. During training, Agent Platform creates holiday categorical features within the model based on the date from the time column and the specified geographical regions.

The following is an excerpt of dates and holiday categorical features for the United States. Note that a categorical feature is assigned to the primary date, one or more preholiday days, and one or more postholiday days. For example, the primary date for Mother's Day in the US in 2013 was on May 12th. Mother's Day features are assigned to the primary date, six preholiday days and one postholiday day.

Date

Holiday categorical feature

2013-05-06

MothersDay

2013-05-07

MothersDay

2013-05-08

MothersDay

2013-05-09

MothersDay

2013-05-10

MothersDay

2013-05-11

MothersDay

2013-05-12

MothersDay

2013-05-13

MothersDay

2013-05-26

US\_MemorialDay

2013-05-27

US\_MemorialDay

2013-05-28

US\_MemorialDay

Acceptable values for holiday regions include the following:

  - `GLOBAL` : Detects holidays for all world regions.
  - `NA` : Detects holidays for North America.
  - `JAPAC` : Detects holidays for Japan and Asia Pacific.
  - `EMEA` : Detects holidays for Europe, the Middle East and Africa.
  - `LAC` : Detects holidays for Latin America and the Caribbean.
  - [ISO 3166-1 Country codes](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#holiday_region) : Detects holidays for individual countries.

To view the full list of holiday dates for each geographic region, refer to the `holidays_and_events_for_forecasting` table in BigQuery. You can open this table via the Google Cloud console using the following steps:

1.  In the Google Cloud console, in the BigQuery section, go to the **BigQuery Studio** page.

2.  In the [Explorer panel](https://docs.cloud.google.com/bigquery/docs/bigquery-web-ui#explorer_panel) , open the `bigquery-public-data` project. If you can't find this project or to learn more, see [Open a public dataset](https://docs.cloud.google.com/bigquery/docs/quickstarts/query-public-dataset-console#open_a_public_dataset) .

3.  Open the `ml_datasets` dataset.

4.  Open the `holidays_and_events_for_forecasting` table.

The following is an excerpt from the `holidays_and_events_for_forecasting` table:

![sample of holidays for forecasting](https://docs.cloud.google.com/static/vertex-ai/docs/tabular-data/images/holidays.png)
