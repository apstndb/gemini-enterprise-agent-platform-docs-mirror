---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/custom-training-pipelines/tabular
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/custom-training-pipelines/tabular
title: Train custom ML models on Gemini Enterprise Agent Platform Pipelines
description: Use Gemini Enterprise Agent Platform Pipelines to import and transform data, train a model using a selected ML framework, and import the trained model to Gemini Enterprise Agent Platform Model Registry.
data_source: docs.cloud.google.com
---

This tutorial shows you how to use Gemini Enterprise Agent Platform Pipelines to run an end-to-end ML workflow, including the following tasks:

  - Import and transform data.
  - Train a model using the selected ML framework.
  - Import the trained model to Gemini Enterprise Agent Platform Model Registry.
  - **Optional** : Deploy the model for online serving with Vertex AI Inference.

## Before you begin

1.  Ensure that you've completed the tasks 1-3 in [Set up a Google Cloud project and a development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#project) .

2.  Install the [Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/libraries/reference#client_libraries) and the Kubeflow Pipelines SDK:
    
        python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet

3.  Ensure that you have the following IAM permissions:
    
      - `**aiplatform.metadataStores.get**`
      - `**storage.buckets.get**`
      - `**storage.objects.create**`
      - `**storage.objects.get**`
    
    You must have these permissions to use Gemini Enterprise Agent Platform Pipelines to run pipelines.
    
    > **Note:** If this is your first time using Gemini Enterprise Agent Platform Pipelines to create a pipeline run in the project, ensure that you also have the `**aiplatform.metadataStores.create**` permission.

## Run the ML model training pipeline

Choose training objective and ML framework in the following tabs to get sample code that you can run in your environment. The sample code does the following:

  - Loads components from a [component repository](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/community-content/pipeline_components) to be used as pipeline building blocks.
  - Composes a pipeline by creating component tasks and passing data between them using arguments.
  - Submits the pipeline for execution on Gemini Enterprise Agent Platform Pipelines. See [Gemini Enterprise Agent Platform Pipelines pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#pipelines) .

Copy the code into your development environment and run it.

### Tabular classification

### TensorFlow

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    binarize_column_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Binarize_column/in_CSV_format/component.yaml")
    split_rows_into_subsets_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/dataset_manipulation/Split_rows_into_subsets/in_CSV/component.yaml")
    create_fully_connected_tensorflow_network_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/tensorflow/Create_fully_connected_network/component.yaml")
    train_model_using_Keras_on_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/tensorflow/Train_model_using_Keras/on_CSV/component.yaml")
    predict_with_TensorFlow_model_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/tensorflow/Predict/on_CSV/component.yaml")
    upload_Tensorflow_model_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_Tensorflow_model/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_classification_model_using_TensorFlow_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        training_set_fraction = 0.8
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        classification_label_column = "class"
        all_columns = [label_column] + feature_columns
    
        dataset = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        dataset = select_columns_using_Pandas_on_CSV_data_op(
            table=dataset,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        dataset = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=dataset,
            replacement_value="0",
            # # Optional:
            # column_names=None,  # =[...]
        ).outputs["transformed_table"]
    
        classification_dataset = binarize_column_using_Pandas_on_CSV_data_op(
            table=dataset,
            column_name=label_column,
            predicate=" > 0",
            new_column_name=classification_label_column,
        ).outputs["transformed_table"]
    
        split_task = split_rows_into_subsets_op(
            table=classification_dataset,
            fraction_1=training_set_fraction,
        )
        classification_training_data = split_task.outputs["split_1"]
        classification_testing_data = split_task.outputs["split_2"]
    
        network = create_fully_connected_tensorflow_network_op(
            input_size=len(feature_columns),
            # Optional:
            hidden_layer_sizes=[10],
            activation_name="elu",
            output_activation_name="sigmoid",
            # output_size=1,
        ).outputs["model"]
    
        model = train_model_using_Keras_on_CSV_op(
            training_data=classification_training_data,
            model=network,
            label_column_name=classification_label_column,
            # Optional:
            loss_function_name="binary_crossentropy",
            number_of_epochs=10,
            #learning_rate=0.1,
            #optimizer_name="Adadelta",
            #optimizer_parameters={},
            #batch_size=32,
            #metric_names=["mean_absolute_error"],
            #random_seed=0,
        ).outputs["trained_model"]
    
        predictions = predict_with_TensorFlow_model_on_CSV_data_op(
            dataset=classification_testing_data,
            model=model,
            # label_column_name needs to be set when doing prediction on a dataset that has labels
            label_column_name=classification_label_column,
            # Optional:
            # batch_size=1000,
        ).outputs["predictions"]
    
        vertex_model_name = upload_Tensorflow_model_to_Google_Cloud_Vertex_AI_op(
            model=model,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func = train_tabular_classification_model_using_TensorFlow_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### PyTorch

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    binarize_column_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Binarize_column/in_CSV_format/component.yaml")
    create_fully_connected_pytorch_network_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/PyTorch/Create_fully_connected_network/component.yaml")
    train_pytorch_model_from_csv_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/PyTorch/Train_PyTorch_model/from_CSV/component.yaml")
    create_pytorch_model_archive_with_base_handler_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/PyTorch/Create_PyTorch_Model_Archive/with_base_handler/component.yaml")
    upload_PyTorch_model_archive_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_PyTorch_model_archive/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_classification_model_using_PyTorch_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        classification_label_column = "class"
        all_columns = [label_column] + feature_columns
    
        training_data = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        training_data = select_columns_using_Pandas_on_CSV_data_op(
            table=training_data,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        # Cleaning the NaN values.
        training_data = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=training_data,
            replacement_value="0",
            #replacement_type_name="float",
        ).outputs["transformed_table"]
    
        classification_training_data = binarize_column_using_Pandas_on_CSV_data_op(
            table=training_data,
            column_name=label_column,
            predicate=" > 0",
            new_column_name=classification_label_column,
        ).outputs["transformed_table"]
    
        network = create_fully_connected_pytorch_network_op(
            input_size=len(feature_columns),
            # Optional:
            hidden_layer_sizes=[10],
            activation_name="elu",
            output_activation_name="sigmoid",
            # output_size=1,
        ).outputs["model"]
    
        model = train_pytorch_model_from_csv_op(
            model=network,
            training_data=classification_training_data,
            label_column_name=classification_label_column,
            loss_function_name="binary_cross_entropy",
            # Optional:
            #number_of_epochs=1,
            #learning_rate=0.1,
            #optimizer_name="Adadelta",
            #optimizer_parameters={},
            #batch_size=32,
            #batch_log_interval=100,
            #random_seed=0,
        ).outputs["trained_model"]
    
        model_archive = create_pytorch_model_archive_with_base_handler_op(
            model=model,
            # Optional:
            # model_name="model",
            # model_version="1.0",
        ).outputs["Model archive"]
    
        vertex_model_name = upload_PyTorch_model_archive_to_Google_Cloud_Vertex_AI_op(
            model_archive=model_archive,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func=train_tabular_classification_model_using_PyTorch_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### XGBoost

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    binarize_column_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Binarize_column/in_CSV_format/component.yaml")
    split_rows_into_subsets_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/dataset_manipulation/Split_rows_into_subsets/in_CSV/component.yaml")
    train_XGBoost_model_on_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/XGBoost/Train/component.yaml")
    xgboost_predict_on_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/XGBoost/Predict/component.yaml")
    upload_XGBoost_model_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_XGBoost_model/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_classification_model_using_XGBoost_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        training_set_fraction = 0.8
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        classification_label_column = "class"
        all_columns = [label_column] + feature_columns
    
        dataset = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        dataset = select_columns_using_Pandas_on_CSV_data_op(
            table=dataset,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        dataset = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=dataset,
            replacement_value="0",
            # # Optional:
            # column_names=None,  # =[...]
        ).outputs["transformed_table"]
    
        classification_dataset = binarize_column_using_Pandas_on_CSV_data_op(
            table=dataset,
            column_name=label_column,
            predicate="> 0",
            new_column_name=classification_label_column,
        ).outputs["transformed_table"]
    
        split_task = split_rows_into_subsets_op(
            table=classification_dataset,
            fraction_1=training_set_fraction,
        )
        classification_training_data = split_task.outputs["split_1"]
        classification_testing_data = split_task.outputs["split_2"]
    
        model = train_XGBoost_model_on_CSV_op(
            training_data=classification_training_data,
            label_column_name=classification_label_column,
            objective="binary:logistic",
            # Optional:
            #starting_model=None,
            #num_iterations=10,
            #booster_params={},
            #booster="gbtree",
            #learning_rate=0.3,
            #min_split_loss=0,
            #max_depth=6,
        ).outputs["model"]
    
        # Predicting on the testing data
        predictions = xgboost_predict_on_CSV_op(
            data=classification_testing_data,
            model=model,
            # label_column needs to be set when doing prediction on a dataset that has labels
            label_column_name=classification_label_column,
        ).outputs["predictions"]
    
        vertex_model_name = upload_XGBoost_model_to_Google_Cloud_Vertex_AI_op(
            model=model,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func = train_tabular_classification_model_using_XGBoost_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### Scikit-learn

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    binarize_column_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Binarize_column/in_CSV_format/component.yaml")
    train_logistic_regression_model_using_scikit_learn_from_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/1f5cf6e06409b704064b2086c0a705e4e6b4fcde/community-content/pipeline_components/ML_frameworks/Scikit_learn/Train_logistic_regression_model/from_CSV/component.yaml")
    upload_Scikit_learn_pickle_model_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_Scikit-learn_pickle_model/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_classification_logistic_regression_model_using_Scikit_learn_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        classification_label_column = "class"
        all_columns = [label_column] + feature_columns
    
        training_data = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        training_data = select_columns_using_Pandas_on_CSV_data_op(
            table=training_data,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        # Cleaning the NaN values.
        training_data = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=training_data,
            replacement_value="0",
            #replacement_type_name="float",
        ).outputs["transformed_table"]
    
        classification_training_data = binarize_column_using_Pandas_on_CSV_data_op(
            table=training_data,
            column_name=label_column,
            predicate="> 0",
            new_column_name=classification_label_column,
        ).outputs["transformed_table"]
    
        model = train_logistic_regression_model_using_scikit_learn_from_CSV_op(
            dataset=classification_training_data,
            label_column_name=classification_label_column,
            # Optional:
            #penalty="l2",
            #solver="lbfgs",
            #max_iterations=100,
            #multi_class_mode="auto",
            #random_seed=0,
        ).outputs["model"]
    
        vertex_model_name = upload_Scikit_learn_pickle_model_to_Google_Cloud_Vertex_AI_op(
            model=model,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            sklearn_vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func = train_tabular_classification_logistic_regression_model_using_Scikit_learn_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### Tabular regression

### TensorFlow

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    split_rows_into_subsets_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/dataset_manipulation/Split_rows_into_subsets/in_CSV/component.yaml")
    create_fully_connected_tensorflow_network_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/tensorflow/Create_fully_connected_network/component.yaml")
    train_model_using_Keras_on_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/tensorflow/Train_model_using_Keras/on_CSV/component.yaml")
    predict_with_TensorFlow_model_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/tensorflow/Predict/on_CSV/component.yaml")
    upload_Tensorflow_model_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_Tensorflow_model/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_regression_model_using_Tensorflow_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        training_set_fraction = 0.8
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        all_columns = [label_column] + feature_columns
    
        dataset = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        dataset = select_columns_using_Pandas_on_CSV_data_op(
            table=dataset,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        dataset = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=dataset,
            replacement_value="0",
            # # Optional:
            # column_names=None,  # =[...]
        ).outputs["transformed_table"]
    
        split_task = split_rows_into_subsets_op(
            table=dataset,
            fraction_1=training_set_fraction,
        )
        training_data = split_task.outputs["split_1"]
        testing_data = split_task.outputs["split_2"]
    
        network = create_fully_connected_tensorflow_network_op(
            input_size=len(feature_columns),
            # Optional:
            hidden_layer_sizes=[10],
            activation_name="elu",
            # output_activation_name=None,
            # output_size=1,
        ).outputs["model"]
    
        model = train_model_using_Keras_on_CSV_op(
            training_data=training_data,
            model=network,
            label_column_name=label_column,
            # Optional:
            #loss_function_name="mean_squared_error",
            number_of_epochs=10,
            #learning_rate=0.1,
            #optimizer_name="Adadelta",
            #optimizer_parameters={},
            #batch_size=32,
            metric_names=["mean_absolute_error"],
            #random_seed=0,
        ).outputs["trained_model"]
    
        predictions = predict_with_TensorFlow_model_on_CSV_data_op(
            dataset=testing_data,
            model=model,
            # label_column_name needs to be set when doing prediction on a dataset that has labels
            label_column_name=label_column,
            # Optional:
            # batch_size=1000,
        ).outputs["predictions"]
    
        vertex_model_name = upload_Tensorflow_model_to_Google_Cloud_Vertex_AI_op(
            model=model,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func=train_tabular_regression_model_using_Tensorflow_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### PyTorch

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    create_fully_connected_pytorch_network_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/PyTorch/Create_fully_connected_network/component.yaml")
    train_pytorch_model_from_csv_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/PyTorch/Train_PyTorch_model/from_CSV/component.yaml")
    create_pytorch_model_archive_with_base_handler_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/PyTorch/Create_PyTorch_Model_Archive/with_base_handler/component.yaml")
    upload_PyTorch_model_archive_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_PyTorch_model_archive/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_regression_model_using_PyTorch_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        all_columns = [label_column] + feature_columns
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        training_data = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        training_data = select_columns_using_Pandas_on_CSV_data_op(
            table=training_data,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        # Cleaning the NaN values.
        training_data = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=training_data,
            replacement_value="0",
            #replacement_type_name="float",
        ).outputs["transformed_table"]
    
        network = create_fully_connected_pytorch_network_op(
            input_size=len(feature_columns),
            # Optional:
            hidden_layer_sizes=[10],
            activation_name="elu",
            # output_activation_name=None,
            # output_size=1,
        ).outputs["model"]
    
        model = train_pytorch_model_from_csv_op(
            model=network,
            training_data=training_data,
            label_column_name=label_column,
            # Optional:
            #loss_function_name="mse_loss",
            #number_of_epochs=1,
            #learning_rate=0.1,
            #optimizer_name="Adadelta",
            #optimizer_parameters={},
            #batch_size=32,
            #batch_log_interval=100,
            #random_seed=0,
        ).outputs["trained_model"]
    
        model_archive = create_pytorch_model_archive_with_base_handler_op(
            model=model,
            # Optional:
            # model_name="model",
            # model_version="1.0",
        ).outputs["Model archive"]
    
        vertex_model_name = upload_PyTorch_model_archive_to_Google_Cloud_Vertex_AI_op(
            model_archive=model_archive,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func=train_tabular_regression_model_using_PyTorch_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### XGBoost

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    split_rows_into_subsets_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/dataset_manipulation/Split_rows_into_subsets/in_CSV/component.yaml")
    train_XGBoost_model_on_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/XGBoost/Train/component.yaml")
    xgboost_predict_on_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/XGBoost/Predict/component.yaml")
    upload_XGBoost_model_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_XGBoost_model/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_regression_model_using_XGBoost_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        training_set_fraction = 0.8
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        all_columns = [label_column] + feature_columns
    
        dataset = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        dataset = select_columns_using_Pandas_on_CSV_data_op(
            table=dataset,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        dataset = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=dataset,
            replacement_value="0",
            # # Optional:
            # column_names=None,  # =[...]
        ).outputs["transformed_table"]
    
        split_task = split_rows_into_subsets_op(
            table=dataset,
            fraction_1=training_set_fraction,
        )
        training_data = split_task.outputs["split_1"]
        testing_data = split_task.outputs["split_2"]
    
        model = train_XGBoost_model_on_CSV_op(
            training_data=training_data,
            label_column_name=label_column,
            # Optional:
            #starting_model=None,
            #num_iterations=10,
            #booster_params={},
            #objective="reg:squarederror",
            #booster="gbtree",
            #learning_rate=0.3,
            #min_split_loss=0,
            #max_depth=6,
        ).outputs["model"]
    
        # Predicting on the testing data
        predictions = xgboost_predict_on_CSV_op(
            data=testing_data,
            model=model,
            # label_column needs to be set when doing prediction on a dataset that has labels
            label_column_name=label_column,
        ).outputs["predictions"]
    
        vertex_model_name = upload_XGBoost_model_to_Google_Cloud_Vertex_AI_op(
            model=model,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func = train_tabular_regression_model_using_XGBoost_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

### Scikit-learn

    # python3 -m pip install "kfp<2.0.0" "google-cloud-aiplatform>=1.16.0" --upgrade --quiet
    from kfp import components
    
    # %% Loading components
    download_from_gcs_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/storage/download/component.yaml")
    select_columns_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Select_columns/in_CSV_format/component.yaml")
    fill_all_missing_values_using_Pandas_on_CSV_data_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/pandas/Fill_all_missing_values/in_CSV_format/component.yaml")
    train_linear_regression_model_using_scikit_learn_from_CSV_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/1f5cf6e06409b704064b2086c0a705e4e6b4fcde/community-content/pipeline_components/ML_frameworks/Scikit_learn/Train_linear_regression_model/from_CSV/component.yaml")
    upload_Scikit_learn_pickle_model_to_Google_Cloud_Vertex_AI_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Upload_Scikit-learn_pickle_model/component.yaml")
    deploy_model_to_endpoint_op = components.load_component_from_url("https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/399405402d95f4a011e2d2e967c96f8508ba5688/community-content/pipeline_components/google-cloud/Vertex_AI/Models/Deploy_to_endpoint/component.yaml")
    
    # %% Pipeline definition
    def train_tabular_regression_linear_model_using_Scikit_learn_pipeline():
        dataset_gcs_uri = "gs://ml-pipeline-dataset/Chicago_taxi_trips/chicago_taxi_trips_2019-01-01_-_2019-02-01_limit=10000.csv"
        feature_columns = ["trip_seconds", "trip_miles", "pickup_community_area", "dropoff_community_area", "fare", "tolls", "extras"]  # Excluded "trip_total"
        label_column = "tips"
        all_columns = [label_column] + feature_columns
        # Deploying the model might incur additional costs over time
        deploy_model = False
    
        training_data = download_from_gcs_op(
            gcs_path=dataset_gcs_uri
        ).outputs["Data"]
    
        training_data = select_columns_using_Pandas_on_CSV_data_op(
            table=training_data,
            column_names=all_columns,
        ).outputs["transformed_table"]
    
        # Cleaning the NaN values.
        training_data = fill_all_missing_values_using_Pandas_on_CSV_data_op(
            table=training_data,
            replacement_value="0",
            #replacement_type_name="float",
        ).outputs["transformed_table"]
    
        model = train_linear_regression_model_using_scikit_learn_from_CSV_op(
            dataset=training_data,
            label_column_name=label_column,
        ).outputs["model"]
    
        vertex_model_name = upload_Scikit_learn_pickle_model_to_Google_Cloud_Vertex_AI_op(
            model=model,
        ).outputs["model_name"]
    
        # Deploying the model might incur additional costs over time
        if deploy_model:
            sklearn_vertex_endpoint_name = deploy_model_to_endpoint_op(
                model_name=vertex_model_name,
            ).outputs["endpoint_name"]
    
    pipeline_func = train_tabular_regression_linear_model_using_Scikit_learn_pipeline
    
    # %% Pipeline submission
    if __name__ == '__main__':
        from google.cloud import aiplatform
        aiplatform.PipelineJob.from_pipeline_func(pipeline_func=pipeline_func).submit()

Note the following about code samples provided:

  - A Kubeflow pipeline is defined as a Python function.
  - The pipeline's workflow steps are created using Kubeflow pipeline components. By using the outputs of a component as an input of another component, you define the pipeline's workflow as a graph. For example, the `fill_all_missing_values_using_Pandas_on_CSV_data_op` component task depends on the `transformed_table` output from the `select_columns_using_Pandas_on_CSV_data_op` component task.
  - You create a pipeline run on Gemini Enterprise Agent Platform Pipelines using the Agent Platform SDK for Python.

## Monitor the pipeline

In the Google Cloud console, in the Agent Platform section, go to the **Pipelines** page and open the **Runs** tab.

## What's next

  - To learn more about Gemini Enterprise Agent Platform Pipelines, see [Introduction to Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) .
