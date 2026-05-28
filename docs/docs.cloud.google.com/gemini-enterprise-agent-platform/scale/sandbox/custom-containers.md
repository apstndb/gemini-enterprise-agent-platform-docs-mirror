---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers
title: Custom container sandbox overview
description: Guide on how to Bring Your Own Container (BYOC) for custom execution environments in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The standard sandboxes provide a predefined set of libraries, which provide turnkey solutions for specific tasks like code execution and computer use. For agentic workloads that require specific dependencies, libraries, custom tools, or specialized data plane interfaces, you can provide your own container images (also known as bring your own container or BYOC). This feature lets you run custom workloads within the secure confines of a sandbox environment.

## Before you begin

Set up your project, image repository, and permissions.

### Set up your container image

1.  **Build a container image** : Create a Docker image that contains your custom environment. To ensure compatibility with Gemini Enterprise Agent Platform sandboxes, your custom image must meet the following requirements:
    
      - **OS** : Linux-based (for example, Debian or Ubuntu).
      - **Runner** : Must include a compatible runner or entry point that Gemini Enterprise Agent Platform can use to execute commands.
      - **Security** : Must not require root privileges or access to restricted system resources, as the image will run within a secure, isolated sandbox.

2.  **Add image to Artifact Registry** : Add your image to Google Cloud Artifact Registry where Agent Platform can access it. When you provision your sandbox, provide Artifact Registry image URI.

### Configure permissions

To allow the Agent Sandbox to pull your custom container image from Artifact Registry, grant the **[Artifact Registry Reader](https://docs.cloud.google.com/artifact-registry/docs/access-control#roles)** ( `roles/artifactregistry.reader` ) role on the repository that contains the image to the Agent Sandbox service agent:

  - **Agent Sandbox service agent** : `service-<var>PROJECT_NUMBER</var>@gcp-sa-vertex-sandbox.iam.gserviceaccount.com`

Replace `<var>PROJECT_NUMBER</var>` with the project number of your project.

For more information about granting roles, see [Grant permissions to a service agent](https://docs.cloud.google.com/iam/docs/create-service-agents) .

### Create an Agent Platform instance

If you don't have an Agent Platform instance, create one.

    import vertexai
    client = vertexai.Client(
        project='PROJECT_ID',
        location='LOCATION',
        http_options={
            "api_version": "v1beta1",
        }
    )
    agent_instance = client.agent_engines.create()
    agent_instance_name = agent_instance.api_resource.name

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.
  - `LOCATION` : The Google Cloud region for your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .

## Create a custom container sandbox

To create a custom container sandbox, you first create a sandbox template ( `SandboxEnvironmentTemplate` ). After you create a template, Agent Platform creates pre-warmed pools that are associated with the template to provide faster and more reliable startup times.

To create a template, define a `SandboxEnvironmentTemplate` resource, which specifies the configuration for your custom container:

  - **Container image** : The URI of a prebuilt custom image that is hosted in Artifact Registry.
  - **Ports** : Network ports to expose from the container.

### Create the template

    # Create a custom sandbox template
    templates_client = client.agent_engines.sandboxes.templates
    
    operation = templates_client.create(
        name=agent_instance_name,
        display_name="DISPLAY_NAME",
        config={
            "custom_container_environment": {
                "custom_container_spec": {
                    "image_uri": "IMAGE_LOCATION"
                },
                "resources": {
                    "requests": {
                        "cpu": "1",
                        "memory": "500Mi"
                    },
                    "limits": {
                        "cpu": "1",
                        "memory": "500Mi"
                    }
                },
                "ports": [
                    {
                        "port": PORT_NUMBER,
                        "protocol": "TCP"
                    }
                ]
            },
            "egress_control_config": {
                "internet_access": True
            }
        }
    )
    template_name = operation.response.name
    print(f"Template created: {template_name}")

### Create the sandbox

After you define your template, you can provision a new sandbox environment by referencing the template resource name.

    # Provision a sandbox referencing the template
    create_operation = client.agent_engines.sandboxes.create(
        name=agent_instance_name,
        config={
            "sandbox_environment_template": template_name,
            "display_name": "DISPLAY_NAME"
        }
    )
    sandbox = create_operation.response
    print(f"Sandbox environment provisioned: {sandbox.name}")

## What's next

  - Learn how to [manage your sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage) .
