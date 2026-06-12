---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-alias
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-alias
title: How to use model version aliases
description: Learn how to manage model aliases.
data_source: docs.cloud.google.com
---

A model alias is a mutable, named reference to a model version unique within a model resource. An alias is "mutable" because aliases can be moved from one model version to another and "named" because they are user-defined, arbitrary strings. Model aliases are helpful for fetching or deploying a particular model version by reference without needing to know the specific version's ID. In this way, they operate similarly to Docker Tags or Branch references in Git.

When you create a new model in Model Registry, the first version automatically gets assigned the *default* alias. The default alias references the model version that is used if a user runs a command on a model without specifying a particular version. One version of a model is required to carry the default alias at all times. Otherwise, the default alias behaves as any other user-defined alias.

From the Google Cloud console the alias marker can help stakeholders understand at a glance which model is the stable version ready for deployment. In addition to the default alias, you can create and assign your own custom aliases to models in the Model Registry.

In Model Registry, you can see at a glance which model version has the default alias by looking at the alias column.

![The Alias column and the Default alias tag.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-registry/images/default_alias.png)

If you decide you want to reassign the alias to a different model version, you can move aliases to a different version.

> **Note:** The required format of the version alias is `[a-z][a-z0-9-]{0,126}[a-z0-9]` to distinguish from `version_id` . A default version alias will be created for the first version of the model, and there must be exactly one default version alias for a model.

Some considerations for using aliases:

  - Your version aliases should be unique; and an alias can only be assigned to a single version, by model, at a time.
  - Version aliases must be non-numerical.
  - If you don't specify a model version for production, the default model is used.
  - An alias is different from a label. [Learn more about model labels here](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-labels) .
  - If you apply an existing alias that is used in another model version, the alias is removed from that version.

## Set a model version as default

1.  In the Google Cloud console, go to the Agent Platform **Model Registry** page.

2.  From the Model Registry, select the name of the model you want to edit. The model details window opens. All of the model versions are listed. One of the model versions has the **default** alias.

3.  Select the **Actions** button for the model version you want to assign the default version.

4.  Click **Set as default** .

## Add an alias to a model version

1.  In the Google Cloud console, go to the Agent Platform **Model Registry** page.

2.  From the Model Registry, select the name of the model you want to edit. The model details window opens.

3.  From the details page, select the model version you want and click **More** .

4.  Click **Edit alias** . Select **Add New.**

5.  **Edit alias:** Click **Add alias** and enter the name of the alias you want to add to the model version.

6.  Click **Save.**

## Upload a new aliased model version

### API

### Python

    from typing import List
    
    from google.cloud import aiplatform
    
    
    def upload_new_aliased_model_version_sample(
        parent_name: str,
        artifact_uri: str,
        serving_container_image: str,
        is_default_version: bool,
        version_aliases: List[str],
        version_description: str,
        project: str,
        location: str,
    ):
        """
        Uploads a new aliased version of a model with ID 'model_id'.
        Args:
            parent_name: The parent resource name of an existing model.
            artifact_uri: The URI of the model artifact to upload.
            serving_container_image: The name of the serving container image to use.
            is_default_version: Whether this version is the default version of the model.
            version_aliases: The aliases of the model version.
            version_description: The description of the model version.
            project: The project ID.
            location: The region name.
        Returns:
            The new version of the model.
        """
        # Initialize the client.
        aiplatform.init(project=project, location=location)
    
        # Upload a new aliased version of the Model resource with the ID 'model_id'. The parent_name of Model resource can be also
        # 'projects/<your-project-id>/locations/<your-region>/models/<your-model-id>'
        model = aiplatform.Model.upload(
            artifact_uri=artifact_uri,
            serving_container_image=serving_container_image,
            parent_name=parent_name,
            is_default_version=is_default_version,
            version_aliases=version_aliases,
            version_description=version_description,
        )
    
        return model

> **Note:** If you don't see the Alias column, you might need to click the **Column display options** button to make sure the Alias column item is selected for display.

## Delete a model alias

When you delete a model version assigned the default alias, the alias is automatically assigned to the next most recent version.

### Console

1.  In the Google Cloud console, go to the Agent Platform **Model Registry** page.

2.  From the Model Registry, select the name of the model you want to edit. The model details window opens.

3.  From the details page click the **Actions** button on the model version.

4.  Click **Edit alias** .

5.  A list of the aliases attached to the model version displays. Hover your cursor to the right of the Alias field for the label to display the delete icon.

6.  Click the delete icon for the alias you want to delete.

7.  Click **Save** .

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
