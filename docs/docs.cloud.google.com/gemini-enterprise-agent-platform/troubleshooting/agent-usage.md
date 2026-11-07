---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-usage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-usage
title: Troubleshoot using an agent with Agent Runtime
description: Learn how to resolve common errors when using an agent, such as empty operation schemas, permission errors, and Reasoning Engine Execution failed errors.
data_source: docs.cloud.google.com
---

This document describes how to resolve errors that you might encounter when [using an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent) .

Note: To search and filter agent error logs, [use the Logs Explorer](https://docs.cloud.google.com/logging/docs/view/logs-explorer-interface) , select `RESOURCE TYPE` to "Vertex AI Reasoning Engine" and select the corresponding `RESOURCE CONTAINER` value (i.e. the project number) and `REASONING ENGINE ID` value.

## Operation schemas is empty

If your agent returns an empty list from `.operation_schemas()` , it might be caused by one of the following issues:

### Failure generating a schema during agent creation

**Issue** :

When you deploy your agent, you receive a warning similar to the following:

```
WARNING:vertexai.agent_engines:failed to generate schema: issubclass() arg 1 must be a class
```

**Possible cause** :

This warning might occur if you deploy an agent using the prebuilt `LangchainAgent` template on a version of `google-cloud-aiplatform` that's earlier than `1.49.0` . To check which version you're using, run the following command in the terminal:

```
pip show google-cloud-aiplatform
```

**Recommended solution** :

Run the following command in your terminal to update your `google-cloud-aiplatform` package:

```
pip install google-cloud-aiplatform --upgrade
```

After you update your `google-cloud-aiplatform` package, run the following command to verify that its version is `1.49.0` or later:

```
pip show google-cloud-aiplatform
```

If you're in a notebook instance (for example, Jupyter or Colab or Workbench), you might need to restart your runtime to use the updated package. After you've verified your version of `google-cloud-aiplatform` is `1.49.0` or later, try to [deploy your agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) again.

## `PermissionDenied` error when querying your agent

Your query might fail if you don't have the required permissions.

### Agent Platform extensions permissions

**Issue**

You might receive a `PermissionDenied` error that's similar to the following:

```
Permission 'aiplatform.extensions.get' denied on resource
'//aiplatform.googleapis.com/projects/{PROJECT_ID}/locations/{LOCATION}/extensions/
{EXTENSION}' (or it may not exist). [reason: "IAM_PERMISSION_DENIED"
domain: "aiplatform.googleapis.com"
metadata {
  key: "permission"
  value: "aiplatform.extensions.get"
}
metadata {
  key: "resource"
  value: "projects/{PROJECT_ID}/locations/{LOCATION}/extensions/{EXTENSION}"
}
]
```

Your agent doesn't have the Agent Platform extensions permissions. To use Agent Platform extensions with Agent Runtime, grant the Agent Platform User ( `roles/aiplatform.user` ) role to your agent identity service account. For more information, see [Set up the identity and permissions for your agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#identity-and-permissions) .

### LLM permissions

**Issue** :

You might receive a `PermissionDenied` error that's similar to the following:

```
PermissionDenied: 403 Permission 'aiplatform.endpoints.predict' denied on resource
'//aiplatform.googleapis.com/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/
google/models/{MODEL}' (or it may not exist). [reason: "IAM_PERMISSION_DENIED"
domain: "aiplatform.googleapis.com"
metadata {
  key: "permission"
  value: "aiplatform.endpoints.predict"
}
metadata {
  key: "resource"
  value: "projects/{PROJECT_ID}/locations/{LOCATION}/publishers/google/models/{MODEL}"
}
]
```

**Possible cause** :

Your agent identity [service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#identity-and-permissions) might not have the proper permissions to query your large language model (LLM).

**Recommended solution** :

Make sure your service account has the proper Identity and Access Management (IAM) permissions listed in the error message. An example of an IAM permission you might be missing is `aiplatform.endpoints.predict` . See [Set up the identity and permissions for your agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#identity-and-permissions) for more information.

## Request rejected before it reaches your agent

If your request fails before Agent Runtime sends it to your agent, one of the following issues might be the cause:

### Agent not found

**Issue** :

The request fails with a `404` , `NOT_FOUND` status ( `REASONING_ENGINE_NOT_FOUND` ) and a message similar to the following:

```
The Reasoning Engine `projects/PROJECT_ID/locations/LOCATION/reasoningEngines/RESOURCE_ID` was not found.
```

**Possible causes** :

- The project, location, or resource ID in the request is incorrect.
- The agent was deleted.

**Recommended solutions** :

- Compare the resource name in the error message with your deployed agents. See [List deployed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#list) .
- Make sure that your client sends the request to the project and region where you deployed the agent.

### Agent isn't active

**Issue** :

The request fails with a `403` , `PERMISSION_DENIED` status ( `REASONING_ENGINE_NOT_ACTIVE` ) and a message similar to the following:

```
The Reasoning Engine `projects/PROJECT_ID/locations/LOCATION/reasoningEngines/RESOURCE_ID` is not active, so it can't serve requests.
```

**Possible causes** :

- The agent is still being created.
- The agent failed to be created.
- The agent is being deleted.

**Recommended solutions** :

- If you just created the agent, wait for the creation to finish, and then retry the request.
- If agent creation failed, check the logs linked in the error metadata's `logs_url` field to find the cause. Fix the error and deploy the agent again. See [Troubleshoot deploying an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment) .

### Agent has no running instances

**Issue** :

The request fails with a `400` , `FAILED_PRECONDITION` status ( `REASONING_ENGINE_NO_RUNNING_INSTANCES` ) and a message similar to the following:

```
The Reasoning Engine `projects/PROJECT_ID/locations/LOCATION/reasoningEngines/RESOURCE_ID` has no running instances because no agent is deployed to it.
```

**Possible cause** :

The resource exists, but no agent (object, source files, or container image) was specified for deployment during its creation or update.

**Recommended solution** :

Update the resource with an agent to deploy. See [Update a deployed agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#update) .

### A2A methods not defined

**Issue** :

An A2A request fails with a `400` , `FAILED_PRECONDITION` status ( `REASONING_ENGINE_A2A_NOT_CONFIGURED` ) and a message similar to the following:

```
The Reasoning Engine `projects/PROJECT_ID/locations/LOCATION/reasoningEngines/RESOURCE_ID` does not define A2A methods, so it can't serve A2A requests.
```

**Possible cause** :

You sent an A2A request, such as a request for the Agent Card or a message, to an agent that wasn't built as an A2A agent.

**Recommended solutions** :

- To serve A2A requests, deploy an A2A agent. See [Create an A2A agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent) .
- To query an agent that isn't an A2A agent, see [Use an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent) .

## Reasoning Engine Execution failed

If you receive the error message "Reasoning Engine Execution failed" when querying your agent, it might be due to one of the issues that's described in this section.

### Invalid inputs to `.query()`

**Issue** :

You might receive a `FailedPrecondition` error that's similar to the following:

```
FailedPrecondition: 400 Reasoning Engine Execution failed. Error Details:
{"detail":"Invalid request: `{'query': ...}`"}
```

**Possible cause** :

This error occurs when you specify the inputs to the query as positional arguments instead of keyword arguments. For example, you call `agent.query(query_str)` instead of `agent.query(input=query_str)` .

**Recommended solution** :

When querying an instance of a reasoning engine that has been deployed, specify all inputs as keyword arguments.

### Out of Gemini model quota

**Issue** :

You might receive an error that's similar to one of the following, which indicates the error is raised from the call to Gemini:

```
FailedPrecondition: 400 Reasoning Engine Execution failed. Error Details:
{"detail":"...langchain_google_vertexai/chat_models.py...google.api_core.exceptions.ResourceExhausted: 429 Unable to submit request because the service is temporarily out of capacity. Try again later."}
```

or, a different error message:

```
FailedPrecondition: 400 Reasoning Engine Execution failed. Error Details:
{"detail":"...langchain_google_vertexai/chat_models.py...google.api_core.exceptions.InternalServerError: 500 Internal error occurred."}
```

**Possible cause** :

This might happen if you have sent too many requests recently and you have used up the Gemini model quota.

**Recommended solution** :

Follow [Gemini model quota management process](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-quotas) to increase quota. Alternatively, rate limit your tests and try again later.

### Incorrect Reasoning Engine ID

**Issue** :

You might receive an error that Reasoning Engine Execution failed with a detail of `Not Found` .

**Possible cause** :

This error can occur if you use an incorrect Reasoning Engine ID when you query your agent.

**Recommended solution** :

Verify that you are using the correct Reasoning Engine ID for your agent.

## Support resources

If your problem is still not resolved, refer to our [support guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-support) to get help.
