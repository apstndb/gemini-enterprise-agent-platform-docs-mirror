---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment
title: Troubleshoot deploying an agent
description: Learn how to resolve common errors when deploying an agent, such as serialization errors, permission issues, and VPC-SC violations.
data_source: docs.cloud.google.com
---

This document describes how to resolve errors that you might encounter when [deploying an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) to Agent Runtime. It covers a variety of common issues, including serialization failures, permission errors, and VPC-SC boundary violations.

> **Note:** To search and filter agent error logs, [use the Logs Explorer](https://docs.cloud.google.com/logging/docs/view/logs-explorer-interface) , select `RESOURCE TYPE` to "Gemini Enterprise Agent Platform Reasoning Engine" and select the corresponding `RESOURCE CONTAINER` value (i.e. the project number) and `REASONING ENGINE ID` value.

## Prebuilt Template errors

If you run into issues with the [LangchainAgent template](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.preview.reasoning_engines.LangchainAgent) during deployment, it might be due to one of the issues in this section.

### Internal server errors

**Issue** :

You receive an error message similar to the following:

    InternalServerError: 500 Revision YYY is not ready and cannot serve traffic.

Unfortunately, this is a catch-all error for any issues with the container at runtime, and the possible cause is one of many errors that might be happening.

**Possible cause(s)** :

  - **Dirty state on `LangchainAgent`** . This might happen if [`.set_up()`](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.preview.reasoning_engines.LangchainAgent#vertexai_preview_reasoning_engines_LangchainAgent_set_up) was called on a `LangchainAgent` before [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .
  - **Inconsistent package versions** . This might happen if the packages installed in the development environment are different from the packages installed in the remote environment in Agent Runtime.

**Recommended solution(s)** :

  - **Dirty state on `LangchainAgent`** . Instantiate a fresh instance of the `LangchainAgent` or remove `agent.set_up()` from the code before [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .
  - **Inconsistent package specs** . See the section on troubleshooting [serialization errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-deployment#serialization-internal-server-errors) .

## Serialization errors

In general, it is important to ensure that the "local" and "remote" environments are in sync when deploying the agent. You can ensure this by specifying [`requirements=`](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.preview.reasoning_engines.ReasoningEngine#vertexai_preview_reasoning_engines_ReasoningEngine_create) when [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .

If you run into issues with serialization (errors related to "pickle" or "pickling" are synonymous with "serialization" errors), it might be due to one of the issues that's described in this section.

### Pydantic version

**Issue** :

You receive an error message similar to the following:

    PicklingError: Can't pickle <cyfunction str_validator at 0x7ca030133d30>: it's
    not the same object as pydantic.validators.str_validator

**Possible cause** :

This might happen if your `pydantic` package is earlier than version `2.6.4` . To check which version you're using, run the following command in your terminal:

    pip show pydantic

**Recommended solution** :

Update your package by running the following command in the terminal:

    pip install pydantic --upgrade

Run the following command in your terminal to verify you're using version `2.6.4` or later:

    pip show pydantic

If you're in a notebook instance (for example, a Jupyter, Colab, or Workbench), you might need to restart your runtime to use the updated packages.

### Cloudpickle version

**Issue** :

You receive an error message similar to the following:

    AttributeError: Can't get attribute '_class_setstate' on <module 'cloudpickle.cloudpickle'
    from '/usr/local/lib/python3.10/site-packages/cloudpickle/cloudpickle.py'>

**Possible cause** :

This might happen if the version of your `cloudpickle` package is different in your development environment and your deployment environment. To check which version you're using in development, run the following command in your terminal:

    pip show cloudpickle

**Recommended solution** :

Deploy the same version of cloudpickle in both environments, such as your local development environment and the remotely deployed agent by specifying `requirements=` when [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .

### Internal server errors

**Issue** :

You receive an error message similar to the following:

    InternalServerError: 500 Revision YYY is not ready and cannot serve traffic.

**Possible cause** :

This might happen if [`sys_version=`](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.preview.reasoning_engines.ReasoningEngine#vertexai_preview_reasoning_engines_ReasoningEngine_create) is different from the development environment when [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .

**Recommended solution** :

After [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) , consider removing `sys_version=` from the input arguments. If you still run into issues, [file a bug report](https://github.com/googleapis/python-aiplatform/issues/new?template=bug_report.md) .

## Cloud Storage bucket errors

If you're running into issues with the Cloud Storage staging bucket that's used at deployment time to collect and upload your agent, it might be due to one of the following issues:

### Permission errors

**Recommended solution** :

If you want to use a pre-existing bucket: make sure the principal that's authenticated to use Agent Platform (either yourself or a service account) has `Storage Admin` access to the bucket, and grant permissions to the [service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#identity-and-permissions) .

Alternatively, you can specify a new bucket when [deploying the agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) and the SDK will create the bucket with the necessary permissions.

If you still run into issues, [file a bug report](https://github.com/googleapis/python-aiplatform/issues/new?template=bug_report.md) .

### Cloud Storage bucket subdirectory isn't created

**Issue** :

You receive an error message similar to the following:

    NotFound: 404 Can not copy from \"gs://[LOCATION]-*/agent_engine/agent_engine.pkl\" to \"gs://*/code.pkl\", check if the source object and target bucket exist.

(The 404 occurs when the system tries to copy into a folder that doesn't exist.)

**Possible cause** :

This is likely due to an issue with string interpolation in versions of `google-cloud-aiplatform` earlier than version `1.49.0` . This is [fixed](https://github.com/googleapis/python-aiplatform/commit/3d22a18abdacc7cb53d4b5fef941fa1a34caec08) in later versions. To check which version of `google-cloud-aiplatform` you're using, run the following command in your terminal:

    pip show google-cloud-aiplatform

**Recommended solution** :

Update your package by running the following command in the terminal:

    pip install google-cloud-aiplatform --upgrade

Verify that you're using version `1.49.0` or later of `google-cloud-aiplatform` by running the following command in your terminal:

    pip show google-cloud-aiplatform

If you're using a notebook instance (for example, Jupyter or Colab or Workbench), you might need to restart your runtime before you can use the updated packages.

## VPC-SC violation errors

If you're experiencing problems with VPC-SC, one of the following issues might be the cause:

### Permission errors

**Issue** :

You receive an error message similar to the following:

    Reasoning Engine instance REASONING_ENGINE_ID failed to start and cannot serve traffic.

or:

    Request is prohibited by organization's policy.

**Possible cause** :

This is likely caused by missing required ingress rules in the VPC-SC perimeter.

**Recommended solution** :

If you use Agent Platform in a VPC-SC environment, you must create an ingress rule in your perimeter to allow ingress from the Reasoning Engine Service Agent ( `service- PROJECT_NUMBER @gcp-sa-aiplatform-re.iam.gserviceaccount.com` ) into the `storage.googleapis.com` service and `artifactregistry.googleapis.com` service.

## Custom service account errors

If you're experiencing problems with service accounts, one of the following issues might be the cause:

### Act as service account

**Issue** :

You receive an error message similar to the following:

    You do not have permission to act as service_account.

**Possible cause** :

You may not have the `iam.serviceAccounts.actAs` permission on the custom service account used for deployment. Note that in a multi-agent system where there are multiple custom service accounts, one agent author or deployer can act as some of the service accounts. If you are using the wrong service account, this error is the expected behavior

In addition, you may encounter this error if the custom service account is located in a project different from the one where you deploy the agent, and the `iam.disableCrossProjectServiceAccountUsage` organization policy is **enforced** in the service account project.

See [Cross-project custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#cross-project-custom-service-account) for the full list of required configurations for this scenario.

**Recommended solution** :

Make sure you are using the intended service account. Check if you have the *Service Account User* ( `roles/iam.serviceAccountUser` ) role on this service account. If not, ask your administrator to grant you the role on this service account.

If you are in the cross-project scenario, check if your service account project has `iam.disableCrossProjectServiceAccountUsage` organization policy enforced. If so, ask your administrator to disable the policy.

### Metadata server unavailable

**Issue** :

You receive an error message similar to the following:

    ServiceUnavailable: 503 Getting metadata from plugin failed with error

or

    Compute Engine Metadata server unavailable due to : Could not fetch URI /computeMetadata/v1/instance/service-accounts/default/token

**Possible cause** :

This can happen if the custom service account and your agent are in different projects and the [AI Platform Reasoning Engine Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#service-agent) does not have the `iam.serviceAccounts.getAccessToken` permission on the custom service account.

See [Cross-project custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup#cross-project-custom-service-account) for the full list of required configurations for this scenario.

**Recommended solution** :

Ask your administrator to grant the AI Platform Reasoning Engine Service Agent of the agent project the *Service Account Token Creator* ( `roles/iam.serviceAccountTokenCreator` ) role on the custom service account.

The AI Platform Reasoning Engine Service Agent should be located in the same project you use to deploy your agent. The IAM binding of the role grant should be in the project where the custom service account resides.

## Resource exhausted or rate limit errors (Error 429)

**Issue** :

Deployment fails with an `Error 429` or `RESOURCE_EXHAUSTED` status.

**Possible cause** :

The project has exceeded its API rate limits or concurrent request quotas.

**Recommended solutions** :

  - Implement an exponential backoff and retry strategy in deployment scripts.
  - Verify current usage against limits in the Google Cloud Quotas page for the "Agent Platform API".
  - Reduce the frequency of concurrent deployments.

## Support resources

If your problem is still not resolved, refer to our [support guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-support) to get help.
