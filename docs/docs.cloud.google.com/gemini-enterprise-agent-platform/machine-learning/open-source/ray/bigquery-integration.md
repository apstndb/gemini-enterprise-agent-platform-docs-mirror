---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/bigquery-integration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/bigquery-integration
title: Use Ray on Agent Platform with BigQuery
description: Covers how to read from and write to a BigQuery database from your Ray cluster on Gemini Enterprise Agent Platform using the Agent Platform SDK for Python.
data_source: docs.cloud.google.com
---

When you run a Ray application on Gemini Enterprise Agent Platform, use [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) as your cloud database. This section covers how to read from and write to a BigQuery database from your Ray cluster on Gemini Enterprise Agent Platform. The steps in this section assume that you use the Agent Platform SDK for Python.

To read from a BigQuery dataset, [create a new BigQuery dataset](https://docs.cloud.google.com/bigquery/docs/datasets) or use an existing dataset.

## Import and initialize Ray on Agent Platform client

If you're connected to your Ray cluster on Gemini Enterprise Agent Platform, restart your kernel and run the following code. The `runtime_env` variable is necessary at connection time to run BigQuery commands.

    import ray
    from google.cloud import aiplatform
    
    # The CLUSTER_RESOURCE_NAME is the one returned from vertex_ray.create_ray_cluster.
    address = 'vertex_ray://{}'.format(CLUSTER_RESOURCE_NAME)
    
    runtime_env = {
        "pip":
           ["google-cloud-aiplatform[ray]","ray==2.47.1"]
      }
    
    ray.init(address=address, runtime_env=runtime_env)

## Read data from BigQuery

Read data from your BigQuery dataset. A [Ray Task](https://docs.ray.io/en/latest/ray-core/tasks.html) must perform the read operation.

> **Note:** The maximum query response size is 10 GB.

    aiplatform.init(project=PROJECT_ID, location=LOCATION)
    
    @ray.remote
    def run_remotely():
        import vertex_ray
        dataset = DATASET
        parallelism = PARALLELISM
        query = QUERY
    
        ds = vertex_ray.data.read_bigquery(
            dataset=dataset,
            parallelism=parallelism,
            query=query
        )
        ds.materialize()

Where:

  - **PROJECT\_ID** : Google Cloud project ID. Find the project ID in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

  - **LOCATION** : The location where the `Dataset` is stored. For example, `us-central1` .

  - **DATASET** : BigQuery dataset. It must be in the format `dataset.table` . Set to `None` if you provide a query.

  - **PARALLELISM** : An integer that influences how many read tasks are created in parallel. There may be fewer read streams created than you requested.

  - **QUERY** : A string containing a SQL query to read from BigQuery database. Set to `None` if no query is required.

## Transform data

Update and delete rows and columns from your BigQuery tables using `pyarrow` or `pandas` . If you want to use `pandas` transformations, keep the input type as pyarrow and convert to `pandas` within the user-defined function (UDF) so you can catch any `pandas` conversion type errors within the UDF. A [Ray Task](https://docs.ray.io/en/latest/ray-core/tasks.html) must perform the transformation.

    @ray.remote
    def run_remotely():
        # BigQuery Read first
        import pandas as pd
        import pyarrow as pa
    
        def filter_batch(table: pa.Table) -> pa.Table:
            df = table.to_pandas(types_mapper={pa.int64(): pd.Int64Dtype()}.get)
            # PANDAS_TRANSFORMATIONS_HERE
            return pa.Table.from_pandas(df)
    
        ds = ds.map_batches(filter_batch, batch_format="pyarrow").random_shuffle()
        ds.materialize()
    
        # You can repartition before writing to determine the number of write blocks
        ds = ds.repartition(4)
        ds.materialize()

## Write data to BigQuery

Insert data to your BigQuery dataset. A [Ray Task](https://docs.ray.io/en/latest/ray-core/tasks.html) must perform the write.

    @ray.remote
    def run_remotely():
        # BigQuery Read and optional data transformation first
        dataset=DATASET
        vertex_ray.data.write_bigquery(
            ds,
            dataset=dataset
        )

Where:

  - **DATASET** : BigQuery dataset. The dataset must be in the format `dataset.table` .

## What's next

  - [Deploy a model on Gemini Enterprise Agent Platform and get predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/deploy-predict)

  - [View logs for your Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/view-logs)

  - [Delete a Ray cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/delete-cluster)
