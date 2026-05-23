---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/migrate-kfp
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/migrate-kfp
title: Migrate from Kubeflow Pipelines to Gemini Enterprise Agent Platform Pipelines
description: Learn the best practices for migrating from Kubeflow Pipelines to Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

For developers with experience building Kubeflow pipelines it is important to understand the following ways that Agent Platform Pipelines is different from Kubeflow Pipelines.

### Data passing (inputs/outputs)

  - Data passing using inputs and outputs differs from Kubeflow Pipelines SDK v1 to Kubeflow Pipelines SDK v2. Kubeflow Pipelines SDK v2 has the separation of parameters and artifacts, and they can't be passed into one another. For more detailed information, see [Kubeflow Pipelines Pipelines Basics](https://www.kubeflow.org/docs/components/pipelines/v2/pipelines/pipeline-basics/) and [Kubeflow Pipelines Data Types](https://www.kubeflow.org/docs/components/pipelines/v2/data-types/) .

### Domain-specific language (DSL) version usage

  - Agent Platform Pipelines can run pipelines that were built using TFX v0.30.0 or later, *or* the Kubeflow Pipelines SDK v2 domain-specific language (DSL).
    
    The Kubeflow Pipelines SDK v2 DSL is available in Kubeflow Pipelines SDK v1.6 or later.
    
    Kubeflow Pipelines can run pipelines that were built using the Kubeflow Pipelines SDK. Kubeflow Pipelines v1.6 or later can also run pipelines built using the Kubeflow Pipelines SDK v2 DSL.

### Storage

  - Kubeflow Pipelines and Agent Platform Pipelines handle storage differently. In Kubeflow Pipelines you can make use of Kubernetes resources such as persistent volume claims. In Agent Platform Pipelines your data is stored on Cloud Storage, and mounted into your components using [Cloud Storage FUSE](https://docs.cloud.google.com/storage/docs/gcs-fuse) .
    
    In Agent Platform Pipelines, you can use Google Cloud services to make resources available — for example, you can use Cloud Storage FUSE to access a Cloud Storage bucket as a mounted volume in a pipeline step. If your Cloud Storage URI is `gs://example-bucket/example-pipeline` , then your pipeline component's container can use Cloud Storage FUSE to access that URI as the following path: `/gcs/example-bucket/example-pipeline` .
    
    > **Important:** It's best practice that you avoid hardcoding the paths to external resources into your pipeline. Instead, pass the paths to external resources into your pipeline as a parameter. This makes it easier for you to run your pipeline in different environments, and to change the location of the resources used in a pipeline run.

  - When you run a pipeline using Agent Platform Pipelines, the pipeline root must have been specified in the `@pipeline` annotation or when you created the pipeline run.
    
    In Kubeflow Pipelines, specifying the pipeline root is optional. The artifacts of a pipeline run are stored using [MinIO](https://min.io/) by default.

### Features not supported in Agent Platform Pipelines

  - The following Kubeflow Pipelines features are not supported in Agent Platform Pipelines.
    
      - **Cache Expiration** : In Kubeflow Pipelines, you can specify that cached component executions expire after a specified amount of time using the Kubeflow Pipelines SDK v1 DSL.
        
        You can't specify that component executions expire after a specified amount of time using the Kubeflow Pipelines SDK v2 DSL.
        
        In Agent Platform Pipelines, when you run a pipeline using `create_run_from_job_spec` you can use the `enable_caching` argument to specify that this pipeline run does not use caching.
    
      - **Recursion** : In Kubeflow Pipelines, you can specify pipeline components that are called recursively.
        
        Agent Platform Pipelines doesn't support pipeline components that are called recursively.
