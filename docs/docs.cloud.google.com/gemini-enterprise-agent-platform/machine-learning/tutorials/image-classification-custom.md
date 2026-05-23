---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom
title: 'Hello custom training: Set up your project and environment'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page walks through setting up your Google Cloud project to use Vertex AI and downloading some TensorFlow code for training. You will also download code for a web app that gets predictions.

This tutorial has several pages:

1.  Setting up your project and environment.

2.  [Training a custom image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/training)

3.  [Serving predictions from a custom image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/serving)

4.  [Cleaning up your project.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/cleanup)

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

## Before you begin

Throughout this tutorial, use Google Cloud console and [Cloud Shell](https://docs.cloud.google.com/shell/docs) to interact with Google Cloud. Alternatively, instead of Cloud Shell, you can use another Bash shell with the [Google Cloud CLI](https://docs.cloud.google.com/sdk/docs) installed.

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  If Cloud Shell does not display `( PROJECT_ID )$` in its prompt (where PROJECT\_ID is replaced by your Google Cloud project ID), then run the following command to configure Cloud Shell to use your project:
    
        gcloud config set project PROJECT_ID

## Create a Cloud Storage bucket

Create a regional [Cloud Storage](https://docs.cloud.google.com/storage/docs) bucket in the `us-central1` region to use for the rest of this tutorial. As you follow the tutorial, use the bucket for several purposes:

  - Store training code for Vertex AI to use in a custom training job.
  - Store the model artifacts that your custom training job outputs.
  - Host the web app that gets predictions from your Vertex AI endpoint.

To create the Cloud Storage bucket, run the following command in your Cloud Shell session:

    gcloud storage buckets create gs://BUCKET_NAME --project=PROJECT_ID --location=us-central1

Replace the following:

  - PROJECT\_ID : The ID of your Google Cloud project.
  - BUCKET\_NAME : A name that you choose for your bucket. For example, ` hello_custom_ PROJECT_ID  ` . Learn about [requirements for bucket names](https://docs.cloud.google.com/storage/docs/buckets#naming) .

## Download sample code

Download sample code to use for the rest of the tutorial.

    gcloud storage cp gs://cloud-samples-data/ai-platform/hello-custom/hello-custom-sample-v1.tar.gz - | tar -xzv

To optionally view the sample code files, run the following command:

    ls -lpR hello-custom-sample

The `hello-custom-sample` directory has four items:

  - `trainer/` : A directory of TensorFlow Keras code for training the flower classification model.

  - `setup.py` : A configuration file for packaging the `trainer/` directory into a Python source distribution that Vertex AI can use.

  - `function/` : A directory of Python code for a [Cloud Run function](https://docs.cloud.google.com/functions/docs) that can receive and preprocess prediction requests from a web browser, send them to Vertex AI, process the prediction responses, and send them back to the browser.

  - `webapp/` : A directory with code and markup for a web app that gets flower classification predictions from Vertex AI.

## What's next

Follow the [next page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/training) to run a custom training job on Vertex AI.
