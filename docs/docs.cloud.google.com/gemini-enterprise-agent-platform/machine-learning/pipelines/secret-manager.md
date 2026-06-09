---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/secret-manager
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/secret-manager
title: Configure secrets with Secret Manager
description: Securely manage sensitive information in Gemini Enterprise Agent Platform Pipelines using Secret Manager.
data_source: docs.cloud.google.com
---

You can use Secret Manager's Python client with Agent Platform Pipelines to access secrets stored on Secret Manager.

## Create a secret using Google Cloud console

1.  [Enable the Secret Manager API](http://console.cloud.google.com/apis/library/secretmanager.googleapis.com) in Google Cloud console.

2.  Go to the **Secret Manager** page in the Cloud console.

3.  On the Secret Manager page, click **Create Secret** .

4.  On the **Create secret** page, under Name, enter a name for the secret (for example \`universe-secret).

5.  To add a secret version when creating the initial secret, in the **Secret value** field, enter a value for the secret (for example `42` ).

6.  Choose your region.

7.  Click the **Create secret** button.

## Build and run a pipeline with Python function based components

The following is a sample component that prints out the previously created secret.

1.  Grant the service account that runs the pipeline with the Secret Manager permission. See the "Configure a service account with granular permissions" section of [Configure your Google Cloud project for Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) for more information.

2.  Using Kubeflow Pipelines SDK, build a simple pipeline with one task.
    
    ``` 
     from kfp import compiler
     from kfp import dsl
    
     # A simple component that prints a secret stored in Secret Manager
     # Be sure to specify "google-cloud-secret-manager" as one of packages_to_install
     @dsl.component(
         packages_to_install=['google-cloud-secret-manager']
     )
     def print_secret_op(project_id: str, secret_id: str, version_id: str) -> str:
         from google.cloud import secretmanager
    
         secret_client = secretmanager.SecretManagerServiceClient()
         secret_name = f'projects/{project_id}/secrets/{secret_id}/versions/{version_id}'
         response = secret_client.access_secret_version(request={"name": secret_name})
         payload = response.payload.data.decode("UTF-8")
         answer = "The secret is: {}".format(payload)
         print(answer)
         return answer
    
     # A simple pipeline that contains a single print_secret task
     @dsl.pipeline(
         name='secret-manager-demo-pipeline')
     def secret_manager_demo_pipeline(project_id: str, secret_id: str, version_id: str):
         print_secret_task = print_secret_op(project_id, secret_id, version_id)
    
     # Compile the pipeline
     compiler.Compiler().compile(pipeline_func=secret_manager_demo_pipeline,
                                 package_path='secret_manager_demo_pipeline.yaml')
    ```

3.  Run the pipeline using the Vertex AI SDK.
    
    ``` 
     from google.cloud import aiplatform
    
     parameter_values = {
         "project_id": PROJECT_ID,
         "secret_id": SECRET_ID,
         "version_id": VERSION_ID
     }
    
     aiplatform.init(
         project=PROJECT_ID,
         location=REGION,
     )
    
     job = aiplatform.PipelineJob(
         display_name=f'test-secret-manager-pipeline',
         template_path='secret_manager_demo_pipeline.yaml',
         pipeline_root=PIPELINE_ROOT,
         enable_caching=False,
         parameter_values=parameter_values
     )
    
     job.submit(
         service_account=SERVICE_ACCOUNT
     )
    ```
    
    Replace the following:
    
      - PROJECT\_ID : The Google Cloud project that this pipeline runs in.
      - SECRET\_ID : The secret ID created in previous steps (for example `universe-secret` ).
      - VERSION\_ID : The version name of the secret.
      - REGION : The region that this pipeline runs in.
      - PIPELINE\_ROOT : Specify a Cloud Storage URI that your pipelines service account can access. The artifacts of your pipeline runs are stored within the pipeline root.
      - SERVICE\_ACCOUNT : The email address of the service account you created with Secret Manager Accessor permission.

In the output of the `job.submit()` function, you should be able to click the link that brings you to view the pipeline execution in the Google Cloud console.
