---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/prepare-data-source
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/prepare-data-source
title: Prepare data source
description: Learn the guidelines to prepare your feature data source for serving features using Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

Before you can start serving features online using Vertex AI Feature Store, you need to set up your feature data source in BigQuery, as follows:

1.  Create a BigQuery table or view using your feature data. To load feature data into a BigQuery table or view, you can create a BigQuery dataset using the data, create a BigQuery table, and then load the feature data from the dataset into the table.

2.  After you load the feature data into the BigQuery table or view, you need to make this data source available to Vertex AI Feature Store for online serving. There are two ways in which you can connect the data source to online serving resources, such as online stores and feature view instances:
    
      - **Register the data source by creating feature groups and features:** You can associate feature groups and features with feature view instances in your online store. You can format the data in either of the following ways:
        
          - Format your data as a time series by including a feature timestamp column. Vertex AI Feature Store serves only the latest feature values for each unique entity ID, based on the feature timestamp in this column.
        
          - Format the data without including a feature timestamp columns. Vertex AI Feature Store manages the timestamps and serves only the latest feature values for each unique entity ID.
        
        For information about how to create feature groups, see [Create a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) . For information about how to create features within a feature group, see [create a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) .
    
      - **Directly serve features from the data source without creating feature groups and features:** You can specify the URI of the data source in the feature view. Note that in this scenario, you can't format your data as a time series or include historical data in the BigQuery source. Each row must contain the latest feature values corresponding to a unique ID. Multiple occurrences of the same entity ID in different rows are not supported.

Since Vertex AI Feature Store lets you maintain feature data in BigQuery and serves features from the BigQuery data source, there's no need to import or copy the features to an offline store.

## Data source preparation guidelines

Follow these guidelines to understand the schema and constraints while preparing the data source in BigQuery:

1.  Include the following columns in the data source:
    
      - **Entity ID columns** : The data source must have at least one entity ID column with `string` or `int` values. The default name for this column is `entity_id` . You can optionally use a different name for this column. The size of each value in this column must be less than 4 KB.
        
        Note that you can also designate a feature record by constructing the entity ID using features from multiple columns. In this scenario, you can include multiple entity ID columns in the data source. The name of each entity ID column must be unique. If you register the data source by creating feature groups, set the entity ID columns for each feature group. Otherwise, if you directly associate the data source with a feature view, configure the feature views to specify the entity ID columns.
        
        Note that you can include multiple ID columns in a data source. In such a scenario, the name of each entity ID column must be unique. You can configure your feature groups or feature views to construct the entity ID using the values from each column for a feature record.
    
      - **Feature timestamp column** : Optional. If you register the data source using feature groups and features, and need to format the data as a time series, include a feature timestamp column. The timestamp column contains values of type `timestamp` . The default name for the timestamp column is `feature_timestamp` . If you want to use a different column name, use the `time_series` parameter to set the timestamp column for the feature group.
        
        If you don't specify a timestamp column to format your data as a time series, Vertex AI Feature Store manages the timestamps for the features and serves the latest feature values.
        
        If you directly associate a BigQuery data source with a feature view, the `feature_timestamp` column isn't required. In this scenario, you must include only the latest feature values in the data source and Vertex AI Feature Store doesn't look up the timestamp.
    
      - **Embedding and filtering columns** : Optional. If you want to use embedding management in an online store created for Optimized online serving ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ), the data source must contain the following columns:
        
          - An `embedding` column containing arrays of type `float` .
        
          - Optional: One or more filtering columns of type `string` or `string` array.
        
          - Optional: A crowding column of type `int` .

2.  Each row in data source is a complete record of feature values associated with an entity ID. If a feature value is missing in one of the columns, then it's considered a null value.

3.  Each column of the BigQuery table or view represents a feature. Provide the values for each feature in a separate column. If you're associating the data source with a feature group and features, associate each column with a separate feature.

4.  Supported data types for feature values include `bool` , `int` , `float` , `string` , `timestamp` , arrays of these data types, and bytes. Note that during [data sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) , feature values of type `timestamp` are converted to `int64` .

5.  The data source must be located in the same region as the online store instance, or in a multi-region that includes or overlaps with the region for the online store. For example, if the online store is in `us-central` , the BigQuery source might be located in `us-central` or `US` .

6.  [Sync the data in a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#sync_featuredata) before online serving to ensure that you serve only the latest feature values. If you're using scheduled data sync, you might need to [manually sync the data in the feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) . However, if you're using continuous data sync with Optimized online serving, then you don't need to manually sync the data.

## What's next

  - Learn how to create [feature groups](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) and [features](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) .

  - Learn how to [create a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

  - [Online serving types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types) in Vertex AI Feature Store.
