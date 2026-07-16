---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl
title: 'Hello image data: Set up your project and environment'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

If you plan to use the Agent Platform SDK for Python, make sure that the service account initializing the client has the [Gemini Enterprise Agent Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.serviceAgent) ( `roles/aiplatform.serviceAgent` ) IAM role.

You'll set up your Google Cloud project to use Gemini Enterprise Agent Platform. Then create a Cloud Storage bucket and copy image files to use for training an AutoML image classification model.

This tutorial has several pages:

1.  Set up your project and environment.

2.  [Create an image classification dataset, and import images.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/dataset)

3.  [Train an AutoML image classification model.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/training)

4.  [Evaluate and analyze model performance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/error-analysis)

5.  [Deploy a model to an endpoint, and send a prediction.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/deploy-predict)

6.  [Clean up your project.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/cleanup)

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

## Before you begin

Complete the following steps before using Gemini Enterprise Agent Platform functionality.

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
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
        gcloud services enable iam.googleapis.com  compute.googleapis.com notebooks.googleapis.com storage.googleapis.com aiplatform.googleapis.com

7.  Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/aiplatform.user, roles/storage.admin`
    
        gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE
    
    Replace the following:
    
      - `  PROJECT_ID  ` : Your project ID.
      - `  USER_IDENTIFIER  ` : The identifier for your user account. For example, `myemail@example.com` .
      - `  ROLE  ` : The IAM role that you grant to your user account.

## What's next

Follow the [next page of this tutorial](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/dataset) to use the Google Cloud console to create an image classification dataset and import images hosted in a public Cloud Storage bucket.
