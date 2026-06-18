---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment
title: Set up a project and a development environment
description: Create a {{dynamic_data.site_values.cloud_name}} project and enable the Agent Platform APIs.
data_source: docs.cloud.google.com
---

To get you started using Gemini Enterprise Agent Platform, this page guides you through how to create a Google Cloud project and enable the Agent Platform APIs. If you don't have the permissions to perform these tasks, [ask an administrator](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment#ask_admin) to setup a project and enable Gemini Enterprise Agent Platform for you. Also covered in this page is how to set up the Google Cloud CLI in your local development environment.

## Set up a project

Follow these steps to set up a project:

> **Note:** If you're an administrator setting up a project for a team, see [Set up a project for a team](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/set-up-project) .

## Set up authentication

Select the tabs for how you plan to access the API:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### gcloud

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  To [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the gcloud CLI, run the following command:
    
        gcloud init

4.  After initializing the gcloud CLI, update it and install the required components:
    
        gcloud components update
        gcloud components install beta

To set up the gcloud CLI to use service account impersonation to authenticate to Google APIs, rather than your user credentials, run the following command:

    gcloud config set auth/impersonate_service_account SERVICE_ACCT_EMAIL

For more information, see [Service account impersonation](https://docs.cloud.google.com/docs/authentication/use-service-account-impersonation) .

### Client libraries

To use client libraries in a local development environment, install and initialize the gcloud CLI, and then set up Application Default Credentials with your user credentials.

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  After initializing the gcloud CLI, update it and install the required components:
    
        gcloud components update
        gcloud components install beta

4.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) in the Google Cloud authentication documentation.

To set up your local ADC file to use service account impersonation to authenticate to Google APIs, rather than your user credentials, run the following command:

    gcloud auth application-default login --impersonate-service-account=SERVICE_ACCT_EMAIL

For more information, see [Service account impersonation](https://docs.cloud.google.com/docs/authentication/use-service-account-impersonation) .

### REST

To use the REST API in a local development environment, you use the credentials you provide to the gcloud CLI.

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  After initializing the gcloud CLI, update it and install the required components:
    
        gcloud components update
        gcloud components install beta

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

You can use service account impersonation to generate an access token for REST API requests. For more information, see [Impersonated service account](https://docs.cloud.google.com/docs/authentication/rest#impersonated-sa) .

For information about setting up authentication for a production environment, see [Set up Application Default Credentials for code running on Google Cloud](https://docs.cloud.google.com/docs/authentication/set-up-adc-attached-service-account) in the Google Cloud authentication documentation.

## Ask an administrator to set up a Gemini Enterprise Agent Platform project for you

This section describes how an administrator grants the roles needed to use Gemini Enterprise Agent Platform.

1.  Determine a meaningful project name and project ID to identify your project. If you are part of an organization or plan to create multiple projects, consider what naming conventions and [folder](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy#folders) hierarchies are followed, or could be followed, to make project organization clear.
2.  Required roles:
    1.  Access to most Gemini Enterprise Agent Platform capabilities is granted by the [Gemini Enterprise Agent Platform User](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.user) `(roles/aiplatform.user)` IAM role and should suffice for most Gemini Enterprise Agent Platform users. For full control of Gemini Enterprise Agent Platform resources, you can request the [Gemini Enterprise Agent Platform Administrator](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.admin) `(roles/aiplatform.admin)` role. To explore the differences between these and other Gemini Enterprise Agent Platform roles, see [Gemini Enterprise Agent Platform access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .
    2.  If you also intend to use [Gemini Enterprise Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) in Google Cloud, ask your administrator to grant you the [Notebooks Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.admin) `(roles/notebooks.admin)` IAM role for the project, as well as the [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser) `(roles/iam.serviceAccountUser)` IAM role on either the project or the [Compute Engine default service account](https://docs.cloud.google.com/compute/docs/access/service-accounts#default_service_account) .
    3.  Additionally, to enable the necessary APIs, you either need the [Service Usage Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/serviceusage#serviceusage.serviceUsageAdmin) `(roles/serviceusage.serviceUsageAdmin)` IAM role or your administrator needs to enable the APIs for you by following the first few steps.
3.  Ask your administrator to enable Agent Platform APIs for you. If you're granted the [Service Usage Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/serviceusage#serviceusage.serviceUsageAdmin) `(roles/serviceusage.serviceUsageAdmin)` IAM role, then you'll be able to do this on your own.

> **Note:** Certain tasks in Agent Platform require that you use additional Google Cloud products besides Agent Platform. For example, in most cases, you must use Cloud Storage and Artifact Registry when you create a custom training pipeline. You might need to perform additional setup tasks to use other Google Cloud products.

## What's next

  - Read an [overview of Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-unified-platform) .

  - Walk through one of the [tutorials for using Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/tutorials) .

  - Learn how to [use the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) , which provides another way to interact with Agent Platform.
