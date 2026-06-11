---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/training-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/training-guide
title: Custom training beginner&#39;s guide
description: Learn about the benefits of using a managed service for custom training, review best practices for packaging training code, and learn how to submit and monitor a training job in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This beginner's guide is an introduction to custom training on Gemini Enterprise Agent Platform. Custom training refers to training a model using an ML framework such as TensorFlow, PyTorch, or XGBoost.

## Learning Objectives

**Gemini Enterprise Agent Platform experience level** : Beginner

**Estimated reading time** : 15 minutes

**What you'll learn** :

  - Benefits of using a managed service for custom training.
  - Best practices for packaging training code.
  - How to submit and monitor a training job.

## Why use a managed training service?

Imagine you're working on a new ML problem. You open up a notebook, import your data, and run experimentation. In this scenario, you create a model with the ML framework of your choice, and execute notebook cells to run a training loop. When training completes, you evaluate the results of your model, make changes, and then re-run training. This workflow is useful for experimentation, but as you start to think about building production applications with ML, you might find that manually executing the cells of your notebook isn't the most convenient option.

For example, if your dataset and model are large you might want to try out distributed training. Additionally, in a production setting it's unlikely that you'll only need to train your model once. Over time, you'll retrain your model to make sure it stays fresh and keeps producing valuable results. When you want to automate experimentation at scale, or retrain models for a production application, utilizing a managed ML training service will simplify your workflows.

This guide provides an introduction to training custom models on Gemini Enterprise Agent Platform. Because the training service is fully managed, Gemini Enterprise Agent Platform automatically provisions compute resources, perform the training task, and ensure deletion of compute resources once the training job is finished. Note that there are additional customizations, features, and ways to interface with the service that are not covered here. This guide is intended to provide an overview. For more detail, refer to the [Gemini Enterprise Agent Platform Training documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) .

## Overview of custom training

Training custom models on Gemini Enterprise Agent Platform follows this standard workflow:

1.  Package up your training application code.

2.  Configure and submit custom training job.

3.  Monitor custom training job.

## Packaging training application code

Running a custom training job on Gemini Enterprise Agent Platform is done with containers. Containers are packages of your application code, in this case your training code, together with dependencies such as specific versions of libraries required to run your code. In addition to helping with dependency management, containers are able to run virtually anywhere, allowing for increased portability. Packaging your training code with its parameters and dependencies into a container to create a portable component is an important step when moving your ML applications from protoype to production.

Before you can launch a custom training job, you'll need to package up your training application. Training application in this case refers to a file, or multiple files, that perform tasks like loading data, preprocessing data, defining a model, and executing a training loop. The Gemini Enterprise Agent Platform training service runs whatever code you provide, so it's entirely up to you what steps you include in your training application.

Gemini Enterprise Agent Platform provides [prebuilt containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) for TensorFlow, PyTorch, XGBoost, and Scikit-learn. These containers are updated regularly and include common libraries you might need in your training code. You can choose to run your training code with one of these containers, or create a custom container that has your training code and dependencies pre-installed.

There are three options for packaging your code on Gemini Enterprise Agent Platform:

1.  Submit a single Python file.
2.  Create a Python source distribution.
3.  Use custom containers.

### Python file

This option is suitable for quick experimentation. You can use this option if all of the code needed to execute your training application is in one Python file and one of the prebuilt Gemini Enterprise Agent Platform training containers has all of the libraries needed to run your application. For an example of packaging your training application as a single Python file, see the notebook tutorial [Custom training and batch inference](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb) .

### Python Source Distribution

