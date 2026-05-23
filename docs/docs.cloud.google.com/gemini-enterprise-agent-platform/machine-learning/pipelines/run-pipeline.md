---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline
title: Run a pipeline
description: Learn how to run ML pipelines using Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

Agent Platform Pipelines lets you run machine learning (ML) pipelines that were built using the Kubeflow Pipelines SDK or TensorFlow Extended in a serverless manner. This document describes how to run an ML pipeline.

You can also create pipeline runs using prebuilt templates in the **Template Gallery** . For more information about the **Template Gallery** , see [Use a prebuilt template from the Template Gallery](https://docs.cloud.google.com/vertex-ai/docs/pipelines/use-template-gallery) .

You can use Gemini Enterprise Agent Platform Experiments to track, analyze, and compare your pipeline runs by [associating the pipeline runs with an experiment or an experiment run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/add-pipelinerun-experiment) . By comparing the parameters, outputs, and performance metrics of the pipeline runs, you can identify the pipeline configuration that works best for your use case. For more information, see [Introduction to Gemini Enterprise Agent Platform Experiments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments) .

## Before you begin

Before you run a pipeline with Agent Platform Pipelines, use the following instructions to set up your Google Cloud project and development environment:

1.  [Build a pipeline.](https://docs.cloud.google.com/vertex-ai/docs/pipelines/build-pipeline)

2.  To run a pipeline using the Agent Platform SDK for Python, install the Vertex SDK.
    
      - Install the [Agent Platform SDK](https://github.com/googleapis/python-aiplatform) .

## Create a pipeline run

Use the following instructions to run an ML pipeline using Google Cloud console or Python.

### Console

Use the following instructions to run an ML pipeline using Google Cloud console.

1.  In the Google Cloud console, in the **Agent Platform** section, go to the **Pipelines** page.

2.  In the **Region** drop-down list, select the region to create the pipeline run.

3.  Click **add\_box Create run** to open the **Create pipeline run** pane.

4.  In the **Run details** section, do the following:
    
    1.  Click a **Run source** . The following options are available:
        
          - **Select from existing pipelines** : To create a pipeline run based on an existing pipeline template, click **Select from existing pipelines** and enter the following details:
            
            1.  Select the **Repository** containing the pipeline or component definition file.
            
            2.  Select the **Pipeline or component** and **Version** .
            
            3.  Specify a **Run name** to uniquely identify the pipeline run.
        
          - **Select a Template Gallery pipeline** : To create a pipeline run based on a Google-authored pipeline template from the **Template Gallery** , click **Select a Template Gallery pipeline** and enter the following details:
            
            1.  In the **Template Gallery pipeline** list, select the pipeline template.
            
            2.  Optional: Modify the default **Run name** that uniquely identifies the pipeline run.
            
            > **Note:** These instructions describe how to create a pipeline run using the default interface of the **Create pipeline run** page, which includes the **Run details** and the **Runtime configuration** sections. For some templates from the **Template gallery** , this page has additional sections. For example, the **AutoML for Tabular Classification / Regression** template also includes the **Training Method** , **Training options** , and **Compute and pricing** sections.
        
          - **Upload file** : To upload a compiled pipeline definition, click **Upload file** and enter the following details:
            
            1.  Click **Browse** to open the file selector. Navigate to the compiled pipeline YAML file that you want to run, select the pipeline, and click **Open** .
            
            2.  The **Pipeline or component name** shows the name specified in the pipeline definition, by default. Optionally, specify a different Pipeline name.
            
            3.  Specify a **Run name** to uniquely identify the pipeline run.
        
          - **Import from Cloud Storage** : To import a pipeline definition file from Cloud Storage, click **Import from Cloud Storage** and enter the following details:
            
            1.  Click **Browse** to navigate to the Cloud Storage bucket containing the pipeline definition object, select the file, and then click **Select** .
                
                Alternatively, enter the Cloud Storage URI or the HTTP/HTTPS URL of the pipeline definition file.
            
            2.  Specify the **Pipeline or component name** .
            
            3.  Specify a **Run name** to uniquely identify the pipeline run.
    
    2.  Optional: To schedule recurring pipeline runs, specify the **Run schedule** , as follows:
        
        1.  Select **Recurring** .
        
        2.  Under **Start time** , specify when the schedule becomes active.
            
              - To schedule the first run to occur immediately after schedule creation, select **Immediately** .
            
              - To schedule the first run to occur at a specific time and date, select **On** .
        
        3.  In the **Frequency** field, specify the frequency to schedule and execute the pipeline runs, using a cron schedule expression based on [unix-cron](https://man7.org/linux/man-pages/man5/crontab.5.html) .
        
        4.  Under **Ends** , specify when the schedule ends.
            
              - To indicate that the schedule creates pipeline runs indefinitely, select **Never** .
            
              - To indicate that the schedule ends on a specific date and time, select **On** , and specify the end date and time for the schedule.
        
        5.  Optional: To specify that the pipeline run uses a custom service account, a customer-managed encryption key (CMEK), or a peered VPC network, click **Advanced options** , and then follow these instructions:
            
              - To specify a service account, select a service account from the **Service account** drop-down list.
                
                If you don't specify a service account, Gemini Enterprise Agent Platform Pipelines runs your pipeline using the default Compute Engine service account.
                
                Learn more about [configuring a service account for use with Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/vertex-ai/docs/pipelines/configure-project#service-account) .
            
              - To use a CMEK, select **Use a customer-managed encryption key** . The **Select a customer-managed key** drop-down list appears. In the **Select a customer-managed key** drop-down list, select the key that you want to use.
            
              - To use a peered VPC network in this pipeline run, enter the VPC network name in the **Peered VPC network** box.
    
    3.  Click **Continue** .

5.  In the **Runtime configuration** section, configure the pipeline run, as follows:
    
    1.  Under **Cloud storage location** , click **Browse** to select the Cloud Storage bucket for storing the pipeline output artifacts, and then click **Select** .
    
    2.  Optional: To configure the failure policy and the cache for the pipeline run, click **Advanced options** , and then use the following instructions:
        
          - Under **Failure policy** , specify the failure policy for the entire pipeline. [Learn more about pipeline failure policies.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-failure-policy)
            
              - To configure the pipeline to continue scheduling tasks after one task fails, select **Run all steps to completion** . This option is selected, by default.
            
              - To configure the pipeline to fail after one task fails, select **Fail this run as soon as one step fails** .
        
          - Under **Caching configuration** , specify the cache configuration for the entire pipeline.
            
              - To use the task-level cache configuration for task in the pipeline, select **Do not override task-level cache configuration** .
            
              - To turn on caching for all the tasks in the pipeline and override any task-level cache configuration, select **Enable read from cache for all steps (fastest)** .
            
              - To turn off caching for all the tasks in the pipeline and override any task-level cache configuration, select **Disable read from cache for all steps (fastest)** .
    
    3.  Optional: If your pipeline has parameters, under **Pipeline parameters** , specify your pipeline run parameters.

6.  To create your pipeline run, click **Submit** .

### Python

Use the following instructions to run an ML pipeline using the Agent Platform SDK for Python. Before you run the following code sample, you must set up authentication.

### Set up authentication

To set up authentication, you must create a service account key, and set an environment variable for the path to the service account key.

1.  Create a service account:
    
    1.  In the Google Cloud console, go to the **Create service account** page.
    
    2.  In the **Service account name** field, enter a name.
    
    3.  Optional: In the **Service account description** field, enter a description.
    
    4.  Click **Create** .
    
    5.  Click the **Select a role** field. Under **All roles** , select **Gemini Enterprise Agent Platform** \> **Agent Platform User** .
    
    6.  Click **Done** to create the service account.
        
        Do not close your browser window. You will use it in the next step.

2.  Create a service account key for authentication:
    
    1.  In the Google Cloud console, click the email address for the service account that you created.
    2.  Click **Keys** .
    3.  Click **Add key** , then **Create new key** .
    4.  Click **Create** . A JSON key file is downloaded to your computer.
    5.  Click **Close** .

3.  Grant your new service account access to the service account that you use to run pipelines.
    
    1.  Click arrow\_back to return to the list of service accounts.
    
    2.  Click the name of the service account that you use to run pipelines. The **Service account details** page appears.
        
        If you followed the instructions in the guide to configuring your project for Gemini Enterprise Agent Platform Pipelines, this is the same service account that you created in the [Configure a service account with granular permissions](https://docs.cloud.google.com/vertex-ai/docs/pipelines/configure-project#service-account) section. Otherwise, Gemini Enterprise Agent Platform uses the Compute Engine default service account to run pipelines. The Compute Engine default service account is named like the following: `  PROJECT_NUMBER -compute@developer.gserviceaccount.com `
    
    3.  Click the **Permissions** tab.
    
    4.  Click **Grant access** . The **Add principals** panel appears.
    
    5.  In the **New principals** box, enter the email address for the service account you created in a previous step.
    
    6.  In the **Role** drop-down list, select **Service accounts** \> **Service account user** .
    
    7.  Click **Save**

4.  Set the environment variable GOOGLE\_APPLICATION\_CREDENTIALS to the path of the JSON file that contains your service account key. This variable only applies to your current shell session, so if you open a new session, set the variable again.
    
    **Example:** Linux or macOS
    
    Replace \[PATH\] with the path of the JSON file that contains your service account key.
    
        export GOOGLE_APPLICATION_CREDENTIALS="[PATH]"
    
    For example:
    
        export GOOGLE_APPLICATION_CREDENTIALS="/home/user/Downloads/service-account-file.json"
    
    **Example:** Windows
    
    Replace \[PATH\] with the path of the JSON file that contains your service account key, and \[FILE\_NAME\] with the filename.
    
    With PowerShell:
    
        $env:GOOGLE_APPLICATION_CREDENTIALS="[PATH]"
    
    For example:
    
        $env:GOOGLE_APPLICATION_CREDENTIALS="C:\Users\username\Downloads\[FILE_NAME].json"
    
    With command prompt:
    
        set GOOGLE_APPLICATION_CREDENTIALS=[PATH]

### Run a pipeline

Running a Gemini Enterprise Agent Platform `PipelineJob` requires you to create a [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) resource and then invoke the `submit` method.

#### Special input types supported by KFP

While creating a pipeline run, you can also pass the following placeholders supported by the KFP SDK as inputs:

  - `{{$.pipeline_job_name_placeholder}}`

  - `{{$.pipeline_job_resource_name_placeholder}}`

  - `{{$.pipeline_job_id_placeholder}}`

  - `{{$.pipeline_task_name_placeholder}}`

  - `{{$.pipeline_task_id_placeholder}}`

  - `{{$.pipeline_job_create_time_utc_placeholder}}`

  - `{{$.pipeline_root_placeholder}}`

For more information, see [Special input types](https://www.kubeflow.org/docs/components/pipelines/v2/pipelines/pipeline-basics/#special-input-types) in the [Kubeflow Pipelines v2 documentation](https://www.kubeflow.org/docs/components/pipelines/v2/introduction/) .

    from google.cloud import aiplatform
    job = aiplatform.PipelineJob(display_name = DISPLAY_NAME,
                                 template_path = COMPILED_PIPELINE_PATH,
                                 job_id = JOB_ID,
                                 pipeline_root = PIPELINE_ROOT_PATH,
                                 parameter_values = PIPELINE_PARAMETERS,
                                 enable_caching = ENABLE_CACHING,
                                 encryption_spec_key_name = CMEK,
                                 labels = LABELS,
                                 credentials = CREDENTIALS,
                                 project = PROJECT_ID,
                                 location = LOCATION,
                                 failure_policy = FAILURE_POLICY)
    job.submit(service_account=SERVICE_ACCOUNT,
               network=NETWORK,
               reserved_ip_ranges=RESERVED_IP_RANGES)

Replace the following:

  - DISPLAY\_NAME : The name of the pipeline, this will show up in the Google Cloud console.

  - COMPILED\_PIPELINE\_PATH : The path to your compiled pipeline YAML file. It can be a Cloud Storage URI, a HTTP/HTTPS URL, or a local path.  
    
    Optional: To specify a particular version of a compiled pipeline, include the version tag in any one of the following formats:
    
      - `  COMPILED_PIPELINE_PATH : TAG  ` , where TAG is the version tag.
    
      - `  COMPILED_PIPELINE_PATH @ SHA256_TAG  ` , where SHA256\_TAG is the `sha256` hash value of the pipeline version.

  - JOB\_ID : ( *optional* ) A unique identifier for this pipeline run. If the job ID is not specified, Agent Platform Pipelines creates a job ID for you using the pipeline name and the timestamp of when the pipeline run was started.

  - PIPELINE\_ROOT\_PATH : ( *optional* ) To override the pipeline root path specified in the pipeline definition, specify a path that your pipeline job can access, such as a Cloud Storage bucket URI.

  - PIPELINE\_PARAMETERS : ( *optional* ) The pipeline parameters to pass to this run. For example, create a `dict()` with the parameter names as the dictionary keys and the parameter values as the dictionary values.

  - ENABLE\_CACHING : ( *optional* ) Specifies if this pipeline run uses execution caching. Execution caching reduces costs by skipping pipeline tasks where the output is known for the current set of inputs. If the enable caching argument is not specified, execution caching is used in this pipeline run. [Learn more about execution caching](https://docs.cloud.google.com/vertex-ai/docs/pipelines/build-pipeline#caching) .

  - CMEK : ( *optional* ) The name of the customer-managed encryption key that you want to use for this pipeline run.

  - LABELS : ( *optional* ) The user defined labels to organize this `PipelineJob` . For more information about resource labels, see [Creating and managing labels](https://docs.cloud.google.com/resource-manager/docs/creating-managing-labels) in the [Resource Manager documentation](https://docs.cloud.google.com/resource-manager/docs) .
    
    Agent Platform Pipelines automatically attaches the following label to your pipeline run:
    
    `vertex-ai-pipelines-run-billing-id: pipeline_run_id`
    
    where `pipeline_run_id` is the unique ID of the pipeline run.
    
    This label connects the usage of Google Cloud resources generated by the pipeline run in billing reports.

  - CREDENTIALS : ( *optional* ) Custom credentials to use to create this `PipelineJob` . Overrides credentials set in `aiplatform.init` .

  - PROJECT\_ID : ( *optional* ) The Google Cloud project that you want to run the pipeline in. If you don't set this parameter, the project set in `aiplatform.init` is used.

  - LOCATION : ( *optional* ) The region that you want to run the pipeline in. For more information about the regions that Agent Platform Pipelines is available in, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) . If you don't set this parameter, the default location set in `aiplatform.init` is used.

  - FAILURE\_POLICY : ( *optional* ) Specify the failure policy for the entire pipeline. The following configurations are available:
    
      - To configure the pipeline to fail after one task fails, enter `fast` .
    
      - To configure the pipeline to continue scheduling tasks after one task fails, enter `slow` .
    
    If you don't set this parameter, the failure policy configuration is set to `slow` , by default. [Learn more about pipeline failure policies.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-failure-policy)

  - SERVICE\_ACCOUNT : ( *optional* ) The name of the service account to use for this pipeline run. If you don't specify a service account, Agent Platform Pipelines runs your pipeline using the default Compute Engine service account.

  - NETWORK : ( *optional* ) :The name of the VPC peered network to use for this pipeline run.

  - RESERVED\_IP\_RANGES : Optional. A list of names for the reserved IP ranges in the VPC network used for the workload of the pipeline run, for example: `['vertex-ai-ip-range']` .

## What's next

  - Learn how to [create and pipeline run and add it to an experiment or an experiment run](https://docs.cloud.google.com/vertex-ai/docs/experiments/add-pipelinerun-experiment) .
