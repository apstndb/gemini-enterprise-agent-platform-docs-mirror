---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart
title: 'Quickstart: Create a Agent Platform Workbench instance by using the Google Cloud console'
description: Learn how to create a Agent Platform Workbench instance by using the {{dynamic_data.site_values.cloud_name_short}} console
data_source: docs.cloud.google.com
---

# Create an instance by using the Google Cloud console

Learn how to create a Gemini Enterprise Agent Platform Workbench instance and open JupyterLab by using the Google Cloud console. This page also describes how to stop, start, reset, or delete an instance.

## Before you begin

> **Note:** The [Notebooks API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest) lets you manage Agent Platform Workbench resources. For managing Agent Platform resources, see the [Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest) .

### Required roles

To get the permissions that you need to create and manage a Agent Platform Workbench instance, ask your administrator to grant you the [Notebooks Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.admin) ( `roles/notebooks.admin` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an instance

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  For **Name** , enter `my-instance` .

4.  Click **Create** .

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart#clean-up) .

## Open JupyterLab

After you create your instance, Agent Platform Workbench automatically starts the instance. The **Open JupyterLab** link is initially disabled while the instance is provisioning. Wait for the instance status to become active.

When the instance is ready to use, next to your instance's name, click **Open JupyterLab** .

Your Agent Platform Workbench instance opens JupyterLab.

## Open a new notebook file

1.  In JupyterLab, select **File \> New \> Notebook** .

2.  In the **Select kernel** dialog, select **Python 3** , and then click **Select** .
    
    Your new notebook file opens.

## Stop your instance

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the instance that you want to stop.

3.  Click square **Stop** .

## Start your instance

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the instance that you want to start.

3.  Click arrow\_right **Start** .

## Reset your instance

Resetting an instance forcibly wipes the memory contents of your instance and resets the instance to its initial state. To learn more about how resetting an instance works, see [Reset operation](https://docs.cloud.google.com/compute/docs/instances/suspend-stop-reset-instances-overview#resetting-instance) .

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the instance that you want to reset.

3.  Click ![Reset icon](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/reset.png) **Reset** , and then click **Reset** to confirm.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used on this page, follow these steps.

If you created a new project to learn about Agent Platform Workbench instances and you no longer need the project, then [delete the project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects) .

If you used an existing Google Cloud project, then delete the resources you created to avoid incurring charges to your account:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the row containing the instance that you want to delete.

3.  Click delete **Delete** . (Depending on the size of your window, the **Delete** button might be in the more\_vert options menu.)

4.  To confirm, click **Confirm** .

## What's next

1.  Read the [Introduction to Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/introduction) .
2.  To use a notebook to help you get started using Gemini Enterprise Agent Platform and other Google Cloud services, see [Agent Platform notebook tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials/jupyter-notebooks) .
