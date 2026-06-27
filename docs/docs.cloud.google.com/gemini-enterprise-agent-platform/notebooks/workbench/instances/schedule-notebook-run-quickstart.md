---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart
title: 'Quickstart: Schedule a notebook run'
description: Shows how to schedule a notebook run in a Agent Platform Workbench instance
data_source: docs.cloud.google.com
---

# Schedule a notebook run

This page shows you how to use the Gemini Enterprise Agent Platform Workbench executor to run a Python notebook file on an hourly schedule.

## Before you begin

### Required roles

To get the permissions that you need to create a Agent Platform Workbench instance and open JupyterLab, ask your administrator to grant you the following IAM roles on the project:

  - [Notebooks Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.admin) ( `roles/notebooks.admin` )
  - [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `roles/iam.serviceAccountUser` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an instance and example notebook file

1.  [Create an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart#create-instance) .
    
    > **Note:** If you choose JupyterLab 4 as the JupyterLab version for the instance, then the instance uses the Gemini Enterprise Agent Platform scheduler to schedule the notebook executions.

2.  [Open JupyterLab](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart#open-jupyterlab) .

3.  [Open a new notebook file](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart#open-a-new-notebook-file) .

4.  In the first cell of the notebook file, enter the following:
    
        # Import datetime
        import datetime
        
        # Get the time and print it
        datetime.datetime.now()
        print(datetime.datetime.now())

5.  To make sure your notebook file is saved, select **File \> Save Notebook** .

## Grant permissions to the instance's service account

To ensure that your instance's service account has the necessary permissions to interact with the Agent Platform Workbench executor, ask your administrator to grant the following IAM roles to your instance's service account on the project:

> **Important:** You must grant these roles to your instance's service account, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

  - [Notebooks Runner](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.runner) ( `roles/notebooks.runner` )
  - [Storage Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.admin) ( `roles/storage.admin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give your instance's service account the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Limitations

Consider the following limitation when scheduling a notebook run in a JupyterLab 4 instance:

  - When scheduling a notebook run in JupyterLab 4, Agent Platform Workbench stores a copy of the notebook in its current state in Cloud Storage, and then runs this copy of the notebook according to the schedule. If you edit the original notebook, you must create a new schedule to run the updated version of the notebook.

## Schedule a run

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your instance name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

3.  In the folder **File Browser** , double-click the example notebook file to open it.

4.  Click the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-executor.png) **Execute** button.

5.  In the **Submit notebooks to Executor** dialog, in the **Type** field, select **Schedule-based recurring executions** .
    
    By default, the executor runs your notebook file every hour at the `00` minute of the hour.

6.  In **Advanced options** , enter a name for your bucket in the **Cloud Storage bucket** field, and then click **Create and select** . The executor stores your notebook output in the Cloud Storage bucket.

7.  Click **Submit** .
    
    Your notebook file runs automatically on the schedule that you set.

> **Note:** If your instance is shut down, the executor still runs your notebook file on schedule.

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart#clean-up) .

## View, share, and import an executed notebook file

By using your instance's JupyterLab interface, you can view your notebook output, share the results with others, and import the executed notebook file into JupyterLab.

> **Note:** To use the Google Cloud console to view and share execution results, on the [**Executions**](https://console.cloud.google.com/agent-platform/workbench/executions) page, click **View result** .

### View the execution results

1.  In JupyterLab's navigation menu, click the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-executor.png) **Notebook Executor** button.

2.  Click the **Executions** tab.

3.  Under the execution that you want to view, click **View result** .
    
    The executor opens your result in a new browser tab.

### Share the execution results

1.  In your instance's JupyterLab user interface, in the navigation menu, click the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-executor.png) **Notebook Executor** button.

2.  Click the **Executions** tab.

3.  Next to the execution that you want to share, click the more\_vert options menu, and select **Share execution result** .

4.  Follow the directions in the dialog to grant users access to the execution result.

### Import the executed notebook into JupyterLab

1.  In your instance's JupyterLab user interface, in the navigation menu, click the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-executor.png) **Notebook Executor** button.

2.  Click the **Executions** tab.

3.  Next to the execution that you want to import, click the more\_vert options menu, and select **Import executed notebook** .

4.  If the **Select Kernel** dialog appears, select the kernel that you want to open the notebook.
    
    The executor opens the executed notebook file in JupyterLab, and stores this notebook file in the JupyterLab File Browser in a folder named **imported\_notebook\_jobs** .

## View or delete a schedule

You can view and delete schedules by using either the Google Cloud console or your instance's JupyterLab user interface.

### View a schedule

View a schedule to see the frequency settings of the schedule or to view the five most recent results of the notebook file execution.

### Console

1.  In the Google Cloud console, go to the **Schedules** page.

2.  For the schedule that you want to view, click its schedule name.
    
    On the **Schedule details** page, you can view the schedule's last five executions.

3.  Next to an execution name, click **View result** to open the executed notebook file.
    
    The executor opens your result in a new browser tab.

### JupyterLab

1.  In your instance's JupyterLab user interface, in the navigation menu, click the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-executor.png) **Notebook Executor** button.

2.  Click the **Schedules** tab.

3.  Under the execution that you want to view, click **View latest execution result** .
    
    The executor opens your result in a new browser tab.

### Delete a schedule

Deleting a schedule doesn't delete the executions that were generated from that schedule.

### Console

1.  In the Google Cloud console, go to the **Schedules** page.

2.  Select the schedule that you want to delete.

3.  Click delete **Delete** .

### JupyterLab

1.  In your instance's JupyterLab user interface, in the navigation menu, click the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-executor.png) **Notebook Executor** button.

2.  Click the **Schedules** tab.

3.  Click the schedule name. The **Schedule details** page for that schedule opens in the Google Cloud console.

4.  Click delete **Delete** .

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used on this page, follow these steps.

### Delete the instance

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the instance that you want to delete.

3.  Click delete **Delete** .

### Delete the project

If you used resources outside of your Agent Platform Workbench instance, such as the Cloud Storage bucket required for creating a schedule, you might want to delete your project to avoid incurring additional charges.

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

## What's next

> To see an example of how to schedule a notebooks run as part of a more comprehensive workflow, run the "Train a multi-class classification model for ads-targeting" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/ads_targetting/training-multi-class-classification-model-for-ads-targeting-usecase.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fads_targetting%2Ftraining-multi-class-classification-model-for-ads-targeting-usecase.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fads_targetting%2Ftraining-multi-class-classification-model-for-ads-targeting-usecase.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/ads_targetting/training-multi-class-classification-model-for-ads-targeting-usecase.ipynb)
