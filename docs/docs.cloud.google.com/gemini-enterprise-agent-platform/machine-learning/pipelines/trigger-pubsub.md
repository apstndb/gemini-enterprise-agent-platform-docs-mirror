---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/trigger-pubsub
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/trigger-pubsub
title: Trigger a pipeline run with Pub/Sub
description: Learn how to automatically trigger pipeline runs in response to Pub/Sub events.
data_source: docs.cloud.google.com
---

This page shows you how to write, deploy, and trigger a pipeline run using an [Event-Driven Cloud Function](https://docs.cloud.google.com/functions/docs/writing#event-driven_functions) with a [Cloud Pub/Sub trigger](https://docs.cloud.google.com/functions/docs/calling/pubsub) . Follow these steps:

1.  Define an ML pipeline using the Kubeflow Pipelines (KFP) SDK and compile it into a YAML file.

2.  Upload the compiled pipeline definition to a Cloud Storage bucket.

3.  Use Cloud Run functions to create, configure, and deploy a function that's triggered by a new or existing Pub/Sub topic.

### Define and compile a pipeline

Using Kubeflow Pipelines SDK, build a scheduled pipeline and compile it into a YAML file.

Sample `hello-world-scheduled-pipeline` :

    from kfp import compiler
    from kfp import dsl
    
    # A simple component that prints and returns a greeting string
    @dsl.component
    def hello_world(message: str) -> str:
        greeting_str = f'Hello, {message}'
        print(greeting_str)
        return greeting_str
    
    # A simple pipeline that contains a single hello_world task
    @dsl.pipeline(
        name='hello-world-scheduled-pipeline')
    def hello_world_scheduled_pipeline(greet_name: str):
        hello_world_task = hello_world(greet_name)
    
    # Compile the pipeline and generate a YAML file
    compiler.Compiler().compile(pipeline_func=hello_world_scheduled_pipeline,
                                package_path='hello_world_scheduled_pipeline.yaml')

### Upload compiled pipeline YAML to Cloud Storage bucket

1.  Open the Cloud Storage browser in the Google Cloud console.  

2.  Click the Cloud Storage bucket you created when you [configured your project](https://docs.cloud.google.com/vertex-ai/docs/pipelines/configure-project) .

3.  Using either an existing folder or a new folder, upload your compiled pipeline YAML (in this example `hello_world_scheduled_pipeline.yaml` ) to the selected folder.

4.  Click the uploaded YAML file to access the details. Copy the **gsutil URI** for later use.

### Create a Cloud Run functions with a Pub/Sub trigger

1.  Visit the Cloud Run functions page in the console.

2.  Click the **Create function** button.

3.  In the **Basics** section, give your function a name (for example `my-scheduled-pipeline-function` ).

4.  In the **Trigger** section, select **Cloud Pub/Sub** as the Trigger type.
    
    ![create function configuration choose pubsub as Trigger type image](https://docs.cloud.google.com/static/vertex-ai/docs/pipelines/images/trigger-type-cloud-pubsub.png)

5.  In the **Select a Cloud Pub/Sub topic** list, click **Create a topic** .

6.  In the **Create a topic** box, give your new topic a name (for example `my-scheduled-pipeline-topic` ), and select **Create topic** .

7.  Leave all other fields as default and click **Save** to save the Trigger section configuration.

8.  Leave all other fields as default and click **Next** to proceed to the Code section.

9.  Under **Runtime** , select **Python 3.7** .

10. In **Entry** point, input "subscribe" (the example code entry point function name).

11. Under **Source code** , select **Inline Editor** if it's not already selected.

12. In the `main.py` file, add in the following code:
    
    ``` 
      import base64
      import json
      from google.cloud import aiplatform
    
      PROJECT_ID = 'your-project-id'                     # <---CHANGE THIS
      REGION = 'your-region'                             # <---CHANGE THIS
      PIPELINE_ROOT = 'your-cloud-storage-pipeline-root' # <---CHANGE THIS
    
      def subscribe(event, context):
        """Triggered from a message on a Cloud Pub/Sub topic.
        Args:
              event (dict): Event payload.
              context (google.cloud.functions.Context): Metadata for the event.
        """
        # decode the event payload string
        payload_message = base64.b64decode(event['data']).decode('utf-8')
        # parse payload string into JSON object
        payload_json = json.loads(payload_message)
        # trigger pipeline run with payload
        trigger_pipeline_run(payload_json)
    
      def trigger_pipeline_run(payload_json):
        """Triggers a pipeline run
        Args:
              payload_json: expected in the following format:
                {
                  "pipeline_spec_uri": "<path-to-your-compiled-pipeline>",
                  "parameter_values": {
                    "greet_name": "<any-greet-string>"
                  }
                }
        """
        pipeline_spec_uri = payload_json['pipeline_spec_uri']
        parameter_values = payload_json['parameter_values']
    
        # Create a PipelineJob using the compiled pipeline from pipeline_spec_uri
        aiplatform.init(
            project=PROJECT_ID,
            location=REGION,
        )
        job = aiplatform.PipelineJob(
            display_name='hello-world-pipeline-cloud-function-invocation',
            template_path=pipeline_spec_uri,
            pipeline_root=PIPELINE_ROOT,
            enable_caching=False,
            parameter_values=parameter_values
        )
    
        # Submit the PipelineJob
        job.submit()
    ```
    
    Replace the following:
    
      - PROJECT\_ID : The Google Cloud project that this pipeline runs in.
      - REGION : The region that this pipeline runs in.
      - PIPELINE\_ROOT : Specify a Cloud Storage URI that your pipelines service account can access. The artifacts of your pipeline runs are stored in the pipeline root.

13. In the `requirements.txt` file, replace the contents with the following package requirements:
    
        google-api-python-client>=1.7.8,<2
        google-cloud-aiplatform

14. Click **deploy** to deploy the Function.

## What's next

  - Learn more about [Google Cloud Pub/Sub](https://docs.cloud.google.com/pubsub/docs) .
  - [Visualize and analyze pipeline results](https://docs.cloud.google.com/vertex-ai/docs/pipelines/visualize-pipeline) .
  - Learn how to [create triggers in Cloud Runfrom Pub/Sub events](https://docs.cloud.google.com/functions/docs/calling/pubsub) .
  - To view code samples for using Pub/Sub, refer to the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?p=pubsub) .
