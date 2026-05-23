---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/cleanup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/cleanup
title: 'Hello custom training: Clean up your project'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page guides you through cleaning up the Google Cloud resources that you created to train your image classification model and serve predictions from it.

This tutorial has several pages:

1.  [Setting up your project and environment.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom)

2.  [Training a custom image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/training)

3.  [Serving predictions from a custom image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/serving)

4.  Cleaning up your project.

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

The rest of this document assumes that you are using the same Cloud Shell environment that you created when following the [first page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom) . If your original Cloud Shell session is no longer open, you can return to the environment by doing the following:

1.  In the Google Cloud console, activate Cloud Shell.

2.  In the Cloud Shell session, run the following command:
    
        cd hello-custom-sample

## Delete Vertex AI resources

This section describes how to delete all of the Vertex AI resources that you created for this tutorial.

### Undeploy your model from your endpoint

This section describes how to undeploy your model from your endpoint. You can think about this action as a way of disconnecting your model from your endpoint.

You must follow this section before you can [delete your endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/cleanup#delete-endpoint) or [delete your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/cleanup#delete-model) .

1.  In the Google Cloud console, in the Vertex AI section, go to the **Endpoints** page.

2.  Click `hello_custom` to go to the endpoint details page.

3.  On the row for your model, `hello_custom` , click **Undeploy model delete** .

4.  In the **Undeploy model from endpoint** dialog, click **Undeploy** .

### Delete your endpoint

Before you delete an endpoint, you must [undeploy your model from your endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/cleanup#undeploy-model) . After you've deleted your endpoint, you won't be able to re-use that endpoint name for up to 7 days.

After you've undeployed your model from the endpoint, do the following to delete your endpoint:

1.  In the Google Cloud console, in the Vertex AI section, go to the **Endpoints** page.

2.  Find your the row of your endpoint, `hello_custom` , again. On that row, click **View more more\_vert** . Then click **Remove endpoint** .

3.  In the **Remove endpoint** dialog, click **Confirm** .

### Delete your model

Before you follow this section, you must [undeploy your model from your endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/cleanup#undeploy-model) . Afterward, do the following to delete your model:

1.  In the Google Cloud console, in the Vertex AI section, go to the **Models** page.

2.  Find your the row of your model, `hello_custom` . On that row, click **View more more\_vert** . Then click **Delete model** .

3.  In the **Delete model** dialog, click **Delete** .

### Delete your custom training pipeline and job

Your training pipeline and custom job are just records of the training that happened earlier. If you want to delete your custom job, do the following:

1.  In the Google Cloud console, in the Vertex AI section, go to the **Training pipelines** page.

2.  Find your the row of your training pipeline, `hello_custom` . On that row, click **View more more\_vert** . Then click **Delete training pipeline** .

3.  In the **Delete training job** dialog, click **Delete** .

4.  To go to the **Custom jobs** page, click **Custom job** in the Google Cloud console, or click the following link:

5.  Find your the row of your custom job, `hello_custom-custom-job` . On that row, click **View more more\_vert** . Then click **Delete custom job** .

6.  In the **Delete training job** dialog, click **Delete** .

## Clean up your Cloud Shell session

Cloud Shell incurs no charges, and it [automatically deletes your home disk after a period of inactivity](https://docs.cloud.google.com/shell/docs/limitations) . However, if you plan to use Cloud Shell for other purposes in the near future, you might want to manually remove the files that you created for this tutorial.

In your Cloud Shell session, run the following commands:

    cd ..
    rm -rf hello-custom-sample

## Delete your Cloud Storage bucket

In your Cloud Shell session, run the following command:

    gcloud storage rm gs://BUCKET_NAME --recursive --continue-on-error

Replace BUCKET\_NAME with the name of the Cloud Storage bucket that you created when reading the [first page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom) .

## Delete your Cloud Run function

In your Cloud Shell session, run the following command:

    gcloud functions delete classify_flower --region=us-central1 --quiet

## What's next

  - To learn about additional ways to train ML models on Vertex AI, try one of the other [Vertex AI tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials) .

  - Read an [overview of how Vertex AI works](https://docs.cloud.google.com/vertex-ai/docs/start/introduction-unified-platform) .
