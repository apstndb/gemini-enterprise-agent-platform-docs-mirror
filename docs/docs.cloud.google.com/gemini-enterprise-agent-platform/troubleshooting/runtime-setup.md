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
