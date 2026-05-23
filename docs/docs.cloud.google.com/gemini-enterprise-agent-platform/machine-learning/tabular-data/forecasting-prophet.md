---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-prophet
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-prophet
title: Forecasting with Prophet
description: Train a model and make inferences with Prophet.
data_source: docs.cloud.google.com
---

> To see an example of how to train a model with Prophet, run the "Train a Prophet Model using Tabular Workflows" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/prophet_on_vertex_pipelines.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftabular_workflows%2Fprophet_on_vertex_pipelines.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftabular_workflows%2Fprophet_on_vertex_pipelines.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/prophet_on_vertex_pipelines.ipynb)

Prophet is a forecasting model maintained by Meta. See the [Prophet paper](https://peerj.com/preprints/3190/) for algorithm details and the [documentation](https://facebook.github.io/prophet/docs/quick_start.html) for more information about the library.

Like [BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-arima/overview) , Prophet attempts to decompose each time series into trends, seasons, and holidays, producing a forecast using the aggregation of these models' inferences. An important difference, however, is that BQML ARIMA+ uses ARIMA to model the trend component, while Prophet attempts to fit a curve using a piecewise logistic or linear model.

Google Cloud offers a pipeline for training a Prophet model and a pipeline for getting batch inferences from a Prophet model. Both pipelines are instances of [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) from [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) (GCPC).

Integration of Prophet with Vertex AI means that you can do the following:

  - Use Vertex AI [data splitting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/prepare-data#split) and [windowing strategies](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/train-model#forecast-window) .
  - Read data from either BigQuery tables or CSVs stored in Cloud Storage. Vertex AI expects each row to have the same format as [Vertex AI Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/prepare-data) .

Although Prophet is a multivariate model, Vertex AI supports only a univariate version of it.

To learn about the service accounts this workflow uses, see [Service accounts for Tabular Workflows](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/service-accounts#fte-workflow) .

## Workflow APIs

This workflow uses the following APIs:

  - Vertex AI
  - Dataflow
  - BigQuery
  - Cloud Storage

## Train a model with Prophet

Prophet is designed for a single time series. Vertex AI aggregates data by time series ID and trains a Prophet model for each time series. The model training pipeline performs hyperparameter tuning using [grid search](https://en.wikipedia.org/wiki/Hyperparameter_optimization#Grid_search) and Prophet's built-in backtesting logic.

To support multiple time series, the pipeline uses a Vertex AI [Custom Training Job](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) and [Dataflow](https://cloud.google.com/dataflow/docs/about-dataflow) to train multiple Prophet models in parallel. Overall, the number of models trained is the product of the number of time series and the number of hyperparameter tuning trials.

The following sample code demonstrates how to run a Prophet model training pipeline:

    job = aiplatform.PipelineJob(
        ...
        template_path=train_job_spec_path,
        parameter_values=train_parameter_values,
        ...
    )
    job.run(service_account=SERVICE_ACCOUNT)

The optional `service_account` parameter in `job.run()` lets you set the Gemini Enterprise Agent Platform Pipelines service account to an account of your choice.

The pipeline and the parameter values are defined by the following function.

    (
        train_job_spec_path,
        train_parameter_values,
    ) = utils.get_prophet_train_pipeline_and_parameters(
        ...
    )

The following is a subset of `get_prophet_train_pipeline_and_parameters` parameters:

| Parameter name                    | Type    | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `project`                         | String  | Your project ID.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `location`                        | String  | Your region.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `root_dir`                        | String  | The Cloud Storage location to store the output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `target_column`                   | String  | The column (value) you want this model to predict.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `time_column`                     | String  | The time column. You must specify a time column and it must have a value for every row. The time column indicates the time at which a given observation was made.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `time_series_identifier_column`   | String  | The time series identifier column. You must specify a time series identifier column and it must have a value for every row. Forecasting training data usually includes multiple time series, and the identifier tells Vertex AI which time series a given observation in the training data is part of. All of the rows in a given time series have the same value in the time series identifier column. Some common time series identifiers might be the product ID, a store ID, or a region. It is possible to train a forecasting model on a single time series, with an identical value for all rows in the time series identifier column. However, Vertex AI is a better fit for training data that contains two or more time series. For best results, use at least 10 time series for every column you use to train the model. |
| `data_granularity_unit`           | String  | The unit to use for the granularity of your training data and your forecast horizon and context window. Can be `minute` , `hour` , `day` , `week` , `month` , or `year` . [Learn how to choose the data granularity](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/bp-tabular#granularity) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `data_source_csv_filenames`       | String  | A URI for a CSV stored in Cloud Storage.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `data_source_bigquery_table_path` | String  | A URI for a BigQuery table.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `forecast_horizon`                | Integer | The forecast horizon determines how far into the future the model forecasts the target value for each row of inference data. The forecast horizon is specified in units of data granularity. [Learn more](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/train-model#forecast-window) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `optimization_objective`          | String  | Optimization objective for the model. [Learn more](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/train-model#optimization-objectives) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `max_num_trials`                  | Integer | Maximum number of tuning trials to perform per time series.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### Dataflow parameters

The following is a subset of `get_prophet_train_pipeline_and_parameters` parameters for Dataflow customization:

| Parameter name                        | Type    | Definition                                                                                                                                                                                                        |
| ------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `trainer_dataflow_machine_type`       | String  | The Dataflow machine type to use for training.                                                                                                                                                                    |
| `trainer_dataflow_max_num_workers`    | Integer | The maximum number of Dataflow workers to use for training.                                                                                                                                                       |
| `evaluation_dataflow_machine_type`    | String  | The Dataflow machine type to use for evaluation.                                                                                                                                                                  |
| `evaluation_dataflow_max_num_workers` | Integer | The maximum number of Dataflow workers to use for evaluation.                                                                                                                                                     |
| `dataflow_service_account`            | String  | Custom service account to run Dataflow jobs. You can configure the Dataflow job to use private IPs and a specific VPC subnet. This parameter acts as an override for the default Dataflow worker service account. |

Because Prophet training jobs run on Dataflow, an initial startup time of 5 - 7 minutes occurs. To reduce additional runtime, you can scale up or scale out. For example, to scale up, change the machine type from `n1-standard-1` to `e2-highcpu-8` . To scale out, increase the number of workers from `1` to `200` .

### Data split parameters

The training pipeline offers the following options for splitting your data:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Data split</th>
<th>Description</th>
<th>Parameters</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Default split</td>
<td>Vertex AI randomly selects 80% of your data rows for the training set, 10% for the validation set, and 10% for the test set. Vertex AI uses the Time column to determine the chronological order of the data rows.</td>
<td>None</td>
</tr>
<tr class="even">
<td>Fraction split</td>
<td>Vertex AI uses values you provide to partition your data into the training set, the validation set, and the test set. Vertex AI uses the Time column to determine the chronological order of the data rows.</td>
<td><ul>
<li><code dir="ltr" translate="no">training_fraction</code></li>
<li><code dir="ltr" translate="no">validation_fraction</code></li>
<li><code dir="ltr" translate="no">test_fraction</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Timestamp split</td>
<td>Vertex AI uses the <code dir="ltr" translate="no">training_fraction</code> , <code dir="ltr" translate="no">validation_fraction</code> , and <code dir="ltr" translate="no">test_fraction</code> values to partition your data into the training set, the validation set, and the test set. Vertex AI uses the <code dir="ltr" translate="no">timestamp_split_key</code> column to determine the chronological order of the data rows.</td>
<td><ul>
<li><code dir="ltr" translate="no">training_fraction</code></li>
<li><code dir="ltr" translate="no">validation_fraction</code></li>
<li><code dir="ltr" translate="no">test_fraction</code></li>
<li><code dir="ltr" translate="no">timestamp_split_key</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Manual (predefined) split</td>
<td>Vertex AI splits the data using the TRAIN, VALIDATE, or TEST values in the <code dir="ltr" translate="no">predefined_split_key</code> column.</td>
<td><ul>
<li><code dir="ltr" translate="no">predefined_split_key</code></li>
</ul></td>
</tr>
</tbody>
</table>

You define the data split parameters in `get_prophet_train_pipeline_and_parameters` as follows:

| Parameter name         | Type   | Definition                                                                                                                          |
| ---------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `predefined_split_key` | String | The name of the column containing the TRAIN, VALIDATE, or TEST values. Set this value if you are using a manual (predefined) split. |
| `training_fraction`    | Float  | The percentage of the data to assign to the training set. Set this value if you are using a fraction split or a timestamp split.    |
| `validation_fraction`  | Float  | The percentage of the data to assign to the validation set. Set this value if you are using a fraction split or a timestamp split.  |
| `test_fraction`        | Float  | The percentage of the data to assign to the test set. Set this value if you are using a fraction split or a timestamp split.        |
| `timestamp_split_key`  | String | The name of the column containing the timestamps for the data split. Set this value if you are using a timestamp split.             |

### Window parameters

Vertex AI generates forecast windows from the input data using a rolling window strategy. If you leave the window parameters unset, Vertex AI uses the Count strategy with a default maximum value of `100,000,000` . The training pipeline offers the following rolling window strategies:

| Rolling window strategy | Description                                                                                                                                                                                                                                                                                                                                                                                                               | Parameters             |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| Count                   | The number of windows generated by Vertex AI must not exceed a user-provided maximum. If the number of rows in the input dataset is less than the maximum number of windows, every row is used to generate a window. Otherwise, Vertex AI performs random sampling to select the rows. The default value for the maximum number of windows is `100,000,000` . The maximum number of windows cannot exceed `100,000,000` . | `window_max_count`     |
| Stride                  | Vertex AI uses one out of every X input rows to generate a window, up to a maximum of 100,000,000 windows. This option is useful for seasonal or periodic inferences. For example, you can limit forecasting to a single day of the week by setting the stride length value to `7` . The value can be between `1` and `1000` .                                                                                            | `window_stride_length` |
| Column                  | You can add a column to your input data where the values are either `True` or `False` . Vertex AI generates a window for every input row where the value of the column is `True` . The `True` and `False` values can be set in any order, as long as the total count of `True` rows is less than `100,000,000` . Boolean values are preferred, but string values are also accepted. String values are not case sensitive. | `window_column`        |

You define the window parameters in `get_prophet_train_pipeline_and_parameters` as follows:

| Parameter name         | Type    | Definition                                             |
| ---------------------- | ------- | ------------------------------------------------------ |
| `window_column`        | String  | The name of the column with `True` and `False` values. |
| `window_stride_length` | Integer | The value of the stride length.                        |
| `window_max_count`     | Integer | The maximum number of windows.                         |

## Make inferences with Prophet

The Vertex AI [model training pipeline for Prophet](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-prophet#train) creates one Prophet model for each time series in the data. The inference pipeline aggregates input data by time series ID and calculates the inferences separately for each time series. The pipeline then disaggregates the inference results to match the format of [Vertex AI Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/get-predictions) .

The following sample code demonstrates how to run a Prophet inference pipeline:

    job = aiplatform.PipelineJob(
        ...
        template_path=prediction_job_spec_path,
        parameter_values=prediction_parameter_values,
        ...
    )
    job.run(...)

The pipeline and the parameter values are defined by the following function.

    (
        prediction_job_spec_path,
        prediction_parameter_values,
    ) = utils.get_prophet_prediction_pipeline_and_parameters(
        ...
    )

The following is a subset of `get_prophet_prediction_pipeline_and_parameters` parameters:

| Parameter name                    | Type    | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `project`                         | String  | Your project ID.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `location`                        | String  | Your region.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `model_name`                      | String  | The name of the Model resource. Format the string as follows: `projects/{project}/locations/{location}/models/{model}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `time_column`                     | String  | The time column. You must specify a time column and it must have a value for every row. The time column indicates the time at which a given observation was made.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `time_series_identifier_column`   | String  | The time series identifier column. You must specify a time series identifier column and it must have a value for every row. Forecasting training data usually includes multiple time series, and the identifier tells Vertex AI which time series a given observation in the training data is part of. All of the rows in a given time series have the same value in the time series identifier column. Some common time series identifiers might be the product ID, a store ID, or a region. It is possible to train a forecasting model on a single time series, with an identical value for all rows in the time series identifier column. However, Vertex AI is a better fit for training data that contains two or more time series. For best results, use at least 10 time series for every column you use to train the model. |
| `target_column`                   | String  | The column (value) you want this model to predict.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `data_source_csv_filenames`       | String  | A URI for a CSV stored in Cloud Storage.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `data_source_bigquery_table_path` | String  | A URI for a BigQuery table.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `bigquery_destination_uri`        | String  | A URI for the selected destination dataset. If this value is not set, resources are created under a new dataset in the project.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `machine_type`                    | String  | The machine type to use for batch inference.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `max_num_workers`                 | Integer | The maximum number of workers to use for batch inference.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
