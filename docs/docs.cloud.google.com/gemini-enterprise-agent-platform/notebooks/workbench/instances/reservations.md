---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/reservations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/reservations
title: Use reservations with Agent Platform Workbench instances
description: Learn how to ensure that VM resources are available when your Agent Platform Workbench instances need them
data_source: docs.cloud.google.com
---

# Use reservations with Agent Platform Workbench instances

This document explains how to use [Compute Engine reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) to gain a high level of assurance that your Gemini Enterprise Agent Platform Workbench instances have enough virtual machine (VM) resources to run.

Reservations are a Compute Engine feature. They help make sure that you have the resources available to create VMs with the same hardware (memory and vCPUs) and optional resources (GPUs and Local SSD disks) whenever you need them.

When you create a reservation, Compute Engine verifies that the requested capacity is available in the specified zone. If so, then Compute Engine reserves the resources, creates the reservation, and the following happens:

  - The reserved resources are immediately available for you to consume, and they remain available until you delete the reservation.

  - You're charged for the reserved resources at the same on-demand rate as running VMs, including any applicable discounts, until the reservation is deleted. While consuming a reservation, a VM doesn't incur duplicate charges for resources since the reservation is already billed for the cost of the reserved resources. To learn more, see [Reservations of Compute Engine zonal resources](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) .

## Limitations and requirements

All limitations of Compute Engine reservations apply when Agent Platform Workbench instances consume reservations. See [How reservations work](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#how-reservations-work) .

In addition, when using reservations with Agent Platform Workbench instances, the following limitations and requirements apply:

  - Your reservation must be one of the following:
    
      - In the same project as your Agent Platform Workbench instance.
      - Shared with the same project as your Agent Platform Workbench instance.

  - A reservation's VM properties must match exactly with your Agent Platform Workbench instance to consume the reservation. For example, if a reservation specifies an `e2-standard-8` machine type, then the Agent Platform Workbench instance can only consume the reservation if it also uses an `e2-standard-8` machine type. See [Requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements%22) .

## Before you begin

1.  Review the [requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions) for reservations.
2.  Review the [quota requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements-shared-reservations) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions-shared-reservations) for shared reservations.

### Required roles

To get the permissions that you need to use reservations with Agent Platform Workbench instances, ask your administrator to grant you the following IAM roles on the project:

  - [Compute Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/compute#compute.admin) ( `roles/compute.admin` )
  - [Notebooks Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.admin) ( `roles/notebooks.admin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a reservation

Create a Compute Engine reservation. It can be a single-project reservation or a shared reservation. The reservation can be on-demand or a future reservation. For more information, see [Choose a reservation type](https://docs.cloud.google.com/compute/docs/instances/choose-reservation-type) .

> **Caution:** If you want to use your Agent Platform Workbench instance after your reservation has ended, use an on-demand reservation. Avoid consuming a future reservation because when a future reservation reaches its end time, Compute Engine automatically deletes the underlying VM of your instance, including its data disk. Your Agent Platform Workbench instance stops functioning and won't incur any further charges. To remove the instance from your list of Agent Platform Workbench instances, you must delete it.

## Use a reservation with a new instance

To create a Agent Platform Workbench instance that consumes a reservation, you can use the Google Cloud console or the REST API.

### Console

To create a Agent Platform Workbench instance that consumes a reservation, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Machine type** section, select the machine type and GPU configuration that matches your reservation.

5.  Under **CPU Platform and GPU** , in the **Reservations** menu, select the reservation to consume.

6.  Click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

### REST

Before using any of the request data, make the following replacements:

`  PROJECT_ID  ` : your project ID

`  LOCATION  ` : the zone where your instance is located

`  INSTANCE_NAME  ` : the name of your instance

`  MACHINE_TYPE  ` : the machine type of your instance

`  RESERVATION_TYPE  ` : the type of reservation; must be `RESERVATION_ANY` or `RESERVATION_SPECIFIC`

`  RESERVATION_NAME  ` : the name of your reservation when using the `RESERVATION_SPECIFIC` type

  - For reservations in the same project, you can use the reservation ID.
  - For reservations in a different project, you must use the full reservation path. For example: ` projects/ PROJECT_ID /reservations/ RESERVATION_NAME  ` .

HTTP method and URL:

    POST https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances?instanceId=INSTANCE_NAME

Request JSON body:

    {
      "gce_setup": {
        "machine_type": "MACHINE_TYPE",
        "reservation_affinity": {
          "consume_reservation_type": "RESERVATION_TYPE",
          "key": "compute.googleapis.com/reservation-name",
          "values": ["RESERVATION_NAME"]
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
         "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances?instanceId=INSTANCE_NAME"

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
        -Uri "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances?instanceId=INSTANCE_NAME" | Select-Object -Expand Content

If successful, the response body contains an instance of [Operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

For more information, see the [`projects.locations.instances.create` REST API documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create) .

## Stop using your reservation

To stop using your reservation, you can [delete your reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-delete) .

If you want to continue using your reservation with other resources, but don't want your existing Agent Platform Workbench instance to use it, you must delete the instance.

## Billing

When consuming a Compute Engine reservation, you're billed for the following:

  - The Compute Engine resources, including any applicable committed use discounts (CUDs), at Compute Engine pricing. These charges have the label `goog-vertex-ai-product: workbench-instances` on the SKU. See [Compute Engine pricing](https://cloud.google.com/compute/all-pricing) .

  - Agent Platform Workbench management fees in addition to your infrastructure usage. See [Agent Platform Workbench pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#notebooks) .

## Troubleshoot

To find methods for diagnosing and resolving errors, related to using reservations with Agent Platform Workbench instances, see [Troubleshooting Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#reservations-instances) .

## What's next

  - To learn more about Compute Engine reservations, see [Reservations of Compute Engine zonal resources](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) .
