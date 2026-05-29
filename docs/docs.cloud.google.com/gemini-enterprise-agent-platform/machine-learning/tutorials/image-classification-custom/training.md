---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/training
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/training
title: 'Hello custom training: Train a custom image classification model'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> To learn more, run the following notebooks in the environment of your choice:
> 
>   - "Use the for Python to train and deploy a custom image classification model for batch prediction.":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb)
> 
>   - "Use the for Python to train and deploy a custom image classification model for online prediction.":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb)

This page shows you how to run a TensorFlow Keras training application on Vertex AI. This particular model trains an image classification model that can classify flowers by type.

This tutorial has several pages:

1.  [Setting up your project and environment.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom)

2.  Training a custom image classification model.

3.  [Serving predictions from a custom image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/serving)

4.  [Cleaning up your project.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/cleanup)

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

The rest of this document assumes that you are using the same Cloud Shell environment that you created when following the [first page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom) . If your original Cloud Shell session is no longer open, you can return to the environment by doing the following:

1.  In the Google Cloud console, activate Cloud Shell.

2.  In the Cloud Shell session, run the following command:
    
        cd hello-custom-sample

## Run a custom training pipeline

This section describes using the training package that you uploaded to Cloud Storage to run an Vertex AI custom training pipeline.

1.  In the Google Cloud console, in the Vertex AI section, go to the **Training pipelines** page.

2.  Click **add\_box Create** to open the **Train new model** pane.

3.  On the **Choose training method** step, do the following:
    
    1.  In the **Dataset** drop-down list, select **No managed dataset** . This particular training application loads data from the [TensorFlow Datasets](https://www.tensorflow.org/datasets/) library rather than a managed Vertex AI dataset.
    
    2.  Ensure that **Custom training (advanced)** is selected.
    
    Click **Continue** .

4.  On the **Model details** step, in the **Name** field, enter `hello_custom` . Click **Continue** .

5.  On the **Training container** step, provide Vertex AI with information it needs to use the training package that you uploaded to Cloud Storage:
    
    1.  Select **Prebuilt container** .
    
    2.  In the **Model framework** drop-down list, select **TensorFlow** .
    
    3.  In the **Model framework version** drop-down list, select **2.3** .
    
    4.  In the **Package location** field, enter `cloud-samples-data/ai-platform/hello-custom/hello-custom-sample-v1.tar.gz` .
    
    5.  In the **Python module** field, enter `trainer.task` . `trainer` is the name of the Python package in your tarball, and `task.py` contains your training code. Therefore, `trainer.task` is the name of the module that you want Vertex AI to run.
    
    6.  In the **Model output directory** field, click **Browse** . Do the following in the **Select folder** pane:
        
        1.  Navigate to your Cloud Storage bucket.
        
        2.  Click **Create new folder create\_new\_folder** .
        
        3.  Name the new folder `output` . Then click **Create** .
        
        4.  Click **Select** .
        
        Confirm that field has the value `gs:// BUCKET_NAME /output` , where BUCKET\_NAME is the name of your Cloud Storage bucket.
        
        This value gets passed to Vertex AI in the [`baseOutputDirectory` API field](https://docs.cloud.google.com/vertex-ai/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) , which sets several environment variables that your training application can access when it runs.
        
        For example, when you set this field to `gs:// BUCKET_NAME /output` , Vertex AI sets the `AIP_MODEL_DIR` environment variable to `gs:// BUCKET_NAME /output/model` . At the end of training, Vertex AI uses any artifacts in the `AIP_MODEL_DIR` directory to create a model resource.
        
        Learn more about the [environment variables set by this field](https://docs.cloud.google.com/vertex-ai/machine-learning/training/code-requirements#environment-variables) .
    
    Click **Continue** .

6.  On the optional **Hyperparameters** step, make sure that the **Enable hyperparameter tuning** checkbox is cleared. This tutorial does not use hyperparameter tuning. Click **Continue** .

7.  On the **Compute and pricing** step, allocate resources for the custom training job:
    
    1.  In the **Region** drop-down list, select **us-central1 (Iowa)** .
    
    2.  In the **Machine type** drop-down list, select **n1-standard-4** from the **Standard** section.
    
    Do not add any accelerators or worker pools for this tutorial. Click **Continue** .

8.  On the **Prediction container** step, provide Vertex AI with information it needs to serve predictions:
    
    1.  Select **Prebuilt container** .
    
    2.  In the **Prebuilt container settings** section, do the following:
        
        1.  In the **Model framework** drop-down list, select **TensorFlow** .
        
        2.  In the **Model framework version** drop-down list, select **2.3** .
        
        3.  In the **Accelerator type** drop-down list, select **None** .
        
        4.  Confirm that **Model directory** field has the value `gs:// BUCKET_NAME /output` , where BUCKET\_NAME is the name of your Cloud Storage bucket. This matches the **Model output directory** value that you provided in a previous step.
    
    3.  Leave the fields in the **Predict schemata** section blank.

9.  Click **Start training** to start the custom training pipeline.

You can now view your new *training pipeline* , which is named `hello_custom` , on the **Training** page. (You might need to refresh the page.) The training pipeline does two main things:

1.  The training pipeline creates a *custom job* resource named `hello_custom-custom-job` . After a few moments, you can view this resource on the **Custom jobs** page of the **Training** section:
    
    The custom job runs the training application using the computing resources that you specified in this section.

2.  After the custom job completes, the training pipeline finds the artifacts that your training application creates in the `output/model/` directory of your Cloud Storage bucket. It uses these artifacts to create a *model* resource.

### Monitor training

To view training logs, do the following:

1.  In the Google Cloud console, in the Vertex AI section, go to the **Custom jobs** page.

2.  To view details for the `CustomJob` that you just created, click `hello_custom-custom-job` in the list.

3.  On the job details page, click **View logs** .

### View your trained model

When the custom training pipeline completes, you can find the trained model in the Google Cloud console, in the Vertex AI section, on the **Models** page.

The model has the name `hello_custom` .

## What's next

Follow the [next page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/serving) to serve predictions from your trained ML model.
