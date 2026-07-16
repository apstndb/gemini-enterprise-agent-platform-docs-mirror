---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/label-using-console
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/label-using-console
title: Label data using the Google Cloud console
description: Label data using the {{dynamic_data.site_values.cloud_name_short}} console.
data_source: docs.cloud.google.com
---

For image data, you can import labeled or unlabeled data and add labels using the Google Cloud console. You can also delete or add new labels to existing labeled datasets.

To learn how to import your data, see the *Prepare data* page of the data type and objective that you're working with on the [Training overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#data) page. Continue with the respective *Create dataset* page for your data type and objective.

After creating the dataset and importing the unlabeled data, you will be in **Browse** mode.  
  
![browse mode](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/datasets/images/browse-mode.png)

## How to add labels

Instructions for labeling objectives are provided here.

The images you have just imported in the dataset are unlabeled, as expected.

### Classification

When in Browse mode, and the dataset with the unlabeled images is selected, you can see your uploaded images.

1.  Click **Add new label** and enter your new label.
2.  Click **Done** .  
    Repeat for each label you want to add.
3.  Select the image you want to label.  
    The list of labels appears.
4.  Select the label you want to associate with the image.
5.  Click **Save** .

### Classification

When in **Browse** mode, and the dataset with the unlabeled images is selected, you can see your uploaded images.

1.  Click **Add new label** and enter your new label.
2.  Click **Done** .  
    Repeat for each label you want to add.
3.  Select the image you want to label.  
    The list of labels appears.
4.  Select the label you want to associate with the image.
5.  Click **Save** .
6.  You can view the labels applied to each image in the **Browse** tab. ![multi-labeled images](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/datasets/images/multi-labeled-images.png)

### Object detection

When in **Browse** mode, and the dataset with the unlabeled images is selected, you can see your uploaded images.

1.  Click **Add new label** and enter your new label.
2.  Click **Done** .  
    Repeat for each label you want to add.
3.  Select the image you want to label.
4.  The list of labels objects appears, if there are any.
5.  In the add annotation window, select the Add bounding box button to add an object bounding box to the image.  
    ![add bounding box to image](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/datasets/images/add-bounding-box-image.png)
6.  After drawing a bounding box, a list of labels to apply to the object will appear. Choose the appropriate label.  
    ![add label bounding boxed image](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/datasets/images/image-bounding-box-label.png)
7.  After you have added all labels and bounding boxes, click **Save** to update the image's annotations.  
    ![save added labels for bounding boxed image](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/datasets/images/image-save-bounding-box-labels.png)

## What's next

  - [Train your AutoML model using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-console) .

  - [Train your AutoML Edge model using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console) . (image only)

  - [Train your AutoML model using the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-api) .

  - [Train your AutoML Edge model using the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api) . (image only)
