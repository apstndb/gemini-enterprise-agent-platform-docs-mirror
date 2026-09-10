---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/shell-sandbox-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/shell-sandbox-quickstart
title: Shell sandbox quickstart
description: Learn how to create a Shell Sandbox and run shell commands in an isolated Linux container using Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

A *shell sandbox* is a managed, isolated Linux container attached to an Agent Platform instance. The sandbox runs a shell command sent by your agent and returns stdout, stderr, and an exit code. Nothing runs on your own infrastructure, and the container is destroyed when the sandbox is deleted.

Use a shell sandbox when an agent needs to run untrusted or generated shell commands, install packages, manipulate files, or drive command-line tools without exposing your environment.

## Limitations

  - `send_command()` and `execute_code()` don't work with shell sandboxes. These methods target [Code Execution sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/code-execution-overview) and send Python payloads, which the shell container doesn't accept. Use `/exec` with shell sandboxes.

## Before you begin

Set up your project and environment.

### Set up your project

### Get the required roles

To use the sandbox, you need the following role:

  - Agent Platform User ( `roles/aiplatform.user` ) on the project.

### Install libraries

Install the SDK with the Agent Platform module:

    pip install "google-cloud-aiplatform[agent_engines]"

### Authenticate

To authenticate with Application Default Credentials:

    gcloud auth application-default login

## Create an Agent Platform instance

To use a shell sandbox, first create an Agent Platform instance. You don't need to deploy an agent to use a shell sandbox. Without deployment, creating an Agent Platform instance should take a few seconds.

    import vertexai
    
    client = vertexai.Client(project='PROJECT_ID', location='LOCATION')
    
    agent_engine = client.agent_engines.create()
    agent_engine_name = agent_engine.api_resource.name

Replace the following:

  - `PROJECT_ID` : Your Google Cloud project ID.

  - `LOCATION` : The Google Cloud region for your Agent Platform instance. See [Supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .

## Create a shell sandbox

You need to provide at least one of the following when creating a sandbox:

  - `spec` with an environment set ( `shell_environment` )
  - `config.sandbox_environment_template` (a default template is created if left unspecified. For more information, see [Reuse templates across sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates#reuse-templates) )
  - `config.sandbox_environment_snapshot`

The following example passes `shell_environment` in the sandbox spec:

    engine = (
        "projects/PROJECT_ID/locations/LOCATION"
        "/reasoningEngines/INSTANCE_ID"
    )
    
    operation = client.agent_engines.sandboxes.create(
        name=engine,
        spec={"shell_environment": {}},
        config={
            "display_name": "my-shell-sandbox",
            "wait_for_completion": True,
            "ttl": "3600s",
        },
    )
    sandbox = operation.response
    print(sandbox.name, sandbox.state)

When the sandbox is ready, it prints a response similar to the following:

    projects/.../sandboxEnvironments/1035360621853409280 SandboxState.STATE_RUNNING

A sandbox typically reaches `STATE_RUNNING` in about 20 seconds.

## Run a command

To run a shell command in the sandbox, use the helper function `execute_bash()` , which sends the command to the container:

    result = client.sandboxes.execute_bash(
        name=sandbox.name,
        command="echo hello && whoami && pwd",
    )
    print(result)

The command returns `stdout` , `stderr` , `returncode` , and `duration_ms` :

    {'stdout': 'hello\nappuser\n/workspace\n', 'stderr': '', 'returncode': 0, 'duration_ms': 8}

`execute_bash()` authenticates with your own credentials, so you don't need a service account or signed JWT.

Optional: You can explicitly set `cwd` to choose the working directory and `timeout` to cap how long the command may run. Otherwise, the sandbox uses its own defaults ( `/workspace` and the sandbox's time limit):

    result = client.sandboxes.execute_bash(
        name=sandbox.name,
        command="pytest -q",
        cwd="/workspace/app",
        timeout=120,
    )

To find out if a command fails, inspect `returncode` and `stderr` :

    result = client.sandboxes.execute_bash(
        name=sandbox.name,
        command="ls /nope",
    )
    print(result)

    {'stdout': '', 'stderr': "ls: cannot access '/nope': No such file or directory\n", 'returncode': 2, 'duration_ms': 5}

When using the container environment, consider the following:

  - Commands run as the unprivileged user `appuser` ; there is no `sudo` .
  - Each command runs in a new shell, so `cd` and shell variables don't carry over between calls. Chain them in one command, or write state to a file under `/workspace` .
  - Outbound internet access is off unless the template enables it.

## Clean up

To delete the sandbox and stop incurring charges, run the following:

    client.agent_engines.sandboxes.delete(name=sandbox.name)
    print("Sandbox deleted.")

## What's next

  - [Manage sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-sandboxes)
  - [Manage sandbox templates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates)
