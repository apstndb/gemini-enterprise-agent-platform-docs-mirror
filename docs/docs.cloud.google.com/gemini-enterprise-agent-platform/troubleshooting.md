---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting
title: Troubleshoot Gemini Enterprise Agent Platform
description: 'Start here to troubleshoot Gemini Enterprise Agent Platform: diagnose an error, look up a status code in the error catalog, find the right guide, and get support.'
data_source: docs.cloud.google.com
---

This page is the starting point for troubleshooting Gemini Enterprise Agent Platform. Use it to [diagnose an error](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#diagnose) , [look up a specific error](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#error-catalog) , [find the guide for your task](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#guides) , or [get support](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#get-support) .

## Diagnose an error

Before you look for a specific fix, collect the following information:

### Read the error

Note the status code, such as `400` or `429` , and the exact message text. You can look up both in the [error catalog](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#error-catalog) .

You can also identify the specific failure from a machine-readable reason, documentation link, or prefiltered log view if those are present in the error message.

### Find the logs

To search and filter agent error logs, [use the Logs Explorer](https://docs.cloud.google.com/logging/docs/view/logs-explorer-interface) , set **Resource type** to **Vertex AI Reasoning Engine** , and select the corresponding **Resource container** value (your project number) and **Reasoning engine ID** value.

### Check quotas and service health

Errors that appear intermittently, or that started without a change on your side, are often caused by quota or by an ongoing incident:

  - Compare your usage against [Quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-quotas) .
  - Check [Google Cloud Service Health](https://status.cloud.google.com/) for an ongoing incident in your region.

## Error catalog

Find the error you received in the following table. If your error isn't listed, use the [troubleshooting guides](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#guides) for the task you were trying to complete.

| Status code or message                                                                                                                   | Resolution                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ImportError: cannot import name 'reasoning_engines'` , `ImportError: cannot import name 'agent_engines'`                                | [Outdated version of the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/runtime-setup#outdated-vertex-sdk-errors)        |
| `401` `Context-Aware Access requirements are not met` , `401` `Request had invalid authentication credentials`                           | [401 authorization errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/runtime-setup#401-errors)                                                     |
| `ValueError: Cannot get the Candidate text`                                                                                              | [Content generation errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-creation#content-generation-errors)                                    |
| `failed to start and cannot serve traffic` , on your first custom container (BYOC) deployment in a region                                | [BYOC first-time creation error](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-creation#byoc-first-creation-error)                               |
| `failed to start and cannot serve traffic` or `Request is prohibited by organization's policy` , inside a VPC Service Controls perimeter | [VPC-SC violation errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#vpc-sc-violation-errors)                                      |
| `429` , `RESOURCE_EXHAUSTED`                                                                                                             | [Resource exhausted or rate limit errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#error-429)                                    |
| `500` internal server error from a prebuilt template                                                                                     | [Prebuilt template errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#prebuilt-template-errors)                                    |
| `cloudpickle` or `pydantic` version conflicts when serializing your agent                                                                | [Serialization errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#serialization-errors)                                            |
| `NotFound: 404 Can not copy from "gs://..."`                                                                                             | [Cloud Storage bucket subdirectory isn't created](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#storage-bucket-subdirectory-errors)   |
| `iam.serviceAccounts.actAs` denied, metadata server unavailable                                                                          | [Custom service account errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#custom-service-account-errors)                          |
| `InvalidArgument: 400 Provided filter is not valid`                                                                                      | [Error when filtering the list of agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/managing-deployed-agents#filter-agents-errors)                 |
| `google.api_core.exceptions.Unknown: None` , `Failed to convert project number to project ID` , during startup                           | [Errors during Agent Runtime startup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway#bootstrap-errors)                       |
| `403 Forbidden` on an outbound request                                                                                                   | [403 Forbidden errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway#confirm-egress-error)                                  |
| Certificate verification failures reaching a self-signed or private CA destination                                                       | [Self-signed or private CA destinations fail to connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway#self-signed-ca-fail) |
| TLS handshake failures from a custom container (BYOC) agent                                                                              | [Agent deployed with custom container (BYOC) fails to connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway#byoc-ca-fail)  |
| Sandbox creation failures                                                                                                                | [Sandbox creation issues](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/code-execution#sandbox-creation-issues)                                        |
| Code execution times out, file I/O failures in a sandbox                                                                                 | [Code execution issues](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/code-execution#code-execution-issues)                                            |
| `RuntimeError: Failed to generate memory` , or no memories returned after a session                                                      | [No memories were generated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/memory-bank#no-memories-generated)                                          |

> **Note:** If your error isn't listed in the table, use the [troubleshooting guides](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#guides) , and report the error through [Get support](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#get-support) .

## Troubleshooting guides

If you don't have a specific error message, or your error isn't in the [error catalog](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting#error-catalog) , see the following table for the corresponding guide for your task:

| Task                                                              | Guide                                                                                                                                        |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Installing the Agent Platform SDK and setting up your environment | [Agent Runtime environment setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/runtime-setup)              |
| Creating an agent                                                 | [Create an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-creation)                             |
| Deploying an agent to Agent Runtime                               | [Agent deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment)                          |
| Calling an external service from an agent                         | [Agent Gateway connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway)      |
| Listing, updating, or deleting a deployed agent                   | [Manage deployed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/managing-deployed-agents)            |
| Running code in a sandbox                                         | [Code Execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/code-execution)                              |
| Generating or retrieving memories                                 | [Agent Platform Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/memory-bank)                     |
| Serving a model or hitting a model quota                          | [Troubleshooting machine learning services](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/troubleshooting) |

## Get support

If the guides on this page don't resolve your issue, see [Getting help for agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-support) for support packages, community forums, and bug reporting. For billing questions, see [Billing questions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/billing-questions) .

If you [file a bug](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-support#file_bugs_or_feature_requests) , provide the following information:

  - Status code
  - Error message
  - (Optional) Feedback if the error message is wrong, misleading, or not actionable.
