---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types
title: Online serving types
description: Learn about Bigtable online serving and Optimized online serving in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

Vertex AI Feature Store offers the following types of online serving that you can use to serve features for online predictions:

  - [Bigtable online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#bigtable_serving)

  - [Optimized online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#optimized_serving) ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ), where you can choose one of the following configurations:
    
      - [Optimized online serving with public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#optimized_public)
    
      - [Optimized online serving with Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#optimized_private)

## Bigtable online serving

Bigtable online serving is suitable for large data volumes (in the order of terabytes of data) with high data durability. Bigtable online serving supports both [scheduled and continuous data sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#sync_featuredata) for its feature views.

Note that Bigtable online serving doesn't support embeddings management. If you want to manage and serve embeddings, use [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

To use Bigtable online serving, you need to perform the following steps:

1.  [Create an online store for Bigtable online serving.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore#create_fos_bigtable)

2.  [Create a feature view instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview)

3.  [Fetch feature values using Bigtable online serving.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#bigtable_serving)

## Optimized online serving

> Gemini Enterprise Agent Platform Feature Store Optimized online serving is [deprecated](https://docs.cloud.google.com/vertex-ai/docs/deprecations) . Beginning on May 17, 2026, no new features will be added and only critical patches will be provided. On February 17, 2027, the capability will be fully sunset and APIs will no longer be available.
> 
> To improve latency and cost optimizations, migrate to [Bigtable online serving](https://docs.cloud.google.com/vertex-ai/docs/featurestore/latest/online-serving-types#bigtable_serving) . To efficiently store and serve embeddings, use the purpose-built [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

With Optimized online serving, you can serve feature values from either a public endpoint or a Private Service Connect endpoint.

All online store instances created for Optimized online serving support embeddings management.

Optimized online serving supports scheduled data sync, but doesn't support continuous data sync for feature views. If you want to use continuous data sync to sync data from the BigQuery data source to your feature views in near real-time, use Bigtable online serving.

### Optimized online serving with public endpoint

By default, an online store created for Optimized online serving lets you serve features with a public endpoint. To use Optimized online serving with a public endpoint, you need to perform the following steps:

1.  [Create an online store for Optimized online serving with a public endpoint.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore#create_fos_optimized_public)

2.  [Create a feature view instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview)

3.  [Fetch feature values using Optimized online serving from a public endpoint.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#optimized_serving_public)

### Optimized online serving with Private Service Connect endpoint

A Private Service Connect endpoint is a dedicated serving endpoint. To use Optimized online serving with a Private Service Connect endpoint, you need to perform the following steps:

1.  [Create an online store for Optimized online serving with a Private Service Connect endpoint.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore#create_fos_optimized_private)

2.  [Create a feature view instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview)

3.  [Fetch feature values using Optimized online serving from the Private Service Connect endpoint.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#optimized_serving_private)

## Set up online serving to serve null feature values or only non-null feature values

During online serving, if you want to serve only the latest feature values, including null values, you must use the following setup:

1.  [Register your feature data source by creating a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) with the `dense` parameter set to `true` .

2.  Choose Bigtable online serving when you [create the online store instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore) .

3.  Use the `cron` parameter to set up scheduled data sync when you [create your feature views](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

If you use any other configuration while setting up your feature data source and online serving, Vertex AI Feature Store serves only the latest non-null feature values. If the latest value of a feature is null, then Vertex AI Feature Store serves the most recent non-null historical value for the feature. If a non-null historical value isn't available, then Vertex AI Feature Store serves null as the feature value.

## What's next

  - Learn how to [create an online store instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore) .

  - Learn how to [create a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

  - Learn how to [serve feature values](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values) .
