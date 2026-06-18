---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/dataproc-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/dataproc-component
title: Managed Service for Apache Spark components
description: Learn how to use Managed Service for Apache Spark components to run Apache Spark batch workloads in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

The Managed Service for Apache Spark components let you run Apache Spark batch workloads from a pipeline within Gemini Enterprise Agent Platform Pipelines. Managed Service for Apache Spark runs the batch workloads on a managed compute infrastructure, autoscaling resources as needed.

Learn more about [Managed Service for Apache Spark](https://docs.cloud.google.com/dataproc-serverless/docs/overview) and [supported Spark workloads](https://docs.cloud.google.com/dataproc-serverless/docs/overview#for_spark_workload_capabilities) .

In Managed Service for Apache Spark, a `Batch` resource represents a batch workload. The Google Cloud SDK includes the following operators to create `Batch` resources and monitor their execution:

  - [`DataprocPySparkBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocPySparkBatchOp)
  - [`DataprocSparkBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocSparkBatchOp)
  - [`DataprocSparkRBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocSparkRBatchOp)
  - [`DataprocSparkSqlBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocSparkSqlBatchOp)

## API reference

  - For component reference, see the [Google Cloud SDK reference for Managed Service for Apache Spark components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html) .

  - For Managed Service for Apache Spark resource reference, see the following API reference page:
    
      - [`Batch`](https://docs.cloud.google.com/dataproc-serverless/docs/reference/rest/v1/projects.locations.batches#resource:-batch) resource

## Tutorials

  - [Get started with Managed Service for Apache Spark pipeline components](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/ml_ops/stage3/get_started_with_dataproc_serverless_pipeline_components.ipynb)

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

## Technical support contacts

If you have any questions, reach out to [kfp-dataproc-components@google.com](mailto:%20kfp-dataproc-components@google.com) .
