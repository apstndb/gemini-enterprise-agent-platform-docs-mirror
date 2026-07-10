---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model
title: Train a forecast model
description: Train a forecast model from a tabular dataset in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to train a forecast model from a tabular dataset using either the Google Cloud console or the Agent Platform API.

## Before you begin

Before you train a forecast model, complete the following:

  - [Prepare your training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data)
  - [Create an Agent Platform dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/create-dataset)

## Train a model

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  Click the name of the dataset you want to use to train your model to open its details page.

3.  If your data type uses annotation sets, select the annotation set you want to use for this model.

4.  Click **Train new model** .

5.  Select **Other** .

6.  In the **Training method** page, configure the following:
    
    1.  Select the model training method. To learn more, see [Model training methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#training-methods) .
    
    2.  Click **Continue** .

7.  In the **Model details** page, configure the following:
    
    1.  Enter the display name for your new model.
    
    2.  Select your target column.
        
        The target column is the value that the model will forecast. Learn more about [target column requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#data-structure) .
    
    3.  If you did not set your [**Series identifier** and **Timestamp** columns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#data-structure) on your dataset, select them now.
    
    4.  Select your **Data granularity** . Select `Daily` if you would like to use holiday effect modeling. [Learn how to choose the data granularity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/bp-tabular#granularity) .
    
    5.  **Optional** : In the **Holiday regions** dropdown, choose one or more geographical regions to enable holiday effect modeling. During training, Agent Platform creates holiday categorical features within the model based on the date from the **Timestamp** column and the specified geographical regions. You can select this option only when **Data granularity** is set to `Daily` . By default, holiday effect modeling is disabled. To learn about the geographical regions used for holiday effect modeling, see [Holiday regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#holiday-regions) .
    
    6.  Enter your **Context window** and **Forecast horizon** .
        
        The forecast horizon determines how far into the future the model forecasts the target value for each row of inference data. The **Forecast horizon** is specified in units of **Data granularity** .
        
        The context window sets how far back the model looks during training (and for forecasts). In other words, for each training datapoint, the context window determines how far back the model looks for predictive patterns. The **Context window** is specified in units of **Data granularity** .
        
        [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) .
    
    7.  If you would like to export your test dataset to BigQuery, check **Export test dataset to BigQuery** and provide the name of the table.
    
    8.  If you want to manually control your data split or configure the forecasting window, open the **Advanced options** .
    
    9.  The default data split is chronological, with the standard 80/10/10 percentages. If you would like to manually specify which rows are assigned to which split, select **Manual** and specify your Data split column.
        
        Learn more about [data splits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/data-splits) .
    
    10. Select a rolling window strategy for forecast window generation. The default strategy is **Count** .
        
          - **Count** : Set the value for the maximum number of windows in the textbox provided.
          - **Stride** : Set the value of the stride length in the textbox provided.
          - **Column** : Select the appropriate column name from the dropdown provided.
        
        To learn more, see [Rolling window strategies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#rolling_window_strategies) .
    
    11. Click **Continue** .

8.  In the **Training options** page, configure the following:
    
    1.  If you haven't already, click **Generate statistics** .
        
        Generating statistics populates the **Transformation** dropdown menus.
    
    2.  Review your column list and exclude any columns from training that should not be used to train the model.
        
        If you are using a data split column, it should be included.
    
    3.  Review the transformations selected for your included features and make any required updates.
        
        Rows containing data that is invalid for the selected transformation are excluded from training. Learn more about [transformations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#transformations) .
    
    4.  For each column you included for training, specify the **Feature type** for how that feature relates to its time series, and whether it is available at forecast time. Learn more about [feature type and availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .
    
    5.  If you want to specify a weight column, change your optimization objective from the default, or enable hierarchical forecasting, open **Advanced options** .
    
    6.  **Optional** . If you want to specify a weight column, select it from the dropdown list. Learn more about [weight columns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#weight) .
    
    7.  **Optional** . If you want to select the optimization objective, select it from the list. Learn more [optimization objectives](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#optimization-objectives) .
    
    8.  **Optional** . If you want to use hierarchical forecasting, select **Enable hierarchical forecasting** . You can choose between three grouping options:
        
          - `No grouping`
          - `Group by columns`
          - `Group all`
        
        You can also choose to set the following aggregate loss weights:
        
          - `Group total weight` . This field can be set only if you select the `Group by columns` or the `Group all` option.
          - `Temporal total weight` .
          - `Group temporal total weight` . This field can be set only if you select the `Group by columns` or the `Group all` option.
        
        Learn more about [hierarchical forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/hierarchical) .
    
    9.  Click **Continue** .

9.  In the **Compute and pricing** page, configure the following:
    
    1.  Enter the maximum number of hours you want your model to train for. This setting helps you put a cap on the training costs. The actual time elapsed can be longer than this value, because there are other operations involved in creating a new model.
        
        Suggested training time is related to the size of your forecast horizon and your training data. The table below provides some sample forecasting training runs, and the range of training time that was needed to train a high-quality model.
        
        | Rows       | Features | Forecast horizon | Training time |
        | ---------- | -------- | ---------------- | ------------- |
        | 12 million | 10       | 6                | 3-6 hours     |
        | 20 million | 50       | 13               | 6-12 hours    |
        | 16 million | 30       | 365              | 24-48 hours   |
        

        For information about training pricing, see the [pricing page](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#tabular-data) .
    
    2.  Click **Start Training** .
        
        Model training can take many hours, depending on the size and complexity of your data and your training budget, if you specified one. You can close this tab and return to it later. You will receive an email when your model has completed training.
        
        > Tabular training data in Cloud Storage or BigQuery is not imported into Agent Platform. (When you import from local files, they are imported into Cloud Storage.) When you create a dataset with tabular data, the data is associated with the dataset. Changes you make to your data source in Cloud Storage or BigQuery after dataset creation are incorporated into models subsequently trained with that dataset. A snapshot of the dataset is taken when model training begins.

### API

> Tabular training data in Cloud Storage or BigQuery is not imported into Agent Platform. (When you import from local files, they are imported into Cloud Storage.) When you create a dataset with tabular data, the data is associated with the dataset. Changes you make to your data source in Cloud Storage or BigQuery after dataset creation are incorporated into models subsequently trained with that dataset. A snapshot of the dataset is taken when model training begins.

Select a tab for your language or environment:

### REST

You use the [trainingPipelines.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create) command to train a model.

Before using any of the request data, make the following replacements:

  - LOCATION : Your region.
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TRAINING\_PIPELINE\_DISPLAY\_NAME : Display name for the training pipeline created for this operation.
  - TRAINING\_TASK\_DEFINITION : The model training method.
      - Time series Dense Encoder (TiDE)  
        `gs://google-cloud-aiplatform/schema/trainingjob/definition/time_series_dense_encoder_forecasting_1.0.0.yaml`
      - Temporal Fusion Transformer (TFT)  
        `gs://google-cloud-aiplatform/schema/trainingjob/definition/temporal_fusion_transformer_time_series_forecasting_1.0.0.yaml`
      - AutoML (L2L)  
        `gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_forecasting_1.0.0.yaml`
      - Seq2Seq+  
        `gs://google-cloud-aiplatform/schema/trainingjob/definition/seq2seq_plus_time_series_forecasting_1.0.0.yaml`
    To learn more, see [Model training methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#training-methods) .
  - TARGET\_COLUMN : The column (value) you want this model to predict.
  - TIME\_COLUMN : The time column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#data-structure) .
  - TIME\_SERIES\_IDENTIFIER\_COLUMN : The time series identifier column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#data-structure) .
  - WEIGHT\_COLUMN : (Optional) The weight column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#weight) .
  - TRAINING\_BUDGET : The maximum amount of time you want the model to train, in milli node hours (1,000 milli node hours equals one node hour).
  - GRANULARITY\_UNIT : The unit to use for the granularity of your training data and your forecast horizon and context window. Can be `minute` , `hour` , `day` , `week` , `month` , or `year` . Select `day` if you would like to use holiday effect modeling. [Learn how to choose the data granularity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/bp-tabular#granularity) .
  - GRANULARITY\_QUANTITY : The number of granularity units that make up the interval between observations in your training data. Must be one for all units except minutes, which can be 1, 5, 10, 15, or 30. [Learn how to choose the data granularity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/bp-tabular#granularity) .
  - GROUP\_COLUMNS : Column names in your training input table that identify the grouping for the hierarchy level. The column(s) must be \`time\_series\_attribute\_columns\`. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/hierarchical) .
  - GROUP\_TOTAL\_WEIGHT : Weight of the group aggregated loss relative to the individual loss. Disabled if set to \`0.0\` or is not set. If the group column is not set, all time series will be treated as part of the same group and is aggregated over all time series. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/hierarchical) .
  - TEMPORAL\_TOTAL\_WEIGHT : Weight of the time aggregated loss relative to the individual loss. Disabled if set to \`0.0\` or is not set. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/hierarchical) .
  - GROUP\_TEMPORAL\_TOTAL\_WEIGHT : Weight of the total (group x time) aggregated loss relative to the individual loss. Disabled if set to \`0.0\` or is not set. If the group column is not set, all time series will be treated as part of the same group and is aggregated over all time series. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/hierarchical) .
  - HOLIDAY\_REGIONS : (Optional) You can select one or more geographical regions to enable holiday effect modeling. During training, Agent Platform creates holiday categorical features within the model based on the date from TIME\_COLUMN and the specified geographical regions. To enable it, set GRANULARITY\_UNIT to `day` and specify one or more regions in the HOLIDAY\_REGIONS field. By default, holiday effect modeling is disabled. To learn more, see [Holiday regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#holiday-regions) .
  - FORECAST\_HORIZON : The forecast horizon determines how far into the future the model forecasts the target value for each row of inference data. The forecast horizon is specified in units of data granularity ( GRANULARITY\_UNIT ). [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) .
  - CONTEXT\_WINDOW : The context window sets how far back the model looks during training (and for forecasts). In other words, for each training datapoint, the context window determines how far back the model looks for predictive patterns. The context window is specified in units of data granularity ( GRANULARITY\_UNIT ). [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#forecast-window) .
  - OPTIMIZATION\_OBJECTIVE : By default, Agent Platform minimizes the root-mean-squared error (RMSE). If you want a different optimization objective for your forecast model, choose one of the options in [Optimization objectives for forecast models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#optimization-objectives) . If you choose to minimize the quantile loss, you must also specify a value for QUANTILES .
  - PROBABILISTIC\_INFERENCE : (Optional) If set to `true` , Agent Platform models the probability distribution of the forecast. Probabilistic inference can improve model quality by handling noisy data and quantifying uncertainty. If QUANTILES are specified, then Agent Platform also returns the quantiles of the probability distribution. Probabilistic inference is compatible only with the `Time series Dense Encoder (TiDE)` and the `AutoML (L2L)` training methods. It is incompatible with hierarchical forecasting and the `minimize-quantile-loss` optimization objective.
  - QUANTILES : Quantiles to use for the `minimize-quantile-loss` optimization objective and probabilistic inference. Provide a list of up to five unique numbers between `0` and `1` , exclusive.
  - TIME\_SERIES\_ATTRIBUTE\_COL : The name or names of the columns that are time series attributes. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .
  - AVAILABLE\_AT\_FORECAST\_COL : The name or names of the covariate columns whose value is known at forecast time. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .
  - UNAVAILABLE\_AT\_FORECAST\_COL : The name or names of the covariate columns whose value is unknown at forecast time. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) .
  - TRANSFORMATION\_TYPE : The transformation type is provided for each column used to train the model. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#transformations) .
  - COLUMN\_NAME : The name of the column with the specified transformation type. Every column used to train the model must be specified.
  - MODEL\_DISPLAY\_NAME : Display name for the newly trained model.
  - DATASET\_ID : ID for the training Dataset.
  - You can provide a `Split` object to control your data split. For information about controlling data split, see [Control the data split using REST](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model#data-split) .
  - You can provide a `windowConfig` object to configure a rolling window strategy for forecast window generation. For further information, see [Configure the rolling window strategy using REST](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model#rolling-window) .
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
        "displayName": "TRAINING_PIPELINE_DISPLAY_NAME",
        "trainingTaskDefinition": "TRAINING_TASK_DEFINITION",
        "trainingTaskInputs": {
            "targetColumn": "TARGET_COLUMN",
            "timeColumn": "TIME_COLUMN",
            "timeSeriesIdentifierColumn": "TIME_SERIES_IDENTIFIER_COLUMN",
            "weightColumn": "WEIGHT_COLUMN",
            "trainBudgetMilliNodeHours": TRAINING_BUDGET,
            "dataGranularity": {"unit": "GRANULARITY_UNIT", "quantity": GRANULARITY_QUANTITY},
            "hierarchyConfig": {"groupColumns": GROUP_COLUMNS, "groupTotalWeight": GROUP_TOTAL_WEIGHT, "temporalTotalWeight": TEMPORAL_TOTAL_WEIGHT, "groupTemporalTotalWeight": GROUP_TEMPORAL_TOTAL_WEIGHT}
            "holidayRegions" : ["HOLIDAY_REGIONS_1", "HOLIDAY_REGIONS_2", ...]
            "forecast_horizon": FORECAST_HORIZON,
            "context_window": CONTEXT_WINDOW,
            "optimizationObjective": "OPTIMIZATION_OBJECTIVE",
            "quantiles": "QUANTILES",
            "enableProbabilisticInference": "PROBABILISTIC_INFERENCE",
            "time_series_attribute_columns": ["TIME_SERIES_ATTRIBUTE_COL_1", "TIME_SERIES_ATTRIBUTE_COL_2", ...]
            "available_at_forecast_columns": ["AVAILABLE_AT_FORECAST_COL_1", "AVAILABLE_AT_FORECAST_COL_2", ...]
            "unavailable_at_forecast_columns": ["UNAVAILABLE_AT_FORECAST_COL_1", "UNAVAILABLE_AT_FORECAST_COL_2", ...]
            "transformations": [
                {"TRANSFORMATION_TYPE_1":  {"column_name" : "COLUMN_NAME_1"} },
                {"TRANSFORMATION_TYPE_2":  {"column_name" : "COLUMN_NAME_2"} },
                ...
        },
        "modelToUpload": {"displayName": "MODEL_DISPLAY_NAME"},
        "inputDataConfig": {
          "datasetId": "DATASET_ID",
        }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAINING_PIPELINE_ID",
      "displayName": "myModelName",
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tabular_1.0.0.yaml",
      "modelToUpload": {
        "displayName": "myModelName"
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-08-18T01:22:57.479336Z",
      "updateTime": "2020-08-18T01:22:57.479336Z"
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_training_pipeline_forecasting_time_series_dense_encoder_sample(
        project: str,
        display_name: str,
        dataset_id: str,
        location: str = "us-central1",
        model_display_name: str = "my_model",
        target_column: str = "target_column",
        time_column: str = "date",
        time_series_identifier_column: str = "time_series_id",
        unavailable_at_forecast_columns: List[str] = [],
        available_at_forecast_columns: List[str] = [],
        forecast_horizon: int = 1,
        data_granularity_unit: str = "week",
        data_granularity_count: int = 1,
        training_fraction_split: float = 0.8,
        validation_fraction_split: float = 0.1,
        test_fraction_split: float = 0.1,
        budget_milli_node_hours: int = 8000,
        timestamp_split_column_name: str = "timestamp_split",
        weight_column: str = "weight",
        time_series_attribute_columns: List[str] = [],
        context_window: int = 0,
        export_evaluated_data_items: bool = False,
        export_evaluated_data_items_bigquery_destination_uri: Optional[str] = None,
        export_evaluated_data_items_override_destination: bool = False,
        quantiles: Optional[List[float]] = None,
        enable_probabilistic_inference: bool = False,
        validation_options: Optional[str] = None,
        predefined_split_column_name: Optional[str] = None,
        sync: bool = True,
    ):
        aiplatform.init(project=project, location=location)
    
        # Create training job
        forecasting_tide_job = aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob(
            display_name=display_name,
            optimization_objective="minimize-rmse",
        )
    
        # Retrieve existing dataset
        dataset = aiplatform.TimeSeriesDataset(dataset_id)
    
        # Run training job
        model = forecasting_tide_job.run(
            dataset=dataset,
            target_column=target_column,
            time_column=time_column,
            time_series_identifier_column=time_series_identifier_column,
            unavailable_at_forecast_columns=unavailable_at_forecast_columns,
            available_at_forecast_columns=available_at_forecast_columns,
            forecast_horizon=forecast_horizon,
            data_granularity_unit=data_granularity_unit,
            data_granularity_count=data_granularity_count,
            training_fraction_split=training_fraction_split,
            validation_fraction_split=validation_fraction_split,
            test_fraction_split=test_fraction_split,
            predefined_split_column_name=predefined_split_column_name,
            timestamp_split_column_name=timestamp_split_column_name,
            weight_column=weight_column,
            time_series_attribute_columns=time_series_attribute_columns,
            context_window=context_window,
            export_evaluated_data_items=export_evaluated_data_items,
            export_evaluated_data_items_bigquery_destination_uri=export_evaluated_data_items_bigquery_destination_uri,
            export_evaluated_data_items_override_destination=export_evaluated_data_items_override_destination,
            quantiles=quantiles,
            enable_probabilistic_inference=enable_probabilistic_inference,
            validation_options=validation_options,
            budget_milli_node_hours=budget_milli_node_hours,
            model_display_name=model_display_name,
            sync=sync,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        print(model.uri)
        return model

## Control the data split using REST

You control how your training data is split between the training, validation, and test sets. Use a split column to manually specify the data split for each row and provide it as part of a `PredefinedSplit` [`Split` object](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#InputDataConfig) in the `inputDataConfig` of the JSON request.

DATA\_SPLIT\_COLUMN is the column containing the data split values ( `TRAIN` , `VALIDATION` , `TEST` ).

    "predefinedSplit": {
      "key": DATA_SPLIT_COLUMN
    },

[Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/data-splits) about data splits.

## Configure the rolling window strategy using REST

Provide a `windowConfig` object to configure a rolling window strategy for forecast window generation. The default strategy is `maxCount` .

  - To use the `maxCount` option, add the following to `trainingTaskInputs` of the JSON request. MAX\_COUNT\_VALUE refers to the maximum number of windows.
    
    ```` 
      "windowConfig": {
        "maxCount": MAX_COUNT_VALUE
      },
      ```
    ````

  - To use the `strideLength` option, add the following to `trainingTaskInputs` of the JSON request. STRIDE\_LENGTH\_VALUE refers to the value of the stride length.
    
    ```` 
      "windowConfig": {
        "strideLength": STRIDE_LENGTH_VALUE
      },
      ```
    ````

  - To use the `column` option, add the following to `trainingTaskInputs` of the JSON request. COLUMN\_NAME refers to the name of the column with `True` or `False` values.
    
    ```` 
      "windowConfig": {
        "column": "COLUMN_NAME"
      },
      ```
    ````

To learn more, see [Rolling window strategies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#rolling-window-strategies) .

## What's next

  - [Evaluate your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/evaluate-model) .
