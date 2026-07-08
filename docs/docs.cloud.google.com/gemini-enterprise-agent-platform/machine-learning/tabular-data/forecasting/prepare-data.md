---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data
title: Prepare training data
description: Prepare your tabular data for training forecast models in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page describes how to prepare your tabular data for training forecast models.

This page covers the following topics:

1.  [Data structure requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#data-structure)
2.  [Prepare your import source](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#import-source)
3.  [Add weights to your training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data#weight)

By default, Agent Platform uses a [chronological split](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits#forecasting-default) algorithm to separate your forecasting data into three data splits. Alternatively, you can use a [manual split](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits#forecasting-manual) , but this requires you to prepare a data split column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits) about data splits.

## Data structure requirements

For forecasting models, your training data must conform to the following basic requirements:

| Requirement Type              | Requirement                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size                          | The dataset must be 100 GB or smaller.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| \# of columns                 | The dataset must have at least 3 and no more than 100 columns. Each of the observations in the dataset must have a target and a time, both of which act as features. Furthermore, each observation must have a time series ID, which identifies the time series that the observation is part of. Ideally, your training data has many more than 3 columns. The maximum number of columns includes both feature and non-feature columns.                                                                                                                                                                                                                                                                                                                                                                     |
| Target column                 | Specify a target column. The target column lets Gemini Enterprise Agent Platform associate the training data with the desired result. It must not contain null values and must be Numerical.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Time column                   | You must specify a time column and it must have a value for every row. The time column indicates the time at which a given observation was made.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Time series identifier column | You must specify a time series identifier column and it must have a value for every row. Forecasting training data usually includes multiple time series, and the identifier tells Agent Platform which time series a given observation in the training data is part of. All of the rows in a given time series have the same value in the time series identifier column. Some common time series identifiers might be the product ID, a store ID, or a region. It is possible to train a forecasting model on a single time series, with an identical value for all rows in the time series identifier column. However, Agent Platform is a better fit for training data that contains two or more time series. For best results, use at least 10 time series for every column you use to train the model. |
| Column name format            | The column name can include any alphanumeric character or an underscore ( `_` ). The column name cannot begin with an underscore.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| \# of rows                    | The dataset must have at least 1,000 and no more than 100,000,000 rows. If there are more than 100,000,000 rows, consider down-sampling. For more information, see [Rolling window strategies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#rolling-window-strategies) . Depending on how many features your dataset has, 1,000 rows might not be enough to train a high-performing model. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/bp-tabular#how-many-rows) .                                                                                                                                                                                                                      |
| Data format                   | Use narrow (sometimes called long) [data format](https://en.wikipedia.org/wiki/Wide_and_narrow_data) . In narrow format, each row represents the item specified by the time series identifier for a specific point in time, along with all of the data for that item at that point in time. [Learn how to choose the data format](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/bp-tabular#data-format) .                                                                                                                                                                                                                                                                                                                                                                     |
| Interval between rows         | The interval between your training rows must be consistent. This is your data *granularity* ; it affects how the model is trained and the frequency of inference results. [Learn how to choose the data granularity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/bp-tabular#granularity) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Time series length            | The length of a time series must not exceed 3000 time steps.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## Prepare your import source

You can provide model training data to Gemini Enterprise Agent Platform in two formats:

  - BigQuery tables
  - Comma-separated values (CSV)

The source you use depends on how you store your data, and the size and complexity of your data. If your dataset is small, and you don't need more complex data types, CSV might be easier. For larger datasets that include arrays and structs, use BigQuery.

### BigQuery

Your BigQuery table or view must conform to the [BigQuery location requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#bq-locations) .

If your BigQuery table or view is in a different project than the project where you are creating your Agent Platform dataset, or your BigQuery table or view is backed by an external data source, add one or more roles to the Agent Platform Service Agent. See [Role addition requirements for BigQuery](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#bq-roles) .

You don't need to specify a schema for your BigQuery table. Agent Platform automatically infers the schema for your table when you import your data.

Your BigQuery URI (specifying the location of your training data) must conform to the following format:

    bq://<project_id>.<dataset_id>.<table_id>

The URI cannot contain any other special characters.

For information about BigQuery data types and how they map into Agent Platform, see [BigQuery tables](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#bq) . For more information about using BigQuery external data sources, see [Introduction to external data sources](https://docs.cloud.google.com/bigquery/external-data-sources) .

### CSV

CSV files can be in Cloud Storage, or on your local computer. They must conform to the following requirements:

  - The first line of the first file must be a header, containing the names of the columns. If the first row of a subsequent file is the same as the header, then it is also treated as a header, otherwise it's treated as data.

  - Column names can include any alphanumeric character or an underscore (\_). The column name cannot begin with an underscore.

  - Each file must not be larger than 10 GB.
    
    You can include multiple files, up to a maximum amount of 100 GB.

  - The delimiter must be a comma (",").

You don't need to specify a schema for your CSV data. Agent Platform automatically infers the schema for your table when you import your data, and uses the header row for column names.

For more information about CSV file format and data types, see [CSV files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#csv) .

If you import your data from Cloud Storage, it must be in a bucket that meets the following requirements:

  - It conforms to the [Agent Platform bucket requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#buckets) .
  - If the bucket is not in the same project as Agent Platform, add one or more roles to the Agent Platform Service Agent. See [Role addition requirements for Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#storage-roles) .

If you import your data from your local computer, you must have a Cloud Storage bucket that meets the following requirements:

  - It conforms to the [Agent Platform bucket requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#buckets) .

  - If the bucket is not in the same project as Agent Platform, add one or more roles to the Agent Platform Service Agent. See [Role addition requirements for Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#storage-roles) .
    
    Agent Platform uses this bucket as a staging area before importing your data.

## Add weights to your training data

By default, Agent Platform weighs each row of your training data equally. For training purposes, no row is considered more important than another.

Sometimes, you might want some rows to have more importance for training. For example, if you use spending data, you might want the data associated with higher spenders to have a larger impact on the model. If you particularly want to avoid missing a specific outcome, then weight rows with that outcome more heavily.

Add a weight column to your dataset to give rows a relative weight. The weight column must be a numeric column. The weight value can be 0‑10,000. Higher values indicate that the row is more important when training the model. A weight of 0 causes the row to be ignored. If you include a weight column, it must contain a value for every row.

Later, when you train your model, specify this column as the `Weight` column.

Custom weighting schemes are used only for training the model; they do not affect the test set used for model evaluation.

## What's next

  - [Create your dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/create-dataset) .
  - Learn about [best practices for creating tabular training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/bp-tabular) .
  - Learn how [Agent Platform works with different types of tabular data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular) .
