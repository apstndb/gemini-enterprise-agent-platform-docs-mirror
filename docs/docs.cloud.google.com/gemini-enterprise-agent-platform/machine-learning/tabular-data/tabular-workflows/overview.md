---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/overview
title: Tabular Workflows on Agent Platform
description: Learn about how Tabular Workflows provides end-to-end machine learning (ML) services for working with tabular data in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Tabular Workflows is a set of integrated, fully managed, and scalable pipelines for end-to-end ML with tabular data. It leverages Google's technology for model development and provides you with customization options to fit your needs.

## Benefits

  - Fully managed: you don't need to worry about updates, dependencies and conflicts.
  - Easy to scale: you don't need to re-engineer infrastructure as workloads or datasets grow.
  - Optimized for performance: the right hardware is automatically configured for the workflow's requirements.
  - Deeply integrated: compatibility with products in the Gemini Enterprise Agent Platform MLOps suite, like Gemini Enterprise Agent Platform Pipelines and Vertex AI Experiments, lets you run many experiments in a short amount of time.

## Technical Overview

Each workflow is a managed instance of Gemini Enterprise Agent Platform Pipelines.

[Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/vertex-ai/docs/pipelines/introduction) is a serverless service that runs Kubeflow pipelines. You can use pipelines to automate and monitor your machine learning and data preparation tasks. Each step in a pipeline performs part of the pipeline's workflow. For example, a pipeline can include steps to split data, transform data types, and train a model. Since steps are instances of pipeline components, steps have inputs, outputs, and a container image. Step inputs can be set from the pipeline's inputs or they can depend on the output of other steps within this pipeline. These dependencies define the pipeline's workflow as a directed acyclic graph.

<https://docs.cloud.google.com/static/vertex-ai/docs/tabular-data/images/tabular-workflows.png>

## Get started

In most cases, define and run the pipeline using the [Google Cloud Pipeline Components SDK](https://pypi.org/project/google-cloud-pipeline-components/) . The following sample code illustrates this process. Note that the actual implementation of the code might differ.

``` 
  // Define the pipeline and the parameters
  template_path, parameter_values = tabular_utils.get_default_pipeline_and_parameters(
     …
      optimization_objective=optimization_objective,
      data_source=data_source,
      target_column_name=target_column_name
     …)
```

``` 
  // Run the pipeline
  job = pipeline_jobs.PipelineJob(..., template_path=template_path, parameter_values=parameter_values)
  job.run(...)
```

For sample colabs and notebooks, contact your sales representative or fill out a [request form](https://forms.gle/PGFzdf5gtZHfWTtw9) .

## Versioning and maintenance

Tabular Workflows have an effective versioning system that allows for continuous updates and improvements without breaking changes to your applications.

Each workflow is releases and updated as part of the [Google Cloud Pipeline Components SDK](https://pypi.org/project/google-cloud-pipeline-components/) . Updates and modifications to any workflow are released as new versions of that workflow. Previous versions of every workflow are always available through the older versions of the SDK. If the SDK version is pinned, the workflow version is also pinned.

## Available workflows

Agent Platform provides the following Tabular Workflows:

| **Name**                                                                                                                                  | **Type**                    | **Availability**    |
| ----------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- | ------------------- |
| [Feature Transform Engine](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview#feature-transform-engine) | Feature Engineering         | Public Preview      |
| [End-to-End AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview#cr-e2e-automl)                   | Classification & Regression | Generally Available |
| [Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview#forecasting)                           | Forecasting                 | Public Preview      |

For additional information and sample notebooks, contact your sales representative or fill out a [request form](https://forms.gle/PGFzdf5gtZHfWTtw9) .

## Feature Transform Engine

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Feature Transform Engine performs feature selection and feature transformations. If feature selection is enabled, Feature Transform Engine creates a ranked set of important features. If feature transformations are enabled, Feature Transform Engine processes the features to ensure that the input for model training and model serving is consistent. Feature Transform Engine can be used on its own or together with any of the [tabular training workflows](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview) . It supports both TensorFlow and non-TensorFlow frameworks.

For more information, see [Feature engineering](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/feature-engineering) .

## Tabular Workflows for classification and regression

### Tabular Workflow for End-to-End AutoML

Tabular Workflow for End-to-End AutoML is a complete AutoML pipeline for classification and regression tasks. It is similar to the [AutoML API](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/overview) , but allows you to choose what to control and what to automate. Instead of having controls for the *whole* pipeline, you have controls for *every step* in the pipeline. These pipeline controls include:

  - Data splitting
  - Feature engineering
  - Architecture search
  - Model training
  - Model ensembling
  - Model distillation

#### Benefits

  - Supports **large datasets** that are multiple TB in size and have up to 1000 columns.
  - Allows you to **improve stability and lower training time** by limiting the search space of architecture types or skipping architecture search.
  - Allows you to **improve training speed** by manually selecting the hardware used for training and architecture search.
  - Allows you to **reduce model size and improve latency** with distillation or by changing the ensemble size.
  - Each AutoML component can be inspected in a powerful pipelines graph interface that lets you see the transformed data tables, evaluated model architectures, and many more details.
  - Each AutoML component gets extended flexibility and transparency, such as being able to customize parameters, hardware, view process status, logs, and more.

#### Input-Output

  - Takes a BigQuery table or a CSV file from Cloud Storage as input.
  - Produces an Agent Platform model as output.
  - Intermediate outputs include dataset statistics and dataset splits.

For more information, see [Tabular Workflow for End-to-End AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/e2e-automl) .

## Tabular Workflows for forecasting

### Tabular Workflow for Forecasting

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Tabular Workflow for Forecasting is the complete pipeline for forecasting tasks. It is similar to the [AutoML API](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) , but lets you to choose what to control and what to automate. Instead of having controls for the *whole* pipeline, you have controls for *every step* in the pipeline. These pipeline controls include:

  - Data splitting
  - Feature engineering
  - Architecture search
  - Model training
  - Model ensembling

#### Benefits

  - Supports **large datasets** that are up to 1TB in size and have up to 200 columns.
  - Lets you **improve stability and lower training time** by limiting the search space of architecture types or skipping architecture search.
  - Lets you **improve training speed** by manually selecting the hardware used for training and architecture search.
  - Lets you **reduce model size and improve latency** by changing the ensemble size.
  - Each component can be inspected in a powerful pipelines graph interface that lets you see the transformed data tables, evaluated model architectures and many more details.
  - Each component gets extended flexibility and transparency, such as being able to customize parameters, hardware, view process status, logs and more.

#### Input-Output

  - Takes a BigQuery table or a CSV file from Cloud Storage as input.
  - Produces an Agent Platform model as output.
  - Intermediate outputs include dataset statistics and dataset splits.

For more information, see [Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting) .

## What's next

  - Learn about [Tabular Workflow for End-to-End AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/e2e-automl) .
  - Learn about [Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting) .
  - Learn about [Pricing for Tabular Workflows](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/pricing) .
