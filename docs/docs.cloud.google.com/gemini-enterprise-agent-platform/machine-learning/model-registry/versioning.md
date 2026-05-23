---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/versioning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/versioning
title: Model versioning with Model Registry
description: Learn how to use model versioning to organize models and understand the impact of changes by viewing models and their versions in a single view within the Model Registry.
data_source: docs.cloud.google.com
---

Model versioning lets you create multiple versions of the same model. With model versioning, you can organize your models in a way that helps navigate and understand which changes had what effect on the models. With Model Registry you can view your models and all of their versions in a single view. You can drill down into specific model versions and see exactly how they performed.

## Import a new model version

From the Model Registry, you can import a model as a new version of an existing model.

### Console

1.  In the Google Cloud console, go to the **Model Registry** page.  
2.  On the top of the page, select **Import** .
3.  Select **Import as new version** .
4.  From the drop-down, select the model this is a new version of. Add an optional version description.
5.  Optionally set this model as the default version. The default version is preselected whenever the model is used for prediction (although you can still select other versions).
6.  Select your Region.
7.  Select **Continue** .
8.  From the Model settings, define what container you want to use. You can select to import model artifacts into a new prebuilt container or import into an existing custom container. To learn more about containers, see [Import models to Vertex AI](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .
9.  Select **Continue** .
10. Optional: Add explainability support to your model.
11. Select **Import** .

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The project ID.
  - LOCATION : The location.
  - MODEL\_DISPLAY\_NAME : The model name.
  - ARTIFACT\_URI : The path to the directory containing the model artifact and any of its supporting files.
  - IMAGE\_URI : Docker image to be used as the custom container for serving predictions.
  - PARENT\_MODEL : The resource name of the model into which to upload the version.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/models:upload

Request JSON body:

    {
    
      "model": {
        "displayName": "MODEL_DISPLAY_NAME",
        "artifactUri": "ARTIFACT_URI",
        "containerSpec": {
           "imageUri": "IMAGE_URI"
        }
       },
     "parentModel": "PARENT_MODEL"
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/models:upload"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/models:upload" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

### Python

    from typing import List
    
    from google.cloud import aiplatform
    
    
    def upload_new_model_version_using_custom_training_pipeline(
        display_name: str,
        script_path: str,
        container_uri,
        model_serving_container_image_uri: str,
        dataset_id: str,
        replica_count: int,
        machine_type: str,
        accelerator_type: str,
        accelerator_count: int,
        parent_model: str,
        args: List[str],
        model_version_aliases: List[str],
        model_version_description: str,
        is_default_version: bool,
        project: str,
        location: str,
    ):
        """
        Uploads a new model version using a custom training pipeline.
        Args:
            display_name: The display name of the model version.
            script_path: The path to the Python script that trains the model.
            container_uri: The URI of the container to use for training.
            model_serving_container_image_uri: The URI of the serving container image to use.
            dataset_id: The ID of the dataset to use for training.
            replica_count: The number of replicas to use for training.
            machine_type: The machine type to use for training.
            accelerator_type: The accelerator type to use for training.
            accelerator_count: The number of accelerators to use for training.
            parent_model: The parent resource name of an existing model.
            args: A list of arguments to pass to the training script.
            model_version_aliases: The aliases of the model version to create.
            model_version_description: The description of the model version.
            is_default_version: Whether the model version is the default version.
            project: The project ID.
            location: The region name.
        Returns:
            The new version of the model.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Create the training job.
        # This job will upload a new, non-default version of the my-training-job model
        job = aiplatform.CustomTrainingJob(
            display_name=display_name,
            script_path=script_path,
            container_uri=container_uri,
            model_serving_container_image_uri=model_serving_container_image_uri,
        )
    
        # Create dataset
        # This examples uses a TabularDataset, but you can use any dataset type.
        dataset = aiplatform.TabularDataset(dataset_id) if dataset_id else None
    
        # Run the training job.
        model = job.run(
            dataset=dataset,
            args=args,
            replica_count=replica_count,
            machine_type=machine_type,
            accelerator_type=accelerator_type,
            accelerator_count=accelerator_count,
            parent_model=parent_model,
            model_version_aliases=model_version_aliases,
            model_version_description=model_version_description,
            is_default_version=is_default_version,
        )
    
        return model

## Train a new model version

From the Model Registry, you can train a new version of a model.

### Console

From the Model Registry, you can create a version of an existing model. To learn more about how to add or create a model version in your training pipeline, see [CustomJob and model upload](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#custom-job-model-upload)

1.  In the Google Cloud console, go to the **Model Registry** page.  
2.  On the top of the page, select **Create** . Enter the training method details and select the model training method.
3.  Click **Continue** .
4.  Under Model details, select the **Train new version** option. From the dropdown select the model you are adding a new version to. Add a description of the version. Click **Continue** .
5.  From the **Compute and pricing** section, enter your budget and select **Start training** when you're ready. When the model training completes, the new version is visible from the Model Registry.

### REST

Before using any of the request data, make the following replacements:

  - TRAINING\_PIPELINE\_NAME : A display name for the trainingPipeline
  - TRAINING\_TASK\_INPUT : The training task's parameter(s).
  - PARENT\_MODEL : The resource name of the model into which to upload the version.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAINING_PIPELINE_NAME",
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/custom_task_1.0.0.yaml",
      "trainingTaskInputs":"TRAINING_TASK_INPUT"
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAY_NAME",
        "containerSpec": {
           "imageUri": "IMAGE_URI"
        },
      },
      "parentModel": "PARENT_MODEL",

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/trainingPipelines"

#### PowerShell (Windows)

Save the request body in a file named `request.json` , and execute the following command:

    $headers = @{  }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

### Python

    from google.cloud import aiplatform
    
    
    def create_default_model_sample(model_id: str, project: str, location: str):
        """
        Initialize a Model resource to represent an existing model version with alias 'default'.
        Args:
            model_id: The ID of the model to initialize. Parent resource name of the model is also accepted.
            project: The project ID.
            location: The region name.
        Returns:
            Model resource.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Initialize the Model resource with the ID 'model_id'. The parent_name of the Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        default_model = aiplatform.Model(model_name=model_id)
    
        return default_model

## How to view a list of all versions of a model

From a model version's details page, you can choose to deploy and test your model, set up batch inference, and evaluate depending on the model type. You can also view the dataset used to train the model version directly from the version details page.

### Console

From the Model Registry, you can view a list of all versions of a model. This can help you gain at a glance insight and helps with model organization.

1.  In the Google Cloud console, go to the **Model Registry** page.  
2.  Under the Name column, select the name of a model which has multiple versions. The versions page opens.
3.  A list of all versions and their associated version IDs is displayed.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The project ID associated to this model
  - LOCATION : The region where you are using Vertex AI.
  - MODEL\_ID : The ID associated with a specific model.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

### Python

    from google.cloud import aiplatform
    
    
    def list_model_versions_sample(model_id: str, project: str, location: str):
        """
        List all model versions of a model.
        Args:
            model_id: The ID of the model to list. Parent resource name of the model is also accepted.
            project: The project ID.
            location: The region name.
        Returns:
            versions: List of model versions.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Initialize the Model Registry resource with the ID 'model_id'.The parent_name of Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        model_registry = aiplatform.models.ModelRegistry(model=model_id)
    
        # List all model versions of the model.
        versions = model_registry.list_versions()
    
        return versions

## How to view model version details

From the Model Registry you can see your models and all of your model versions. When selecting a model from the Model Registry, the detail page displays model details and specific model version details. From the details screen, you can evaluate and test your model version, run a batch inference, or deploy the model to an endpoint for online inference.

### Console

Use the following instructions to view your model details page. To view version details, click the version name.

1.  In the Google Cloud console, go to the **Model Registry** page.  
2.  From the Gemini Enterprise Agent Platform Model Registry, click a model name to open the model details page.
3.  A list of all versions and their associated version IDs displays. You see model versions separated by row. Model version details include the version ID, the model alias, status, description, and labels.
4.  To view the details of one of the model versions, select a version ID. The model details page opens
5.  From the details page you can evaluate, deploy and test, use batch prediction, and take a closer look at the version details. Additionally, from this page you can use [Vertex AI Model Evaluation](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction) to compare your model versions.

### Python

### Python

    from google.cloud import aiplatform
    
    
    def get_model_version_info_sample(
        model_id: str, version_id: str, project: str, location: str
    ):
        """
        Get model version info.
        Args:
            model_id: The ID of the model.
            version_id: The version ID of the model version.
            project: The project ID.
            location: The region name.
        Returns:
            VersionInfo resource.
        """
    
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Initialize the Model Registry resource with the ID 'model_id'.The parent_name of Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        model_registry = aiplatform.models.ModelRegistry(model=model_id)
    
        # Get model version info with the version 'version_id'.
        model_version_info = model_registry.get_version_info(version=version_id)
    
        return model_version_info
