---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes
title: Prompt management
description: Understand Gemini Enterprise Agent Platform prompt management. Define, version, and deploy prompts for Gemini models using `vertexai.v1.prompts`.
data_source: docs.cloud.google.com
---

This page introduces a unified set of capabilities to define, save, retrieve, and manage prompts within your Google Cloud project using the Agent Platform SDK prompt management module.

## Overview

Gemini Enterprise Agent Platform offers tooling to help manage prompt templates and prompt data. Prompt templates can be versioned and used with generative models on Agent Platform. Each prompt can be assembled and versioned in Agent Studio on Gemini Enterprise Agent Platform or the Agent Platform SDK.

Prompt management in the Agent Platform SDK includes full enterprise support, including support for Customer-Managed Encryption Keys (CMEK) and VPC Service Controls (VPCSC).

## Prompt management capabilities

To use any of the generative AI capabilities from the Agent Platform SDK, do the following:

1.  Install the latest version of the Agent Platform SDK.
    
        pip install --upgrade google-cloud-aiplatform

2.  Create a generative AI client using the following Python code sample:
    
    ``` 
        import vertexai
        from vertexai import types
    
        # Instantiate GenAI client from Agent Platform
        # Replace with your project ID and location
        client = vertexai.Client(project='my-project', location='my-location')
    ```

