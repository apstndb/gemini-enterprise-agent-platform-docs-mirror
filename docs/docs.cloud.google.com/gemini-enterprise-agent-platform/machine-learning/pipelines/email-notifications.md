---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/email-notifications
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/email-notifications
title: Configure email notifications
description: Learn how to set up and customize email notifications to monitor your ML workflows in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform Pipelines can notify you of the success or failure of a pipeline run. When the pipeline exits, Google Cloud sends a final status notification email to the email addresses that you specify.

This guide shows how to configure email notifications from a pipeline by using the [Email notification component](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/email-notification-component) in the Google Cloud SDK.

> **Note:** Google retains the email addresses that you send notifications to for up to 14 days for debugging purposes and 30 days for analytics purposes.

## Before you begin

Before you build a pipeline that sends notifications, use the following instructions to set up your Google Cloud project and development environment.

1.  To get your Google Cloud project ready to run ML pipelines, follow the instructions in the guide to [configuring your Google Cloud project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project) .

2.  Install v2 or later of the Kubeflow Pipelines SDK.
    
        pip install --upgrade "kfp>=2,<3"

> **Note:** To upgrade to the latest version of the Kubeflow Pipelines SDK, run the following command:  
> `pip install kfp --upgrade`  
> If an updated version is available, running this command uninstalls KFP and installs the latest version.\\

1.  To use Gemini Enterprise Agent Platform Python client in your pipelines, [install the Gemini Enterprise Agent Platform client libraries v1.7 or later](https://github.com/googleapis/python-aiplatform) .

2.  To use Gemini Enterprise Agent Platform services in your pipelines, [install the Google Cloud Pipeline Components](https://github.com/kubeflow/pipelines/tree/master/components/google-cloud#installation) .

## Send a notification from a pipeline

The following example shows how to configure email notifications by defining an email notification task ( `notify_email_task` ) and adding it to the pipeline's exit handler ( `dsl.ExitHandler` ). This notification task invokes the `VertexNotificationEmailOp` operator in the email notification component when the pipeline exits.

    from kfp import dsl
    from kfp import compiler
    from google_cloud_pipeline_components.v1.vertex_notification_email import VertexNotificationEmailOp
    
    @dsl.pipeline(
        name='PIPELINE_NAME',
        pipeline_root=PIPELINE_ROOT_PATH,
    )
    def TASK_NAME():
        notify_email_task = VertexNotificationEmailOp(recipients=RECIPIENTS_LIST)
    
        with dsl.ExitHandler(notify_email_task):
            # Add your pipeline tasks here.
    
    compiler.Compiler().compile(pipeline_func=notification_email_pipeline,
            package_path='notification_email_pipeline.yaml')

Replace the following:

  - PIPELINE\_NAME : The name of the pipeline.

  - PIPELINE\_ROOT\_PATH : Specify a Cloud Storage URI that your [pipelines service account can access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) . The artifacts of your pipeline runs are stored within the pipeline root.
    
    The pipeline root can be set as an argument of the `@kfp.dsl.pipeline` annotation on the pipeline function, or it can be set when you call `create_run_from_job_spec` to create a pipeline run.

  - TASK\_NAME : The name of the pipeline task for which you're configuring email notifications.

  - RECIPIENTS\_LIST : A comma-separated list of up to three email addresses to send the notification email to.

Add your pipeline tasks in the body of the `dsl.ExitHandler` exit handler function. By wrapping the tasks in the exit handler function in this way, you specify that the notification email component should report the status of these tasks when the pipeline exits. For example, if a task within the exit handler's contents fails, then the notification reports the status as failed.

## Example of a notification email

If you configure email notifications for a pipeline using the code sample in [Send a notification from a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/email-notifications#sending-notification-from-pipeline) , Gemini Enterprise Agent Platform sends an email notification similar to the following when the pipeline exits:

> Subject: Vertex Pipelines job " PIPELINE\_NAME " task " TASK\_NAME "  
> From: Google Notifications \<notify-noreply@google.com\>  
>   
> Hello Agent Platform Customer,  
>   
> Gemini Enterprise Agent Platform Pipelines job " PIPELINE\_NAME " task " TASK\_NAME " ended with the following state: {status}.  
>   
> Additional details:  
> \- Project: {project}  
> \- Pipeline name: PIPELINE\_NAME  
> \- Pipeline job ID: {pipeline\_job\_id}  
> \- Start time: {start\_time}  
>   
> To view this pipeline job in Cloud Console, use the following link: {console\_link}  
>   
> Sincerely,  
> The Google Cloud AI Team  

In this example:

  - `{status}` represents the final state of the task, which can be `SUCCEEDED` , `FAILED` , or `CANCELLED` .
  - `{project}` is the project name.
  - `{pipeline_job_id}` is the unique pipeline job ID.
  - `{start_time}` represents the start time for the pipeline.
  - `{console_link}` is a hyperlink to the pipeline job in the Google Cloud console.
