---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/serve-gemma-with-saxml-tpu
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/serve-gemma-with-saxml-tpu
title: Serve Gemma open models using TPUs on Gemini Enterprise Agent Platform with Saxml
description: Learn about serving Gemma open models using TPUs with Saxml.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This guide shows you how to serve a Gemma open models large language model (LLM) using [Tensor Processing Units (TPUs)](https://docs.cloud.google.com/tpu/docs/intro-to-tpu) on Gemini Enterprise Agent Platform with Saxml. In this guide, you download the 2B and 7B parameter instruction tuned Gemma models to Cloud Storage and deploy them on Gemini Enterprise Agent Platform that runs Saxml on TPUs.

## Background

By serving Gemma using TPUs on Gemini Enterprise Agent Platform with Saxml. You can take advantage of a managed AI solution that takes care of low level infrastructure and offers a cost effective way for serving LLMs. This section describes the key technologies used in this tutorial.

### Gemma

Gemma is a set of openly available, lightweight, and generative artificial intelligence (AI) models released under an open license. These AI models are available to run in your applications, hardware, mobile devices, or hosted services. You can use the Gemma models for text generation, however you can also tune these models for specialized tasks.

To learn more, see the [Gemma documentation](https://ai.google.dev/gemma/docs) .

### Saxml

[Saxml](https://github.com/google/saxml) is an experimental system that serves [Paxml](https://github.com/google/paxml) , [JAX](https://github.com/google/jax) , and [PyTorch](https://github.com/google/jax) models for inference. For the sake of this tutorial we'll cover how to serve Gemma on TPUs that are more cost efficient for Saxml. Setup for GPUs is similar. Saxml offers scripts to build containers for [Gemini Enterprise Agent Platform](https://github.com/google/saxml/tree/main/saxml/vertex) that we are going to use in this tutorial.

### TPUs

TPUs are Google's custom-developed application-specific integrated circuits (ASICs) used to accelerate data processing frameworks such as TensorFlow, PyTorch, and JAX.

This tutorial serves the Gemma 2B and Gemma 7B models. Gemini Enterprise Agent Platform hosts these models on the following single-host TPU v5e node pools:

  - **Gemma 2B** : Hosted in a TPU v5e node pool with `1x1` topology that represents one TPU chip. The machine type for the nodes is `ct5lp-hightpu-1t` .
  - **Gemma 7B** : Hosted in a TPU v5e node pool with `2x2` topology that represents four TPU chips. The machine type for the nodes is `ct5lp-hightpu-4t` .

## Before you begin

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

This tutorial assumes that you are using [Cloud Shell](https://docs.cloud.google.com/shell/docs) to interact with Google Cloud. If you want to use a different shell instead of Cloud Shell, then perform the following additional configuration:

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  To [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the gcloud CLI, run the following command:
    
        gcloud init

4.  Make sure that you have sufficient quota for TPU v5e chips for [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-tpu#ensure-quota) . By default, this quota is 0. For a `1x1` topology, it must be 1. For `2x2` , it must be 4. To run both topologies, it must be 5.

5.  Create a [Kaggle account](https://www.kaggle.com/) , if you don't already have one.

## Get access to the model

Note that Cloud Shell might not have sufficient resources to download model weights. If so, you can create a [Gemini Enterprise Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) instance for performing that task.

To get access to the Gemma models for deployment to Gemini Enterprise Agent Platform, you must sign in to the [Kaggle platform](https://www.kaggle.com/) , sign the license consent agreement, and get a Kaggle API token. In this tutorial, you use a Kubernetes Secret for the Kaggle credentials.

### Sign the license consent agreement

You must sign the consent agreement to use Gemma. Follow these instructions:

1.  Access the [model consent page](https://www.kaggle.com/models/google/gemma) on Kaggle.com.
2.  Sign in to Kaggle if you haven't done so already.
3.  Click **Request Access** .
4.  In the **Choose Account for Consent** section, select **Verify via Kaggle Account** to use your Kaggle account for consent.
5.  Accept the model **Terms and Conditions** .

### Generate an access token

To access the model through Kaggle, you need a [Kaggle API token](https://github.com/Kaggle/kaggle-api) .

Follow these steps to generate a new token if you don't have one already:

1.  In your browser, go to [Kaggle settings](https://www.kaggle.com/settings) .

2.  Under the **API** section, click **Create New Token** .
    
    A file named `kaggle.json` is downloaded.

### Upload the access token to Cloud Shell

In Cloud Shell, you can upload the Kaggle API token to your Google Cloud project:

1.  In Cloud Shell, click more\_vert **More** \> **Upload** .
2.  Select File and click **Choose Files** .
3.  Open the `kaggle.json` file.
4.  Click **Upload** .

### Create the Cloud Storage bucket

Create Cloud Storage bucket to store the model checkpoints.

In Cloud Shell, run the following:

    gcloud storage buckets create gs://CHECKPOINTS_BUCKET_NAME

Replace the CHECKPOINTS\_BUCKET\_NAME with the name of the Cloud Storage bucket that stores the model checkpoints.

### Copy model to Cloud Storage bucket

In Cloud Shell, run the following:

    pip install kaggle --break-system-packages
    
    # For Gemma 2B
    mkdir -p /data/gemma_2b-it
    kaggle models instances versions download google/gemma/pax/2b-it/1 --untar -p /data/gemma_2b-it
    gcloud storage cp /data/gemma_2b-it/* gs://CHECKPOINTS_BUCKET_NAME/gemma_2b-it/ --recursive
    
    # For Gemma 7B
    mkdir -p /data/gemma_7b-it
    kaggle models instances versions download google/gemma/pax/7b-it/1 --untar -p /data/gemma_7b-it
    gcloud storage cp /data/gemma_7b-it/* gs://CHECKPOINTS_BUCKET_NAME/gemma_7b-it/ --recursive

## Deploying the model

### Upload a model

To upload a `Model` resource that uses your Saxml container, run the following [`gcloud ai models upload` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload) :

### Gemma 2B-it

    gcloud ai models upload \
      --region=LOCATION \
      --display-name=DEPLOYED_MODEL_NAME \
      --container-image-uri=us-docker.pkg.dev/vertex-ai/prediction/sax-tpu:latest \
      --artifact-uri='gs://CHECKPOINTS_BUCKET_NAME/gemma_2b-it/' \
      --container-args='--model_path=saxml.server.pax.lm.params.gemma.Gemma2BFP16' \
      --container-args='--platform_chip=tpuv5e' \
      --container-args='--platform_topology=2x2' \
      --container-args='--ckpt_path_suffix=checkpoint_00000000' \
      --container-ports=8502

### Gemma 7B-it

    gcloud ai models upload \
      --region=LOCATION \
      --display-name=DEPLOYED_MODEL_NAME \
      --container-image-uri=us-docker.pkg.dev/vertex-ai/prediction/sax-tpu:latest \
      --artifact-uri='gs://CHECKPOINTS_BUCKET_NAME/gemma_7b-it/' \
      --container-args='--model_path=saxml.server.pax.lm.params.gemma.Gemma7BFP16' \
      --container-args='--platform_chip=tpuv5e' \
      --container-args='--platform_topology=2x2' \
      --container-args='--ckpt_path_suffix=checkpoint_00000000' \
      --container-ports=8502

Replace the following:

  - PROJECT\_ID : the ID of your [Google Cloud project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects)
  - LOCATION\_ID : The region where you are using Agent Platform. Note that TPUs are only available in us-west1.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.

### Create an endpoint

You must deploy the model to an endpoint before the model can be used to serve online inferences. If you are deploying a model to an existing endpoint, you can skip this step. The following example uses the [`gcloud ai endpoints create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/create) :

    gcloud ai endpoints create \
      --region=LOCATION \
      --display-name=ENDPOINT_NAME

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.

The Google Cloud CLI tool might take a few seconds to create the endpoint.

### Deploy the model to endpoint

After the endpoint is ready, deploy the model to the endpoint.

    ENDPOINT_ID=$(gcloud ai endpoints list \
       --region=LOCATION \
       --filter=display_name=ENDPOINT_NAME \
       --format="value(name)")
    
    MODEL_ID=$(gcloud ai models list \
       --region=LOCATION \
       --filter=display_name=DEPLOYED_MODEL_NAME \
       --format="value(name)")
    
    gcloud ai endpoints deploy-model $ENDPOINT_ID \
      --region=LOCATION \
      --model=$MODEL_ID \
      --display-name=DEPLOYED_MODEL_NAME \
      --machine-type=ct5lp-hightpu-4t \
      --traffic-split=0=100

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.

`Gemma 2B` can be deployed on a smaller ct5lp-hightpu-1t machine, in such case you should specify `--platform_topology=1x1` when uploading model.

The Google Cloud CLI tool might take a few minutes to deploy the model to the endpoint. When the model is successfully deployed, this command prints the following output:

``` 
  Deployed a model to the endpoint xxxxx. Id of the deployed model: xxxxx.
```

## Getting online inferences from the deployed model

To invoke the model through the Gemini Enterprise Agent Platform endpoint, format the inference request by using a [standard Inference Request JSON Object](https://github.com/kserve/kserve/blob/master/docs/predict-api/v2/required_api.md#inference) .

The following example uses the [`gcloud ai endpoints predict` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/predict) :

    ENDPOINT_ID=$(gcloud ai endpoints list \
       --region=LOCATION \
       --filter=display_name=ENDPOINT_NAME \
       --format="value(name)")
    
    gcloud ai endpoints predict $ENDPOINT_ID \
      --region=LOCATION \
      --http-headers=Content-Type=application/json \
      --json-request instances.json

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.
  - instances.json has following format: `{"instances": [{"text_batch": "<your prompt>"},{...}]}`

## Cleaning up

To avoid incurring further [Gemini Enterprise Agent Platform charges](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) and [Artifact Registry charges](https://cloud.google.com/artifact-registry/pricing) , delete the Google Cloud resources that you created during this tutorial:

1.  To undeploy model from endpoint and delete the endpoint, run the following command in your shell:
    
        ENDPOINT_ID=$(gcloud ai endpoints list \
           --region=LOCATION \
           --filter=display_name=ENDPOINT_NAME \
           --format="value(name)")
        
        DEPLOYED_MODEL_ID=$(gcloud ai endpoints describe $ENDPOINT_ID \
           --region=LOCATION \
           --format="value(deployedModels.id)")
        
        gcloud ai endpoints undeploy-model $ENDPOINT_ID \
          --region=LOCATION \
          --deployed-model-id=$DEPLOYED_MODEL_ID
        
        gcloud ai endpoints delete $ENDPOINT_ID \
           --region=LOCATION \
           --quiet
    
    Replace LOCATION with the region where you created your model in a previous section.

2.  To delete your model, run the following command in your shell:
    
        MODEL_ID=$(gcloud ai models list \
           --region=LOCATION \
           --filter=display_name=DEPLOYED_MODEL_NAME \
           --format="value(name)")
        
        gcloud ai models delete $MODEL_ID \
           --region=LOCATION \
           --quiet
    
    Replace LOCATION with the region where you created your model in a previous section.

## Limitations

  - On Gemini Enterprise Agent Platform Cloud TPUs are supported only in `us-west1` . For more information, see [locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#region_considerations) .

## What's next

  - Learn how to deploy other [Saxml models](https://github.com/google/saxml/tree/main/saxml/vertex) such as Llama2 and GPT-J.
