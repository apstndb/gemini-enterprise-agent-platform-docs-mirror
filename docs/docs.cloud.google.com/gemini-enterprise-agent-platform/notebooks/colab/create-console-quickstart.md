---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-console-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-console-quickstart
title: 'Quickstart: Create a Colab Enterprise notebook by using the Google Cloud console'
description: Learn how to create a Colab Enterprise notebook by using the {{dynamic_data.site_values.cloud_name_short}} console
data_source: docs.cloud.google.com
---

# Create a Colab Enterprise notebook by using the Google Cloud console

Learn how to create a Colab Enterprise notebook and run its code on a default runtime by using the Google Cloud console. This page also describes how to rename, import, and delete a notebook.

## Before you begin

### Required roles

To get the permissions that you need to create a Colab Enterprise notebook and run the notebook's code on a runtime, ask your administrator to grant you the Colab Enterprise User ( [`roles/aiplatform.colabEnterpriseUser`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.colabEnterpriseUser) ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

> One or more of the required roles includes the `dataform.repositories.list` permission. Users who are granted the `dataform.repositories.list` permission or the [Code Creator ( `roles/dataform.codeCreator` )](https://docs.cloud.google.com/dataform/docs/access-control#dataform.codeCreator) role in a project can list the names of code assets in that project by using the Dataform API or the Dataform command-line interface (CLI). Non-administrators using BigQuery Studio can only see code assets that they created or that were shared with them.

## Create a notebook

To create a Colab Enterprise notebook by using the Google Cloud console:

1.  In the Google Cloud console, go to the Colab Enterprise **My notebooks** page.

2.  In the **Region** menu, select the region where you want to create your notebook.

3.  Click add\_box **New notebook** .
    
    Agent Platform creates and opens your notebook.

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/colab/create-console-quickstart#clean-up) .

## Run code in a default runtime

To run a Colab Enterprise notebook's code on the default runtime, do the following:

1.  In the Google Cloud console, go to the Colab Enterprise **My notebooks** page.

2.  In the **Region** menu, select the region that contains your notebook.

3.  Click the notebook that you want to open.

4.  Hold the pointer over the code cell that you want to run, and then click the ![](https://docs.cloud.google.com/static/colab/images/icon-run-cell.png) **Run cell** button.

5.  If this is your first time connecting to a runtime with end-user credentials enabled, a **Sign in** dialog appears.
    
    > The default runtime has end-user credentials enabled to make it easier to [run code that interacts with Google Cloud](https://docs.cloud.google.com/colab/docs/run-code-adc) .
    
    To grant Colab Enterprise access to your user credentials, complete the following steps:
    
    1.  In the **Sign in** dialog, click your user account.
    
    2.  Select **See, edit, configure, and delete your Google Cloud data...** to grant Colab Enterprise access to your user credentials.
        
        ![The checkbox is next to a statement that says, "See, edit, configure, and delete your Google Cloud data and see the email address for your Google Account."](https://docs.cloud.google.com/static/colab/images/access-checkbox.png)
    
    3.  Click **Continue** .

After your runtime starts, Colab Enterprise connects to the runtime and runs the code in the cell.

## Rename your notebook

To rename a Colab Enterprise notebook:

1.  In the Google Cloud console, go to the Colab Enterprise **My notebooks** page.

2.  In the **Region** menu, select the region that contains your notebook.

3.  Next to the notebook that you want to rename, click the more\_vert **Actions** menu, and then select **Rename** .

4.  In the **Rename notebook** dialog, change the name of the notebook, and then click **Rename** .

## Import a notebook

To import a notebook into Colab Enterprise:

1.  In the Google Cloud console, go to the Colab Enterprise **My notebooks** page.

2.  In the **Region** menu, select the region where you want to import your notebook.

3.  Click upload **Import** .

4.  In the **Import notebooks** dialog, select an **Import source** .

5.  If you selected:
    
      - **Your computer** , navigate to and select a notebook file to import.
      - **Cloud Storage** , navigate to and select a notebook in Cloud Storage.
      - **URL** , enter the URL of the notebook file to import.
    
    > The notebook must be fewer than 20 MB.

6.  To add another notebook, click add\_box **Add notebook** .

7.  After you've added the notebooks that you want to import, click **Import** .
    
    Colab Enterprise imports your notebook files.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used on this page, follow these steps.

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

### Delete the project

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

### Delete your notebook

To delete a Colab Enterprise notebook:

1.  In the Google Cloud console, go to the Colab Enterprise **My notebooks** page.

2.  In the **Region** menu, select the region that contains the notebook that you want to delete.

3.  Next to the notebook that you want to delete, click the more\_vert **Actions** menu, and then select delete **Delete notebook** .

4.  In the **Delete notebook** dialog, click **Confirm** .

## What's next

  - Read the [Introduction to Colab Enterprise](https://docs.cloud.google.com/colab/docs/introduction) .

  - To find a notebook that can help you get your project started quickly, see the [notebook gallery](https://console.cloud.google.com/agent-platform/colab/notebook-gallery) .

  - [Connect to a runtime](https://docs.cloud.google.com/colab/docs/connect-to-runtime) .
