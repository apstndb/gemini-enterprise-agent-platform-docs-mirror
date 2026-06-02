---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-failure-policy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-failure-policy
title: Configure failure policy
description: Learn how to configure the failure policies for an ML pipeline in case one or more pipeline tasks fail.
data_source: docs.cloud.google.com
---

You can use the `failure_policy` parameter of the [`aiplatform.PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) class to configure whether a pipeline should fail immediately if one of the task fails.

The following failure policy configurations are supported in Gemini Enterprise Agent Platform Pipelines:

  - **Fail fast** ( `failure_policy = 'fast'` ): Choose this configuration if you want the pipeline to stop scheduling new tasks after a task fails. Tasks that are already scheduled continue running until they are completed.

  - **Fail slow** ( `failure_policy = 'slow'` ): Choose this configuration if you want the pipeline to continue to run even after a task fails. The pipeline continues to run until all tasks have been executed.
    
    > **Note:** If you don't specify the `failure_policy` parameter for a pipeline, the failure policy configuration is set to `slow` , by default.

Use the following code sample to configure the failure policy for a pipeline using the Agent Platform SDK for Python:

    job = aiplatform.PipelineJob(display_name = 'DISPLAY_NAME',
                                 template_path = 'COMPILED_PIPELINE_PATH',
                                 pipeline_root = 'PIPELINE_ROOT',
                                 project = 'PROJECT_ID',
                                 location = 'LOCATION',
                                 failure_policy = 'FAILURE_POLICY')

Replace the following:

  - DISPLAY\_NAME : The name of the pipeline, this will show up in the Google Cloud console.

  - COMPILED\_PIPELINE\_PATH : The path to your compiled pipeline YAML file. It can be a local path or a Google Cloud Storage URI.

  - PIPELINE\_ROOT : Specify a Cloud Storage URI that your pipelines service account can access. The artifacts of your pipeline runs are stored within the pipeline root.

  - PROJECT\_ID : The Google Cloud project that this pipeline runs in.

  - LOCATION : The region that the pipeline runs in. For more information about the regions that Agent Platform Pipelines is available in, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) . If you don't set this parameter, the default location set in `aiplatform.init` is used.

  - FAILURE\_POLICY : Specify the failure policy for the entire pipeline. The following configurations are available:
    
      - To configure the pipeline to fail after one task fails, enter `fast` .
    
      - To configure the pipeline to continue scheduling tasks after one task fails, enter `slow` .
    
    If you don't set this parameter, the failure policy configuration is set to `slow` , by default.

## What's next

  - Learn how to [configure retries for failed pipeline tasks](https://docs.cloud.google.com/vertex-ai/docs/pipelines/configure-retries) .
