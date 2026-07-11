---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/serve-llama3-with-saxml-tpu
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/serve-llama3-with-saxml-tpu
title: Serve Llama 3 open models using multi-host Cloud TPUs on Gemini Enterprise Agent Platform with Saxml
description: Learn about serving Llama 3 open models using multi-host Cloud TPUs with Saxml.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

[Llama 3](https://github.com/meta-llama/llama3) is an open-source large language model (LLM) from Meta. This guide shows you how to serve a Llama 3 LLM using multi-host [Tensor Processing Units (TPUs)](https://docs.cloud.google.com/tpu/docs/intro-to-tpu) on Gemini Enterprise Agent Platform with [Saxml](https://github.com/google/saxml) .

In this guide, you download the Llama 3 70B model weights and tokenizer and deploy them on Gemini Enterprise Agent Platform that runs Saxml on TPUs.

> **Note:** A GPU-only version of Llama 3 is [available](https://cloud.google.com/blog/products/ai-machine-learning/meta-llama-3-available-today-on-google-cloud-vertex-ai) in [Model Garden](https://console.cloud.google.com/vertex-ai/publishers/meta/model-garden/llama3) . For more information about Model Garden, see [Explore AI models in Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .

## Before you begin

We recommend that you use an [M2 memory-optimized VM](https://docs.cloud.google.com/compute/docs/memory-optimized-machines#m2_series) for downloading the model and converting it to Saxml. This is because the model conversion process requires significant memory and may fail if you choose a machine type that doesn't have enough memory.

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Follow the Artifact Registry documentation to [Install Docker.](https://docs.cloud.google.com/artifact-registry/docs/docker/quickstart#before-you-begin)

3.  Make sure that you have sufficient quotas for 16 TPU v5e chips for [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-tpu#ensure-quota) .

This tutorial assumes that you are using [Cloud Shell](https://docs.cloud.google.com/shell/docs) to interact with Google Cloud. If you want to use a different shell instead of Cloud Shell, then perform the following additional configuration:

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  To [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the gcloud CLI, run the following command:
    
        gcloud init

If you're using a different shell instead of Cloud Shell for model deployment, make sure that the [Google Cloud CLI](https://docs.cloud.google.com/sdk/docs/install) version is later than `475.0.0` . You can update the Google Cloud CLI by running the [gcloud components update](https://docs.cloud.google.com/sdk/gcloud/reference/components/update) command.

If you're deploying your model using the Vertex AI SDK, make sure that you have version `1.50.0` or later.

## Get access to the model and download the model weights

The following steps are for a Agent Platform Workbench instance that has an [M2 memory-optimized VM](https://docs.cloud.google.com/compute/docs/memory-optimized-machines#m2_series) . For information on changing the machine type of a Agent Platform Workbench instance, see [Change machine type of an Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/change-machine-type) .

1.  Go to the [Llama model consent page](https://llama.com/llama-downloads/) .

2.  Select Llama 3, fill out the consent form, and accept the terms and conditions.

3.  Check your inbox for an email containing a signed URL.

4.  Download the [`download.sh` script](https://github.com/meta-llama/llama3/blob/main/download.sh) from GitHub by executing the following command:
    
        wget https://raw.githubusercontent.com/meta-llama/llama3/main/download.sh
        chmod +x download.sh

5.  To download the model weights, run the `download.sh` script that you downloaded from GitHub.

6.  When prompted, enter the signed URL from the email you received in the previous section.

7.  When prompted for the models to download, enter `70B` .

## Convert the model weights to Saxml format

1.  Run the following command to download Saxml:
    
        git clone https://github.com/google/saxml.git

2.  Run the following commands to configure a Python virtual environment:
    
        python -m venv .
        source bin/activate

3.  Run the following commands to install dependencies:
    
        pip install --upgrade pip
        
        pip install paxml
        
        pip install praxis
        
        pip install torch

4.  To convert the model weights to Saxml format, run the following command:
    
        python3 saxml/saxml/tools/convert_llama_ckpt.py \
            --base PATH_TO_META_LLAMA3 \
            --pax PATH_TO_PAX_LLAMA3 \
            --model-size llama3_70b
    
    Replace the following:
    
      - `PATH_TO_META_LLAMA3` : the path to the directory containing the downloaded model weights
      - `PATH_TO_PAX_LLAMA3` : the path to the directory in which to store the converted model weights
    
    > **Note:** You can use this command for any Llama 2 or Llama 3 model.
    
    Converted models will be put into the `$PATH_TO_PAX_LLAMA3/checkpoint_00000000` folder.

5.  Copy the tokenizer file from original directory into a subfolder named `vocabs` as follows:
    
        cp $PATH_TO_META_LLAMA3/tokenizer.model $PATH_TO_PAX_LLAMA3/vocabs/tokenizer.model

6.  Add an empty `commit_success.txt` file in the `$PATH_TO_PAX_LLAMA3` folder and the `metadata` and `state` subfolders in that folder as follows:
    
        touch $PATH_TO_PAX_LLAMA3/checkpoint_00000000/commit_success.txt
        touch $PATH_TO_PAX_LLAMA3/checkpoint_00000000/metadata/commit_success.txt
        touch $PATH_TO_PAX_LLAMA3/checkpoint_00000000/state/commit_success.txt
    
    The `$PATH_TO_PAX_LLAMA3` folder now contains the following folders and files:
    
        $PATH_TO_PAX_LLAMA3/checkpoint_00000000/commit_success.txt
        $PATH_TO_PAX_LLAMA3/checkpoint_00000000/metadata/
        $PATH_TO_PAX_LLAMA3/checkpoint_00000000/metadata/commit_success.txt
        $PATH_TO_PAX_LLAMA3/checkpoint_00000000/state/
        $PATH_TO_PAX_LLAMA3/checkpoint_00000000/state/commit_success.txt
        $PATH_TO_PAX_LLAMA3/vocabs/tokenizer.model

## Create a Cloud Storage bucket

Create a Cloud Storage bucket to store the converted model weights.

1.  In Cloud Shell, run the following commands, replacing PROJECT\_ID with your project ID:
    
        projectid=PROJECT_ID
        gcloud config set project ${projectid}

2.  To create the bucket, run the following command:
    
        gcloud storage buckets create gs://WEIGHTS_BUCKET_NAME
    
    Replace WEIGHTS\_BUCKET\_NAME with the name you want to use for the bucket.

## Copy the model weights to the Cloud Storage bucket

To copy the model weights to your bucket, run the following command:

    gcloud storage cp PATH_TO_PAX_LLAMA3/* gs://WEIGHTS_BUCKET_NAME/llama3/pax_70b/ --recursive

## Upload the model

A prebuilt Saxml container is available at `us-docker.pkg.dev/vertex-ai/prediction/sax-tpu:latest` .

To upload a `Model` resource to Gemini Enterprise Agent Platform using the prebuilt Saxml container, run the [`gcloud ai models upload` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload) as follows:

    gcloud ai models upload \
        --region=LOCATION \
        --display-name=MODEL_DISPLAY_NAME \
        --container-image-uri=us-docker.pkg.dev/vertex-ai/prediction/sax-tpu:latest \
        --artifact-uri='gs://WEIGHTS_BUCKET_NAME/llama3/pax_70b' \
        --container-args='--model_path=saxml.server.pax.lm.params.lm_cloud.LLaMA3_70BFP16x16' \
        --container-args='--platform_chip=tpuv5e' \
        --container-args='--platform_topology=4x4' \
        --container-args='--ckpt_path_suffix=checkpoint_00000000' \
        --container-deployment-timeout-seconds=2700 \
        --container-ports=8502 \
        --project=PROJECT_ID

Make the following replacements:

  - `LOCATION` : the region where you are using Gemini Enterprise Agent Platform. Note that TPUs are only available in `us-west1` .
  - `MODEL_DISPLAY_NAME` : the display name you want for your model
  - `PROJECT_ID` : the ID of your Google Cloud project

> **Note:** You can use this command for any Llama model that's listed on the following GitHub link: <https://github.com/google/saxml/blob/main/saxml/server/pax/lm/params/lm_cloud.py>

## Create an online inference endpoint

To create the endpoint, run the following command:

    gcloud ai endpoints create \
        --region=LOCATION \
        --display-name=ENDPOINT_DISPLAY_NAME \
        --project=PROJECT_ID

Replace `ENDPOINT_DISPLAY_NAME` with the display name you want for your endpoint.

## Deploy the model to the endpoint

After the endpoint is ready, deploy the model to the endpoint.

In this tutorial, you deploy a Llama 3 70B model that's sharded for 16 Cloud TPU v5e chips using 4x4 topology. However, you can specify any of the following supported multi-host Cloud TPU topologies:

| Machine Type       | Topology | Number of TPU chips | Number of Hosts |
| ------------------ | -------- | ------------------- | --------------- |
| `ct5lp-hightpu-4t` | 4x4      | 16                  | 2               |
| `ct5lp-hightpu-4t` | 4x8      | 32                  | 4               |
| `ct5lp-hightpu-4t` | 8x8      | 64                  | 8               |
| `ct5lp-hightpu-4t` | 8x16     | 128                 | 16              |
| `ct5lp-hightpu-4t` | 16x16    | 256                 | 32              |

If you're deploying a different Llama model that's defined in the [Saxml GitHub repo](https://github.com/google/saxml/blob/main/saxml/server/pax/lm/params/lm_cloud.py) , make sure that it's partitioned to match the number of devices you're targeting and that Cloud TPU has sufficient memory to load the model.

For information about deploying a model on single-host Cloud TPUs, see [Deploy a model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-tpu#deploy_a_model) .

For a full list of supported Cloud TPU types and regions see [Gemini Enterprise Agent Platform Locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

1.  Get the endpoint ID for the online inference endpoint:
    
        ENDPOINT_ID=$(gcloud ai endpoints list \
            --region=LOCATION \
            --filter=display_name=ENDPOINT_NAME \
            --format="value(name)")

2.  Get the model ID for your model:
    
        MODEL_ID=$(gcloud ai models list \
            --region=LOCATION \
            --filter=display_name=DEPLOYED_MODEL_NAME \
            --format="value(name)")

3.  Deploy the model to the endpoint:
    
        gcloud ai endpoints deploy-model $ENDPOINT_ID \
            --region=LOCATION \
            --model=$MODEL_ID \
            --display-name=DEPLOYED_MODEL_NAME \
            --machine-type=ct5lp-hightpu-4t \
            --tpu-topology=4x4 \
            --traffic-split=0=100
    
    Replace DEPLOYED\_MODEL\_NAME with a name for the deployed. This can be the same as the model display name ( MODEL\_DISPLAY\_NAME ).
    
    The deployment operation might time out.
    
    The `deploy-model` command returns an operation ID that can be used to check when the operation is finished. You can poll for the status of the operation until the response includes `"done": true` . Use the following command to poll the status:
    
        gcloud ai operations describe \
        --region=LOCATION \
        OPERATION_ID
    
    Replace OPERATION\_ID with the operation ID that was returned by the previous command.

## Get online inferences from the deployed model

To get online inferences from the Gemini Enterprise Agent Platform endpoint, run the [`gcloud ai endpoints predict` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/predict) .

1.  Run the following command to create a `request.json` file containing a sample inference request:
    
        cat << EOF > request.json
        {"instances": [{"text_batch": "the distance between Earth and Moon is "}]}
        EOF

2.  To send the online inference request to the endpoint, run the following command:
    
        gcloud ai endpoints predict $ENDPOINT_ID \
            --project=PROJECT_ID \
            --region=LOCATION \
            --json-request=request.json

## Clean up

To avoid incurring further [Gemini Enterprise Agent Platform charges](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) , delete the Google Cloud resources that you created during this tutorial:

1.  To undeploy the model from the endpoint and delete the endpoint, run the following commands:
    
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

2.  To delete your model, run the following commands:
    
        MODEL_ID=$(gcloud ai models list \
           --region=LOCATION \
           --filter=display_name=DEPLOYED_MODEL_NAME \
           --format="value(name)")
        
        gcloud ai models delete $MODEL_ID \
           --region=LOCATION \
           --quiet
