---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/create-annotation-set
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/create-annotation-set
title: Create an annotation set for AutoML image training
description: Describes how to create annotation sets.
data_source: docs.cloud.google.com
---

An *annotation set* is a set of labels that you apply to the data of an unstructured dataset for model training. Annotation sets are associated with a data type and model objective (for example, `image/classification` ). You create an annotation set for image data types.

To learn how to apply the labels of your annotation set to your dataset's data, see [Label using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/label-using-console) .

## How to create an annotation set

When you create a dataset in Gemini Enterprise Agent Platform, if the imported CSV or [JSON Lines](https://jsonlines.org/) file contains labels, Gemini Enterprise Agent Platform automatically creates an annotation set and assigns it the objective that you selected for the dataset. For example, if you select *image* as the data type and *Classification* as the objective, the annotation set `  DATASET_NAME \_icn ` is created, where "icn" stands for "image classification."

If the dataset is already created and you want to add an annotation set or additional annotation sets, you can create them in the Google Cloud console as detailed in the following section.

## Create a new annotation set

You can create a new annotation set for an existing dataset in the Google Cloud console only.

1.  In the Google Cloud console, go to the Gemini Enterprise Agent Platform **Datasets** page.

2.  Click the dataset that you want to create an annotation set for.
    
    The dataset appears.
    
    ![Agent Platform dashboard](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/datasets/images/dataset-appears-vcn.png)

3.  In the selector box next to the name of your dataset, select **Create annotation set** .

4.  In the **Create annotation set** pane, enter a name for the annotation set.

5.  Select the model objective.

6.  Click **Create** .
    
    The dataset view appears with your new annotation set displayed. You are now ready to apply the labels of your new annotation set to your data.

## What's next

  - Edit, or add labels to your dataset [using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/label-using-console) .
