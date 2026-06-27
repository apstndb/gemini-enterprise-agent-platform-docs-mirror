---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create
title: Create a Agent Platform Workbench instance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page shows you how to create a Gemini Enterprise Agent Platform Workbench instance by using the Google Cloud console or the Google Cloud CLI. While creating your instance, you can configure your instance's hardware, encryption type, network, and other details.

## Before you begin

Before you create a Agent Platform Workbench instance, you must complete the following steps:

> **Note:** The [Notebooks API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest) lets you manage Agent Platform Workbench resources. For managing Agent Platform resources, see the [Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest) .

### Required roles

To get the permissions that you need to create and manage a Agent Platform Workbench instance, ask your administrator to grant you the [Notebooks Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.admin) ( `roles/notebooks.admin` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an instance

You can create a Agent Platform Workbench instance by using the Google Cloud console, the gcloud CLI, or Terraform:

### Console

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Details** section, provide the following information for your new instance:
    
      - **Name** : Provide a name for your new instance. The name must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen.
      - **Region** and **Zone** : Select a region and zone for the new instance. For best network performance, select the region that is geographically closest to you. See the available [Agent Platform Workbench locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances) .
      - **Labels** : Optional. Provide custom key-value labels for the instance.
      - **Network tags** : Optional. Provide [network tags](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#network-tags) for the instance.

5.  In the **Environment** section, provide the following:
    
      - **JupyterLab version** : Select a JupyterLab version.
      - **Version** : Use the latest version or a previous version of Agent Platform Workbench instances.
      - **Post-startup script** : Optional. Click **Browse** to select a script to run one time, after the instance is created. The path must be a URL or Cloud Storage path, for example: ` gs:// PATH_TO_FILE / FILE_NAME  ` .
      - **Metadata** : Optional. Provide custom metadata keys for the instance.

6.  In the **Machine type** section, provide the following:
    
      - **Machine type** : Select the number of CPUs and amount of RAM for your new instance. Agent Platform Workbench provides monthly cost estimates for each machine type that you select.
    
      - **GPU** : Optional. If you want GPUs, select the **GPU type** and **Number of GPUs** for your new instance. The accelerator type that you want must be available in your instance's zone. To learn about accelerator availability by zone, see [GPU regions and zones availability](https://docs.cloud.google.com/compute/docs/gpus/gpu-regions-zones) . For information about the different GPUs, see [GPUs on Compute Engine](https://docs.cloud.google.com/compute/docs/gpus) .
        
        > **Note:** You can modify the machine type and GPU configuration for your instance after it is created. For more information, see [Change machine type and configure GPUs of a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/change-machine-type) .
    
      - **Shielded VM** : Optional. Select or clear the following checkboxes:
        
          - **Secure Boot**
          - **Virtual Trusted Platform Module (vTPM)**
          - **Integrity monitoring**
    
      - **Idle shutdown** : Optional.
        
          - To change the number of minutes before shutdown, in the **Time of inactivity before shutdown (Minutes)** field, change the value to an integer from 10 through 1440.
        
          - To turn off idle shutdown, clear **Enable Idle Shutdown** .

7.  In the **Disks** section, provide the following:
    
      - **Disks** : Optional. To change the default data disk settings, select a **Data disk type** and **Data disk size in GB** . For more information about disk types, see [Storage options](https://docs.cloud.google.com/compute/docs/disks#introduction) .
    
      - **Delete to trash** : Optional. Select this checkbox to use the operating system's default trash behavior, If you use the default trash behavior, files deleted by using the JupyterLab user interface are recoverable but these deleted files do use disk space.
    
      - **Encryption** : Select **Google-managed encryption key** or **Customer-managed encryption key (CMEK)** . To use CMEK, see [Customer-managed encryption keys](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek) .

8.  In the **Networking** section, provide the following:
    
      - **Networking** : Adjust the network options to use a network in your current project or a [Shared VPC network](https://docs.cloud.google.com/vpc/docs/shared-vpc) from a host project, if one is configured. If you are using a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) in the host project, you must also grant the [Compute Network User role](https://docs.cloud.google.com/compute/docs/access/iam#compute.networkUser) ( `roles/compute.networkUser` ) to the [Notebooks Service Agent](https://docs.cloud.google.com/iam/docs/service-agents#cloud-ai-platform-notebooks-service-account) from the service project.
        
        1.  In the **Network** field, select the network that you want. You can select a VPC network, as long as the network has [Private Google Access](https://docs.cloud.google.com/vpc/docs/private-google-access) enabled or can access the internet. For more information, see [network configuration options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#network-options) .
        
        2.  In the **Subnetwork** field, select the subnetwork that you want.
        
        3.  To turn off the external IP address, clear the **Assign external IP address** checkbox.
            
            > **Note:** If you disable **Assign external IP address** , make sure to add DNS entries from the [Network configuration options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#network-options) section.
        
        4.  To turn off proxy access, clear the **Allow proxy access** checkbox.
            
            > **Note:** If you turn off proxy access, you must [use SSH to connect to your instance's JupyterLab interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/ssh-access) .

9.  In the **IAM and security** section, provide the following:
    
      - **IAM and security** : To grant access to the instance's JupyterLab interface, complete one of the following steps:
        
          - To grant access to JupyterLab through a service account, select **Service account** .
            
            > **Caution:** After you create the instance, you can't change the specified service account, either directly or by modifying the underlying Compute Engine VM. To use a different service account, you must create a new instance specifying the service account that you want.
            
              - To use the default Compute Engine service account, select **Use default Compute Engine service account** .
            
              - To use a custom service account, clear **Use default Compute Engine service account** , and then, in the **Service account email** field, enter your custom service account email address.
        
          - To grant a single user access to the JupyterLab interface, do the following:
            
            1.  Select **Single user** , and then, in the **User email** field, enter the user account that you want to grant access. If the specified user is not the creator of the instance, you must grant the specified user the [Service Account User role](https://docs.cloud.google.com/iam/docs/service-account-permissions#user-role) ( `roles/iam.serviceAccountUser` ) on the instance's service account.
            
            2.  Your instance uses a service account to interact with Google Cloud services and APIs.
                
                  - To use the default Compute Engine service account, select **Use default Compute Engine service account** .
                
                  - To use a custom service account, clear **Use default Compute Engine service account** , and then, in the **Service account email** field, enter your custom service account email address.
        
        > **Note:** To grant access to the instance through the service account or single user option, you must use an individual's user account email address. Group access is not supported.
        
        To learn more about granting access, see [Manage access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access) .
    
      - **Security options** : Select or clear the following checkboxes:
        
          - **Root access to the instance**
          - **nbconvert**
          - **File downloading**
          - **Terminal access**

10. In the **System health** section, provide the following:
    
      - <span id="auto-upgrade"></span> **Environment upgrade and system health** : To automatically upgrade to newly released environment versions, select **Environment auto-upgrade** and complete the **Upgrade schedule** .
    
      - In **Reporting** , select or clear the following checkboxes:
        
          - **Report system health**
          - **Report custom metrics to Cloud Monitoring**
          - **Install Cloud Monitoring**
          - **Report DNS status for required Google domains**

11. Click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

### gcloud

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance; must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen

  - `  PROJECT_ID  ` : your project ID

  - `  LOCATION  ` : the zone where you want your instance to be located

  - `  VM_IMAGE_PROJECT  ` : the ID of the Google Cloud project that VM image belongs to; the default Google Cloud project ID for supported images is `cloud-notebooks-managed`

  - `  VM_IMAGE_NAME  ` : the image name; to find the image name of a specific version, see [Find the specific version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version#find_the_specific_version_that_you_want)

  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM

  - `  METADATA  ` : custom metadata to apply to this instance; for example, to specify a post-startup-script, you can use the `post-startup-script` metadata tag, in the format: `--metadata=post-startup-script=gs:// BUCKET_NAME /hello.sh`
    
    > To enable the JupyterLab 4 preview, use `--metadata=enable-jupyterlab4-preview=true` . For more information, see [JupyterLab 4 preview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#jupyterlab-preview) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --vm-image-project=VM_IMAGE_PROJECT \
        --vm-image-name=VM_IMAGE_NAME \
        --machine-type=MACHINE_TYPE \
        --metadata=METADATA

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --vm-image-project=VM_IMAGE_PROJECT `
        --vm-image-name=VM_IMAGE_NAME `
        --machine-type=MACHINE_TYPE `
        --metadata=METADATA

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --vm-image-project=VM_IMAGE_PROJECT ^
        --vm-image-name=VM_IMAGE_NAME ^
        --machine-type=MACHINE_TYPE ^
        --metadata=METADATA

For more information about the command for creating an instance from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/create) .

Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

### Terraform

The following sample uses the [`google_workbench_instance`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/workbench_instance) Terraform resource to create a Agent Platform Workbench instance named `workbench-instance-example` .

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

```terraform
resource "google_workbench_instance" "default" {
  name     = "workbench-instance-example"
  location = "us-central1-a"

  gce_setup {
    machine_type = "n1-standard-1"
    accelerator_configs {
      type       = "NVIDIA_TESLA_T4"
      core_count = 1
    }
    vm_image {
      project = "cloud-notebooks-managed"
      family  = "workbench-instances"
    }
  }
}
```

## Change the version of JupyterLab on an existing instance

This section describes how to change the JupyterLab version on your instance by using the Google Cloud console or the gcloud CLI.

### Console

To change the JupyterLab version on an existing instance, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  [Shut down your instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/shut-down) .

3.  Click the name of your instance to open the **Instance details** page.

4.  On the **System** tab, do one of the following:
    
      - To enable JupyterLab 3, clear the **Enable JupyterLab 4** checkbox.
    
      - To enable JupyterLab 4, leave the **Enable JupyterLab 4** checkbox selected.

5.  Click **Submit** .

6.  To restart your instance, select the instance and click arrow\_right **Start** .

### gcloud

You can change the JupyterLab version on an existing instance by using the following command:

    gcloud workbench instances update INSTANCE_NAME \
        --project="PROJECT_ID" \
        --location="LOCATION" \
        --metadata=enable-jupyterlab4=ENABLEMENT_BOOLEAN

Replace the following:

  - `  PROJECT_ID  ` : your project ID

  - `  LOCATION  ` : the zone where you want your instance to be located

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance

  - `  ENABLEMENT_BOOLEAN  ` : use one of the following:
    
      - `false` : changes to JupyterLab 3.
      - `true` : changes to JupyterLab 4. JupyterLab 4 is enabled, by default.

## Limitation of JupyterLab 4

When scheduling a notebook run in JupyterLab 4, Agent Platform Workbench stores a copy of the notebook in its current state in Cloud Storage, and then runs this copy of the notebook according to the schedule. If you edit the original notebook, you must create a new schedule to run the updated version of the notebook.

## Network configuration options

A Agent Platform Workbench instance must access service endpoints that are outside your VPC network.

You can provide this access in one of the following ways:

  - Assign an external IP address to the instance. This is done by default when you create a new instance. Make sure your environment meets the [requirements for accessing Google APIs and services](https://docs.cloud.google.com/vpc/docs/access-apis-external-ip#requirements) .

  - Connect the instance to a subnet where [Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) is enabled. Make sure your environment meets the [requirements for Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access#requirements) .

If you use the `private.googleapis.com` or `restricted.googleapis.com` VIP to provide access to the service endpoints, [add DNS entries for each of the required service endpoints](https://docs.cloud.google.com/vpc/docs/configure-private-google-access#config-domain) :

  - `notebooks.cloud.google.com`
  - `notebooks.googleapis.com`
  - `*.notebooks.byoid.googleusercontent.com`
  - `*.notebooks.cloud.google.com`
  - `*.notebooks.googleusercontent.com`
  - `*.kernels.googleusercontent.com`

If you use [third party credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance) , you must use `restricted.googleapis.com` and add the following DNS entry:

  - `*.byoid.googleusercontent.com`

> **Note:** When using Agent Platform with Private Google Access to access Google Cloud APIs, the instances must be configured to bypass any web proxies or other network traffic inspection or filtering devices (for example next generation firewalls) for any hostnames in the domains listed in the [Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) documentation.

## Network tags

Your new Agent Platform Workbench instance automatically has the `deeplearning-vm` and `notebook-instance` network tags assigned.

![The Virtual machines section of the console navigation menu, with VM instances selected, showing the currently assigned network tags.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/notebook-network-tags.png)

These tags let you manage network access to and from your Agent Platform Workbench instance by referencing the tags in your VPC networking firewall rules. For more information about network tags, see [Add network tags](https://docs.cloud.google.com/vpc/docs/add-remove-network-tags) .

To view the network tags for a Agent Platform Workbench instance, do the following:

1.  In the Google Cloud console, go to the **VM instances** page.

2.  Click the name of the instance.

3.  In the **Networking** section, find **Network tags** .

## Troubleshooting

If you encounter a problem when you create an instance, see [Troubleshooting Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#instances) for help with common issues.

## What's next

  - To use a notebook to help you get started using Gemini Enterprise Agent Platform and other Google Cloud services, see [Agent Platform notebook tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials/jupyter-notebooks) .
  - [Create an instance with Confidential Computing enabled](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-confidential-computing) .
  - To check on the health status of your Agent Platform Workbench instance, see [Monitor health status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health) .
  - For a Terraform solution for simplified Agent Platform networking setup, see [Simplified Cloud Networking Configuration Solutions](https://github.com/GoogleCloudPlatform/cloudnetworking-config-solutions) .
  - You can create a Agent Platform Workbench instance using a private IP. For a Terraform solution, see [Workbench](https://github.com/GoogleCloudPlatform/cloudnetworking-config-solutions/tree/main/execution/06-consumer/Workbench) .
  - To learn more about granting access, see [Manage access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access) .
  - To use CMEK, see [Customer-managed encryption keys](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek) .
