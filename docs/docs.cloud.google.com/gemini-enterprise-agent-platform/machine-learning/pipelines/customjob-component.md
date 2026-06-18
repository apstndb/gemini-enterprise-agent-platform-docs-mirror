---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/customjob-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/customjob-component
title: CustomJob components
description: Learn how to run custom training jobs as components within Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

[Custom training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) let you run your custom machine learning (ML) training code in Gemini Enterprise Agent Platform.

## `CustomTrainingJobOp`

The [`CustomTrainingJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.CustomTrainingJobOp) component exposes the full functionalities of the [`CustomJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs) , to allow both single and distributed training using a [`ContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#ContainerSpec) or [`PythonPackageSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec) instance.

## `create_custom_training_job_from_component` function

The [`create_custom_training_job_from_component`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component) utility converts a given container or Python component to a component that runs a custom job in Gemini Enterprise Agent Platform. This simplifies the creation of custom training jobs. All inputs and outputs of the supplied component will be copied over to the constructed training job operator.

Note that this utility constructs a `ClusterSpec` , where the primary and all the workers use the same specification, meaning all disk and machine specification-related parameters will apply to all replicas. This is suitable for use cases where, for example, you are training with [`MultiWorkerMirroredStrategy`](https://www.tensorflow.org/api_docs/python/tf/distribute/experimental/MultiWorkerMirroredStrategy) or [`MirroredStrategy`](https://www.tensorflow.org/api_docs/python/tf/distribute/MirroredStrategy) .

This component does not support `CustomJob` Python package training, or distributed training with different worker pool specs.

## API reference

  - For component reference, see the [Google Cloud SDK reference for CustomJob components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html) .
  - For Agent Platform API reference, see the [`CustomJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs) page.

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

## Technical support contacts

If you have any questions, reach out to [kubeflow-pipelines-components@google.com](mailto:%20kubeflow-pipelines-components@google.com) .
