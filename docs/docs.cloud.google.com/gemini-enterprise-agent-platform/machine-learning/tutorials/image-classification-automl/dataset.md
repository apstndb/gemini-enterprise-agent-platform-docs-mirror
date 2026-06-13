---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/dataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/dataset
title: 'Hello image data: Create an image classification dataset and import images'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Use the Google Cloud console to create an image classification dataset. After your dataset is created, use a CSV pointing to images in a public Cloud Storage bucket to import those images into the dataset.

This tutorial has several pages:

1.  [Set up your project and environment.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl)

2.  Create an image classification dataset, and import images.

3.  [Train an AutoML image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/training)

4.  [Evaluate and analyze model performance.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/error-analysis)

5.  [Deploy a model to an endpoint, and send a prediction.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/deploy-predict)

6.  [Clean up your project.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/cleanup)

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

## Image data input file

> **Key point** : A single dataset can be used for multiple objectives. This tutorial focuses on *image classification* (applying a label to an image), but the same data could be used for another objective, such as *object detection* (object identification and labeling).

The image files you use in this tutorial are from the flower dataset used in this [Tensorflow blog post](https://cloud.google.com/blog/products/gcp/how-to-classify-images-with-tensorflow-using-google-cloud-machine-learning-and-cloud-dataflow) . These input images are stored in a public Cloud Storage bucket. This publicly-accessible bucket also contains a CSV file you use for data import. This file has two columns: the first column lists an image's URI in Cloud Storage, and the second column contains the image's label. Below you can see some sample rows:

`gs://cloud-samples-data/ai-platform/flowers/flowers.csv` :

    gs://cloud-samples-data/ai-platform/flowers/daisy/10559679065_50d2b16f6d.jpg,daisy
    gs://cloud-samples-data/ai-platform/flowers/dandelion/10828951106_c3cd47983f.jpg,dandelion
    gs://cloud-samples-data/ai-platform/flowers/roses/14312910041_b747240d56_n.jpg,roses
    gs://cloud-samples-data/ai-platform/flowers/sunflowers/127192624_afa3d9cb84.jpg,sunflowers
    gs://cloud-samples-data/ai-platform/flowers/tulips/13979098645_50b9eebc02_n.jpg,tulips

## Create an image classification dataset and import data

Visit the [Google Cloud console](https://console.cloud.google.com/vertex-ai/) to begin the process of creating your dataset and training your image classification model.

When prompted, make sure to select the project that you used for your Cloud Storage bucket.

1.  From the Get started with Gemini Enterprise Agent Platform page, click **Create dataset** .
    
    ![Agent Platform dashboard](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/images/create-dataset.png)

2.  Specify a name for this dataset (optional).

3.  In the Image tab of the "Select a data type and objective" section, choose the radio\_button\_checked **Image classification (Single-label)** radio option. In the Region drop-down menu select **US Central** .
    
    ![New dataset window](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/images/create-dataset-objective.png)

4.  Select **Create** to create the empty dataset. After selecting Create you will advance to the data import window.

5.  Select the radio\_button\_checked **Select import files from Cloud Storage** and specify the Cloud Storage URI of the CSV file with the image location and label data. For this quickstart, the CSV file is at `gs://cloud-samples-data/ai-platform/flowers/flowers.csv` . Copy and paste the following into the "Import file path" field:
    
      - ``` 
        cloud-samples-data/ai-platform/flowers/flowers.csv
        ```
    
    ![Select file import window](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/images/select-import-file.png)

6.  Click **Continue** to begin image import. The import process takes a few minutes. When it completes, you are taken to the next page that shows all of the images identified for your dataset, both labeled and unlabeled images.
    
    > When using the indicated flower dataset, you will see several warning alerts. This is purposeful, to show you error messages you may encounter with your own data.

## What's next

Follow the [next page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/training) to start an AutoML model training job.
