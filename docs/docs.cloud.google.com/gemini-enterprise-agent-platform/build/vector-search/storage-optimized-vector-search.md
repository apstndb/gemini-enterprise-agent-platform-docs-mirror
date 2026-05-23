---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/storage-optimized-vector-search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/storage-optimized-vector-search
title: Storage-optimized Vector Search
description: Learn about storage-optimized Vector Search.
data_source: docs.cloud.google.com
---

The storage-optimized performance tier for Vector Search is designed for indexing and searching massive datasets. This tier implements a disk-based architecture instead of using RAM, significantly reducing your operational costs. When your priority is cost efficiency at scale as opposed to the lowest possible query latency, the storage-optimized tier is your best choice.

> **Important:** Currently, when using Vector Search, you are billed for 2 replicas.

## When to use a storage-optimized index

Consider storage-optimized indexes if you have any of the following:

  - **A very large dataset** : You must index very large numbers of vectors, and the cost of hosting a large number of performance-optimized shards is prohibitive.

  - **A low-QPS workload** : In low-query-volume applications, the cost savings from using fewer shards can be significant.

  - **Flexible latency requirements** : Your application can tolerate a minor increase in query latency, which is the time it takes to get a search result.

## Performance trade-offs

Compared to the default performance-optimized index, a storage-optimized index has the following characteristics:

  - **Increased query latency** : Queries have a slightly higher latency at a given recall level.

## How to configure a storage-optimized index

[To create an index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/create-manage-index) that is storage-optimized, set the `shardSize` parameter to `SHARD_SIZE_SO_DYNAMIC` in your index configuration.

> **Important:** Don't specify the `algorithm_config` field. Over time, Vector Search automatically picks which algorithm to use and adjusts its configuration based on your data and query patterns.

## Example: Creating a storage-optimized index

The following example demonstrates the JSON that's required to create a new storage-optimized streaming index.

    {
      "displayName": "my-storage-optimized-index",
      "description": "An index configured to prioritize storage over performance.",
      "metadata": {
        "contentsDeltaUri": "gs://your-bucket/source-data/",
        "config": {
          "dimensions": 100,
          "approximateNeighborsCount": 150,
          "distanceMeasureType": "DOT_PRODUCT_DISTANCE",
          "shardSize": "SHARD_SIZE_SO_DYNAMIC"
        }
      },
      "indexUpdateMethod": "STREAM_UPDATE"
    }

In the example, `shardSize` is set to `SHARD_SIZE_SO_DYNAMIC` , which instructs Vector Search to build a denser index. This allows each shard to hold significantly more data points, thereby reducing the total number of shards needed for your dataset. Other fields, such as `dimensions` and `distanceMeasureType` , are configured according to your needs.

## Endpoints

Storage-optimized deployments can be used with any existing endpoint.

## Deploy an index

The following example demonstrates the JSON required to deploy a storage-optimized index to an endpoint you've created.

    {
      "deployedIndex": {
        "id": "PROJECT_UNIQUE_ID_NAME",
        "index": "projects/PROJECT_ID/locations/LOCATION/indexes/INDEX_ID",
        "displayName": "INDEX_DISPLAY_NAME",
        "deploymentTier": "STORAGE"
      }
    }

Setting `deploymentTier` to `STORAGE` deploys the storage-optimized index with the specified `displayName` to an endpoint.

You can also specify the minimum replicant count ( `minReplicaCount` ) and maximum replicant count ( `minReplicaCount` ) to control the number of machine replicas to deploy on. Setting the machine type ( `machineType` ) is not supported.

## What's next?

  - [Create and manage your index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/create-manage-index)
  - [Index configuration parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/configuring-indexes)
