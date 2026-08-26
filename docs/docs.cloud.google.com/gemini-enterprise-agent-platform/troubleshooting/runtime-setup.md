---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/runtime-setup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/runtime-setup
title: Troubleshoot environment setup for Agent Runtime
description: Learn how to resolve common errors, such as package import errors, when setting up your environment for the agent platform runtime.
data_source: docs.cloud.google.com
---

This document describes how to resolve errors that you might encounter when [setting up an environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup) for Agent Runtime. It covers troubleshooting steps for package import problems.

## Errors when importing the Agent Platform SDK

If you can't import the Agent Platform SDK for Python, it might be caused by one of the following issues:

### Outdated version of the Agent Platform SDK for Python

**Issue** :

You receive an error message similar to the following:

    ImportError: cannot import name 'reasoning_engines' from 'vertexai.preview'

or

    ImportError: cannot import name 'agent_angines' from 'vertexai'

**Possible cause** :

This might happen if the version of your `google-cloud-aiplatform` package is earlier than `1.82.0` (for `agent_engines` ) or `1.47.0` (for `reasoning_engines` ). To check the version of your `google-cloud-aiplatform` package, run the following command in the terminal:

    pip show google-cloud-aiplatform

**Recommended solution** :

Run the following command in your terminal to update your `google-cloud-aiplatform` package:

    pip install google-cloud-aiplatform --upgrade

Verify your updated version is `1.82.0` or later by running the following command:

    pip show google-cloud-aiplatform

If you're in a notebook instance (For example, Jupyter or Colab or Workbench), you might need to restart your runtime to use the updated packages.

## 401 Authorization Errors

**Issue** :

You receive an error message similar to the following:

    Error Code: "401"
    Error Details: "Context-Aware Access requirements are not met"

OR

    Agent Engine Error: An error occurred during invocation. Exception: API request failed with status 401:
    Request had invalid authentication credentials. Expected OAuth 2 access token, login cookie or other valid authentication credential.

**Possible cause** :

By default, when you use Agent Identity with Agent Runtime, certificate bound access tokens are used for authentication to prevent token theft. A 401 error can occur at runtime in one of the following two scenarios:

1.  User or Agent attempting to use an access token outside of the context in which it was issued, such as passing the token between agents.
2.  Agent calling a non-mTLS compatible API endpoint, such as telemetry.googleapis.com instead of telemetry.mtls.googleapis.com.

**Recommended solution** :

For scenario \#1, if you have a legitimate reason to share tokens between agents, you can opt out of the default Context-Aware Access (CAA) policy. This action is strongly discouraged, as it leaves an agent vulnerable to credential theft.

Opt out of the default CAA policy by setting the following environment variable when you create your Agent Runtime instance:

    config={
      "env_vars": {
        "GOOGLE_API_PREVENT_AGENT_TOKEN_SHARING_FOR_GCP_SERVICES": False,
      }
    }

For scenario \#2, you can similarly set the `GOOGLE_API_PREVENT_AGENT_TOKEN_SHARING_FOR_GCP_SERVICES` variable to `False` to allow agents to use the non-mTLS API endpoints as a temporary workaround. In this case, the underlying issue could be a known issue with ADK.
