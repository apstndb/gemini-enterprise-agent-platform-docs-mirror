---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-runtime
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-runtime
title: Create a runtime in Colab Enterprise
description: Learn how to create a runtime in Colab Enterprise
data_source: docs.cloud.google.com
---

This page shows you how to create, start, and delete a runtime in Colab Enterprise.

You can create a runtime to run code on a runtime that has a different configuration than the default. Runtimes are created based on a runtime template, which includes specifications like machine type and disk size.

To learn more about runtimes, see [Runtimes and runtime templates](https://docs.cloud.google.com/colab/docs/runtimes) .

## Before you begin

### Required roles

To get the permissions that you need to create a runtime in Colab Enterprise, ask your administrator to grant you the Colab Enterprise Admin ( [`roles/aiplatform.colabEnterpriseAdmin`](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#aiplatform.colabEnterpriseAdmin) ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

> One or more of the required roles includes the `dataform.repositories.list` permission. Users who are granted the `dataform.repositories.list` permission or the [Code Creator ( `roles/dataform.codeCreator` )](https://docs.cloud.google.com/dataform/docs/access-control#dataform.codeCreator) role in a project can list the names of code assets in that project by using the Dataform API or the Dataform command-line interface (CLI). Non-administrators using BigQuery Studio can only see code assets that they created or that were shared with them.

## Create a runtime

To create a runtime, you can use the Google Cloud console or the Google Cloud CLI.

### Console

To create a runtime:

1.  In the Google Cloud console, go to the Colab Enterprise **Runtimes** page.

2.  In the **Region** menu, select the region where you want your runtime. It must be in the same region as the notebook that uses it.

3.  Click add\_box **Create** .
    
    The **Create Vertex AI runtime** dialog appears.

4.  In the **Runtime template** menu, select a runtime template. If there aren't any runtime templates listed, [create a runtime template](https://docs.cloud.google.com/colab/docs/create-runtime-template) .

5.  In the **Runtime name** field, enter a name for your runtime.

6.  Click **Create** .

By default, when you create a runtime, you automatically have the required permissions to start and delete that runtime.

### gcloud

Before using any of the command data below, make the following replacements:

  - `  DISPLAY_NAME  ` : the display name for your runtime.
  - `  RUNTIME_TEMPLATE_ID  ` : the ID of the runtime template. The runtime template specifies your runtime's compute configuration.
  - `  PROJECT_ID  ` : your project ID.
  - `  REGION  ` : the region where you want your runtime.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes create --display-name="DISPLAY_NAME" \
        --runtime-template=RUNTIME_TEMPLATE_ID \
        --project=PROJECT_ID \
        --region=REGION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes create --display-name="DISPLAY_NAME" `
        --runtime-template=RUNTIME_TEMPLATE_ID `
        --project=PROJECT_ID `
        --region=REGION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes create --display-name="DISPLAY_NAME" ^
        --runtime-template=RUNTIME_TEMPLATE_ID ^
        --project=PROJECT_ID ^
        --region=REGION

By default, when you create a runtime, you automatically have the required permissions to start and delete that runtime.

For more information about the command for creating a runtime template from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/colab/runtimes/create) .

## Start a runtime

To start a runtime, you can use the Google Cloud console or the gcloud CLI.

### Console

To start a runtime:

1.  In the Google Cloud console, go to the Colab Enterprise **Runtimes** page.

2.  In the **Region** menu, select the region that contains your runtime.

3.  Select the runtime that you want to start.

4.  Click **Start** .

### gcloud

Before using any of the command data below, make the following replacements:

  - `  RUNTIME_ID  ` : the ID of your runtime.
  - `  PROJECT_ID  ` : your project ID.
  - `  REGION  ` : the region where your runtime is located.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes start RUNTIME_ID \
        --project=PROJECT_ID \
        --region=REGION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes start RUNTIME_ID `
        --project=PROJECT_ID `
        --region=REGION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes start RUNTIME_ID ^
        --project=PROJECT_ID ^
        --region=REGION

For more information about the command for creating a runtime template from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/colab/runtime-templates/create) .

## Delete a runtime

To delete a runtime, you can use the Google Cloud console or the gcloud CLI.

### Console

To delete a runtime:

1.  In the Google Cloud console, go to the Colab Enterprise **Runtimes** page.

2.  In the **Region** menu, select the region that contains your runtime.

3.  Select the runtime that you want to delete.

4.  Click delete **Delete** .

5.  Click **Confirm** .

### gcloud

Before using any of the command data below, make the following replacements:

  - `  RUNTIME_ID  ` : the ID of your runtime.
  - `  PROJECT_ID  ` : your project ID.
  - `  REGION  ` : the region where your runtime is located.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes delete RUNTIME_ID \
        --project=PROJECT_ID \
        --region=REGION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes delete RUNTIME_ID `
        --project=PROJECT_ID `
        --region=REGION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtimes delete RUNTIME_ID ^
        --project=PROJECT_ID ^
        --region=REGION

For more information about the command for creating a runtime template from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/colab/runtimes/delete) .

## Troubleshoot

This section shows you how to resolve issues with creating runtimes in Colab Enterprise.

### Unable to create a runtime

This issue occurs when you're unable to create a runtime. See also [Unable to create a default runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-runtime#unable-to-create-default-runtime-no-template-create-permission) . The most common causes are:

#### Insufficient quota

If you are unable to create a runtime, you might have exceeded your Compute Engine runtime quota.

Colab Enterprise uses Compute Engine quota for runtimes. For more information, see the [Compute Engine quota and limits overview](https://docs.cloud.google.com/compute/quotas-limits) .

To resolve this issue, [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase) .

#### Unavailable resources

The following error occurs when you try to create a runtime.

    No available zone found for runtime RUNTIME_ID
    for machine type MACHINE_TYPE
    with accelerator type: ACCELERATOR. Please try again later.

This error occurs if there are no resources available for your machine type configuration within your notebook's region.

To resolve this issue, try any of the following:

  - Create a runtime in a different region.
  - Create a runtime template with a different machine type configuration, and then create a runtime based on the new runtime template.

#### Default runtime already exists

The following error occurs when you try to create a runtime from the default runtime template when the default runtime already exists.

    Failed to create runtime
    
    One click runtime already exists.

If you try to create a runtime from a default runtime template, Colab Enterprise tries to create a default runtime. There can only be one default runtime per user, project, and region. If the default runtime already exists, Colab Enterprise is unable to create another default runtime.

To resolve this issue, connect to the existing default runtime or create a runtime from a non-default runtime template.

### Unable to create a default runtime

When Colab Enterprise creates a default runtime, it first creates a default runtime template that it uses to generate the default runtime. If you try to create a default runtime without the permissions required to create a runtime template, then Colab Enterprise can't create the default runtime.

To resolve this issue, ask your administrator to grant you a role that includes the `aiplatform.notebookRuntimeTemplates.create` permission.

## What's next

  - Learn more about [runtimes and runtime templates](https://docs.cloud.google.com/colab/docs/runtimes) .
  - [Connect to your runtime](https://docs.cloud.google.com/colab/docs/connect-to-runtime) .
  - Learn how to [create a runtime template](https://docs.cloud.google.com/colab/docs/create-runtime-template) .
