---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline
title: Build a pipeline
description: Learn how to define, build, and compile your machine learning pipelines in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

> To learn more, run the "Learn how to use control structures in a Kubeflow pipeline" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/control_flow_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcontrol_flow_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcontrol_flow_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/control_flow_kfp.ipynb)

Agent Platform Pipelines lets you orchestrate your machine learning (ML) workflows in a serverless manner. Before Agent Platform Pipelines can orchestrate your ML workflow, you must describe your workflow as a pipeline. ML pipelines are portable and scalable ML workflows that are based on containers and Google Cloud services.

This guide describes how to get started building ML pipelines.

## Which pipelines SDK should I use?

Agent Platform Pipelines can run pipelines built using any of the following SDKs:

  - Kubeflow Pipelines SDK v2.0 or later
    
    > **Note:** Install Kubeflow Pipelines SDK v2 to use the code samples provided in the Agent Platform Pipelines documentation.

  - TensorFlow Extended v0.30.0 or later

If you use TensorFlow in an ML workflow that processes terabytes of structured data or text data, we recommend that you build your pipeline using TFX.

  - To learn more about building a TFX pipeline, [follow the TFX getting started tutorials](https://www.tensorflow.org/tfx/tutorials#getting-started-tutorials) .
  - To learn more about using Agent Platform Pipelines to run a TFX pipeline, [follow the TFX on Google Cloud tutorials](https://www.tensorflow.org/tfx/tutorials#tfx-on-google-cloud) .

For other use cases, we recommend that you build your pipeline using the Kubeflow Pipelines SDK. By building a pipeline with the Kubeflow Pipelines SDK, you can implement your workflow by building custom components or reusing prebuilt components, such as the [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) . Google Cloud Pipeline Components make it easier to use Gemini Enterprise Agent Platform services like AutoML in your pipeline.

This guide describes how to build pipelines using the Kubeflow Pipelines SDK.

## Before you begin

Before you build and run your pipelines, use the following instructions to set up your Google Cloud project and development environment.

1.  To get your Google Cloud project ready to run ML pipelines, follow the instructions in the guide to [configuring your Google Cloud project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project) .

2.  Install v2 or later of the Kubeflow Pipelines SDK.
    
        pip install --upgrade "kfp>=2,<3"

> **Note:** To upgrade to the latest version of the Kubeflow Pipelines SDK, run the following command:  
> `pip install kfp --upgrade`  
> If an updated version is available, running this command uninstalls KFP and installs the latest version.

1.  To use Gemini Enterprise Agent Platform Python client in your pipelines, [install the Gemini Enterprise Agent Platform client libraries v1.7 or later](https://github.com/googleapis/python-aiplatform) .

2.  To use Gemini Enterprise Agent Platform services in your pipelines, [install the Google Cloud SDK](https://github.com/kubeflow/pipelines/tree/master/components/google-cloud#installation) .

## Getting started building a pipeline

To orchestrate your ML workflow on Agent Platform Pipelines, you must first describe your workflow as a pipeline. The following sample demonstrates how to use the [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) with Gemini Enterprise Agent Platform to create a dataset, train a model using AutoML, and deploy the trained model for predictions.

Before you run the following code sample, you must set up authentication.

**How to set up authentication**

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
        
        If you followed the instructions in the guide to configuring your project for Gemini Enterprise Agent Platform Pipelines, this is the same service account that you created in the [Configure a service account with granular permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) section. Otherwise, Gemini Enterprise Agent Platform uses the Compute Engine default service account to run pipelines. The Compute Engine default service account is named like the following: `  PROJECT_NUMBER -compute@developer.gserviceaccount.com `
    
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

### Define your workflow using Kubeflow Pipelines DSL package

The `kfp.dsl` package contains the domain-specific language (DSL) that you can use to define and interact with pipelines and components.

Kubeflow pipeline components are factory functions that create pipeline steps. Each component describes the inputs, outputs, and implementation of the component. For example, in the code sample below, `ds_op` is a component.

Components are used to create pipeline steps. When a pipeline runs, steps are executed as the data they depend on becomes available. For example, a training component could take a CSV file as an input and use it to train a model.

    import kfp
    from google.cloud import aiplatform
    from google_cloud_pipeline_components.v1.dataset import ImageDatasetCreateOp
    from google_cloud_pipeline_components.v1.automl.training_job import AutoMLImageTrainingJobRunOp
    from google_cloud_pipeline_components.v1.endpoint import EndpointCreateOp, ModelDeployOp
    
    project_id = PROJECT_ID
    pipeline_root_path = PIPELINE_ROOT
    
    # Define the workflow of the pipeline.
    @kfp.dsl.pipeline(
        name="automl-image-training-v2",
        pipeline_root=pipeline_root_path)
    def pipeline(project_id: str):
        # The first step of your workflow is a dataset generator.
        # This step takes a Google Cloud Pipeline Component, providing the necessary
        # input arguments, and uses the Python variable `ds_op` to define its
        # output. Note that here the `ds_op` only stores the definition of the
        # output but not the actual returned object from the execution. The value
        # of the object is not accessible at the dsl.pipeline level, and can only be
        # retrieved by providing it as the input to a downstream component.
        ds_op = ImageDatasetCreateOp(
            project=project_id,
            display_name="flowers",
            gcs_source="gs://cloud-samples-data/vision/automl_classification/flowers/all_data_v3.csv",
            import_schema_uri=aiplatform.schema.dataset.ioformat.image.single_label_classification,
        )
    
        # The second step is a model training component. It takes the dataset
        # outputted from the first step, supplies it as an input argument to the
        # component (see `dataset=ds_op.outputs["dataset"]`), and will put its
        # outputs into `training_job_run_op`.
        training_job_run_op = AutoMLImageTrainingJobRunOp(
            project=project_id,
            display_name="train-iris-automl-mbsdk-1",
            prediction_type="classification",
            model_type="CLOUD",
            dataset=ds_op.outputs["dataset"],
            model_display_name="iris-classification-model-mbsdk",
            training_fraction_split=0.6,
            validation_fraction_split=0.2,
            test_fraction_split=0.2,
            budget_milli_node_hours=8000,
        )
    
        # The third and fourth step are for deploying the model.
        create_endpoint_op = EndpointCreateOp(
            project=project_id,
            display_name = "create-endpoint",
        )
    
        model_deploy_op = ModelDeployOp(
            model=training_job_run_op.outputs["model"],
            endpoint=create_endpoint_op.outputs['endpoint'],
            automatic_resources_min_replica_count=1,
            automatic_resources_max_replica_count=1,
        )

Replace the following:

  - PROJECT\_ID : The Google Cloud project that this pipeline runs in.

  - PIPELINE\_ROOT\_PATH : Specify a Cloud Storage URI that your [pipelines service account can access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) . The artifacts of your pipeline runs are stored within the pipeline root. The Cloud Storage URI must start with `gs://` .
    
    The pipeline root can be set as an argument of the `@kfp.dsl.pipeline` annotation on the pipeline function, or it can be set when you call `create_run_from_job_spec` to create a pipeline run.

### Compile your pipeline into a YAML file

After the workflow of your pipeline is defined, you can proceed to compile the pipeline into YAML format. The YAML file includes all the information for executing your pipeline on Agent Platform Pipelines.

    from kfp import compiler
    
    compiler.Compiler().compile(
        pipeline_func=pipeline,
        package_path='image_classif_pipeline.yaml'
    )

### Submit your pipeline run

After the workflow of your pipeline is compiled into the YAML format, you can use the Gemini Enterprise Agent Platform Python client to submit and run your pipeline.

    import google.cloud.aiplatform as aip
    
    # Before initializing, make sure to set the GOOGLE_APPLICATION_CREDENTIALS
    # environment variable to the path of your service account.
    aip.init(
        project=project_id,
        location=PROJECT_REGION,
    )
    
    # Prepare the pipeline job
    job = aip.PipelineJob(
        display_name="automl-image-training-v2",
        template_path="image_classif_pipeline.yaml",
        pipeline_root=pipeline_root_path,
        parameter_values={
            'project_id': project_id
        }
    )
    
    job.submit()

Replace the following:

  - PROJECT\_REGION : The region that this pipeline runs in.

In the preceding example:

1.  A Kubeflow pipeline is defined as a Python function. The function is annotated with the `@kfp.dsl.pipeline` decorator, which specifies the pipeline's name and root path. The pipeline root path is the location where the pipeline's artifacts are stored.
2.  The pipeline's workflow steps are created using the [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) . By using the outputs of a component as an input of another component, you define the pipeline's workflow as a graph. For example: `training_job_run_op` depends on the `dataset` output of `ds_op` .
3.  You compile the pipeline using `kfp.compiler.Compiler` .
4.  You create a pipeline run on Agent Platform Pipelines using the Gemini Enterprise Agent Platform Python client. When you run a pipeline, you can override the pipeline name and the pipeline root path. Pipeline runs can be grouped using the pipeline name. Overriding the pipeline name can help you distinguish between production and experimental pipeline runs.

To learn more about building pipelines, read the [building Kubeflow pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline#build-pipeline) section, and [follow the samples and tutorials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/notebooks#general-tutorials) .

## Test a pipeline locally (optional)

After you define your pipelines and components, you can test the component code by executing the code in your local authoring environment. By executing your pipeline or a component locally, you can identify and debug potential issues before you [create a pipeline run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline) in a remote environment, such as Agent Platform Pipelines. For more information about locally executing pipelines and components, see [Local execution](https://www.kubeflow.org/docs/components/pipelines/v2/local-execution) in the [KFP documentation](https://www.kubeflow.org/docs/components/pipelines/v2/introduction) .

> **Note:** You can't locally test your pipeline code if any of the components requires authentication to use Google Cloud services. These include Google Cloud Pipeline Components. [Learn more about the limitations of local execution.](https://www.kubeflow.org/docs/components/pipelines/v2/local-execution/#limitations)

This page shows you how to define and run a pipeline that consists of two tasks.

### Set up your local environment

1.  Optional: [Install Docker](https://docs.docker.com/engine/install/) .
    
    > **Note:** To verify whether Docker is installed or not, run the following command:  
    > `docker --version`  
    > If the command is unavailable, then you need to install Docker.

2.  Use the following code sample to define a simple pipeline:
    
        from kfp import dsl
        
        # Define a component to add two numbers.
        @dsl.component
        def add(a: int, b: int) -> int:
            return a + b
        
        # Define a simple pipeline using the component.
        @dsl.pipeline
        def addition_pipeline(x: int, y: int, z: int) -> int:
            task1 = add(a=x, b=y)
            task2 = add(a=task1.output, b=z)
            return task2.output

### Invoke a local execution

Initialize a local session using the `local.init()` function. When you use `local.init()` , the KFP SDK locally executes your pipelines and components when you call them.

When you use `local.init()` , you must specify a runner type. The runner type indicates how KFP should run each task.

Use the following sample to specify the `DockerRunner` runner type for running each task in a container. For more information about local runners supported by KFP, see [Local runners](https://www.kubeflow.org/docs/components/pipelines/v2/local-execution/#local-runners) in the KFP documentation.

    from kfp import local
    
    local.init(runner=local.DockerRunner())
    
    pipeline_task = addition_pipeline(x=1, y=2, z=3)

Use the following code to view the output of the pipeline task upon local execution:

    print(f'Result: {pipeline_task.output}')

## Building Kubeflow pipelines

Use the following process to build a pipeline.

1.  Design your pipeline as a series of components. To promote reusability, each component should have a single responsibility. Whenever possible, design your pipeline to reuse proven components such as the [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) .
    
    [Learn more about designing pipelines](https://www.kubeflow.org/docs/components/pipelines/v2/hello-world/) .

2.  Build any custom components that are required to implement your ML workflow using Kubeflow Pipelines SDK. Components are self-contained sets of code that perform a step in your ML workflow. Use the following options to create your pipeline components.
    
      - Package your component's code as a container image. This option lets you include code in your pipeline that was written in any language that can be packaged as a container image.
        
        [Learn how to build a Kubeflow pipeline component](https://www.kubeflow.org/docs/components/pipelines/v2/components/) .
    
      - Implement your component's code as a standalone Python function and use the Kubeflow Pipelines SDK to package your function as a component. This option makes it easier to build Python-based components.
        
        [Learn how to build Python function-based components](https://www.kubeflow.org/docs/components/pipelines/v2/components/lightweight-python-components/) .

3.  Build your pipeline as a Python function.
    
    [Learn more about defining your pipeline as a Python function](https://www.kubeflow.org/docs/components/pipelines/v2/pipelines/pipeline-basics/) .

4.  Use the Kubeflow Pipelines SDK compiler to compile your pipeline.
    
        from kfp import compiler
        
        compiler.Compiler().compile(
            pipeline_func=PIPELINE_FUNCTION,
            package_path=PIPELINE_PACKAGE_PATH)
    
    Replace the following:
    
      - PIPELINE\_FUNCTION : The name of your pipeline's function.
      - PIPELINE\_PACKAGE\_PATH : The path to where to store your compiled pipeline.

5.  [Run your pipeline using Google Cloud console or Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline) .

## Accessing Google Cloud resources in a pipeline

If you don't specify a service account when you run a pipeline, Agent Platform Pipelines uses the Compute Engine default service account to run your pipeline. Agent Platform Pipelines also uses a pipeline run's service account to authorize your pipeline to access Google Cloud resources. The Compute Engine default service account has the [**Project Editor** role](https://docs.cloud.google.com/iam/docs/roles-overview#basic) by default. This may grant your pipelines excessive access to Google Cloud resources in your Google Cloud project.

We recommend that you [create a service account to run your pipelines and then grant this account granular permissions to the Google Cloud resources that are needed to run your pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) .

Learn more about using Identity and Access Management to [create a service account](https://docs.cloud.google.com/iam/docs/creating-managing-service-accounts) and [manage the access granted to a service account](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

## Keep your pipelines up-to-date

The SDK clients and container images that you use to build and run pipelines are periodically updated to new versions to patch security vulnerabilities and add new functionality. To keep your pipelines up to date with the latest version, we recommend that you do the following:

  - Review the [Gemini Enterprise Agent Platform framework support policy](https://docs.cloud.google.com/vertex-ai/docs/framework-support-policy) and [Supported frameworks list](https://docs.cloud.google.com/vertex-ai/docs/supported-frameworks-list#pipelines) .

  - Subscribe to the [Gemini Enterprise Agent Platform release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/release-notes) and the PyPi.org RSS feeds for SDKs you use ( [Kubeflow Pipelines](https://www.kubeflow.org/docs/components/pipelines/overview/) SDK, [Google Cloud Pipeline Components SDK](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/index.html) , or [TensorFlow Extended SDK](https://github.com/tensorflow/tfx) ) to stay aware of new releases.

  - If you have a pipeline template or definition that references a container with security vulnerabilities, you should do the following:
    
    1.  Install the latest patched version of the SDK.
    
    2.  Rebuild and recompile your pipeline template or definition.
    
    3.  Re-upload the template or definition to Artifact Registry or Cloud Storage.

## What's next

  - Read the [introduction to Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) to learn more about orchestrating ML workflows.
  - Learn how to [run a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline) .
  - [Visualize and analyze the results of your pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/visualize-pipeline) .
