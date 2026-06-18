---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/dataflow-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/dataflow-component
title: Dataflow components
description: Learn how to use Dataflow components in Gemini Enterprise Agent Platform Pipelines to execute Apache Beam jobs in Dataflow.
data_source: docs.cloud.google.com
---

The Dataflow components let you submit Apache Beam jobs to Dataflow for execution. In Dataflow, a [`Job`](https://docs.cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.jobs#Job) resource represents a Dataflow job.

The Google Cloud SDK includes the following operators for creating `Job` resources and monitor their execution:

  - [`DataflowFlexTemplateJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#preview.dataflow.DataflowFlexTemplateJobOp)
  - [`DataflowPythonJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowPythonJobOp)

Additionally, the Google Cloud SDK includes the [`WaitGcpResourcesOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/wait_gcp_resources.html#v1.wait_gcp_resources.WaitGcpResourcesOp) component, which you can use to mitigate costs while running Dataflow jobs.

## `DataflowFlexTemplateJobOp`

The [`DataflowFlexTemplateJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowFlexTemplateJobOp) operator lets you create a Gemini Enterprise Agent Platform Pipelines component to launch a [Dataflow Flex Template](https://docs.cloud.google.com/dataflow/docs/guides/templates/using-flex-templates) .

In Dataflow, a [`LaunchFlexTemplateParameter`](https://docs.cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.locations.flexTemplates/launch#LaunchFlexTemplateParameter) resource represents a Flex Template to launch. This component creates a `LaunchFlexTemplateParameter` resource and then requests Dataflow to create a job by launching the template. If the template is launched successfully, Dataflow returns a [`Job`](https://docs.cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.jobs#Job) resource.

The Dataflow Flex Template component terminates upon receiving a `Job` resource from Dataflow. The component outputs a `job_id` as a [serialized `gcp_resources` proto](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/google_cloud_pipeline_components/proto/README.md#usage) . You can pass this parameter to a [`WaitGcpResourcesOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/wait_gcp_resources.html#v1.wait_gcp_resources.WaitGcpResourcesOp) component, to wait for the Dataflow job to complete.

## `DataflowPythonJobOp`

The [`DataflowPythonJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowPythonJobOp) operator lets you create a Gemini Enterprise Agent Platform Pipelines component that prepares data by submitting a Python-based Apache Beam job to Dataflow for execution.

The Python code of the Apache Beam job runs with Dataflow Runner. When you run your pipeline with the Dataflow service, the runner uploads your executable code to the location specified by the `python_module_path` parameter and dependencies to a Cloud Storage bucket (specified by `temp_location` ), and then creates a Dataflow job that executes your Apache Beam pipeline on managed resources in Google Cloud.

To learn more about the Dataflow Runner, see [Using the Dataflow Runner](https://beam.apache.org/documentation/runners/dataflow/) .

The Dataflow Python component accepts a list of arguments that are passed using the Beam Runner to your Apache Beam code. These arguments are specified by `args` . For example, you can use these arguments to set the [`apache_beam.options.pipeline_options`](https://beam.apache.org/releases/pydoc/2.33.0/apache_beam.options.pipeline_options.html#apache_beam.options.pipeline_options.PipelineOptions) to specify a network, a subnetwork, customer-managed encryption key (CMEK), and other options when you run Dataflow jobs.

## `WaitGcpResourcesOp`

Dataflow jobs can often take long time to complete. The costs of a `busy-wait` container (the container that launches Dataflow job and wait for the result) can become expensive.

After submitting the Dataflow job using the Beam runner, the [`DataflowPythonJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowPythonJobOp) component terminates immediately and returns a `job_id` output parameter as a [serialized `gcp_resources` proto](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/google_cloud_pipeline_components/proto/README.md#usage) . You can pass this parameter to a `WaitGcpResourcesOp` component, to wait for the Dataflow job to complete.

``` 
    dataflow_python_op = DataflowPythonJobOp(
        project=project_id,
        location=location,
        python_module_path=python_file_path,
        temp_location = staging_dir,
        requirements_file_path = requirements_file_path,
        args = ['--output', OUTPUT_FILE],
    )
  
    dataflow_wait_op =  WaitGcpResourcesOp(
        gcp_resources = dataflow_python_op.outputs["gcp_resources"]
    )
```

Gemini Enterprise Agent Platform Pipelines optimizes the `WaitGcpResourcesOp` to execute it in a serverless fashion, and has zero cost.

If `DataflowPythonJobOp` and `DataflowFlexTemplateJobOp` don't meet your requirements, you can also create your own component that outputs the `gcp_resources` parameter and pass it to the `WaitGcpResourcesOp` component.

For more information about how to create `gcp_resources` output parameter, see [Write a component to show a Google Cloud console link](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-own-components#show-console-link) .

## API reference

  - For component reference, see the [Google Cloud SDK reference for Dataflow components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html) .

  - For Dataflow resource reference, see the following API reference pages:
    
      - [`LaunchFlexTemplateParameter`](https://docs.cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.locations.flexTemplates/launch#LaunchFlexTemplateParameter) resource
    
      - [`Job`](https://docs.cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.jobs#Job) resource

### Tutorials

  - [Get started with the Dataflow Flex Template component](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/fe7d3e4b8edc137d90ec061789b879b7cc8d3854/notebooks/community/ml_ops/stage3/get_started_with_dataflow_flex_template_component.ipynb)
  - [Get started with the Dataflow Python Job component](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/139d805c9fac45f3a663d4f4651fbca4bb0932b7/notebooks/community/ml_ops/stage3/get_started_with_dataflow_pipeline_components.ipynb)
  - [Specify a network and subnetwork](https://docs.cloud.google.com/dataflow/docs/guides/specifying-networks#network_parameter)
  - [Using customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/dataflow/docs/guides/customer-managed-encryption-keys)

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

## Technical support contacts

If you have any questions, reach out to [kubeflow-pipelines-components@google.com](mailto:%20kubeflow-pipelines-components@google.com) .
