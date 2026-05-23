---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance
title: Create a Agent Platform Workbench instance with third party credentials
description: Learn how to create a Agent Platform Workbench instance with third party crentials
data_source: docs.cloud.google.com
---

# Create an instance with third party credentials

This page describes how to create a Gemini Enterprise Agent Platform Workbench instance with third party credentials.

## Overview

You can create and manage Gemini Enterprise Agent Platform Workbench instances with third party credentials provided by Workforce Identity Federation. Workforce Identity Federation uses your external identity provider (IdP) to grant a group of users access to Agent Platform Workbench instances through a proxy.

Access to a Agent Platform Workbench instance is granted by assigning a [workforce pool principal](https://docs.cloud.google.com/iam/docs/workforce-identity-federation#representing-workforce-users) to the Agent Platform Workbench instance's service account.

## Before you begin

1.  Configure your IdP with a [workforce identity pool](https://docs.cloud.google.com/iam/docs/workforce-identity-federation#workforce-identity-pools) .

### Required role for creating an instance

To ensure that your workforce pool principal has the necessary permissions to create a Agent Platform Workbench instance, ask your administrator to grant the [Notebooks Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.admin) ( `roles/notebooks.admin` ) IAM role to your workforce pool principal on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give your workforce pool principal the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Required roles for using third party credentials

Your workforce pool principal needs access to your Agent Platform Workbench instance's service account, with specific permissions.

To ensure that the workforce pool principal has the necessary permissions to use a Agent Platform Workbench instance with third party credentials, ask your administrator to grant the following IAM roles to the workforce pool principal on the service account that you'll specify when you create your instance:

  - [Service Account Token Creator](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountTokenCreator) ( `roles/iam.serviceAccountTokenCreator` )
  - [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `roles/iam.serviceAccountUser` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give the workforce pool principal the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create the instance using third party credentials

To ensure that your Agent Platform Workbench instance contains a `byoid.googleusercontent.com` domain, you must do one of the following:

  - Create the instance by using the Google Cloud Workforce Identity Federation console.

  - Use the `enable_third_party_identity` flag when you create your instance.

You can create a Gemini Enterprise Agent Platform Workbench using third party credentials by using the Google Cloud console or the gcloud CLI:

### Console

1.  Sign in to the Google Cloud console using a workforce pool provider.

2.  In the Google Cloud console, go to the **Instances** page.

3.  Click add\_box **Create new** .

4.  In the **New instance** dialog, click **Advanced options** .

5.  In the **Create instance** dialog, in the **IAM and security** section, do the following:
    
    1.  Make sure **Service account** is selected.
    
    2.  Clear **Use default Compute Engine service account** , and then, in the **Service account email** field, enter the service account email address that is associated with your workforce principal.

6.  Click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

### gcloud

Follow the [IAM guide](https://docs.cloud.google.com/iam/docs/workforce-obtaining-short-lived-credentials) for authenticating the gcloud CLI with a workforce identity pool.

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance; must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where you want your instance to be located
  - `  VM_IMAGE_PROJECT  ` : the ID of the Google Cloud project that VM image belongs to, in the format: ` projects/ IMAGE_PROJECT_ID  `
  - `  VM_IMAGE_NAME  ` : the full image name; to find the image name of a specific version, see [Find the specific version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version#find_the_specific_version_that_you_want)
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM
  - `  METADATA  ` : custom metadata to apply to this instance; for example, to specify a post-startup-script, you can use the `post-startup-script` metadata tag, in the format: `"--metadata=post-startup-script=gs:// BUCKET_NAME /hello.sh"`
  - `  SERVICE_ACCOUNT_EMAIL  ` : the service account email address that is associated with your workforce principal

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --vm-image-project=VM_IMAGE_PROJECT \
        --vm-image-name=VM_IMAGE_NAME \
        --machine-type=MACHINE_TYPE \
        --metadata=METADATA \
        --service-account-email=SERVICE_ACCOUNT_EMAIL \
        --enable-third-party-identity 

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --vm-image-project=VM_IMAGE_PROJECT `
        --vm-image-name=VM_IMAGE_NAME `
        --machine-type=MACHINE_TYPE `
        --metadata=METADATA `
        --service-account-email=SERVICE_ACCOUNT_EMAIL `
        --enable-third-party-identity 

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --vm-image-project=VM_IMAGE_PROJECT ^
        --vm-image-name=VM_IMAGE_NAME ^
        --machine-type=MACHINE_TYPE ^
        --metadata=METADATA ^
        --service-account-email=SERVICE_ACCOUNT_EMAIL ^
        --enable-third-party-identity 

For more information about the command for creating an instance from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/create) .

Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

## Access Jupyterlab with third party credentials

Your new Gemini Enterprise Agent Platform Workbench instance creates two separate proxy URLs with the following domains:

  - `byoid.googleusercontent.com` : This domain can only be used by users authenticating with a workforce identity pool. Its value is stored in your instance's metadata field `proxy-byoid-url` . This metadata value activates an **Open JupyterLab** link in the [Google Cloud Workforce Identity Federation console](https://docs.cloud.google.com/iam/docs/workforce-console-learn-more) ( `console.cloud.google/` ).

  - `googleusercontent.com` : This domain can only be used by users authenticating with the default Google's First Party Authentication. Its value is stored in your instance's metadata field `proxy-url` . This metadata value activates an **Open JupyterLab** link in the Google Cloud console ( `console.cloud.google.com` ).

## What's next

  - To learn more about third party principals to use for provisioning notebooks, see [Workforce Identity Federation](https://docs.cloud.google.com/iam/docs/workforce-identity-federation#what_is_workforce_identity_federation) .
