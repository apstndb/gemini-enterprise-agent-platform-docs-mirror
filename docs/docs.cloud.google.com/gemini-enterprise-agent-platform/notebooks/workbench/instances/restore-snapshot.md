---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-snapshot
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-snapshot
title: Back up and restore data by using a snapshot
description: Back up and restore the data on a Agent Platform Workbench instance by using a snapshot.
data_source: docs.cloud.google.com
---

# Back up and restore data by using a snapshot

This page describes how to use a snapshot to back up and restore the data on your Gemini Enterprise Agent Platform Workbench instance.

## Back up the data

To back up data on a Agent Platform Workbench instance, you can take a snapshot of the underlying Compute Engine virtual machine (VM) data disk.

You can create a snapshot of your instance's data disk by using the Google Cloud console, the Google Cloud CLI, or the REST API:

### Console

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click the instance name.

3.  On the **Instance details** page, click **View in Compute Engine** to open **VM details** .

4.  In the **Additional disks** section, click the name of the data disk. The name of the data disk is in this format: `  INSTANCE_NAME -data-workspace ` .

5.  Click **Create snapshot** .

6.  In the **Create a snapshot** dialog, click **Create** .

Compute Engine creates a snapshot of the data disk.

### gcloud

To create a snapshot of your instance's data disk, use the [`gcloud compute snapshots create`](https://docs.cloud.google.com/sdk/gcloud/reference/compute/snapshots/create) command.