After you've created a generative AI client, you can use any of the following prompt management capabilities in the Agent Platform SDK:

  - [Create a local prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes#create-local-prompt) .
  - [Save a prompt to a Google Cloud project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes#create-prompt) .
  - [Get a saved prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes#get-saved-prompt) .
  - [List prompts and versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes#list-prompts-versions) .
  - [Delete a prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes#delete-prompt) .
  - [Restore a prompt version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/prompt-classes#restore-prompt-version) .

### Create a local prompt

This section provides an example of how to define a `types.Prompt` variable for use throughout this page.

The `Prompt` class is used for defining, assembling, and using prompts. The `prompt_data` attribute is defined for the `Prompt` class and includes the following:

Attribute

`model`

Required: The model name.

`contents`

Required: The content of the conversation with the model. Only single-turn prompts are supported.

`generation_config`

Optional: Generation configuration

`tool_config`

Optional: This configuration is shared for all tools provided in the request.

`tools`

Optional: A list of `Tools` the model might use to generate the next response. A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of the knowledge and scope of the model.

`safety_settings`

Optional: The request settings for blocking unsafe content, which are enforced on `GenerateContentResponse.candidates` .

`system_instruction`

Optional: The user-provided system instructions for the model.

`variables`

Optional: If your prompt contains a template variable, provide the values to use for that variable. For example, if your prompt text contents are "Hello, {name}". Your variables list should include a dictionary of all possible values for the "{name}" variable. Example:

``` 
        "variables": [
            {"name": {"text": "Alice"}},
            {"name": {"text": "Bob"}},
        ],
        
```

This code sample demonstrates how to define a `types.Prompt` variable.

``` 
  import vertexai
  from vertexai import generative_models
  from vertexai import types

  prompt = types.Prompt(
      prompt_data=types.PromptData(
        contents=[generative_models.Content(parts=[generative_models.Part(text="Hello, {name}! How are you?")])],
        variables=[
          {"name": generative_models.Part(text="Alice")},
          {"name": generative_models.Part(text="Bob")},
        ],
        model="your-model",
      ),
  )
```

### Save a prompt to a Google Cloud project

This section presents the parameters and an example for how to save a prompt to a Google Cloud project.

#### Parameters

This table describes the parameters used by the `create` method:

Parameters

`prompt`

The data for a specific prompt.

`config`

Optional: A `types.CreatePromptConfig` object representing the configuration for creating a prompt.

This table describes the parameters used by the `create_version` method:

Parameters

`prompt`

Required: The data for a specific prompt.

`config`

Optional: A `types.CreatePromptConfig` object representing the configuration for creating a prompt version.

A `Prompt` is returned by the `create_version` method.

#### Example

To save a prompt to a Google Cloud project, use the `client.prompts.create` and `client.prompts.create_version` methods.

The `client.prompts.create` method creates a prompt resource in a Google Cloud project. The `client.prompts.create_version` method creates a prompt version within that resource, and you can access the resource in the Google Cloud console.

The `client.prompts.create` method takes a `Prompt` object as input and creates a prompt in the Google Cloud project. The `client.prompts.create_version` method also requires passing in `prompt_id` , which is the ID of the prompt resource to create the version under. A new `Prompt` object is returned, which is associated with the Google Cloud project. Any updates made to a `Prompt` object are local until `create` or `create_version` is called.

The following code sample shows you how to save a prompt and a prompt version:

``` 
  # Save `Prompt` to a Google Cloud project.
  # Returns a new `Prompt` object associated with the saved prompt resource.
  prompt_resource = client.prompts.create(prompt=prompt)
  prompt_version_resource = client.prompts.create_version(prompt=prompt, prompt_id=prompt_resource.prompt_id)
```

### Get a saved prompt

This section presents the parameters and an example for how to get a prompt and a prompt version.

There are two methods: `client.prompts.get` and `client.prompts.get_version` .

#### Parameters

This table describes the parameters used by the `client.prompts.get` method:

Parameters

`prompt_id`

Required: The ID for the prompt to retrieve.

`config`

Optional: A `types.GetPromptConfig` object representing the configuration for getting a prompt.

This table describes the parameters used by the `client.prompts.get_version` method:

Parameters

`prompt_id`

Required: The ID for the prompt to retrieve.

`version_id`

Required: The ID of the prompt version that you want to retrieve.

`config`

Optional: A `types.GetPromptConfig` object representing the configuration for getting a prompt.

A `Prompt` is returned by the `get` and `get_version` methods.

#### Examples

To get (load) a prompt that has been saved to the Google Cloud project, use the `client.prompts.get` method. This method takes the prompt ID as input and returns the corresponding `Prompt` object. This code sample shows how to load a saved prompt:

``` 
  # Get prompt
  retrieved_prompt = client.prompts.get(prompt_id=prompt_resource.prompt_id)
```

The following code sample shows you how to get a version of a prompt.

``` 
  retrieved_prompt_version = client.prompts.get_version(prompt_id='your-prompt-id', version_id='your-prompt-version-id')
```

The following code demonstrates how to use the retrieved prompt to generate content:

``` 
  import vertexai
  from vertexai import generative_models

  model = generative_models.GenerativeModel(retrieved_prompt.prompt_data.model)

  response = model.generate_content(
      contents=retrieved_prompt.assemble_contents(),
  )
```

### List prompts and versions

This section presents the parameters and an example for how to list prompts and prompt versions.

There are two methods: `client.prompts.list` and `client.prompts.list_versions` .

#### Parameters

This table describes the parameters used by the `list` method:

Parameters

`config`

Optional: A `types.ListPromptsConfig` object representing the configuration for listing prompts.

This table describes the parameters used by the `list_versions` method:

Parameters

`prompt_id`

Required: The ID of the prompt to list versions for.

`config`

Optional: A `types.ListPromptsConfig` object representing the configuration for listing prompt versions.

Both the `list` and `list_versions` methods return an `Iterator` of `types.PromptRef` objects. The `PromptRef` contains a reference to a prompt.

#### Example

To see the prompt ID and model for all prompts saved in your Google Cloud project, use the `list` method.

The following code sample demonstrates how to retrieve a `PromptRef` for all saved prompts in the current project:

``` 
  prompt_refs = list(client.prompts.list())

  # Get a prompt from the list
  prompt1 = client.prompts.get(prompt_id=prompt_refs[0].prompt_id)
```

The following code sample demonstrates how to list prompt and version IDs for all prompt versions saved within the prompt:

``` 
  prompt_versions_metadata = client.prompts.list_versions(prompt_id="123456789")

  # Get a specific prompt version from the versions metadata list
  prompt1 = client.prompts.get_version(
      prompt_id=prompt_versions_metadata[0].prompt_id,
      version_id=prompt_versions_metadata[0].version_id
  )
```

### Delete a prompt

This section presents the parameters and an example for how to delete a prompt.

There are two methods: `delete` and `delete_version` .

#### Parameters

This table describes the parameters used by the `delete` method:

> **Important:** The `delete` method deletes a prompt and all of the versions associated with the prompt. After a prompt is deleted, it can't be restored.

Parameters

`prompt_id`

The ID of the prompt to delete.

`config`

Optional: A `types.DeletePromptConfig` object representing the configuration for deleting a prompt.

This table describes the parameters used by the `delete_version` method:

Parameters

`prompt_id`

The ID for the prompt to delete a version from.

`version_id`

The version of the prompt to delete.

`config`

Optional: A `types.DeletePromptConfig` object representing the configuration for deleting a prompt version.

#### Examples

To delete a prompt and all of its versions, use the `delete` method.

``` 
  client.prompts.delete(prompt_id=retrieved_prompt.prompt_id)
```

To delete a specific version from a prompt resource, use the `delete_version` method.

``` 
  client.prompts.delete_version(prompt_id=retrieved_prompt.prompt_id, version_id='your-version-id')
```

### Restore a prompt version

This section presents the parameters and an example for how to restore a prompt version.

#### Parameters

This table describes the parameters used by the `restore_version` method:

Parameters

`prompt_id`

The ID for a specific prompt.

`version_id`

The version of the prompt to restore.

`config`

The configuration for restoring a prompt version.

A `Prompt` object is returned by the `restore_version` method.

#### Example

A prompt resource also contains version history that stores previous saved versions of the prompt. You can use the `restore_version()` method to restore an older version as the latest version of the prompt. This returns a `Prompt` object.

``` 
  # Restore to prompt version id 1
  restored_prompt = client.prompts.restore_version(prompt_id=retrieved_prompt.prompt_id, version_id='1')
```

## What's next

  - To learn more about prompts supporting function calling, see [Introduction to function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .
