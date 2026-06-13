---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/cleanup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/cleanup
title: 'Hello image data: Clean up your project'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Clean up the Google Cloud resources that you created to train your image classification model and get predictions from it. Follow these steps to avoid incurring unexpected charges from some of the resources.

This tutorial has several pages:

1.  [Set up your project and environment.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl)

2.  [Create an image classification dataset, and import images.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/dataset)

3.  [Train an AutoML image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/training)

4.  [Evaluate and analyze model performance.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/error-analysis)

5.  [Deploy a model to an endpoint, and send a prediction.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/deploy-predict)

6.  Clean up your project.

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

## Delete Gemini Enterprise Agent Platform resources

This section describes how to undeploy your model, and then delete the following project resources: endpoint, model, dataset, and Cloud Storage bucket.

### Undeploy your model

Before you can delete your model and endpoint, you must undeploy the model.

1.  In the Google Cloud console, in the Gemini Enterprise Agent Platform section, go to the **Training** page.

2.  Select your trained AutoML model. This takes you to the **Evaluate** tab.

3.  Click the **Deploy & test** tab.

4.  Find your model. On your model's row, click the three vertical dots more\_vert , then click **Undeploy model** .

5.  In **Undeploy model** , click **Confirm** .

### Delete your endpoint

1.  In the Google Cloud console, in the Gemini Enterprise Agent Platform section, go to the **Endpoints** page.

2.  Find your endpoint, `hello_automl_image` . On that row, click the three vertical dots more\_vert , then click **Remove endpoint** .

3.  In **Remove endpoint** , click **Confirm** .

### Delete your model

1.  In the Google Cloud console, in the Gemini Enterprise Agent Platform section, go to the **Models** page.

2.  Find your model. On that row, click the three vertical dots more\_vert , then click **Delete model** .

3.  In **Delete model and all of its associated versions** , click **Delete** .

### Delete your dataset

1.  In the Google Cloud console, in the Gemini Enterprise Agent Platform section, go to the **Datasets** page.

2.  Find your dataset. On that row, click the three vertical dots more\_vert , then click **Delete dataset** .

3.  In **Delete dataset** , click **Delete** .

## Clean up your Cloud Shell session

Cloud Shell incurs no charges, and it [automatically deletes your home disk after a period of inactivity](https://docs.cloud.google.com/shell/docs/limitations) .

## Delete your Cloud Storage bucket

1.  In the Google Cloud console, go to the Cloud Storage **Buckets** page.
2.  Click the checkbox for the bucket that you want to delete.
3.  To delete the bucket, click delete **Delete** , and then follow the instructions.

## What's next

  - To learn about additional ways to train ML models on Gemini Enterprise Agent Platform, try one of the other [Gemini Enterprise Agent Platform tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials) .

  - Read an [overview of how Gemini Enterprise Agent Platform works](https://docs.cloud.google.com/vertex-ai/docs/start/introduction-unified-platform) .
