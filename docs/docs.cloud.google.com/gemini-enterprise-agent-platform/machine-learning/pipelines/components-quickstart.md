---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-quickstart
title: 'Quickstart: Google Cloud Pipeline Components'
description: Install and use the {{dynamic_data.site_values.cloud_name}} Pipeline Components SDK to define and run ML pipelines in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

This quickstart guides you through the installation of the Google Cloud Pipeline Components (GCPC) SDK.

## Install latest release

Use the following command to install the Google Cloud SDK from the Python Package Index (PyPI):

    pip install --upgrade google-cloud-pipeline-components

## Import a prebuilt component by using the Google Cloud SDK

After you install the Google Cloud SDK, you can use it to import a prebuilt component.

For SDK reference information for supported components, see the [Google Cloud SDK documentation](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/index.html) .

For example, you can use the following code to import and use the [Dataflow component](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html) in a pipeline.

    from google_cloud_pipeline_components.v1.dataflow import DataflowPythonJobOp
    from kfp import dsl
    
    @dsl.pipeline(
        name=PIPELINE_NAME,
        description='Dataflow launch python pipeline'
    )
    def pipeline(
        python_file_path:str = 'gs://ml-pipeline-playground/samples/dataflow/wc/wc.py',
        project_id:str = PROJECT_ID,
        location:str = LOCATION,
        staging_dir:str = PIPELINE_ROOT,
        requirements_file_path:str = 'gs://ml-pipeline-playground/samples/dataflow/wc/requirements.txt',
    ):
        dataflow_python_op = DataflowPythonJobOp(
            project=project_id,
            location=location,
            python_module_path=python_file_path,
            temp_location = staging_dir,
            requirements_file_path = requirements_file_path,
            args = ['--output', OUTPUT_FILE],
        )

## What's next

  - Read the [Introduction to Google Cloud Pipeline Components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/components-introduction) .
  - See all [tutorials that use the `google_cloud_pipeline_components` SDK](https://docs.cloud.google.com/vertex-ai/docs/pipelines/notebooks) .
  - Get started with [Dataflow components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/dataflow-component) .
