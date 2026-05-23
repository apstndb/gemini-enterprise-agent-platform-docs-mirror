---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/prerequisites
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/prerequisites
title: Prerequisites
description: Create your {{dynamic_data.site_values.cloud_name_short}} account and project to prepare for a tutorial on using the Agent Platform SDK for Python to train a model.
data_source: docs.cloud.google.com
---

Before you start this tutorial, you need a Google Cloud account and a Google Cloud project that's enabled for billing. The following steps walk you through creating these prerequisites.

## Create a Google Cloud account

If you don't have a Google Cloud account, go to <https://console.cloud.google.com/> to create one.

## Create a Google Cloud project

If you have a Google Cloud project that you want to use for this tutorial, you can skip this step and continue with [Find your project ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/prerequisites#find-project-id) . Otherwise, follow the steps in [Set up a project](https://docs.cloud.google.com/vertex-ai/docs/start/cloud-environment#set_up_a_project) . For more information, see [Creating and managing projects](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects) .

## Find your Google Cloud project ID

A Google Cloud project ID is a unique string used to differentiate your project from all others in Google Cloud. You use your Google Cloud project ID in this tutorial to initialize the Agent Platform SDK for Python. If you know your Google Cloud project ID, you can skip this step.

To locate your Google Cloud project ID:

1.  In the Google Cloud console, click the list of projects in the top menu.

2.  In the dialog that appears, locate your project. If you don't see your project, you might need to choose a different [organization](https://docs.cloud.google.com/resource-manager/docs/creating-managing-organization) . Select **No organization** to view projects that aren't associated with an organization or that are associated with an organization that you don't have access to view.
    
    To find a Google Cloud project that you haven't accessed recently, you might need to click **All** instead of **Recent** or **Starred** .

3.  After you locate your project, make a note of its Google Cloud project ID in the **ID** column.

![Fine your project ID](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/images/find-project-id.png)
