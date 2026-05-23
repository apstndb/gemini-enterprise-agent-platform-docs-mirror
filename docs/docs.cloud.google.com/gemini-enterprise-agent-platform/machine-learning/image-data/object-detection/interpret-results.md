---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/interpret-results
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/interpret-results
title: Interpret prediction results from image object detection models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

After requesting a prediction, Gemini Enterprise Agent Platform returns results based on your model's objective. AutoML image object detection prediction responses return all objects found in an image. Each found object has an annotation (label and normalized bounding box) with a corresponding confidence score. The bounding box is written as:

`"bboxes": [ [xMin, xMax, yMin, yMax], ...]`

Where `xMin, xMax` are the minimum and maximum x values and `yMin, yMax` are the minimum and maximum y values respectively.

#### Example batch prediction output

Batch AutoML image object detection prediction responses are stored as JSON Lines files in Cloud Storage buckets. Each line of the JSON Lines file contains all objects found in a single image file. Each found object has an annotation (label and normalized bounding box) with a corresponding confidence score.

> **Note: Zero coordinate values omitted.** When the API detects a coordinate ("x" or "y") value of 0, ***that coordinate is omitted in the JSON response*** . Thus, a response with a bounding poly around the entire image would be  
> **\[{},{"x": 1,"y": 1}\]** . For more information, see [Method: projects.locations.models.predict](https://cloud.google.com/automl/docs/reference/rest/v1/projects.locations.models/predict#boundingpoly) .

> **Note** : The following JSON Lines example includes line breaks for readability. In your JSON Lines files, line breaks are included only after each each JSON object.

**Important:** Bounding boxes are specified as:

`"bboxes": [ [xMin, xMax, yMin, yMax], ...]`

Where `xMin` and `xMax` are the minimum and maximum x values and `yMin` and `yMax` are the minimum and maximum y values respectively.

    {
      "instance": {"content": "gs://bucket/image.jpg", "mimeType": "image/jpeg"},
      "prediction": {
        "ids": [1, 2],
        "displayNames": ["cat", "dog"],
        "bboxes":  [
          [0.1, 0.2, 0.3, 0.4],
          [0.2, 0.3, 0.4, 0.5]
        ],
        "confidences": [0.7, 0.5]
      }
    }
