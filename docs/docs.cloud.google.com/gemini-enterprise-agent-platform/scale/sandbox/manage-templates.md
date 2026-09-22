---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates
title: Manage sandbox templates
description: Learn how to manage agent sandbox templates, including listing them, viewing their details, and deleting them.
data_source: docs.cloud.google.com
---

Every sandbox is backed by a *sandbox environment template* , which describes the container image to run. Sandbox templates serve as blueprints for [custom container sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers) . This page demonstrates how to manage the lifecycle of sandbox templates using the Agent Platform SDK. You can list existing templates, view their details, or delete them when they are no longer needed.

To modify a template's configuration (such as changing the container image), delete the existing template and create a new one with the updated configuration.

## Before you begin

To manage sandbox templates, you need the following roles on your project:

  - Agent Platform User ( `roles/aiplatform.user` )

## Reuse templates across sandboxes

For Computer Use and shell sandboxes, if you don't specify a template, the default template ( `DEFAULT_CONTAINER_CATEGORY_COMPUTER_USE` or `DEFAULT_CONTAINER_CATEGORY_SHELL_SANDBOX` ) is created for the sandbox.

A new template is created during every `create()` call that doesn't name a template. Deleting the sandbox doesn't delete the template, so you need to delete the templates separately. If you create many sandboxes, we recommend re-using templates to conserve resources.

Create a template:

    from agentplatform._genai import types
    
    template_op = client.agent_engines.sandboxes.templates.create(
        name=instance_name,
        display_name="shell-sandbox-template",
        config=types.CreateSandboxEnvironmentTemplateConfig(
            default_container_environment=types.SandboxEnvironmentTemplateDefaultContainerEnvironment(
                default_container_category=types.DefaultContainerCategory.DEFAULT_CONTAINER_CATEGORY_SHELL_SANDBOX,
            ),
        ),
    )
    template = template_op.response.name

Associate each sandbox with the template by setting `sandbox_environment_template` :

    operation = client.sandboxes.create(
        name=instance_name,
        spec={"shell_environment": {}},
        config={
            "sandbox_environment_template": template,
            "wait_for_completion": True,
        },
    )

## List templates

To list all sandbox templates associated with an Agent Platform instance:

    import agentplatform
    
    client = agentplatform.Client(project='PROJECT_ID', location='LOCATION')
    instance_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID'
    
    templates_response = client.sandboxes.templates.list(name=instance_name)
    
    for template in templates_response.sandbox_environment_templates:
        print(template.name)

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID.

## View template details

To view the configuration of a specific sandbox template:

    template_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/SandboxEnvironmentTemplate/TEMPLATE_ID'
    
    template = client.sandboxes.templates.get(name=template_name)
    print(template)

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID that contains your sandbox template.
  - `TEMPLATE_ID` : The sandbox template ID.

## View a sandbox's template

To view the sandbox template associated with a sandbox, run the following:

    print(sandbox.sandbox_environment_template)

## Delete a template

To delete a sandbox template:

    client.sandboxes.templates.delete(name=template_name)
    print("Template deleted.")

> **Note:** Deactivating a template is done by deleting it. You cannot delete a template if a warm pool is actively using it (meaning the template is being created) or if sandboxes are being created from it.
