---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/data-classes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/data-classes
title: Data classes
description: Learn about each data-related class in the Vertex AI SDK.
data_source: docs.cloud.google.com
---

The Vertex AI SDK includes classes that store and read data used to train a model. Each data-related class represents a Gemini Enterprise Agent Platform managed dataset that has structured data, unstructured data, or Vertex AI Feature Store data. After you create a dataset, you use it to train your model.

The following topics provide brief explanations of each data-related class in the Vertex AI SDK. The topic for each class includes a code example that shows how to create an instance of that class. After you create a dataset, you can use its ID to retrieve it:

    dataset = aiplatform.ImageDataset('projects/my-project/location/my-region/datasets/{DATASET_ID}')

## Structured data classes

The following classes work with structured data, which is organized in rows and columns. Structured data is often used to store numbers, dates, values, and strings.

### [`TabularDataset`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset)

Use this class to work with tabular datasets. You can use a CSV file, BigQuery, or a pandas [`DataFrame`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) to create a tabular dataset. For more information about paging through BigQuery data, see [Read data with BigQuery API using pagination](https://docs.cloud.google.com/bigquery/docs/paging-results) . For more information about tabular data, see [Tabular data](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/overview) .

The following code shows you how to create a tabular dataset by importing a CSV file.

    my_dataset = aiplatform.TabularDataset.create(
        display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])

The following code shows you how to create a tabular dataset by importing a CSV file in two distinct steps.

    my_dataset = aiplatform.TextDataset.create(
        display_name="my-dataset")
    
    my_dataset.import(
        gcs_source=['gs://path/to/my/dataset.csv']
        import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
    )

If you create a tabular dataset with a pandas [`DataFrame`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) , you need to use a BigQuery table to stage the data for Gemini Enterprise Agent Platform:

    my_dataset = aiplatform.TabularDataset.create_from_dataframe(
        df_source=my_pandas_dataframe,
        staging_path=f"bq://{bq_dataset_id}.table-unique"
    )

### [`TimeSeriesDataset`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDataset)

Use this class to work with time series datasets. A time series is a dataset that contains data recorded at different time intervals. The dataset includes time and at least one variable that's dependent on time. You use a time series dataset for forecasting predictions. For more information, see [Forecasting overview](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) .

You can create a managed time series dataset from CSV files in a Cloud Storage bucket or from a BigQuery table.

The following code shows you how to create a `TimeSeriesDataset` by importing a CSV data source file that has the time series dataset:

    my_dataset = aiplatform.TimeSeriesDataset.create(
        display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])

The following code shows you how to create a `TimeSeriesDataset` by importing a BigQuery table file that has the time series dataset:

    my_dataset = aiplatform.TimeSeriesDataset.create(
        display_name="my-dataset", bq_source=['bq://path/to/my/bigquerydataset.train'])

## Unstructured data classes

The following classes work with unstructured data, which can't be stored in a traditional relational database. It's often stored as audio, text, video files, or as a NoSQL database.

### [`ImageDataset`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ImageDataset)

Use this class to work with a managed image dataset. To create a managed image dataset, you need a data source file in CSV format and a schema file in YAML format. A schema is optional for a custom model. The CSV file and the schema are accessed in Cloud Storage buckets.

Use image data for the following objectives:

  - Single-label classification. For more information, see [Prepare image training data for single-label classification](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#single-label-classification) .
  - Multi-label classification. For more information, see [Prepare image training data for multi-label classification](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#multi-label-classification) .
  - Object detection. For more information, see [Prepare image training data for object detection](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/prepare-data) .

The following code shows you how to create image dataset by importing a CSV data source file and a YAML schema file. The schema file you use depends on whether your image dataset is used for single-label classification, multi-label classification, or object detection.

    my_dataset = aiplatform.ImageDataset.create(
        display_name="my-image-dataset",
        gcs_source=['gs://path/to/my/image-dataset.csv'],
        import_schema_uri=['gs://path/to/my/schema.yaml']
        )

## Vertex AI Feature Store data classes

Vertex AI Feature Store is a managed service used to store, serve, manage, and share ML features at scale.

Vertex AI Feature Store uses a time series data model composed of three classes that maintain features as they change over time. The three classes are organized in the following hierarchical order:

![Vertex AI Feature Store class hierarchy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/images/FeatureStore-class-hierarchy.svg "Vertex AI Feature Store class hierarchy diagram")

For more information about the Vertex AI Feature Store data model, see [Data model and resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/concepts) . To learn about Vertex AI Feature Store data source requirements, see [Source data requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/source-data) .

The following classes are used with Vertex AI Feature Store data:

### [`Featurestore`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore)

The featurestore resource, represented by the [`Featurestore`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore) class, is the top-level class in the Vertex AI Feature Store data model hierarchy. The next level resource in the data model is entity type, which is a collection of semantically related features that you create. The following are some of the [`Featurestore`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore) methods that work with entity types:

#### Create an entity type

Use the [`Featurestore`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore) . [`create_entity_type`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatformFeaturestore#google_cloud_aiplatform_Featurestore_create_entity_type) method with an `entity_type_id` to create an entity type resource. An entity type resource is represented by the `EntityType` class. The `entity_type_id` is alphanumeric and must be unique in a featurestore. The following is an example of how you can create an entity type:

    entity_type = aiplatform.featurestore.create_entity_type(
            entity_type_id=my_entity_type_name, description=my_entity_type_description
            )

#### Serve entity types

Use one of three [`Featurestore`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore) methods to serve entity data items:

  - [`batch_serve_to_bq`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore#google_cloud_aiplatform_Featurestore_batch_serve_to_bq) serves data to a BigQuery table.

  - [`batch_serve_to_df`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore#google_cloud_aiplatform_Featurestore_batch_serve_to_df) serves data to a pandas [`DataFrame`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) .

  - [`batch_serve_to_gcs`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore#google_cloud_aiplatform_Featurestore_batch_serve_to_gcs) serves data to a CSV file or a TensorFlow [`TFRecord`](https://www.tensorflow.org/tutorials/load_data/tfrecord#tfrecords_format_details) file.

### [`EntityType`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType)

The [`EntityType`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType) class represents an entity type resource, which is a collection of semantically related features that you define. For example, a music service might have the entity types `musical_artist` and `user` . You can use use the [`FeatureStore.create_entity_type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/data-classes#feature-store-create-entity-type) method or the [`EntityType.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType#google_cloud_aiplatform_EntityType_create) method to create an entity type. The following code shows how to use [`EntityType.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType#google_cloud_aiplatform_EntityType_create) :

    entity_type = aiplatform.EntityType.create(
            entity_type_id=my_entity_type_name, featurestore_name=featurestore_name
        )

### [`Feature`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature)

The [`Feature`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature) class represents a feature resource which is a measurable property or attribute of an entity type. For example, the `musical_artist` entity type might have features, such as `date_of_birth` and `last_name` , to track various properties of musical artists. Features must be unique to an entity type, but don't need to be globally unique.

When you create a [`Feature`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature) , you must specify its value type (for example, `BOOL_ARRAY` , `DOUBLE` , `DOUBLE_ARRAY` , or `STRING` ). The following code shows an example of how to to create a feature:

    my_feature = aiplatform.Feature.create(
        feature_id='my_feature_id',
        value_type='INT64',
        entity_type_name='my_entity_type_id',
        featurestore_id='my_featurestore_id',
    )

## What's next

  - Learn about the [Vertex AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .
