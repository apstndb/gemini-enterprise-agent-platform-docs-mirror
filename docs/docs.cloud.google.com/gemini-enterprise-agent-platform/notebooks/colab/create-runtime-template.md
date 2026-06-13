---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-runtime-template
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-runtime-template
title: Create a runtime template in Colab Enterprise
description: Learn how to create a runtime template in Colab Enterprise
data_source: docs.cloud.google.com
---

This page shows you how to create a runtime template in Colab Enterprise.

To run code in your notebook, you use a compute resource called a *runtime* . You can use the default runtime or a runtime created from a runtime template. By creating a runtime template, you can configure the template to optimize a runtime's performance, cost, and other characteristics based on your needs.

Learn more about [runtimes and runtime templates](https://docs.cloud.google.com/colab/docs/runtimes) .

## Before you begin

### Required roles

To get the permissions that you need to create a runtime template in Colab Enterprise, ask your administrator to grant you the Colab Enterprise Admin ( [`roles/aiplatform.colabEnterpriseAdmin`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.colabEnterpriseAdmin) ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

> One or more of the required roles includes the `dataform.repositories.list` permission. Users who are granted the `dataform.repositories.list` permission or the [Code Creator ( `roles/dataform.codeCreator` )](https://docs.cloud.google.com/dataform/docs/access-control#dataform.codeCreator) role in a project can list the names of code assets in that project by using the Dataform API or the Dataform command-line interface (CLI). Non-administrators using BigQuery Studio can only see code assets that they created or that were shared with them.

## Create the runtime template

To create a runtime template, you can use the Google Cloud console, the Google Cloud CLI, the REST API, or Terraform.

### Console

To create a runtime template:

1.  In the Google Cloud console, go to the Colab Enterprise **Runtime templates** page.

2.  Click add\_box **New template** .
    
    The **Create new runtime template** dialog appears.

### Runtime basics

1.  In the **Runtime basics** section, enter a **Display name** .

2.  In the **Region** menu, select the region where you want your runtime template.

3.  Optional: Add a **Description** of your runtime template.

4.  Optional: To add a label, click add **Add label** , and then enter a **Key** and **Value** pair. To add more labels, repeat this step.

5.  Click **Continue** .

### Configure compute

1.  In the **Configure compute** section, in the **Machine type** menu, select a machine type. For information on machine types, see the [Machine families resource and comparison guide](https://docs.cloud.google.com/compute/docs/machine-resource) .
    
    If you select a machine type that has GPUs, select the **Accelerator type** and **Accelerator count** . If you're unable to select the number of GPUs that you want, you might need to increase your quota. See [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase) .

2.  In the **Data disk type** menu, select a disk type.

3.  In the **Data disk size** field, enter a size in GB.

4.  In the **Idle shutdown** section:
    
      - To turn off idle shutdown, clear **Enable idle shutdown** .
    
      - To change the inactivity time period, in **Time of inactivity before shutdown (Minutes)** , change the number to the number of minutes of inactivity that you want. In the Google Cloud console, this setting can be set to any integer value from 10 to 1440.

5.  Click **Continue** .

### Environment

1.  In the **Environment** section, select an **Environment** . The default is **Latest** (currently Python 3.12).

2.  Optional: In the **Post-startup script** field, enter the URI for a post-startup script. For more information about using a post-startup script, see [Use a post-startup script](https://docs.cloud.google.com/colab/docs/post-startup-script) .

3.  Optional: Under the post-startup script URL, select your post-startup script's behavior. The default behavior is **Run once** . For more information, see [Post-startup script behavior](https://docs.cloud.google.com/colab/docs/post-startup-script#behavior) .

4.  Optional: To add an environment variable, click add **Add env variable** , and then enter a **Key** and **Value** pair. To add more environment variables, repeat this step.

5.  Click **Continue** .

### Networking and security

1.  In the **Networking and security** section, in the **Network** menu, select a network. If you don't select a network, your default network is selected.

2.  In the **Subnetwork** menu, select a subnetwork.

3.  To turn off public internet access, clear **Enable public internet access** .

4.  To turn off end-user credential access, clear **Enable end-user credentials** .

### Finish creating the runtime template

Click **Create** to finish creating the runtime template.

Your runtime template appears in the list on the **Runtime templates** tab.

### gcloud

Before using any of the command data below, make the following replacements:

  - `  DISPLAY_NAME  ` : the display name of your runtime template.
  - `  PROJECT_ID  ` : your project ID.
  - `  REGION  ` : the region where you want your runtime template.
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) to use for your runtime.
  - `  ACCELERATOR_TYPE  ` : the type of hardware accelerator to use for your runtime.
  - `  ACCELERATOR_COUNT  ` : the number of accelerators to use for your runtime.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtime-templates create --display-name="DISPLAY_NAME" \
        --project=PROJECT_ID \
        --region=REGION \
        --machine-type=MACHINE_TYPE \
        --accelerator-type=ACCELERATOR_TYPE \
        --accelerator-count=ACCELERATOR_COUNT

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtime-templates create --display-name="DISPLAY_NAME" `
        --project=PROJECT_ID `
        --region=REGION `
        --machine-type=MACHINE_TYPE `
        --accelerator-type=ACCELERATOR_TYPE `
        --accelerator-count=ACCELERATOR_COUNT

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud colab runtime-templates create --display-name="DISPLAY_NAME" ^
        --project=PROJECT_ID ^
        --region=REGION ^
        --machine-type=MACHINE_TYPE ^
        --accelerator-type=ACCELERATOR_TYPE ^
        --accelerator-count=ACCELERATOR_COUNT

For more information about the command for creating a runtime template from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/colab/runtime-templates/create) .

### REST

Before using any of the request data, make the following replacements:

  - `  REGION  ` : the region where you want your runtime template.
  - `  PROJECT_ID  ` : your project ID.
  - `  DISPLAY_NAME  ` : the display name of your runtime template.
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) to use for your runtime.
  - `  ACCELERATOR_TYPE  ` : the type of hardware accelerator to use for your runtime.
  - `  ACCELERATOR_COUNT  ` : the number of accelerators to use for your runtime.

HTTP method and URL:

    POST https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/notebookRuntimeTemplates

Request JSON body:

    {
      "displayName": "DISPLAY_NAME",
      "machineSpec": {
        {
          "machineType": MACHINE_TYPE
          "acceleratorType": ACCELERATOR_TYPE,
          "acceleratorCount": ACCELERATOR_COUNT,
        }
      },
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/notebookRuntimeTemplates"

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
        -Uri "https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/notebookRuntimeTemplates" | Select-Object -Expand Content

If successful, the response body contains an instance of [Operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

For more information, see the [`notebookRuntimeTemplates.create` REST API documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimeTemplates/create) .

### Terraform

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) . For more information, see the [Terraform provider reference documentation](https://registry.terraform.io/providers/hashicorp/google/latest/docs) .

The following sample uses the [`google_colab_runtime_template`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/colab_runtime_template) Terraform resource to create an Colab Enterprise runtime template.

    resource "google_compute_network" "my_network" {
      name = "{{index $.Vars "network_name"}}"
      auto_create_subnetworks = false
    }
    
    resource "google_compute_subnetwork" "my_subnetwork" {
      name   = "{{index $.Vars "network_name"}}"
      network = google_compute_network.my_network.id
      region = "us-central1"
      ip_cidr_range = "10.0.1.0/24"
    }
    
    resource "google_colab_runtime_template" "{{$.PrimaryResourceId}}" {
      name        = "{{index $.Vars "runtime_template_name"}}"
      display_name = "Runtime template full"
      location    = "us-central1"
      description = "Full runtime template"
      machine_spec {
        machine_type     = "n1-standard-2"
        accelerator_type = "NVIDIA_TESLA_T4"
        accelerator_count = "1"
      }
    
      data_persistent_disk_spec {
        disk_type    = "pd-standard"
        disk_size_gb = 200
      }
    
      network_spec {
        enable_internet_access = true
        network = google_compute_network.my_network.id
        subnetwork = google_compute_subnetwork.my_subnetwork.id
      }
    
      labels = {
        k = "val"
      }
    
      idle_shutdown_config {
        idle_timeout = "3600s"
      }
    
      euc_config {
        euc_disabled = false
      }
    
      shielded_vm_config {
        enable_secure_boot = false
      }
    
      network_tags = ["abc", "def"]
    
      encryption_spec {
        kms_key_name = "{{index $.Vars "key_name"}}"
      }
    
      software_config {
        env {
          name    = "TEST"
          value   = 1
        }
    
        post_startup_script_config {
          post_startup_script = "echo 'hello world'"
          post_startup_script_url = "gs://colab-enterprise-pss-secure/secure_pss.sh"
          post_startup_script_behavior = "RUN_ONCE"
        }
    
        colab_image {
          release_name = "py312"
        }
      }
    }

## Granting access to the runtime template

After you create a runtime template, you must grant access to it for a principal to be able to use it. A principal can [create a runtime](https://docs.cloud.google.com/colab/docs/create-runtime) from a runtime template only when they have the following:

  - Access to the runtime template.
  - The required permissions for creating runtimes.

## What's next

  - Learn more about [runtimes and runtime templates](https://docs.cloud.google.com/colab/docs/runtimes) .
  - Learn how to [create a runtime](https://docs.cloud.google.com/colab/docs/create-runtime) based on a runtime template.
