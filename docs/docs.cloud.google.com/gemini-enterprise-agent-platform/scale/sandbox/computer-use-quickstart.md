---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use-quickstart
title: Computer Use quickstart
description: Learn how to create and use a Computer Use sandbox.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides a sandbox environment for AI Agents, and so the "Agentic AI Services" Service Specific Terms apply. To utilize this feature, you will need to enable full network access for your AI Agent so please consider applicable safeguards (including human supervision) and your organization's policies before doing so. For built-in computer use safeguards, consider the Agent Platform [Computer Use Tool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use#safety-and-security) .
> 
> Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

This page demonstrates how to make direct API calls to create and use a Computer Use sandbox environment. In this quickstart, you perform the follow tasks:

  - Create an Agent Platform instance to access the sandbox.
  - Create a Computer Use sandbox.
  - Generate an access token for the sandbox.
  - Send a request to check status.
  - Clean up resources.

## Before you begin

Set up your project and environment.

### Set up your project

### Get the required roles

To use the sandbox and generate tokens, you need the following roles:

  - Agent Platform User ( `roles/aiplatform.user` ) on the project.
  - Service Account Token Creator ( `roles/iam.serviceAccountTokenCreator` ) on the service account used for token generation.
  - The service account used for token generation must also have the Agent Platform User ( `roles/aiplatform.user` ) role on the project.

### Install libraries

Install the Agent Platform SDK: `posix-terminal pip install google-cloud-aiplatform>=1.112.0`

## Create an Agent Platform instance

To use the sandbox, first create an Agent Platform instance.

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
  - `LOCATION` : The region for your instance (such as `us-central1` ).

## Create a template for Computer Use

Create a sandbox template that you'll use when you create a Computer Use sandbox.

    # Create a default Computer Use sandbox template
    templates_client = client.agent_engines.sandboxes.templates
    tmplt_operation = templates_client.create(
        name=agent_instance_name,
        display_name='DISPLAY_NAME',
        config={
            "default_container_environment": {
                "default_container_category": "DEFAULT_CONTAINER_CATEGORY_COMPUTER_USE",
            },
            "egress_control_config": {
                "internet_access": True,
            },
        },
    )
    template_name = tmplt_operation.response.name
    print(f"Created template: {template_name}")

## Create a Computer Use sandbox

Create a sandbox environment from the template.

    # Create a sandbox environment referencing the template
    create_operation = client.agent_engines.sandboxes.create(
        name=agent_instance_name,
        config={
            "sandbox_environment_template": template_name,
            "display_name": 'DISPLAY_NAME',
        }
    )
    sandbox = create_operation.response
    print(f"Created sandbox environment: {sandbox.name}")

## Generate an access token

To interact with the sandbox, generate a JSON web token (JWT) access token by using a service account.

    service_account_email = "SERVICE_ACCOUNT_EMAIL"
    access_token = client.agent_engines.sandboxes.generate_access_token(
        service_account_email=service_account_email,
    )

Replace `SERVICE_ACCOUNT_EMAIL` with the email of the service account that has the Service Account Token Creator role.

## Send a request to the sandbox

Send an HTTP GET request to the sandbox API server to check its status.

    response = client.agent_engines.sandboxes.send_command(
        http_method="GET",
        access_token=access_token,
        sandbox_environment=sandbox
    )
    print(f"Sandbox response: {response.body}")

Send an HTTP POST request to navigate to a specific page.

    data = {"command": "Page.navigate", "params": {"url": "https://example.com"}}
    
    response = client.agent_engines.sandboxes.send_command(
        http_method="POST",
        path="cdp",
        access_token=access_token,
        request_dict=data,
        sandbox_environment=sandbox
    )

The following table lists additional methods and paths you can send to your sandbox:

| Method | Path                     | Description                                           |
| :----- | :----------------------- | :---------------------------------------------------- |
| GET    | /                        | Gets sandbox health check                             |
| POST   | /tabs                    | Creates a new tab and returns its details.            |
| GET    | /tabs                    | Lists details for all open tabs.                      |
| POST   | /tabs/{tab\_id}/activate | Sets a tab as active and brings it to the foreground. |
| DELETE | /tabs/{tab\_id}          | Closes a specific tab.                                |
| GET    | /cdp\_ws\_endpoint       | Returns the CDP WebSocket endpoint path.              |
| POST   | /cdp                     | Runs a CDP command on the active tab.                 |
| POST   | /cdps                    | Runs multiple CDP commands on the active tab.         |

For more information about the supported CDP commands and format, see the [CDP site](https://chromedevtools.github.io/devtools-protocol/) .

## Clean up

To avoid incurring charges, delete the resources created in this quickstart.

    client.agent_engines.sandboxes.delete(name=sandbox.name)
    agent_instance.delete()

## What's next

  - Explore [Snapshots](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-snapshots) for sandbox lifecycle management.
