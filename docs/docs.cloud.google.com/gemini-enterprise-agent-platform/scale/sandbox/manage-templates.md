---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates
title: Manage sandbox templates
description: Learn how to manage agent sandbox templates, including listing them, viewing their details, and deleting them.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Sandbox templates serve as blueprints for [custom container sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers) . This page demonstrates how to manage the lifecycle of sandbox templates using the Python SDK. You can list existing templates, view their details, or delete them when they are no longer needed.

To modify a template's configuration (such as changing the container image), delete the existing template and create a new one with the updated configuration.

## Before you begin

To manage sandbox templates, you need the following roles on your project:

  - Agent Platform User ( `roles/aiplatform.user` )

## List templates

To list all sandbox templates associated with an Agent Platform instance:

    import vertexai
    
    client = vertexai.Client(project='<var>PROJECT_ID</var>', location='<var>LOCATION</var>')
    instance_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID'
    
    templates_response = client.agent_engines.sandboxes.templates.list(name=instance_name)
    
    for template in templates_response.sandbox_environment_templates:
        print(template.name)

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID.

## View template details

To view the configuration of a specific sandbox template:

    template_name = 'projects/PROJECT_ID/locations/LOCATION/reasoningEngines/INSTANCE_ID/SandboxEnvironmentTemplate/TEMPLATE_ID'
    
    template = client.agent_engines.sandboxes.templates.get(name=template_name)
    print(template)

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region of your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
  - `INSTANCE_ID` : The Agent Platform instance ID that contains your sandbox template.
  - `TEMPLATE_ID` : The sandbox template ID.

## Delete a template

To delete a sandbox template:

    client.agent_engines.sandboxes.templates.delete(name=template_name)
    print("Template deleted.")

> **Note:** Deactivating a template is done by deleting it. You cannot delete a template if a warm pool is actively using it (meaning the template is being created) or if sandboxes are being created from it.
