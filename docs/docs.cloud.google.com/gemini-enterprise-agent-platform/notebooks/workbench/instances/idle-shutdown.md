---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown
title: Idle shutdown
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Vertex AI Workbench instances shut down after a specified period of inactivity by default. This page describes the idle shutdown feature and how to change the default idle shutdown settings during instance creation.

## Overview

To help manage costs, Vertex AI Workbench instances shut down after being idle for a specific time period by default. You can change the amount of time or turn this feature off.

## Requirements for running idle shutdown

For idle shutdown to run, your Vertex AI Workbench instance must have guest attributes enabled. Guest attributes are enabled by default but if you've turned off guest attributes, you can enable guest attributes by setting the `enable-guest-attributes` metadata key to `true` . See [Update an instance's metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata#update) .

## Billing

While your instance is shut down, there are no CPU or GPU usage charges except for scheduled executions that run during the shutdown. For more information about scheduled executions, see [Scheduled executions run while instance is shut down](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown#executions) on this page.

Disk storage charges still apply while your instance is shut down. For more information, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/pricing#notebooks) .

## Turn off idle shutdown or change the default inactivity time period

Idle shutdown is enabled and set to shut down your instance after 180 inactive minutes by default.

You can change these settings when you [create an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) .

To turn off idle shutdown or to change the inactivity time period on an existing instance:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click the instance name.

3.  On the **Instance details** page, click the **Software and security** tab.

4.  In the **Modify software and security configuration** section:
    
      - To turn off idle shutdown, clear the check mark next to **Enable Idle Shutdown** .
    
      - To change the inactivity time period, in **Time of inactivity before shutdown (Minutes)** , change the number to the number of minutes of inactivity that you want. In the Google Cloud console, this setting can be set to any integer value from 10 to 1440.

5.  Click **Submit** .

## Manage idle shutdown using the gcloud CLI

Idle shutdown for Vertex AI Workbench instances is managed using the `metadata` flag. To enable idle shutdown, create an instance with the `idle-timeout-seconds` key in the metadata with the value set to the number of seconds.

    gcloud workbench instances create INSTANCE_NAME --metadata=idle-timeout-seconds=86400

To change the idle shutdown time period, update the value for the `idle-timeout-seconds` key in the metadata.

    gcloud workbench instances update INSTANCE_NAME --metadata=idle-timeout-seconds=43200

To turn off idle shutdown, use the following command:

    gcloud workbench instances update INSTANCE_NAME --metadata=idle-timeout-seconds=

## Manage idle shutdown on Terraform

Idle shutdown for workbench instances on Terraform is managed using the `idle-timeout-seconds` key in the metadata field.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

```terraform
resource "google_workbench_instance" "default" {
  name     = "workbench-instance-example"
  location = "us-central1-a"

  gce_setup {
    machine_type = "n1-standard-1"
    vm_image {
      project = "cloud-notebooks-managed"
      family  = "workbench-instances"
    }
    metadata = {
      idle-timeout-seconds = "10800"
    }
  }
}
```

## How idle shutdown works

Your instance shuts down when there is no kernel activity for the specified time period. For example, running a cell or new output printing to a notebook is activity that resets the idle shutdown timer. CPU usage doesn't reset the idle shutdown timer.

If you leave JupyterLab open and you don't interact with the window, the instance will shut down after the idle shutdown period.

By default, idle shutdown looks for activity in kernels running in the following addresses of the instance:

  - `127.0.0.1:8080/api/sessions`
  - `127.0.0.1:8080/api/terminals`
  - `127.0.0.1:8080/api/kernels`

> **Warning:** By default Jupyter runs on port 8080. If this port is changed, idle shutdown won't detect any kernel activity.

### Scheduled executions run while instance is shut down

If you have scheduled an execution of a notebook file in a Vertex AI Workbench instance that is shut down, the execution still runs on schedule.

## What's next

  - To run a notebook file on a schedule, even when your instance is shut down, see [schedule a notebook run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart) .