Before using any of the command data below, make the following replacements:

  - `  SNAPSHOT_NAME  ` : a name for your snapshot
  - `  SOURCE_ZONE  ` : the zone where your instance is located
  - `  INSTANCE_NAME  ` : the name of your instance
  - `  STORAGE_LOCATION  ` : the [Cloud Storage multi-region](https://docs.cloud.google.com/storage/docs/bucket-locations#location-mr) or the [Cloud Storage region](https://cloud.google.com/storage/docs/bucket-locations#location-r) where you want to store your snapshot. You can specify only one storage location.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud compute snapshots create SNAPSHOT_NAME \
        --source-disk-zone=SOURCE_ZONE \
        --source-disk=INSTANCE_NAME-data-workspace \
        --storage-location=STORAGE_LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud compute snapshots create SNAPSHOT_NAME `
        --source-disk-zone=SOURCE_ZONE `
        --source-disk=INSTANCE_NAME-data-workspace `
        --storage-location=STORAGE_LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud compute snapshots create SNAPSHOT_NAME ^
        --source-disk-zone=SOURCE_ZONE ^
        --source-disk=INSTANCE_NAME-data-workspace ^
        --storage-location=STORAGE_LOCATION

### REST

To create a snapshot of your instance's data disk, make a `POST` request to Compute Engine's [`snapshots.insert`](https://docs.cloud.google.com/compute/docs/reference/rest/v1/snapshots/insert) method.

Before using any of the request data, make the following replacements:

  - `  DESTINATION_PROJECT_ID  ` : the ID of the project where you want to create the snapshot
  - `  SNAPSHOT_NAME  ` : a name for your snapshot
  - `  SOURCE_PROJECT_ID  ` : the ID of the project where your instance is located
  - `  SOURCE_ZONE  ` : the zone where your instance is located
  - `  INSTANCE_NAME  ` : the name of your instance
  - `  STORAGE_LOCATION  ` : the [Cloud Storage multi-region](https://docs.cloud.google.com/storage/docs/bucket-locations#location-mr) or the [Cloud Storage region](https://cloud.google.com/storage/docs/bucket-locations#location-r) where you want to store your snapshot. You can specify only one storage location.

HTTP method and URL:

    POST https://compute.googleapis.com/compute/v1/projects/DESTINATION_PROJECT_ID/global/snapshots

Request JSON body:

    {
      "name": "SNAPSHOT_NAME",
      "sourceDisk": "projects/SOURCE_PROJECT_ID/zones/SOURCE_ZONE/disks/INSTANCE_NAME-data-workspace",
      "storageLocations": [
          "STORAGE_LOCATION"
      ],
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://compute.googleapis.com/compute/v1/projects/DESTINATION_PROJECT_ID/global/snapshots"

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
        -Uri "https://compute.googleapis.com/compute/v1/projects/DESTINATION_PROJECT_ID/global/snapshots" | Select-Object -Expand Content

### Schedule backup

> **Preview — Scheduled backups**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

One or more backup schedules can be configured for a workbench instance by attaching [resource policies](https://docs.cloud.google.com/compute/docs/reference/rest/v1/resourcePolicies) to the data disk. You can attach multiple resource policies to have several backup schedules active at the same time.

You can create an instance with snapshot schedules attached using the Google Cloud CLI or the REST API:

### gcloud

To create an instance with a snapshot schedule, use the [`gcloud workbench instances create`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/create) command and specify your resource policies by using the `--data-disk-resource-policies` flag.

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance; must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where you want your instance to be located
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM, for example: `n2d-standard-2`
  - `  REGION  ` : the region where the resource policy is located
  - `  RESOURCE_POLICY  ` : the resource policy to apply to the data disk.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --machine-type=MACHINE_TYPE \
        --data-disk-resource-policies=projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --machine-type=MACHINE_TYPE `
        --data-disk-resource-policies=projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --machine-type=MACHINE_TYPE ^
        --data-disk-resource-policies=projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY

### REST

To create an instance with a snapshot schedule, use the [`projects.locations.instances.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create) method and set the `resourcePolicies` in your [`DataDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#datadisk) .

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where you want your instance to be located
  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM, for example: `n2d-standard-2`
  - `  REGION  ` : the region where the resource policy is located
  - `  RESOURCE_POLICY  ` : the resource policy to apply to the data disk.

HTTP method and URL:

    POST https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances

Request JSON body:

    {
      "gce_setup": {
        "machine_type": "MACHINE_TYPE",
        "data_disks": [
          {
            "resource_policies": [
              "projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY"
            ]
          }
        ]
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

### Update backup schedules

You can add, replace, or update the backup schedules on an existing instance by using the Google Cloud CLI or the REST API. To set multiple schedules, include multiple resource policies in the `resourcePolicies` list:

### gcloud

To update the backup schedules on an existing instance, use the [`gcloud workbench instances update`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/update) command and specify your resource policies by using the `--data-disk-resource-policies` flag. The provided list of resource policies replaces the existing list entirely.

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where your instance is located
  - `  INSTANCE_ID  ` : the ID of your instance
  - `  REGION  ` : the region where the resource policy is located
  - `  RESOURCE_POLICY  ` : the resource policy to apply to the data disk.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances update INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --data-disk-resource-policies=projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances update INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --data-disk-resource-policies=projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances update INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --data-disk-resource-policies=projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY

### REST

To update the backup schedules on an existing instance, make a `PATCH` request to the [`projects.locations.instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method with the `updateMask` set to `gceSetup.dataDisks.resourcePolicies` . The provided list of resource policies replaces the existing list entirely.

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where your instance is located
  - `  INSTANCE_ID  ` : the ID of your instance
  - `  REGION  ` : the region where the resource policy is located
  - `  RESOURCE_POLICY  ` : the resource policy to apply to the data disk.

HTTP method and URL:

    PATCH https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID?updateMask=gceSetup.dataDisks.resourcePolicies

Request JSON body:

    {
      "gce_setup": {
        "data_disks": [
          {
            "resource_policies": [
              "projects/PROJECT_ID/regions/REGION/resourcePolicies/RESOURCE_POLICY"
            ]
          }
        ]
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID?updateMask=gceSetup.dataDisks.resourcePolicies"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID?updateMask=gceSetup.dataDisks.resourcePolicies" | Select-Object -Expand Content

### Remove all backup schedules

You can remove all backup schedules from an existing instance by setting the resource policies to an empty list using the Google Cloud CLI or the REST API:

### gcloud

To remove all backup schedules from an existing instance, use the [`gcloud workbench instances update`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/update) command and pass an empty value for the `--data-disk-resource-policies` flag. This removes all active schedules from the instance.

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where your instance is located
  - `  INSTANCE_ID  ` : the ID of your instance

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances update INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --data-disk-resource-policies=

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances update INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --data-disk-resource-policies=

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances update INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --data-disk-resource-policies=

### REST

To remove all backup schedules from an existing instance, make a `PATCH` request to the [`projects.locations.instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method with the `updateMask` set to `gceSetup.dataDisks.resourcePolicies` and an empty `resourcePolicies` list. This removes all active schedules from the instance.

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where your instance is located
  - `  INSTANCE_ID  ` : the ID of your instance

HTTP method and URL:

    PATCH https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID?updateMask=gceSetup.dataDisks.resourcePolicies

Request JSON body:

    {
      "gce_setup": {
        "data_disks": [
          {
            "resource_policies": []
          }
        ]
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID?updateMask=gceSetup.dataDisks.resourcePolicies"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID?updateMask=gceSetup.dataDisks.resourcePolicies" | Select-Object -Expand Content

## Restore data from a snapshot

You can restore data on an instance by using a snapshot. When you restore data on an instance, Agent Platform Workbench deletes the existing data disk that is attached to the instance, creates a new data disk based on the snapshot, and attaches the new data disk to the instance.

You can restore data on an instance by using the gcloud CLI or the REST API:

> **Caution:** Restoring a snapshot is supported only for snapshots of data disks taken from Agent Platform Workbench instances. Restoring a snapshot that was taken from a different source can cause the instance to function incorrectly.

### gcloud

To restore data on an instance, use the [`gcloud workbench instances restore`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/restore) command.

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your instance
  - `  LOCATION  ` : the zone where your instance is located
  - `  SNAPSHOT_PROJECT_NAME  ` : the project name where your snapshot is located
  - `  SNAPSHOT_NAME  ` : the name of the snapshot to restore

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances restore INSTANCE_NAME \
        --location=LOCATION \
        --snapshot-project=SNAPSHOT_PROJECT_NAME \
        --snapshot=SNAPSHOT_NAME

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances restore INSTANCE_NAME `
        --location=LOCATION `
        --snapshot-project=SNAPSHOT_PROJECT_NAME `
        --snapshot=SNAPSHOT_NAME

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances restore INSTANCE_NAME ^
        --location=LOCATION ^
        --snapshot-project=SNAPSHOT_PROJECT_NAME ^
        --snapshot=SNAPSHOT_NAME

### REST

To restore data on an instance, make a `POST` request to the [`projects.locations.instances.restore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/restore) method.

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where your instance is located
  - `  INSTANCE_ID  ` : the ID of your instance
  - `  SNAPSHOT_ID  ` : the ID of the snapshot to restore; to get the ID of a snapshot, use Compute Engine's [snapshots.get](https://docs.cloud.google.com/compute/docs/reference/rest/v1/snapshots/get) method
  - `  SNAPSHOT_PROJECT_ID  ` : the project ID of the snapshot

HTTP method and URL:

    POST https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID:restore

Request JSON body:

    {
      "snapshot": {
        {
          "snapshotId": SNAPSHOT_ID,
          "projectId": SNAPSHOT_PROJECT_ID
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
         "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID:restore"

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
        -Uri "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances/INSTANCE_ID:restore" | Select-Object -Expand Content

## What's next

  - [Use Cloud Storage to back up and restore files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-cloud-storage)

  - [Save a notebook to GitHub](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/save-to-github)
