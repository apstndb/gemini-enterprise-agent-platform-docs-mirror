---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-automl/setup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-automl/setup
title: 'Hello tabular data: Set up your project and environment'
description: Set up your project and environment for a tutorial that guides you through building a binary classification model from tabular data using Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This tutorial walks you through the required steps to train and get predictions from your tabular data model in the Google Cloud console. If you plan to use the Agent Platform SDK for Python, make sure that the service account initializing the client has the [Gemini Enterprise Agent Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.serviceAgent) ( `roles/aiplatform.serviceAgent` ) IAM role.

For this part of the tutorial, you set up your Google Cloud project to use Gemini Enterprise Agent Platform and a Cloud Storage bucket that contains the documents for training your AutoML model.

## Set up your project and environment

1.  In the Google Cloud console, go to the project selector page.

2.  Select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `roles/resourcemanager.projectCreator` ), which contains the `resourcemanager.projects.create` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    > **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  Open [Cloud Shell](https://docs.cloud.google.com/shell/docs/launching-cloud-shell-editor) . Cloud Shell is an interactive shell environment for Google Cloud that lets you manage your projects and resources from your web browser.

5.  In the Cloud Shell, set the current project to your Google Cloud project ID and store it in the `projectid` shell variable:
    
    ``` 
      gcloud config set project PROJECT_ID &&
      projectid=PROJECT_ID &&
      echo $projectid
    ```
    
    Replace PROJECT\_ID with your project ID. You can locate your project ID in the Google Cloud console. For more information, see [Find your project ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/prerequisites#find-project-id) .

6.  Enable the IAM, Compute Engine, Notebooks, Cloud Storage, and Agent Platform APIs:
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
        gcloud services enable iam.googleapis.com  compute.googleapis.com notebooks.googleapis.com storage.googleapis.com aiplatform.googleapis.com

7.  Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/aiplatform.user, roles/storage.admin`
    
        gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE
    
    Replace the following:
    
      - `  PROJECT_ID  ` : Your project ID.
      - `  USER_IDENTIFIER  ` : The identifier for your user account. For example, `myemail@example.com` .
      - `  ROLE  ` : The IAM role that you grant to your user account.

## What's next

Follow the [next page of this tutorial](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-automl/dataset-train) to create a tabular dataset and train a classification model.
