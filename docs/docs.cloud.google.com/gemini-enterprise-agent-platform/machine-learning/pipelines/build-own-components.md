---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-own-components
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-own-components
title: Build your own pipeline components
description: Extend Gemini Enterprise Agent Platform Pipelines by building your own custom components to integrate specialized tasks.
data_source: docs.cloud.google.com
---

> To learn more, run the "Custom training workflow with prebuilt Pipeline Components and custom components" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_model_train_upload_deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_model_train_upload_deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_model_train_upload_deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_model_train_upload_deploy.ipynb)

## Write a component to show a Google Cloud console link

It's common that when running a component, you want to not only see the link to the component job being launched, but also the link to the underlying cloud resources, such as the Vertex batch prediction jobs or dataflow jobs.

The [`gcp_resource` proto](https://github.com/kubeflow/pipelines/tree/master/components/google-cloud/google_cloud_pipeline_components/proto) is a special parameter that you can use in your component to enable the Google Cloud console to provide a customized view of the resource's logs and status in the Gemini Enterprise Agent Platform Pipelines console.

### Output the `gcp_resource` parameter

#### Using a container-based component

First, you'll need to define the `gcp_resource` parameter in your component as shown in the following example `component.py` file:

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    # Copyright 2023 The Kubeflow Authors. All Rights Reserved.
    #
    # Licensed under the Apache License, Version 2.0 (the "License");
    # you may not use this file except in compliance with the License.
    # You may obtain a copy of the License at
    #
    #     http://www.apache.org/licenses/LICENSE-2.0
    #
    # Unless required by applicable law or agreed to in writing, software
    # distributed under the License is distributed on an "AS IS" BASIS,
    # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    # See the License for the specific language governing permissions and
    # limitations under the License.
    from typing import List
    
    from google_cloud_pipeline_components import _image
    from google_cloud_pipeline_components import _placeholders
    from kfp.dsl import container_component
    from kfp.dsl import ContainerSpec
    from kfp.dsl import OutputPath
    
    
    @container_component
    def dataflow_python(
        python_module_path: str,
        temp_location: str,
        gcp_resources: OutputPath(str),
        location: str = 'us-central1',
        requirements_file_path: str = '',
        args: List[str] = [],
        project: str = _placeholders.PROJECT_ID_PLACEHOLDER,
    ):
      # fmt: off
      """Launch a self-executing Beam Python file on Google Cloud using the
      Dataflow Runner.
    
      Args:
          location: Location of the Dataflow job. If not set, defaults to `'us-central1'`.
          python_module_path: The GCS path to the Python file to run.
          temp_location: A GCS path for Dataflow to stage temporary job files created during the execution of the pipeline.
          requirements_file_path: The GCS path to the pip requirements file.
          args: The list of args to pass to the Python file. Can include additional parameters for the Dataflow Runner.
          project: Project to create the Dataflow job. Defaults to the project in which the PipelineJob is run.
    
      Returns:
          gcp_resources: Serialized gcp_resources proto tracking the Dataflow job. For more details, see https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/google_cloud_pipeline_components/proto/README.md.
      """
      # fmt: on
      return ContainerSpec(
          image=_image.GCPC_IMAGE_TAG,
          command=[
              'python3',
              '-u',
              '-m',
              'google_cloud_pipeline_components.container.v1.dataflow.dataflow_launcher',
          ],
          args=[
              '--project',
              project,
              '--location',
              location,
              '--python_module_path',
              python_module_path,
              '--temp_location',
              temp_location,
              '--requirements_file_path',
              requirements_file_path,
              '--args',
              args,
              '--gcp_resources',
              gcp_resources,
          ],
      )

Next, inside the container, install the Google Cloud Pipeline Components package:

    pip install --upgrade google-cloud-pipeline-components

Next, in the Python code, define the resource as a `gcp_resource` parameter:

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google_cloud_pipeline_components.proto.gcp_resources_pb2 import GcpResources
    from google.protobuf.json_format import MessageToJson
    
    dataflow_resources = GcpResources()
    dr = dataflow_resources.resources.add()
    dr.resource_type='DataflowJob'
    dr.resource_uri='https://dataflow.googleapis.com/v1b3/projects/[your-project]/locations/us-east1/jobs/[dataflow-job-id]'
    
    with open(gcp_resources, 'w') as f:
        f.write(MessageToJson(dataflow_resources))

#### Using a Python component

Alternatively, you can return the `gcp_resources` output parameter as you would any string output parameter:

    @dsl.component(
        base_image='python:3.9',
        packages_to_install=['google-cloud-pipeline-components==2.22.0'],
    )
    def launch_dataflow_component(project: str, location:str) -> NamedTuple("Outputs",  [("gcp_resources", str)]):
      # Launch the dataflow job
      dataflow_job_id = [dataflow-id]
      dataflow_resources = GcpResources()
      dr = dataflow_resources.resources.add()
      dr.resource_type='DataflowJob'
      dr.resource_uri=f'https://dataflow.googleapis.com/v1b3/projects/{project}/locations/{location}/jobs/{dataflow_job_id}'
      gcp_resources=MessageToJson(dataflow_resources)
      return gcp_resources

#### Supported `resource_type` values

You can set the `resource_type` to be an arbitrary string, but only the following types have links in the Google Cloud console:

  - BatchPredictionJob
  - BigQueryJob
  - CustomJob
  - DataflowJob
  - HyperparameterTuningJob

## Write a component to cancel the underlying resources

When a pipeline job is canceled, the default behavior is for the underlying Google Cloud resources to keep running. They are not canceled automatically. To change this behavior, you should attach a [SIGTERM](https://docs.python.org/3/library/signal.html#signal.SIGTERM) handler to the pipeline job. A good place to do this is just before a polling loop for a job that could run for a long time.

Cancellation has been implemented on several Google Cloud Pipeline Components, including:

  - Batch prediction job
  - BigQuery ML job
  - Custom job
  - Managed Service for Apache Spark batch job
  - Hyperparameter tuning job

For more information, including sample code that shows how to attach a SIGTERM handler, see the following GitHub links:

  - <https://github.com/kubeflow/pipelines/blob/google-cloud-pipeline-components-2.22.0/components/google-cloud/google_cloud_pipeline_components/container/utils/execution_context.py>
  - <https://github.com/kubeflow/pipelines/blob/google-cloud-pipeline-components-2.22.0/components/google-cloud/google_cloud_pipeline_components/container/v1/gcp_launcher/job_remote_runner.py#L124>

Consider the following when implementing your SIGTERM handler:

  - Cancellation propagation works only after the component has been running for a few minutes. This is typically due to background startup tasks that need to be [processed](https://docs.python.org/3/library/signal.html#execution-of-python-signal-handlers) before the Python signal handlers are called.
  - Some Google Cloud resources might not have cancellation implemented. For example, creating or deleting a Gemini Enterprise Agent Platform Endpoint or Model could create a long-running operation that accepts a cancellation request through its REST API, but doesn't implement the cancellation operation itself.
