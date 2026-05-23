---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-multihost-gpu
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-multihost-gpu
title: Serve a DeepSeek-V3 model using multi-host GPU deployment
description: Learn about serving a DeepSeek-V3 model using multi-host GPU deployment.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Overview

Gemini Enterprise Agent Platform supports multi-host GPU deployment for serving models that exceed the memory capacity of a single GPU node, such as [DeepSeek-V3](https://huggingface.co/deepseek-ai/DeepSeek-V3) , [DeepSeek-R1](https://huggingface.co/deepseek-ai/DeepSeek-R1) , and [Meta LLama 3.1 405B](https://huggingface.co/meta-llama/Llama-3.1-405B) (non-quantized version).

This guide describes how to serve a DeepSeek-V3 model using multi-host graphical processing units (GPUs) on Gemini Enterprise Agent Platform with [vLLM](https://github.com/vllm-project/vllm) . Setup for other models is similar. For more information, see [vLLM serving for text and multimodal language models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/vllm/use-vllm) .

Before you begin, ensure you are familiar with the following:

  - [GPU version availability by region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators)
  - [GPU pricing by region](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#accelerators)
  - [Cloud Storage pricing](https://cloud.google.com/storage/pricing)
  - [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing)

Use the [Pricing Calculator](https://cloud.google.com/products/calculator/) to generate a cost estimate based on your projected usage.

> **Note:** [DeepSeek V3](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-v3) and [DeepSeek R1](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-r1) are also available in Model Garden. For more information about Model Garden, see [Explore AI models in Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .

## Containers

To support multi-host deployments, this guide uses a prebuilt vLLM container image with [Ray](https://docs.ray.io/en/latest/ray-overview/index.html) integration from [Model Garden](https://console.cloud.google.com/vertex-ai/model-garden) . Ray enables the distributed processing required to run models across multiple GPU nodes.

If desired, you can [create your own vLLM multi-node image](https://docs.cloud.google.com/kubernetes-engine/docs/tutorials/serve-multihost-gpu#create_your_own_vllm_multi-node_image) . Note that this custom container image needs to be [compatible with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) .

## Before you begin

Before you begin your model deployment, complete the prerequisites listed in this section.

### Set up a Google Cloud project

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

### Request GPU quota

To deploy DeepSeek-V3, you need two [`a3-highgpu-8g`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#a3-series) VMs with eight [H100](https://docs.cloud.google.com/compute/docs/gpus#h100-gpus) GPUs each, for a total of 16 H100 GPUs. It's likely that you'll need to request an H100 GPU quota increase, as the default value is less than 16.

1.  To view the H100 GPU quota, go to the Google Cloud console **Quotas & System Limits** page.

2.  [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase) .

## Upload the model

1.  To upload your model as a `Model` resource to Gemini Enterprise Agent Platform, run the [`gcloud ai models upload` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload) as follows:
    
        gcloud ai models upload \
            --region=LOCATION \
            --project=PROJECT_ID \
            --display-name=MODEL_DISPLAY_NAME \
            --container-image-uri=us-docker.pkg.dev/vertex-ai/vertex-vision-model-garden-dockers/pytorch-vllm-serve:20250312_0916_RC01 \
            --container-args='^;^/vllm-workspace/ray_launcher.sh;python;-m;vllm.entrypoints.api_server;--host=0.0.0.0;--port=7080;--model=deepseek-ai/DeepSeek-V3;--tensor-parallel-size=8;--pipeline-parallel-size=2;--gpu-memory-utilization=0.82;--max-model-len=163840;--max-num-seqs=64;--enable-chunked-prefill;--kv-cache-dtype=auto;--trust-remote-code;--disable-log-requests' \
            --container-deployment-timeout-seconds=7200 \
            --container-ports=7080 \
            --container-env-vars=MODEL_ID=deepseek-ai/DeepSeek-V3
    
    Make the following replacements:
    
      - `LOCATION` : the region where you are using Gemini Enterprise Agent Platform
      - `PROJECT_ID` : the ID of your Google Cloud project
      - `MODEL_DISPLAY_NAME` : the display name you want for your model

## Create a dedicated online inference endpoint

To support chat completion requests, the Model Garden container requires a [dedicated endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#create-dedicated-endpoint) . Dedicated endpoints are in preview and don't support Google Cloud CLI, so you need to use the REST API to create the endpoint.

1.  To create the dedicated endpoint, run the following command:
    
        PROJECT_ID=PROJECT_ID
        REGION=LOCATION
        ENDPOINT="${REGION}-aiplatform.googleapis.com"
        
        curl \
          -X POST \
          -H "Authorization: Bearer $(gcloud auth print-access-token)" \
          -H "Content-Type: application/json" \
          https://${ENDPOINT}/v1/projects/${PROJECT_ID}/locations/${REGION}/endpoints \
          -d '{
            "displayName": "ENDPOINT_DISPLAY_NAME",
            "dedicatedEndpointEnabled": true
            }'
    
    Make the following replacements:
    
      - `ENDPOINT_DISPLAY_NAME` : the display name for your endpoint

## Deploy the model

1.  Get the endpoint ID for the online inference endpoint by running the [`gcloud ai endpoints list`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/list) command:
    
        ENDPOINT_ID=$(gcloud ai endpoints list \
         --project=PROJECT_ID \
         --region=LOCATION \
         --filter=display_name~'ENDPOINT_DISPLAY_NAME' \
         --format="value(name)")

2.  Get the model ID for your model by running the [`gcloud ai models list`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/list) command:
    
        MODEL_ID=$(gcloud ai models list \
         --project=PROJECT_ID \
         --region=LOCATION \
         --filter=display_name~'MODEL_DISPLAY_NAME' \
         --format="value(name)")

3.  Deploy the model to the endpoint by running the [`gcloud ai deploy-model`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/ai/endpoints/deploy-model) command:
    
        gcloud alpha ai endpoints deploy-model $ENDPOINT_ID \
         --project=PROJECT_ID \
         --region=LOCATION \
         --model=$MODEL_ID \
         --display-name="DEPLOYED_MODEL_NAME" \
         --machine-type=a3-highgpu-8g \
         --traffic-split=0=100 \
         --accelerator=type=nvidia-h100-80gb,count=8 \
         --multihost-gpu-node-count=2
    
    Replace DEPLOYED\_MODEL\_NAME with a name for the deployed model. This can be the same as the model display name ( MODEL\_DISPLAY\_NAME ).
    
    Deploying large models like DeepSeek-V3 can take longer than the default deployment timeout. If the `deploy-model` command times out, the deployment process continues to run in the background.
    
    The `deploy-model` command returns an operation ID that can be used to check when the operation is finished. You can poll for the status of the operation until the response includes `"done": true` . Use the following command to poll the status:
    
        gcloud ai operations describe \
        --region=LOCATION \
        OPERATION_ID
    
    Replace OPERATION\_ID with the operation ID that was returned by the previous command.

## Get online inferences from the deployed model

This section describes how to [send an online inference request to the dedicated public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#inference-request-dedicated) where the DeepSeek-V3 model is deployed.

1.  Get the project number by running the [`gcloud projects describe`](https://docs.cloud.google.com/sdk/gcloud/reference/projects/describe) command:
    
        PROJECT_NUMBER=$(gcloud projects describe PROJECT_ID --format="value(projectNumber)")

2.  Send a raw predict request:
    
        curl \
        -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json" \
        https://${ENDPOINT_ID}.${REGION}-${PROJECT_NUMBER}.prediction.vertexai.goog/v1/projects/${PROJECT_NUMBER}/locations/${REGION}/endpoints/${ENDPOINT_ID}:rawPredict \
        -d '{
           "prompt": "Write a short story about a robot.",
           "stream": false,
           "max_tokens": 50,
           "temperature": 0.7
           }'

3.  Send a chat completion request:
    
        curl \
        -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json" \
        https://${ENDPOINT_ID}.${REGION}-${PROJECT_NUMBER}.prediction.vertexai.goog/v1/projects/${PROJECT_NUMBER}/locations/${REGION}/endpoints/${ENDPOINT_ID}/chat/completions \
        -d '{"stream":false, "messages":[{"role": "user", "content": "Summer travel plan to Paris"}], "max_tokens": 40,"temperature":0.4,"top_k":10,"top_p":0.95, "n":1}'
    
    To enable streaming, change the value of `"stream"` from `false` to `true` .

## Clean up

To avoid incurring further [Gemini Enterprise Agent Platform charges](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) , delete the Google Cloud resources that you created during this tutorial:

1.  To undeploy the model from the endpoint and delete the endpoint, run the following commands:
    
        ENDPOINT_ID=$(gcloud ai endpoints list \
           --region=LOCATION \
           --filter=display_name=ENDPOINT_DISPLAY_NAME \
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

2.  To delete your model, run the following commands:
    
        MODEL_ID=$(gcloud ai models list \
           --region=LOCATION \
           --filter=display_name=DEPLOYED_MODEL_NAME \
           --format="value(name)")
        
        gcloud ai models delete $MODEL_ID \
           --region=LOCATION \
           --quiet

## What's next

  - For comprehensive reference information about multi-host GPU deployment on Gemini Enterprise Agent Platform with vLLM, see [vLLM serving for text and multimodal language models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/vllm/use-vllm) .
  - Learn to [create your own vLLM multi-node image](https://docs.cloud.google.com/kubernetes-engine/docs/tutorials/serve-multihost-gpu#create_your_own_vllm_multi-node_image) . Note that your custom container image needs to be [compatible with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) .
