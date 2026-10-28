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

### Vertex AI extensions permissions

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

Your agent doesn't have the Vertex AI extensions permissions. To use Vertex AI extensions with Agent Runtime, grant the Vertex AI User ( `roles/aiplatform.user` ) role to your agent identity service account. For more information, see [Set up the identity and permissions for your agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#identity-and-permissions) .

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