You can create a [Python Source Distribution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container#create-source-distribution) that contains your training application. You'll store your source distribution with the training code and dependencies in a Cloud Storage bucket. For an example of packaging your training application as a Python Source Distribution, see the notebook tutorial [Training, tuning and deploying a PyTorch classification model](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb) .

### Custom Container

This option is useful when you want more control over your application, or maybe you want to run code not written in Python. In this case you'll need to write a Dockerfile, build your custom image, and push it to Artifact Registry. For an example of containerizing your training application see the notebook tutorial [Profile model training performance using Profiler](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom_training_tensorboard_profiler.ipynb) .

### Recommended training application structure

If you choose to package up your code as a Python source distribution or as a custom container, it's recommended that you structure your application as follows:

    training-application-dir/
    ....setup.py
    ....Dockerfile
    ....trainer/
    ........task.py
    ........model.py
    ........utils.py

Create a directory to store all of your training application code, in this case, `training-application-dir` . This directory will contain a `setup.py` file if you're using a Python Source Distribution, or a `Dockerfile` if you're using a custom container.

In both scenarios, this high level directory will also contain a subdirectory `trainer` , that contains all the code to execute training. Within `trainer` , `task.py` is the main entrypoint to your application. This file executes model training. You can choose to put all of your code in this file, but for production applications you're likely to have additional files, for example `model.py` , `data.py` , `utils.py` to name a few.

## Running custom training

Training jobs on Gemini Enterprise Agent Platform automatically provisions compute resources, execute the training application code, and ensure deletion of compute resources once the training job is finished.

As you build out more complicated workflows, it's likely that you'll use the [Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) to configure, submit, and monitor your training jobs. However, the first time you run a custom training job it can be easier to use the Google Cloud console.

1.  In the Google Cloud console, go to the **Training** page.

2.  Click **Train new model** .

3.  Under model **Training method** , select **Custom training (advanced)** .
    
    ![specify training method](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/start/images/custom_training/custom_training_method.png)

4.  Under the Training Container section, select either prebuilt or custom container, depending on how you packaged your application.
    
    ![specify training container](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/start/images/custom_training/choose_container.png)

5.  Under **Compute and pricing** , specify the hardware for the training job. For single node training, you only need to configure Worker Pool 0. If you're interested in running distributed training, you'll need to understand the other worker pools, and you can learn more on [Distributed training](https://docs.cloud.google.com/vertex-ai/docs/training/distributed-training) .
    
    ![training compute](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/start/images/custom_training/training_compute.png)

Configuring the inference container is optional. If you only want to train a model on Gemini Enterprise Agent Platform and access the resulting saved model artifacts, you can skip this step. If you want to host and deploy the resulting model on the Gemini Enterprise Agent Platform managed inference service, you'll need to configure an inference container. To learn more, see [Get inferences from a custom trained model](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-predictions) .

## Monitoring Training jobs

You can monitor your training job in the Google Cloud console. You'll see a list of all the jobs that have run. You can click a particular job and examine the logs if something goes wrong.

![training dashboard](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/start/images/custom_training/monitor_training.png)

## Notebooks

> To see examples of how to enable Profiler for a custom training job, run the following notebooks in the environment of your choice:
> 
>   - "Training, tuning and deploying a PyTorch text sentiment classification model on ":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fpytorch-text-sentiment-classification-custom-train-deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fpytorch-text-sentiment-classification-custom-train-deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb)
> 
>   - "Get started with Distributed Training":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/get_started_with_vertex_distributed_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fget_started_with_vertex_distributed_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fget_started_with_vertex_distributed_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/get_started_with_vertex_distributed_training.ipynb)
> 
>   - "Run hyperparameter tuning for a TensorFlow model":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fhyperparameter_tuning_tensorflow.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fhyperparameter_tuning_tensorflow.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb)
> 
>   - " TensorBoard custom training with prebuilt container":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb)
> 
>   - "PyTorch distributed training with Reduction Server":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Freduction_server%2Fpytorch_distributed_training_reduction_server.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Freduction_server%2Fpytorch_distributed_training_reduction_server.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb)
> 
>   - "Custom training and batch prediction (image classification)":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb)
> 
>   - "Custom training and online prediction (image classification)":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb)

## Video

  - [Training custom models](https://www.youtube.com/watch?v=VRQXIiNLdAk)
