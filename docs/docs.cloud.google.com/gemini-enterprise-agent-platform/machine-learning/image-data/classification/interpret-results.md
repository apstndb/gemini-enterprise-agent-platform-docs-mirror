---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/interpret-results
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/interpret-results
title: Interpret prediction results from image classification models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

After requesting a prediction, Gemini Enterprise Agent Platform returns results based on your model's objective. AutoML single-label image classification predictions return a single label category and its corresponding confidence score. Multi- label classification predictions return multiple label categories and their corresponding confidence scores.

The confidence score communicates how strongly your model associates each class or label with a test item. The higher the number, the higher the model's confidence that the label should be applied to that item. You decide how high the confidence score must be for you to accept the model's results.

#### Score threshold slider

In the Google Cloud console, Gemini Enterprise Agent Platform provides a slider that's used to adjust the confidence threshold for all classes or labels, or an individual class or label. The slider is available on a model's detail page in the **Evaluate** tab. The confidence threshold is the confidence level that the model must have for it to assign a class or label to a test item. As you adjust the threshold, you can see how your model's precision and recall changes. Higher thresholds typically increase precision and lower recall.

#### Example batch prediction output

Batch AutoML image classification prediction output are stored as [JSON Lines](https://jsonlines.org/) files in Cloud Storage buckets. Each line of the JSON Lines file contains all annotation (label) categories and their corresponding confidence scores for a single image file.

> **Note** : The following JSON Lines example includes line breaks for readability. In your JSON Lines files, line breaks are included only after each each JSON object.

    {
      "instance": {"content": "gs://bucket/image.jpg", "mimeType": "image/jpeg"},
      "prediction": {
        "ids": [1, 2],
        "displayNames": ["cat", "dog"],
        "confidences": [0.7, 0.5]
      }
    }
