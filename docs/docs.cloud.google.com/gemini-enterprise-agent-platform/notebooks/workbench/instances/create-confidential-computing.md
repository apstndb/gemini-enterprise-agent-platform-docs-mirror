---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-confidential-computing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-confidential-computing
title: Create an instance with Confidential Computing
description: Create a Agent Platform Workbench instance that encrypts data-in-use by using Confidential Computing
data_source: docs.cloud.google.com
---

# Create an instance with Confidential Computing

This document describes how to create a Gemini Enterprise Agent Platform Workbench instance with Confidential Computing enabled.

## Overview

Confidential Computing is the protection of data in-use with hardware-based Trusted Execution Environment (TEE). TEEs are secure and isolated environments that prevent unauthorized access or modification of applications and data while they are in use. This security standard is defined by the [Confidential Computing Consortium](https://confidentialcomputing.io/) .

When you create a Agent Platform Workbench instance with Confidential Computing enabled, your new Agent Platform Workbench instance is a Confidential VM instance. To learn more about Confidential VM instances, see the [Confidential VM overview](https://docs.cloud.google.com/confidential-computing/confidential-vm/docs/confidential-vm-overview) .

## Before you begin

### Required roles

To get the permissions that you need to create a Agent Platform Workbench instance, ask your administrator to grant you the [Notebooks Runner](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.runner) ( `roles/notebooks.runner` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an instance

You can create an instance with Confidential Computing enabled by using the Google Cloud console, the gcloud CLI, or the REST API:

### Console

To create a Agent Platform Workbench instance with Confidential Computing enabled, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Machine type** section, select an N2D machine type. Only N2D machine types are supported.

5.  Under **Confidential VM service** , select **Enable Confidential Computing** .

6.  In the **Enable Confidential Computing** dialog, click **Enable** .

7.  Click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

### gcloud

To create a Agent Platform Workbench instance with Confidential Computing enabled, use the [`gcloud workbench instances create`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/create) command and set `--confidential-compute-type` to `SEV` .

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance; must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where you want your instance to be located
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM, for example: `n2d-standard-2`

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --machine-type=MACHINE_TYPE \
        --confidential-compute-type=SEV

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --machine-type=MACHINE_TYPE `
        --confidential-compute-type=SEV

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --machine-type=MACHINE_TYPE ^
        --confidential-compute-type=SEV

Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

### REST

To create a Agent Platform Workbench instance with Confidential Computing enabled, use the [`projects.locations.instances.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create) method and include a `confidentialInstanceConfig` in your [`GceSetup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#gcesetup) .

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where you want your instance to be located
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM, for example: `n2d-standard-2`

HTTP method and URL:

    POST https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances

Request JSON body:

    {
      "gce_setup": {
        "machine_type": "MACHINE_TYPE",
        "confidentialInstanceConfig": {
          "confidentialInstanceType": SEV
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances" | Select-Object -Expand Content

Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

## Confirm whether an instance has Confidential Computing enabled

To confirm whether a Agent Platform Workbench instance has Confidential Computing enabled, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  In the **Instance name** column, click the name of the instance that you want to check.
    
    The **Instance details** page opens.

3.  Next to **VM details** , click **View in Compute Engine** .

4.  On the Compute Engine details page, the value for **Confidential VM service** shows either `Enabled` or `Disabled` .

## Limitations

When you create or use a Agent Platform Workbench instance with Confidential Computing enabled, the following limitations apply:

  - Only N2D machine types are supported. See [N2D machine types](https://docs.cloud.google.com/compute/docs/general-purpose-machines#n2d_machine_types) .

  - Only AMD SEV confidential computing technology is supported. For more information, see [AMD SEV](https://docs.cloud.google.com/confidential-computing/confidential-vm/docs/confidential-vm-overview#amd_sev) .

  - Confidential Computing can't be enabled or turned off after you create the Agent Platform Workbench instance.

## Billing

When using Agent Platform Workbench instances with Confidential Computing you are charged for the following:

  - Agent Platform Workbench instances usage. See [Agent Platform pricing](https://cloud.google.com/gemini-enterprise-agent-platform/pricing#notebooks) .

  - Confidential Computing usage. See [Confidential VM pricing](https://cloud.google.com/confidential-computing/confidential-vm/pricing) .

## What's next

  - To use a notebook to help you get started using Gemini Enterprise Agent Platform and other Google Cloud services, see [Agent Platform notebook tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials/jupyter-notebooks) .
  - To check on the health status of your Agent Platform Workbench instance, see [Monitor health status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health) .
