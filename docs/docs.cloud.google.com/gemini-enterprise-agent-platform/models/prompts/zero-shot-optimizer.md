---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/zero-shot-optimizer
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/zero-shot-optimizer
title: Zero-shot optimizer
description: Learn how to use the zero-shot prompt optimizer to automatically refine and improve user-written prompts.
data_source: docs.cloud.google.com
---

The **zero-shot optimizer** lets you automatically refine and improve user-written prompts. Often, a prompt may not produce the model response you want due to ambiguous language, missing context, or the inclusion of irrelevant information. This optimizer analyzes and rewrites an existing prompt to be clearer, more effective, and better aligned with the model's capabilities, ultimately leading to higher-quality responses.

The zero-shot optimizer is particularly useful for:

  - **Adapting to Model Updates:** When you upgrade to a newer version of a model, your existing prompts might no longer perform optimally.

  - **Enhancing Prompt Comprehension:** When the phrasing of a prompt is complex or could be misinterpreted, the tool can rephrase it for maximum clarity and precision, reducing the chance of an undesirable outcome.

There are two ways to use the optimizer:

  - **Instruction Generation** : Instead of writing complex system instructions from scratch, you can describe your goal or task in plain language. The optimizer will then generate a complete and well-structured set of system instructions designed to achieve your objective.

  - **Prompt Refinement** : You have a working prompt, but the model's output is inconsistent, slightly off-topic, or lacks the detail you want. The optimizer can help improve the prompt for a better output.

The optimizer supports prompt optimization in all languages supported by Gemini and is available through the [Agent Platform SDK](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/reference/libraries)

## Before you begin

To ensure that the [Compute Engine default service account](https://docs.cloud.google.com/iam/docs/service-account-types#default) has the necessary permissions to optimize prompts, ask your administrator to grant the following IAM roles on the project to it and to a user account that has the Agent Platform User ( `roles/aiplatform.user` ) role:

> **Important:** You must grant these roles to the Compute Engine default service account, along with a user account that has the Agent Platform User ( `roles/aiplatform.user` ) role. Failure to grant the roles to the correct principals might result in permission errors.

  - [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )
  - [Agent Platform Service Agent](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent) ( `roles/aiplatform.serviceAgent` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give the [Compute Engine default service account](https://docs.cloud.google.com/iam/docs/service-account-types#default) and your user account the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Optimize a prompt

    # Import libraries
    import vertexai
    import logging
    
    # Google Colab authentication
    from google.colab import auth
    PROJECT_NAME = "PROJECT"
    auth.authenticate_user(project_id=PROJECT_NAME)
    
    # Initialize the Agent Platform client
    client = vertexai.Client(project=PROJECT_NAME, location='us-central1')
    
    # Input original prompt to optimize
    prompt = """You are a professional chef. Your goal is teaching how to cook healthy cooking recipes to your apprentice.
    
    Given a question from your apprentice and some context, provide the correct answer to the question.
    Use the context to return a single and correct answer with some explanation.
    """
    
    # Optimize prompt
    output = client.prompt_optimizer.optimize_prompt(prompt=prompt)
    
    # View optimized prompt
    print(output.model_dump_json(indent=2))

This `output` object is of type `OptimizeResponse` and provides information about the optimization process. The most important part is the `suggested_prompt` which contains the optimized prompt that you can use to get better results from your model. The other fields, especially `applicable_guidelines` , are useful for understanding why and how your prompt was improved, which can help you write better prompts in the future. Here's an example of the output:

    {
      "optimization_mode": "zero_shot",
      "applicable_guidelines": [
        {
          "applicable_guideline": "Structure",
          "suggested_improvement": "Add role definition.",
          "text_before_change": "...",
          "text_after_change": "Role: You are an AI assistant...\n\nTask Context:\n..."
        },
        {
          "applicable_guideline": "RedundancyInstructions",
          "suggested_improvement": "Remove redundant explanation.",
          "text_before_change": "...",
          "text_after_change": ""
        }
      ],
      "original_prompt": "...",
      "suggested_prompt": "Role: You are an AI assistant...\n\nTask Context:\n..."
    }

### Optimizing for smaller models

Smaller models like Gemma 3n E4B have different instruction-following capabilities than larger models. Prompts that perform well for large models might not be optimal for these smaller models. The zero-shot optimizer provides a `gemini_nano` mode to address this issue. The `gemini_nano` mode refines your prompt to align specifically with the characteristics of smaller models, which helps to generate prompts that better fit the capabilities of smaller models.

The following example shows how to optimize a prompt for smaller models:

    client = vertexai.Client(project=PROJECT_NAME, location='us-central1')
    prompt = 'Generate system instructions for analyzing medical articles'
    
    # optimize_prompt returns OptimizeResponse type, which has 2 fields: raw_text_response and parsed_response
    # raw_text_response is guaranteed and always will be given to the user.
    # parsed_response is not guaranteed. If parsing is possible, the parsed response is stored in this field.
    #    parsed_response contains the following 4 fields:
    #    optimization_type, applicable_guidelines, original_prompt, suggested_prompt
    response = client.prompt_optimizer.optimize_prompt(
        prompt=prompt,
        config=vertexai.types.OptimizeConfig(
            optimization_target=vertexai.types.OptimizeTarget.OPTIMIZATION_TARGET_GEMINI_NANO
            )
        )
    
    # print(response.raw_text_response)
    print(response.parsed_response.suggested_prompt)
