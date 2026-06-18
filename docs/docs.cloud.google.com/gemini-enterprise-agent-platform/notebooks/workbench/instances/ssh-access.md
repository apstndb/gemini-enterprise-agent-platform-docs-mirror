---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/ssh-access
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/ssh-access
title: Use SSH to access JupyterLab
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This guide describes how to access your Gemini Enterprise Agent Platform Workbench instance's JupyterLab user interface by using SSH port forwarding.

## Set up SSH port forwarding and access the JupyterLab user interface

To set up [SSH port forwarding](https://cloud.google.com/solutions/connecting-securely#port-forwarding-over-ssh) , complete the following steps, and then access your JupyterLab session through a local browser:

1.  Run the following command by using the [Google Cloud CLI](https://docs.cloud.google.com/sdk/gcloud) in your preferred terminal or in [Cloud Shell](https://console.cloud.google.com/?cloudshell=true) :
    
        gcloud compute ssh \
            --project PROJECT_ID \
            --zone ZONE \
            INSTANCE_NAME \
            -- -L 8080:localhost:8080
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your [Google Cloud project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects)
      - `  ZONE  ` : the [zone](https://docs.cloud.google.com/compute/docs/regions-zones) where your instance is located
      - `  INSTANCE_NAME  ` : the name of your instance
    
    If using Cloud Shell to run the command, add a `-4` to the SSH flags to use IPv4 to connect. For example:
    
        -- -4 -L LOCAL_PORT:localhost:REMOTE_PORT

2.  Access your JupyterLab session through a local browser:
    
      - If you ran the command on your local machine, visit `https://localhost:8080` to access JupyterLab.
    
      - If you ran the command using [Cloud Shell](https://console.cloud.google.com/?cloudshell=true) , access JupyterLab through the ![](https://docs.cloud.google.com/static/shell/docs/images/web_preview.svg) Web Preview on port 8080.

## Why you might need to access your instance by using SSH

To get HTTPS access to JupyterLab, your Agent Platform Workbench instance must have access to a Google Cloud proxy service. When the instance starts, it attempts to register itself with the proxy service. If it fails to get proxy access, your instance prompts you to access JupyterLab through SSH.

The following are common reasons why you might not have HTTPS access to JupyterLab:

  - Your JupyterLab instance's proxy-mode metadata setting is incorrect.

  - Your network is configured to block internet access for the virtual machines (VMs) running JupyterLab notebooks.

  - Your instance doesn't have an external IP address.

  - Your [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) settings block access to [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) .

The following sections show how to resolve these issues.

For changes to take effect, you might need to restart the notebook's VM when attempting to resolve these issues.

## Your JupyterLab instance's proxy-mode metadata setting is incorrect

By default, when you create a Agent Platform Workbench instance, Agent Platform Workbench adds the proxy-mode metadata setting. If you change or remove the proxy-mode metadata setting, then the instance can't connect to the proxy service.

To add or modify the metadata to ensure there's a proxy-mode entry set to the correct value (for example: `project_editors` ), use the [`projects.locations.instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method in the Notebooks API or the [`gcloud workbench instances update`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/update) command in the Agent Platform SDK.

## The network is blocking internet access

Your JupyterLab instance accesses the proxy service through a public URL. If your Virtual Private Cloud network settings block access to the public internet or your firewall rules block egress traffic, you must use SSH to access your Agent Platform Workbench instance. If possible, you might want to work with your network and firewall administrators to allow access to your instance through the public internet.

## Your instance doesn't have an external IP address

You might have created your Agent Platform Workbench instance without an external IP address. If you need to change this, complete the following steps.

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click the name of the instance that you need to modify.

3.  Click **View VM details** .

4.  Click **Edit** .

5.  In the **Network interfaces** section, expand the network that you want to have an external IP address.

6.  Click the **External IP address** drop-down menu, and select the option that you want. To resolve this issue, you must not choose **None** .

7.  In the **Network interfaces** section, click **Done** .

8.  Click **Save** .

## VPC Service Controls settings are blocking access to Artifact Registry

To connect to the proxy service, your Agent Platform Workbench instance runs an agent that it downloads from Artifact Registry. Without this agent your instance cannot connect to the proxy service.

If your VPC Service Controls settings are blocking access to Artifact Registry, you must add the Artifact Registry service to the service perimeter of your VPC Service Controls. [Learn more about how service perimeters work and what services VPC Service Controls can be used to secure](https://docs.cloud.google.com/vpc-service-controls/docs/overview#capabilities) .

## Further troubleshooting

If you are still having trouble connecting, try reviewing the console logs for your virtual machine. These logs might help you discover why the Agent Platform Workbench instance is unable to register with the proxy service.

To access these logs, complete the following steps:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the instance that you want to troubleshoot.

3.  In **Logs** , click **Serial port 1 (console)** .

## What's next

For tips on resolving other issues, see the [troubleshooting section on Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#instances) .
