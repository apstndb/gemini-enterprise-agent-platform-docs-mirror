---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/delete-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/delete-model
title: Delete a model from Gemini Enterprise Agent Platform Model Registry
description: Delete a model that you no longer need from the Gemini Enterprise Agent Platform Model Registry.
data_source: docs.cloud.google.com
---

Learn how to delete a model you no longer need from the Gemini Enterprise Agent Platform Model Registry.

If you want to delete a BigQuery ML from Gemini Enterprise Agent Platform Model Registry, you must first delete it from BigQuery ML. To learn more, see [BigQuery ML and Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/bigquery-ml/docs/managing-models-vertex) .

If you want to delete a model that is deployed to an endpoint, you need to undeploy it first. Otherwise, you are unable to delete the model.

## Delete a model

### Console

1.  Go to the **Model Registry** page from the Agent Platform section in the Google Cloud console.

2.  Select **More actions** from the model you want to delete. more\_vert

3.  Select **Delete model** . When you delete the model, all associated model versions and evaluations are deleted from your Google Cloud project.

4.  Click **Delete** on the confirmation screen.

### gcloud

Before using any of the command data below, make the following replacements:

  - MODEL\_ID : The ID of your model.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
  - LOCATION : Your project's region. For example, `us-central1` . If the region in the API endpoint URL conflicts with the location in the resource path, the location in the path is ignored..

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai models delete MODEL_ID \
        --project=PROJECT_ID \
        --region=LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai models delete MODEL_ID `
        --project=PROJECT_ID `
        --region=LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai models delete MODEL_ID ^
        --project=PROJECT_ID ^
        --region=LOCATION

### API

Delete a model using the Agent Platform SDK for Python.

### Python

    from google.cloud import aiplatform
    
    
    def delete_model_sample(model_id: str, project: str, location: str):
        """
        Delete a Model resource.
        Args:
            model_id: The ID of the model to delete. Parent resource name of the model is also accepted.
            project: The project.
            location: The region name.
        Returns
            None.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Get the model with the ID 'model_id'. The parent_name of Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        model = aiplatform.Model(model_name=model_id)
    
        # Delete the model.
        model.delete()

## Delete a model version

### Console

1.  Go to the **Model Registry** page from the Vertex AI section in the Google Cloud console.

2.  Expand the model to view its model versions. Select the version that you want to delete.

3.  Select the **More actions** from the model version. menu more\_vert .

4.  Select **Delete version** . All associated model evaluations are deleted when you delete your version.

### gcloud

Before using any of the command data below, make the following replacements:

  - MODEL\_VERSION\_ID : The ID of the model version to delete.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
  - LOCATION : Your project's region. For example, `us-central1` . If the region in the API endpoint URL conflicts with the location in the resource path, the location in the path is ignored..

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai models delete-version MODEL_VERSION_ID \
        --project=PROJECT_ID \
        --region=LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai models delete-version MODEL_VERSION_ID `
        --project=PROJECT_ID `
        --region=LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai models delete-version MODEL_VERSION_ID ^
        --project=PROJECT_ID ^
        --region=LOCATION

### API

### Python

    from google.cloud import aiplatform
    
    
    def delete_model_version_sample(
        model_id: str, version_id: str, project: str, location: str
    ):
        """
        Delete a Model version.
        Args:
            model_id: The ID of the model to delete. Parent resource name of the model is also accepted.
            version_id: The version ID or version alias of the model to delete.
            project: The project ID.
            location: The region name.
        Returns
            None.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Initialize the Model Registry resource with the ID 'model_id'.The parent_name of Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        model_registry = aiplatform.models.ModelRegistry(model=model_id)
    
        # Delete the model version with the version 'version'.
        model_registry.delete_version(version=version_id)

## Delete a model version with the default alias

### Console

1.  From the Model Registry, select the model name to view its model versions.
2.  Select the version that you want, and from the **Actions** button more\_vert click **Delete** . A warning opens since you're attempting to delete the default alias version. Set another version as default first.
3.  Select what version you want to make default for the model from the drop-down.
4.  On the confirmation screen, click **Set and delete.**

### API

### Python

    from typing import List
    
    from google.cloud import aiplatform
    
    
    def delete_aliases_model_version_sample(
        model_id: str,
        version_aliases: List[str],
        version_id: str,
        project: str,
        location: str,
    ):
        """
        Delete aliases to a model version.
        Args:
            model_id: The ID of the model.
            version_aliases: The version aliases to assign.
            version_id: The version ID of the model to assign the aliases to.
            project: The project ID.
            location: The region name.
        Returns
            None.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Initialize the Model Registry resource with the ID 'model_id'.The parent_name of Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        model_registry = aiplatform.models.ModelRegistry(model=model_id)
    
        # Remove the version aliases to the model version with the version 'version'.
        model_registry.remove_version_aliases(
            target_aliases=version_aliases, version=version_id
        )
