---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-training-script
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-training-script
title: Create a training script
description: Create a Python script to pass to a training job as part of a tutorial that shows you how to use the Agent Platform SDK for Python to create a custom-trained model.
data_source: docs.cloud.google.com
---

To create a custom model, you need a Python training script that creates and trains the custom model. You initialize your training job with the Python training script, then invoke the training job's [`run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob#google_cloud_aiplatform_CustomTrainingJob_run) method to run the script.

In this topic, you create the training script, then specify command arguments for your training script.

## Create a training script

In this section, you create a training script. This script is a new file in your notebook environment named `task.py` . Later in this tutorial, you pass this script to the [`aiplatform.CustomTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) constructor. When the script runs, it does the following:

  - Loads the data in the BigQuery dataset you created.

  - Uses the [TensorFlow Keras API](https://www.tensorflow.org/api_docs/python/tf/keras) to build, compile, and train your model.

  - Specifies the number of epochs and the batch size to use when the Keras [`Model.fit`](https://www.tensorflow.org/api_docs/python/tf/keras/Model#fit) method is invoked.

  - Specifies where to save model artifacts using the `AIP_MODEL_DIR` environment variable. `AIP_MODEL_DIR` is set by Gemini Enterprise Agent Platform and contains the URI of a directory for saving model artifacts. For more information, see [Environment variables for special Cloud Storage directories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) .

  - Exports a TensorFlow [`SavedModel`](https://www.tensorflow.org/api_docs/python/tf/saved_model) to the model directory. For more information, see [Using the `SavedModel` format](https://www.tensorflow.org/guide/saved_model#the_savedmodel_format_on_disk) on the TensorFlow website.

To create your training script, run the following code in your notebook:

    %%writefile task.py
    
    import argparse
    import numpy as np
    import os
    
    import pandas as pd
    import tensorflow as tf
    
    from google.cloud import bigquery
    from google.cloud import storage
    
    # Read environmental variables
    training_data_uri = os.getenv("AIP_TRAINING_DATA_URI")
    validation_data_uri = os.getenv("AIP_VALIDATION_DATA_URI")
    test_data_uri = os.getenv("AIP_TEST_DATA_URI")
    
    # Read args
    parser = argparse.ArgumentParser()
    parser.add_argument('--label_column', required=True, type=str)
    parser.add_argument('--epochs', default=10, type=int)
    parser.add_argument('--batch_size', default=10, type=int)
    args = parser.parse_args()
    
    # Set up training variables
    LABEL_COLUMN = args.label_column
    
    # See https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/workbench/managed/executor#explicit-project-selection for issues regarding permissions.
    PROJECT_NUMBER = os.environ["CLOUD_ML_PROJECT_ID"]
    bq_client = bigquery.Client(project=PROJECT_NUMBER)
    
    
    # Download a table
    def download_table(bq_table_uri: str):
        # Remove bq:// prefix if present
        prefix = "bq://"
        if bq_table_uri.startswith(prefix):
            bq_table_uri = bq_table_uri[len(prefix) :]
    
        # Download the BigQuery table as a dataframe
        # This requires the "BigQuery Read Session User" role on the custom training service account.
        table = bq_client.get_table(bq_table_uri)
        return bq_client.list_rows(table).to_dataframe()
    
    # Download dataset splits
    df_train = download_table(training_data_uri)
    df_validation = download_table(validation_data_uri)
    df_test = download_table(test_data_uri)
    
    def convert_dataframe_to_dataset(
        df_train: pd.DataFrame,
        df_validation: pd.DataFrame,
    ):
        df_train_x, df_train_y = df_train, df_train.pop(LABEL_COLUMN)
        df_validation_x, df_validation_y = df_validation, df_validation.pop(LABEL_COLUMN)
    
        y_train = tf.convert_to_tensor(np.asarray(df_train_y).astype("float32"))
        y_validation = tf.convert_to_tensor(np.asarray(df_validation_y).astype("float32"))
    
        # Convert to numpy representation
        x_train = tf.convert_to_tensor(np.asarray(df_train_x).astype("float32"))
        x_test = tf.convert_to_tensor(np.asarray(df_validation_x).astype("float32"))
    
        # Convert to one-hot representation
        num_species = len(df_train_y.unique())
        y_train = tf.keras.utils.to_categorical(y_train, num_classes=num_species)
        y_validation = tf.keras.utils.to_categorical(y_validation, num_classes=num_species)
    
        dataset_train = tf.data.Dataset.from_tensor_slices((x_train, y_train))
        dataset_validation = tf.data.Dataset.from_tensor_slices((x_test, y_validation))
        return (dataset_train, dataset_validation)
    
    # Create datasets
    dataset_train, dataset_validation = convert_dataframe_to_dataset(df_train, df_validation)
    
    # Shuffle train set
    dataset_train = dataset_train.shuffle(len(df_train))
    
    def create_model(num_features):
        # Create model
        Dense = tf.keras.layers.Dense
        model = tf.keras.Sequential(
            [
                Dense(
                    100,
                    activation=tf.nn.relu,
                    kernel_initializer="uniform",
                    input_dim=num_features,
                ),
                Dense(75, activation=tf.nn.relu),
                Dense(50, activation=tf.nn.relu),
                Dense(25, activation=tf.nn.relu),
                Dense(3, activation=tf.nn.softmax),
            ]
        )
    
        # Compile Keras model
        optimizer = tf.keras.optimizers.RMSprop(lr=0.001)
        model.compile(
            loss="categorical_crossentropy", metrics=["accuracy"], optimizer=optimizer
        )
    
        return model
    
    # Create the model
    model = create_model(num_features=dataset_train._flat_shapes[0].dims[0].value)
    
    # Set up datasets
    dataset_train = dataset_train.batch(args.batch_size)
    dataset_validation = dataset_validation.batch(args.batch_size)
    
    # Train the model
    model.fit(dataset_train, epochs=args.epochs, validation_data=dataset_validation)
    
    tf.saved_model.save(model, os.getenv("AIP_MODEL_DIR"))

After you create the script, it appears in the root folder of your notebook: ![View training script.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/images/training-script.png)

## Define arguments for your training script

You pass the following command-line arguments to your training script:

  - `label_column` - This identifies the column in your data that contains what you want to predict. In this case, that column is `species` . You defined this in a variable named `LABEL_COLUMN` when you processed your data. For more information, see [Download, preprocess, and split the data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-dataset#download-process-public-dataset) .

  - `epochs` - This is the number of epochs used when you train your model. An *epoch* is an iteration over the data when training your model. This tutorial uses 20 epochs.

  - `batch_size` - This is the number of samples that are processed before your model updates. This tutorial uses a batch size of 10.

To define the arguments that are passed to your script, run the following code:

    JOB_NAME = "custom_job_unique"
    
    EPOCHS = 20
    BATCH_SIZE = 10
    
    CMDARGS = [
        "--label_column=" + LABEL_COLUMN,
        "--epochs=" + str(EPOCHS),
        "--batch_size=" + str(BATCH_SIZE),
    ]
