---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/model-garden-published-notebooks/model_garden_advanced_features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/model-garden-published-notebooks/model_garden_advanced_features
title: Agent Platform Model Garden - Advanced Features
data_source: docs.cloud.google.com
---

    # Copyright 2025 Google LLC
    #
    # Licensed under the Apache License, Version 2.0 (the "License");
    # you may not use this file except in compliance with the License.
    # You may obtain a copy of the License at
    #
    #     https://www.apache.org/licenses/LICENSE-2.0
    #
    # Unless required by applicable law or agreed to in writing, software
    # distributed under the License is distributed on an "AS IS" BASIS,
    # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    # See the License for the specific language governing permissions and
    # limitations under the License.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td style="text-align: center;"><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/model-garden-published-notebooks/%7B%20%7Bconsole_url%7D%20%7Dvertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_advanced_features"><img src="https://lh3.googleusercontent.com/JmcxdQi-qOpctIvWKgPtrzZdJJK-J3sWE1RsfjZNwshCFgE_9fULcNpuXYTilIR2hjwN" width="32" alt="Google Cloud Colab Enterprise logo" /><br />
Run in Colab Enterprise</a></td>
<td style="text-align: center;"><a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_advanced_features.ipynb"><img src="https://cloud.google.com/ml-engine/images/github-logo-32px.png" width="32" alt="GitHub logo" /><br />
View on GitHub</a></td>
</tr>
</tbody>
</table>

## Overview

Model optimization has emerged as a crucial step, allowing customers to balance cost-effectiveness, throughput and latency performance. We believe that there is no one-size-fits-all approach to deliver optimal performance for every customer. Even with the same model, the variation can occur as user traffic patterns and requirements may vary for different customers. For example, for chat applications, minimizing latency is key to offer an interactive experience, whereas other applications like recommendations may require maximizing throughput.

This notebook offers a suite of advanced optimization techniques that would help users to customize and optimize AI model performance tailored to your unique use cases and workloads.

### Contents

This tutorial will cover the following topics using Meta-Llama models as examples. You can replace them with any supported models available from Vertex Model Garden.

1.  [**Prefix Caching**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/model-garden-published-notebooks/model_garden_advanced_features#prefix-caching)
2.  [**Speculative Decoding**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/model-garden-published-notebooks/model_garden_advanced_features#spec-decoding)

#### Prefix Caching

Prefix caching reuses computations from previously generated text, eliminating redundant processing. It’s a popular technique to reduce Time-To-First-Token for requests with common prompt prefixes. Typical use cases: Ask different questions with the same long documents as context; Multi-turn chat conversations.

#### Speculative Decoding

Serving large LLM could be slow, and speculative decoding is a very effective optimization technique to reduce generation Time-Per-Output-Token latency. The standard LLM would generate tokens one-by-one sequentially with autoregressive decoding. In contrast, with speculative decoding, we use a fast drafter to efficiently guess multiple tokens and then utilize the larger LLM to verify them in parallel.

### Costs

This tutorial uses billable components of Google Cloud:

  - Agent Platform
  - Cloud Storage

Learn about [Agent Platform pricing](https://cloud.google.com/vertex-ai/pricing) , [Cloud Storage pricing](https://cloud.google.com/storage/pricing) , and use the [Pricing Calculator](https://cloud.google.com/products/calculator/) to generate a cost estimate based on your projected usage.

## Before you begin

### Request for quota

You may require the following quotas to be able to try out the examples from this notebook:

  - Custom model serving TPU v5e cores per region
  - Custom model serving Nvidia A100 80GB GPUs per region

By default, the quota for TPU deployment `Custom model serving TPU v5e cores per region` is 4, which is sufficient for serving the Llama 3.1 8B model. The Llama 3.1 70B model requires 16 TPU v5e cores. TPU quota is only available in `us-west1` . You can request for higher TPU quota following the instructions at ["Request a higher quota"](https://cloud.google.com/docs/quota/view-manage#requesting_higher_quota) .

The quota for A100\_80GB deployment `Custom model serving Nvidia A100 80GB GPUs per region` is 0. You need to request at least 4 for 70B model and 1 for 8B model following the instructions at ["Request a higher quota"](https://cloud.google.com/docs/quota/view-manage#requesting_higher_quota) .

    # @title Setup Google Cloud Project
    
    # @markdown 1. [Make sure that billing is enabled for your project](https://cloud.google.com/billing/docs/how-to/modify-project).
    
    # @markdown 2. **[Optional]** [Create a Cloud Storage bucket](https://cloud.google.com/storage/docs/creating-buckets) for storing experiment outputs. Set the BUCKET_URI for the experiment environment. The specified Cloud Storage bucket (`BUCKET_URI`) should be located in the same region as where the notebook was launched. Note that a multi-region bucket (eg. "us") is not considered a match for a single region covered by the multi-region range (eg. "us-central1"). If not set, a unique GCS bucket will be created instead.
    
    BUCKET_URI = "gs://"  # @param {type:"string"}
    
    # @markdown 3. **[Optional]** Set region. If not set, the region will be set automatically according to Colab Enterprise environment.
    
    REGION = ""  # @param {type:"string"}
    
    # @markdown 4. If you want to run predictions with A100 80GB or H100 GPUs, we recommend using the regions listed below. **NOTE:** Make sure you have associated quota in selected regions. Click the links to see your current quota for each GPU type: [Nvidia A100 80GB]({ {console_url} }iam-admin/quotas?metric=aiplatform.googleapis.com%2Fcustom_model_serving_nvidia_a100_80gb_gpus), [Nvidia H100 80GB]({ {console_url} }iam-admin/quotas?metric=aiplatform.googleapis.com%2Fcustom_model_serving_nvidia_h100_gpus). You can request for quota following the instructions at ["Request a higher quota"](https://cloud.google.com/docs/quota/view-manage#requesting_higher_quota).
    
    # @markdown > | Machine Type | Accelerator Type | Recommended Regions |
    # @markdown | ----------- | ----------- | ----------- |
    # @markdown | a2-ultragpu-1g | 1 NVIDIA_A100_80GB | us-central1, us-east4, europe-west4, asia-southeast1, us-east4 |
    # @markdown | a3-highgpu-2g | 2 NVIDIA_H100_80GB | us-west1, asia-southeast1, europe-west4 |
    # @markdown | a3-highgpu-4g | 4 NVIDIA_H100_80GB | us-west1, asia-southeast1, europe-west4 |
    # @markdown | a3-highgpu-8g | 8 NVIDIA_H100_80GB | us-central1, europe-west4, us-west1, asia-southeast1 |
    
    # Install and import the necessary packages
    ! pip install -q openai google-auth requests
    
    ! git clone https://github.com/GoogleCloudPlatform/vertex-ai-samples.git
    
    import datetime
    import importlib
    import os
    import uuid
    from typing import Tuple
    
    from google.cloud import aiplatform
    
    common_util = importlib.import_module(
        "vertex-ai-samples.community-content.vertex_model_garden.model_oss.notebook_util.common_util"
    )
    
    models, endpoints = {}, {}
    
    # Get the default cloud project id.
    PROJECT_ID = os.environ["GOOGLE_CLOUD_PROJECT"]
    
    # Get the default region for launching jobs.
    if not REGION:
        REGION = os.environ["GOOGLE_CLOUD_REGION"]
    
    # Enable the Agent Platform API and Compute Engine API, if not already.
    print("Enabling Agent Platform API and Compute Engine API.")
    ! gcloud services enable aiplatform.googleapis.com compute.googleapis.com
    
    # Cloud Storage bucket for storing the experiment artifacts.
    # A unique GCS bucket will be created for the purpose of this notebook. If you
    # prefer using your own GCS bucket, change the value yourself below.
    now = datetime.datetime.now().strftime("%Y%m%d%H%M%S")
    BUCKET_NAME = "/".join(BUCKET_URI.split("/")[:3])
    
    if BUCKET_URI is None or BUCKET_URI.strip() == "" or BUCKET_URI == "gs://":
        BUCKET_URI = f"gs://{PROJECT_ID}-tmp-{now}-{str(uuid.uuid4())[:4]}"
        BUCKET_NAME = "/".join(BUCKET_URI.split("/")[:3])
        ! gsutil mb -l {REGION} {BUCKET_URI}
    else:
        assert BUCKET_URI.startswith("gs://"), "BUCKET_URI must start with `gs://`."
        shell_output = ! gsutil ls -Lb {BUCKET_NAME} | grep "Location constraint:" | sed "s/Location constraint://"
        bucket_region = shell_output[0].strip().lower()
        if bucket_region != REGION:
            raise ValueError(
                "Bucket region %s is different from notebook region %s"
                % (bucket_region, REGION)
            )
    print(f"Using this GCS Bucket: {BUCKET_URI}")
    
    STAGING_BUCKET = os.path.join(BUCKET_URI, "temporal")
    MODEL_BUCKET = os.path.join(BUCKET_URI, "llama3_1")
    
    
    # Initialize Agent Platform API.
    print("Initializing Agent Platform API.")
    aiplatform.init(project=PROJECT_ID, location=REGION, staging_bucket=STAGING_BUCKET)
    
    # Gets the default SERVICE_ACCOUNT.
    shell_output = ! gcloud projects describe $PROJECT_ID
    project_number = shell_output[-1].split(":")[1].strip().replace("'", "")
    SERVICE_ACCOUNT = f"{project_number}-compute@developer.gserviceaccount.com"
    print("Using this default Service Account:", SERVICE_ACCOUNT)
    
    
    # Provision permissions to the SERVICE_ACCOUNT with the GCS bucket
    ! gsutil iam ch serviceAccount:{SERVICE_ACCOUNT}:roles/storage.admin $BUCKET_NAME
    
    ! gcloud config set project $PROJECT_ID
    ! gcloud projects add-iam-policy-binding --no-user-output-enabled {PROJECT_ID} --member=serviceAccount:{SERVICE_ACCOUNT} --role="roles/storage.admin"
    ! gcloud projects add-iam-policy-binding --no-user-output-enabled {PROJECT_ID} --member=serviceAccount:{SERVICE_ACCOUNT} --role="roles/aiplatform.user"

### Access Llama 3.1, 3.2, and 3.3 models on Agent Platform for serving

    # @title Llama Model Artifacts
    # @markdown The original models from Meta are converted into the Hugging Face format for serving in Agent Platform.
    # @markdown Accept the model agreement to access the models:
    # @markdown 1. Open the Llama model card from [Agent Platform Model Garden](https://cloud.google.com/model-garden).
    # @markdown    - [Llama 3.1 model card]({ {console_url} }vertex-ai/publishers/meta/model-garden/llama3_1).
    # @markdown    - [Llama 3.2 model card]({ {console_url} }vertex-ai/publishers/meta/model-garden/llama3-2).
    # @markdown    - [Llama 3.3 model card]({ {console_url} }vertex-ai/publishers/meta/model-garden/llama3-3).
    # @markdown 2. Review and accept the agreement in the pop-up window on the model card page. If you have previously accepted the model agreement, there will not be a pop-up window on the model card page and this step is not needed.
    # @markdown 3. After accepting the agreement of the model, a `gs://` URI containing Llama pretrained and instruction-tuned models will be shared.
    # @markdown 4. Paste the URI in the `VERTEX_AI_MODEL_GARDEN_LLAMA_3_1`, `VERTEX_AI_MODEL_GARDEN_LLAMA_3_2`, or `VERTEX_AI_MODEL_GARDEN_LLAMA_3_3` field below.
    
    
    VERTEX_AI_MODEL_GARDEN_LLAMA_3_1 = ""  # @param {type:"string", isTemplate:true}
    assert VERTEX_AI_MODEL_GARDEN_LLAMA_3_1, (
        "Click the agreement of Llama 3.1 in Agent Platform Model Garden, and get the"
        " GCS path of Llama 3.1 model artifacts."
    )
    
    VERTEX_AI_MODEL_GARDEN_LLAMA_3_2 = ""  # @param {type:"string", isTemplate:true}
    assert VERTEX_AI_MODEL_GARDEN_LLAMA_3_2, (
        "Click the agreement of Llama 3.2 in Agent Platform Model Garden, and get the"
        " GCS path of Llama 3.2 model artifacts."
    )
    
    VERTEX_AI_MODEL_GARDEN_LLAMA_3_3 = ""  # @param {type:"string", isTemplate:true}
    assert VERTEX_AI_MODEL_GARDEN_LLAMA_3_3, (
        "Click the agreement of Llama 3.3 in Agent Platform Model Garden, and get the"
        " GCS path of Llama 3.1 model artifacts."
    )

## Prefix Caching <span id="prefix-caching"></span>

Prefix caching reduces Time-to-First-Token (TTFT) for prompts that have identical content at the beginning of the prompt, such as company-wide preambles, common system instructions, and multi-turn conversation history. Instead of processing the same input tokens repeatedly, vLLM and Hex-LLM can retain a temporary cache of the processed input token computations to improve TTFT. This can reduce latency by up to 90% for long prompts. For instance, our benchmark using `Meta-Llama-3.1-8B-Instruct` on [SharedGPT dataset](https://huggingface.co/datasets/anon8231489123/ShareGPT_Vicuna_unfiltered/blob/main/ShareGPT_V3_unfiltered_cleaned_split.json) shows signficant TTFT reductions:

| Use case                            | Latency w/o caching (TTFT) | Latency w/ caching (TTFT) |
| :---------------------------------- | -------------------------: | ------------------------: |
| Multi-turn conversation (252 turns) |                     80.34s |           5.28s (-93.43%) |
| Chat with a document (32k tokens)   |                      4.83s |           0.17s (-96.48%) |

### Supported models

Prefix caching supports the following models:

| Serving solution | Model                                                                                                                                                                                                 |
| :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| vLLM             | Text-only LLMs with decoder-only architecture, e.g. Llama 3.1 (8b, 70b), Llama 3.3 (70b) etc.                                                                                                         |
| Hex-LLM          | Llama 2 (7b, 13b), Llama 3 (8b), Llama 3.1 (8b, 70b), Llama 3.2 (1b, 3b), Llama Guard (1b, 8b), CodeLlama (7b, 13b), Gemma (2b, 7b), CodeGemma (2b, 7b), Mistral-7B (v0.2, v0.3), Mixtral-8x7B (v0.1) |

In the following section, you will try out prefix caching with vLLM/Hex-LLM.

### Try out Prefix Caching with Hex-LLM

**Hex-LLM** is a **H** igh- **E** fficiency **L** arge **L** anguage **M** odel (LLM) TPU serving solution built with **XLA** , which is being developed by Google Cloud.

Refer to the "Request for quota" section for TPU quota.

    # @title Deploy the model with `enable_prefix_cache_hbm=True`
    
    # @markdown This section uploads prebuilt Llama 3.1 models to Model Registry and deploys it to a Agent Platform Endpoint. It takes 15 minutes to 1 hour to finish depending on the size of the model.
    
    # @markdown Select one of the four model variations. More model variants will be supported by Hex-LLM in the future.
    MODEL_ID = "Meta-Llama-3.1-8B-Instruct"  # @param ["Meta-Llama-3.1-8B-Instruct", "Meta-Llama-3.1-70B-Instruct"] {allow-input: true, isTemplate: true}
    TPU_DEPLOYMENT_REGION = "us-west1"  # @param ["us-west1"] {isTemplate:true}
    model_id = os.path.join(VERTEX_AI_MODEL_GARDEN_LLAMA_3_1, MODEL_ID)
    hf_model_id = "meta-llama/" + MODEL_ID
    
    # The pre-built serving docker images.
    HEXLLM_DOCKER_URI = "us-docker.pkg.dev/vertex-ai-restricted/vertex-vision-model-garden-dockers/hex-llm-serve:20241210_2323_RC00"
    
    # @markdown Find Agent Platform prediction TPUv5e machine types in
    # @markdown https://cloud.google.com/vertex-ai/docs/predictions/use-tpu#deploy_a_model.
    # @markdown The 8B model variant requires 4 TPU v5e cores single host, and the 70B model variant requires 16 TPU v5e cores 4x4 multi host.
    # @markdown Choose `ct5lp-hightpu-4t` for both 8B and 70B model variants. The multi-host topology will be automatically set based on the model size.
    
    # Sets ct5lp-hightpu-4t (4 TPU chips) to deploy models.
    machine_type = "ct5lp-hightpu-4t"  # @param ["ct5lp-hightpu-4t", "ct5lp-hightpu-8t"]
    # Note: 1 TPU V5 chip has only one core.
    tpu_type = "TPU_V5e"
    
    
    if "8B" in MODEL_ID:
        tpu_count = 4
        tpu_topo = "1x4"
    elif "70B" in MODEL_ID:
        tpu_count = 16
        tpu_topo = "4x4"
    else:
        raise ValueError(f"Unsupported MODEL_ID: {MODEL_ID}")
    
    
    common_util.check_quota(
        project_id=PROJECT_ID,
        region=TPU_DEPLOYMENT_REGION,
        accelerator_type=tpu_type,
        accelerator_count=tpu_count,
        is_for_training=False,
    )
    
    # Server parameters.
    tensor_parallel_size = tpu_count
    
    # @markdown Set the server parameters:
    
    # Fraction of HBM memory allocated for KV cache after model loading. A larger value improves throughput but gives higher risk of TPU out-of-memory errors with long prompts.
    hbm_utilization_factor = 0.8  # @param
    # Maximum number of running sequences in a continuous batch.
    max_running_seqs = 256  # @param
    # Maximum context length for a request.
    max_model_len = 4096  # @param
    # Whether to turn on prefix caching.
    enable_prefix_cache_hbm = True  # @param {type:"boolean"}
    
    # Endpoint configurations.
    min_replica_count = 1
    max_replica_count = 1
    use_dedicated_endpoint = True
    
    
    def deploy_model_hexllm(
        model_name: str,
        model_id: str,
        service_account: str,
        base_model_id: str = None,
        data_parallel_size: int = 1,
        tensor_parallel_size: int = 1,
        machine_type: str = "ct5lp-hightpu-1t",
        tpu_topology: str = "1x1",
        disagg_topology: str = None,
        hbm_utilization_factor: float = 0.6,
        max_running_seqs: int = 256,
        max_model_len: int = 4096,
        enable_prefix_cache_hbm: bool = False,
        endpoint_id: str = "",
        min_replica_count: int = 1,
        max_replica_count: int = 1,
        use_dedicated_endpoint: bool = False,
    ) -> Tuple[aiplatform.Model, aiplatform.Endpoint]:
        """Deploys models with Hex-LLM on TPU in Agent Platform."""
        if endpoint_id:
            aip_endpoint_name = (
                f"projects/{PROJECT_ID}/locations/{REGION}/endpoints/{endpoint_id}"
            )
            endpoint = aiplatform.Endpoint(aip_endpoint_name)
        else:
            endpoint = aiplatform.Endpoint.create(
                display_name=f"{model_name}-endpoint",
                location=TPU_DEPLOYMENT_REGION,
                dedicated_endpoint_enabled=use_dedicated_endpoint,
            )
    
        if not base_model_id:
            base_model_id = model_id
    
        if not tensor_parallel_size:
            tensor_parallel_size = int(machine_type[-2])
    
        num_hosts = int(tpu_topology.split("x")[0])
    
        # Learn more about the supported arguments and environment variables at https://cloud.google.com/gemini-enterprise-agent-platform/models/open-models/use-hex-llm#config-server.
        hexllm_args = [
            "--host=0.0.0.0",
            "--port=7080",
            f"--model={model_id}",
            f"--data_parallel_size={data_parallel_size}",
            f"--tensor_parallel_size={tensor_parallel_size}",
            f"--num_hosts={num_hosts}",
            f"--hbm_utilization_factor={hbm_utilization_factor}",
            f"--max_running_seqs={max_running_seqs}",
            f"--max_model_len={max_model_len}",
        ]
        if disagg_topology:
            hexllm_args.append(f"--disagg_topo={disagg_topology}")
        if enable_prefix_cache_hbm and not disagg_topology:
            hexllm_args.append("--enable_prefix_cache_hbm")
    
        env_vars = {
            "MODEL_ID": base_model_id,
            "HEX_LLM_LOG_LEVEL": "info",
            "DEPLOY_SOURCE": "notebook",
        }
    
        # HF_TOKEN is not a compulsory field and may not be defined.
        try:
            if HF_TOKEN:
                env_vars.update({"HF_TOKEN": HF_TOKEN})
        except:
            pass
    
        model = aiplatform.Model.upload(
            display_name=model_name,
            serving_container_image_uri=HEXLLM_DOCKER_URI,
            serving_container_command=["python", "-m", "hex_llm.server.api_server"],
            serving_container_args=hexllm_args,
            serving_container_ports=[7080],
            serving_container_predict_route="/generate",
            serving_container_health_route="/ping",
            serving_container_environment_variables=env_vars,
            serving_container_shared_memory_size_mb=(16 * 1024),  # 16 GB
            serving_container_deployment_timeout=7200,
            location=TPU_DEPLOYMENT_REGION,
        )
    
        model.deploy(
            endpoint=endpoint,
            machine_type=machine_type,
            tpu_topology=tpu_topology if num_hosts > 1 else None,
            deploy_request_timeout=1800,
            service_account=service_account,
            min_replica_count=min_replica_count,
            max_replica_count=max_replica_count,
            system_labels={
                "NOTEBOOK_NAME": "model_garden_advanced_features",
            },
        )
        return model, endpoint
    
    
    models["hexllm_tpu"], endpoints["hexllm_tpu"] = deploy_model_hexllm(
        model_name=common_util.get_job_name_with_datetime(prefix=MODEL_ID),
        model_id=model_id,
        service_account=SERVICE_ACCOUNT,
        base_model_id=hf_model_id,
        tensor_parallel_size=tensor_parallel_size,
        machine_type=machine_type,
        tpu_topology=tpu_topo,
        hbm_utilization_factor=hbm_utilization_factor,
        max_running_seqs=max_running_seqs,
        max_model_len=max_model_len,
        enable_prefix_cache_hbm=enable_prefix_cache_hbm,
        min_replica_count=min_replica_count,
        max_replica_count=max_replica_count,
        use_dedicated_endpoint=use_dedicated_endpoint,
    )

    # @title Query the model and check cache hits
    
    _region = REGION
    REGION = TPU_DEPLOYMENT_REGION
    
    if use_dedicated_endpoint:
        DEDICATED_ENDPOINT_DNS = endpoints["hexllm_tpu"].gca_resource.dedicated_endpoint_dns
    ENDPOINT_RESOURCE_NAME = endpoints["hexllm_tpu"].resource_name
    
    # @markdown Once deployment succeeds, you can send requests to the endpoint using the OpenAI SDK.
    
    # @markdown Next fill out some request parameters:
    
    # @markdown **Note**: For Hex-LLM, prefix caching only takes effect for prompts exceeding a certain length (512 tokens by default, configurable using [prefill_len_padding](http://cloud/gemini-enterprise-agent-platform/models/open-models/use-hex-llm#config-server)). Therefore, try to collect some long texts like "Shakespeare's Hamlet" and replace the placeholder below.
    
    user_message = "Summarize: [LONG TEXT PLACEHOLDER]"  # @param {type: "string"}
    # @markdown If you encounter the issue like `ServiceUnavailable: 503 Took too long to respond when processing`, you can reduce the maximum number of output tokens, such as set `max_tokens` as 20.
    max_tokens = 50  # @param {type: "integer"}
    temperature = 1.0  # @param {type: "number"}
    
    # @markdown Now we can send a request. Afterwards, you can check the `cached_tokens` field of `usage.prompt_tokens_details` in the response to see how many of the prompt tokens were a cache hit.
    
    # @markdown **Note**: You won't hit cache for the first run. Try to run again with the same `user_message` and you should hit the cache.
    
    import google.auth
    import openai
    
    creds, project = google.auth.default()
    auth_req = google.auth.transport.requests.Request()
    creds.refresh(auth_req)
    
    BASE_URL = (
        f"https://{REGION}-aiplatform.googleapis.com/v1beta1/{ENDPOINT_RESOURCE_NAME}"
    )
    try:
        if use_dedicated_endpoint:
            BASE_URL = f"https://{DEDICATED_ENDPOINT_DNS}/v1beta1/{ENDPOINT_RESOURCE_NAME}"
    except NameError:
        pass
    
    client = openai.OpenAI(base_url=BASE_URL, api_key=creds.token)
    
    model_response = client.chat.completions.create(
        model="",
        messages=[{"role": "user", "content": user_message}],
        temperature=temperature,
        max_tokens=max_tokens,
    )
    if model_response.usage:
        print(f"usage:\n\n{model_response.usage}")
    
    REGION = _region
    
    # @markdown Click "Show Code" to see more details.

    # @title [Optional] Tiny TTFT benchmark (Cache Hit vs Cache Miss)
    
    # @markdown Here is a tiny benchmark to compare TTFTs between Cache Hit and Cache Miss. You can try with different lengthes of prompts to see the impact of cache hits.
    
    import random
    import string
    import time
    
    import matplotlib.pyplot as plt
    import numpy as np
    
    # @markdown **Note**: For Hex-LLM, prefix caching only takes effect for prompts exceeding a certain length (512 tokens by default, configurable using [prefill_len_padding](http://cloud/gemini-enterprise-agent-platform/models/open-models/use-hex-llm#config-server)). Therefore, try to collect some long texts like "Shakespeare's Hamlet" and replace the placeholder below.
    prompt = "Summarize: [LONG TEXT PLACEHOLDER]"  # @param {type: "string"}
    
    # Warm up the prefix cache
    instances = [
        {
            "prompt": prompt,
            "max_tokens": 1,
        },
    ]
    response = endpoints["hexllm_tpu"].predict(
        instances=instances, use_dedicated_endpoint=use_dedicated_endpoint
    )
    
    # TTFT benchmarks for both cache hit and miss
    num_of_trials = 10
    
    # Benchmark for cache hit
    cache_hit_ttft_ms = []
    for _ in range(num_of_trials):
        start_time = time.perf_counter()
        response = endpoints["hexllm_tpu"].predict(
            instances=instances, use_dedicated_endpoint=use_dedicated_endpoint
        )
        cache_hit_ttft_ms.append((time.perf_counter() - start_time) * 1000)
    
    
    # Benchmark for cache miss
    cache_miss_ttft_ms = []
    for _ in range(num_of_trials):
        # Avoid using Prefix Caching
        instances[0]["prompt"] = (
            random.choice(string.printable) + instances[0]["prompt"][1:]
        )
        start_time = time.perf_counter()
        response = endpoints["hexllm_tpu"].predict(
            instances=instances, use_dedicated_endpoint=use_dedicated_endpoint
        )
        cache_miss_ttft_ms.append((time.perf_counter() - start_time) * 1000)
    
    # Plot to reveal TTFT reduction in case of cache hit
    fig, ax = plt.subplots()
    
    ax.bar(
        ["Cache Miss", "Cache Hit"],
        [np.median(cache_miss_ttft_ms), np.median(cache_hit_ttft_ms)],
        color=["skyblue", "lightcoral"],
    )
    ax.set_ylabel("TTFT (ms)")
    ax.set_title("Time-to-First-Token (TTFT) by Cache Hit/Miss")
    
    plt.show()

#### Delete the models and endpoints

    # @markdown  Delete the models and endpoints to recycle the resources
    # @markdown  for the next experiment.
    
    # Undeploy model and delete endpoint.
    for endpoint in endpoints.values():
        try:
            endpoint.delete(force=True)
        except google.api_core.exceptions.NotFound:
            pass
    
    # Delete models.
    for model in models.values():
        try:
            model.delete()
        except google.api_core.exceptions.NotFound:
            pass

### Try out Prefix Caching with vLLM

### Caching in GPU Memory

OSS vLLM provides an option to enable GPU memory prefix kv caching. The GPU memory cache is fast yet relatively small in size. For example, if using a3-high-gpu-4g VM (with 4xH100\_80G) to serve a Llama3.1-70B model, the capacity for GPU cache size will be capped below 180GB (320GB - 140GB (model weight)).

### Caching in VM Host Memory

Vertex Model Garden’s prebuilt vLLM additionally supports caching prefix kv in the VM host memory. Caching in VM host memory is not as fast as caching in GPU memory. On cache hit, the cached kv state needs to be transferred from host memory to GPU memory before it can be reused by the LLM computation. However, the host memory cache is larger in size, allowing more data to be cached and therefore improving Time to First Token (TTFT). Same example: using a3-high-gpu-4g VM to serve a Llama3.1-70B model, the capacity for the host memory cache can be up to 936 GB.

When host memory kv cache is enabled, the processed requests’ kv state will be written to both GPU cache and host cache. The write-to-host-memory-cache operation runs asynchronously in the background, without hurting the performance of vLLM inference requests.

We benchmarked workloads without common prefixes (each request has \~3k tokens prompt, \~250 output-tokens): the extra write-to-host-memory-cache operation has **\<2%** impact on latency of inference requests.

We also benchmarked workloads that cache-miss in GPU cache and cache-hit in host cache with various prompt-lengths (1k-3k), number-of-concurrent-requests (1-30), and cache-hit-ratio (50%-100%), and see **20-75%** TTFT improvement. For example: For Llama3-1-8B, with 1 concurrent-request, 3k-tokens prompt’s TTFT improves by 43%, if fully cached in the host memory cache. For Llama3-1-70B, the improvement is 57%. The observed TTFT improvement grows with longer cached prompt prefixes and higher system load.

    # @title Deploy the model to vLLM with GPU memory cache and host memory cache enabled
    
    # @markdown This section uploads prebuilt Llama 3.1 models to Model Registry and deploys it to a Agent Platform Endpoint. It takes 15 minutes to 1 hour to finish depending on the size of the model.
    
    # @markdown NVIDIA_A100_80GB is used for demonstration, plase make sure you have quota.
    
    # @markdown Set the model to deploy.
    
    base_model_name = "Meta-Llama-3.1-8B-Instruct"  # @param ["Meta-Llama-3.1-8B-Instruct", "Meta-Llama-3.1-70B-Instruct"] {isTemplate:true}
    model_id = os.path.join(VERTEX_AI_MODEL_GARDEN_LLAMA_3_1, base_model_name)
    hf_model_id = "meta-llama/" + base_model_name
    
    # The pre-built serving docker images.
    VLLM_DOCKER_URI = "us-docker.pkg.dev/vertex-ai/vertex-vision-model-garden-dockers/pytorch-vllm-serve:20250116_0916_RC00"
    
    # @markdown Set **enable-prefix-caching** to True to enable [GPU memory cache](https://docs.vllm.ai/en/latest/features/automatic_prefix_caching.html).
    
    # @markdown Set **host-prefix-kv-cache_utilization-target** to a value (0, 1) to additionally enable host memory cache. It configures the ratio of idle host memory set aside for host memory cache. Setting **host-prefix-kv-cache_utilization-target** to 0 will disable host memory cache. Optionally, we could tune **host-prefix-kv-cache-min-len**. It’s a knob that controls the minimum sequence length that will be cached in the host memory cache. The default value is 1024. Given that the self-attention computation of prompt is quadratic to sequence length, short sequences may not see benefit of using host cache as their prompt prefill time is too short to justify the overhead of host memory to GPU memory data transfer.
    if "8b" in base_model_name.lower():
        accelerator_type = "NVIDIA_A100_80GB"
        machine_type = "a2-ultragpu-1g"
        accelerator_count = 1
    elif "70b" in base_model_name.lower():
        accelerator_type = "NVIDIA_A100_80GB"
        machine_type = "a2-ultragpu-4g"
        accelerator_count = 4
    else:
        raise ValueError(f"Recommended GPU setting not found for: {base_model_name}.")
    
    use_dedicated_endpoint = True
    
    common_util.check_quota(
        project_id=PROJECT_ID,
        region=REGION,
        accelerator_type=accelerator_type,
        accelerator_count=accelerator_count,
        is_for_training=False,
    )
    
    gpu_memory_utilization = 0.85
    max_model_len = 131072  # Maximum context length.
    
    
    # Enable automatic prefix caching using GPU HBM
    enable_prefix_cache = True  # @param {type:"boolean"}
    # Setting this value >0 will use the idle host memory for a second-tier prefix kv
    # cache beneath the HBM cache. It only has effect if enable_prefix_cache=True.
    # The range of this value: [0, 1)
    # Setting host_prefix_kv_cache_utilization_target to 0 will disable the host memory prefix kv cache.
    host_prefix_kv_cache_utilization_target = 0.75  # @param {type:"number"}
    host_prefix_kv_cache_min_len = 1024  # @param {type:"integer"}
    
    
    def deploy_model_vllm(
        model_name: str,
        model_id: str,
        service_account: str,
        base_model_id: str = None,
        machine_type: str = "g2-standard-8",
        accelerator_type: str = "NVIDIA_L4",
        accelerator_count: int = 1,
        gpu_memory_utilization: float = 0.9,
        max_model_len: int = 4096,
        dtype: str = "auto",
        enable_trust_remote_code: bool = False,
        enforce_eager: bool = False,
        enable_lora: bool = False,
        enable_chunked_prefill: bool = False,
        enable_prefix_cache: bool = False,
        host_prefix_kv_cache_utilization_target: float = 0.0,
        host_prefix_kv_cache_min_len: int = 1024,
        max_loras: int = 1,
        max_cpu_loras: int = 8,
        use_dedicated_endpoint: bool = False,
        max_num_seqs: int = 256,
        model_type: str = None,
    ) -> Tuple[aiplatform.Model, aiplatform.Endpoint]:
        """Deploys trained models with vLLM into Agent Platform."""
        endpoint = aiplatform.Endpoint.create(
            display_name=f"{model_name}-endpoint",
            dedicated_endpoint_enabled=use_dedicated_endpoint,
        )
    
        if not base_model_id:
            base_model_id = model_id
    
        # See https://docs.vllm.ai/en/latest/models/engine_args.html for a list of possible arguments with descriptions.
        vllm_args = [
            "python",
            "-m",
            "vllm.entrypoints.api_server",
            "--host=0.0.0.0",
            "--port=8080",
            f"--model={model_id}",
            f"--tensor-parallel-size={accelerator_count}",
            "--swap-space=16",
            f"--gpu-memory-utilization={gpu_memory_utilization}",
            f"--max-model-len={max_model_len}",
            f"--dtype={dtype}",
            f"--max-loras={max_loras}",
            f"--max-cpu-loras={max_cpu_loras}",
            f"--max-num-seqs={max_num_seqs}",
            "--disable-log-stats",
        ]
    
        if enable_trust_remote_code:
            vllm_args.append("--trust-remote-code")
    
        if enforce_eager:
            vllm_args.append("--enforce-eager")
    
        if enable_lora:
            vllm_args.append("--enable-lora")
    
        if enable_chunked_prefill:
            vllm_args.append("--enable-chunked-prefill")
    
        if enable_prefix_cache:
            vllm_args.append("--enable-prefix-caching")
    
        if 0 < host_prefix_kv_cache_utilization_target < 1:
            vllm_args.append(
                f"--host-prefix-kv-cache-utilization-target={host_prefix_kv_cache_utilization_target}"
            )
            vllm_args.append(
                f"--host-prefix-kv-cache-min-len={host_prefix_kv_cache_min_len}"
            )
    
        if model_type:
            vllm_args.append(f"--model-type={model_type}")
    
        env_vars = {
            "MODEL_ID": base_model_id,
            "DEPLOY_SOURCE": "notebook",
        }
    
        # HF_TOKEN is not a compulsory field and may not be defined.
        try:
            if HF_TOKEN:
                env_vars["HF_TOKEN"] = HF_TOKEN
        except NameError:
            pass
    
        model = aiplatform.Model.upload(
            display_name=model_name,
            serving_container_image_uri=VLLM_DOCKER_URI,
            serving_container_args=vllm_args,
            serving_container_ports=[8080],
            serving_container_predict_route="/generate",
            serving_container_health_route="/ping",
            serving_container_environment_variables=env_vars,
            serving_container_shared_memory_size_mb=(16 * 1024),  # 16 GB
            serving_container_deployment_timeout=7200,
        )
        print(
            f"Deploying {model_name} on {machine_type} with"
            f" {accelerator_count} {accelerator_type} GPU(s)."
        )
        model.deploy(
            endpoint=endpoint,
            machine_type=machine_type,
            accelerator_type=accelerator_type,
            accelerator_count=accelerator_count,
            deploy_request_timeout=1800,
            service_account=service_account,
            system_labels={
                "NOTEBOOK_NAME": "model_garden_advanced_features",
            },
        )
        print("endpoint_name:", endpoint.name)
    
        return model, endpoint
    
    
    models["vllm_gpu"], endpoints["vllm_gpu"] = deploy_model_vllm(
        model_name=common_util.get_job_name_with_datetime(prefix="llama3_1-serve"),
        model_id=model_id,
        base_model_id=hf_model_id,
        service_account=SERVICE_ACCOUNT,
        machine_type=machine_type,
        accelerator_type=accelerator_type,
        accelerator_count=accelerator_count,
        gpu_memory_utilization=gpu_memory_utilization,
        max_model_len=max_model_len,
        enforce_eager=True,
        enable_chunked_prefill=True,
        enable_prefix_cache=enable_prefix_cache,
        host_prefix_kv_cache_utilization_target=host_prefix_kv_cache_utilization_target,
        host_prefix_kv_cache_min_len=host_prefix_kv_cache_min_len,
        use_dedicated_endpoint=use_dedicated_endpoint,
    )
    # @markdown Click "Show Code" to see more details.

    # @title Query the model and check cache hits
    
    if use_dedicated_endpoint:
        DEDICATED_ENDPOINT_DNS = endpoints["vllm_gpu"].gca_resource.dedicated_endpoint_dns
    ENDPOINT_RESOURCE_NAME = endpoints["vllm_gpu"].resource_name
    
    # @markdown Once deployment succeeds, you can send requests to the endpoint using the OpenAI SDK.
    
    # @markdown Next fill out some request parameters:
    
    # @markdown **Note**: For vLLM, the smallest unit of cache hit is a token block, which is 32 tokens by default. Therefore, try to collect some long texts like "Shakespeare's Hamlet" and replace the placeholder below.
    
    user_message = "Summarize: [LONG TEXT PLACEHOLDER]"  # @param {type: "string"}
    # @markdown If you encounter the issue like `ServiceUnavailable: 503 Took too long to respond when processing`, you can reduce the maximum number of output tokens, such as set `max_tokens` as 20.
    max_tokens = 50  # @param {type: "integer"}
    temperature = 1.0  # @param {type: "number"}
    
    # @markdown Now you can send a request. Afterwards, you can check the `cached_tokens` field of `usage.prompt_tokens_details` in the response to see how many of the prompt tokens were a cache hit.
    
    # @markdown **Note**: You won't hit cache for the first run. Try to run again with the same `user_message` and you should hit the cache. Note that hitting in either GPU memory or host memory will be counted as a cache hit.
    
    import google.auth
    import openai
    
    creds, _ = google.auth.default()
    auth_req = google.auth.transport.requests.Request()
    creds.refresh(auth_req)
    
    BASE_URL = (
        f"https://{REGION}-aiplatform.googleapis.com/v1beta1/{ENDPOINT_RESOURCE_NAME}"
    )
    try:
        if use_dedicated_endpoint:
            BASE_URL = f"https://{DEDICATED_ENDPOINT_DNS}/v1beta1/{ENDPOINT_RESOURCE_NAME}"
    except NameError:
        pass
    
    client = openai.OpenAI(base_url=BASE_URL, api_key=creds.token)
    
    model_response = client.chat.completions.create(
        model="",
        messages=[{"role": "user", "content": user_message}],
        temperature=temperature,
        max_tokens=max_tokens,
    )
    print(model_response)
    if model_response.usage:
        print(f"usage:\n\n{model_response.usage}")
    
    
    # @markdown Click "Show Code" to see more details.

    # @title [Optional] Tiny TTFT benchmark (Cache Hit vs Cache Miss)
    
    # @markdown Here is a tiny benchmark to compare TTFTs between Cache Hit and Cache Miss. You can try with different lengthes of prompts to see the impact of cache hits.
    
    import random
    import string
    import time
    
    import matplotlib.pyplot as plt
    import numpy as np
    
    # @markdown **Note**: The beneit of prefix caching is more prominent for long prompts. Therefore, try to collect some long texts like "Shakespeare's Hamlet" and replace the placeholder below.
    prompt = "Summarize: [LONG TEXT PLACEHOLDER]"  # @param {type: "string"}
    
    # Warm up the prefix cache
    instances = [
        {
            "prompt": prompt,
            "max_tokens": 1,
        },
    ]
    response = endpoints["vllm_gpu"].predict(
        instances=instances, use_dedicated_endpoint=use_dedicated_endpoint
    )
    
    # TTFT benchmarks for both cache hit and miss
    num_of_trials = 30
    
    # Benchmark for cache hit
    cache_hit_ttft_ms = []
    for _ in range(num_of_trials):
        start_time = time.perf_counter()
        response = endpoints["vllm_gpu"].predict(
            instances=instances, use_dedicated_endpoint=use_dedicated_endpoint
        )
        cache_hit_ttft_ms.append((time.perf_counter() - start_time) * 1000)
    
    
    # Benchmark for cache miss
    cache_miss_ttft_ms = []
    for _ in range(num_of_trials):
        # Avoid using Prefix Caching
        instances[0]["prompt"] = (
            random.choice(string.printable) + instances[0]["prompt"][1:]
        )
        start_time = time.perf_counter()
        response = endpoints["vllm_gpu"].predict(
            instances=instances, use_dedicated_endpoint=use_dedicated_endpoint
        )
        cache_miss_ttft_ms.append((time.perf_counter() - start_time) * 1000)
    
    # Plot to reveal TTFT reduction in case of cache hit
    fig, ax = plt.subplots()
    
    ax.bar(
        ["Cache Miss", "Cache Hit"],
        [np.median(cache_miss_ttft_ms), np.median(cache_hit_ttft_ms)],
        color=["skyblue", "lightcoral"],
    )
    ax.set_ylabel("TTFT (ms)")
    ax.set_title("Time-to-First-Token (TTFT) by Cache Hit/Miss")
    
    plt.show()

#### Delete the models and endpoints

    # @markdown  Delete the models and endpoints to recycle the resources
    # @markdown  for the next experiment.
    
    # Undeploy model and delete endpoint.
    for endpoint in endpoints.values():
        try:
            endpoint.delete(force=True)
        except google.api_core.exceptions.NotFound:
            pass
    
    # Delete models.
    for model in models.values():
        try:
            model.delete()
        except google.api_core.exceptions.NotFound:
            pass

### Best practices

As you can see from the try-out session above, you need to structure your prompts properly to increase cache hits:

  - Put static contents at the beginning of the prompts and dynamic contents at the end.
  - Try to warm up cache first before running batch queries in order to leverage caching.
  - Monitor metrics (e.g. cache hit rates, latency, and the percentage of tokens cached) to optimize your prompts and caching strategy.

## Speculative Decoding <span id="spec-decoding"></span>

Speculative decoding is an algorithm to sample from autoregressive models faster without any changes to the outputs, by computing several tokens in parallel using a drafter. The algorithm is based on 2 core ideas:

  - A smaller and faster drafter can approximate the target model well enough.
  - The target model can verify multiple drafter outputs in parallel, generating several tokens concurrently without changing the output distribution or model architecture.

How the algorithm works:

  - A small but much faster drafter efficiently proposes multiple tokens
  - Target model verifies all these tokens in one single model forward pass. If target model output differs from the drafted tokens, the first different token and the following ones are rejected
  - This approach can significantly reduce latency without compromising the response quality. For greedy sampling, it's clear that the target model output distribution remains unchanged. For non greedy sampling, we use a [modified rejection sampling algorithm](https://arxiv.org/pdf/2302.01318) to recover the target model distribution which theoretically guarantees the output distribution remains the same

Vertex prebuilt vLLM container supports the following speculation methods:

  - Draft model: The most popular drafter is to use a smaller LLM model that autoregressively generates multiple tokens. Speculation with draft models offers good quality/accuracy, but it requires training or identifying a drafter model that closely aligns with the target LLM
  - N-gram: N-gram matching is an extremely simple method, the good thing about it is it doesn't require any model, and it could still work well for input grounded generation where there is a significant overlap between the prompt and the answer. This could be entity names, phrases, or code chunks that the LLM directly copies from the input while generating the output. So N-gram is suitable for tasks like context based question answering, code editing, etc.

Speculative decoding reduces Time-per-Output-Token (TPOT) up to 55% in our experiments. Here is a list of pre-verified list of model pairs that shows good performance improvements.

| Target Model  | Draft Model  | Speculative Token Count | Machine type  | TPOT w/o Speculative Decoding (ms) | TPOT w/ Speculative Decoding (ms) |
| ------------- | ------------ | ----------------------- | ------------- | ---------------------------------- | --------------------------------- |
| Llama 3.3 70B | Llama 3.2 1B | 3                       | a3-highgpu-8g | 14.96                              | 6.7 (-55.21%)                     |
| Llama 3.1 70B | Llama 3.2 1B | 3                       | a3-highgpu-8g | 18.8                               | 8.05 (-57.18%)                    |
| Llama 3.1 8B  | Llama 3.2 1B | 3                       | a3-highgpu-1g | 8.03                               | 4.53 (-43.59%)                    |

For 70B models, we recommend having at least 4 accelerators. The exact speedup ratio will vary depending on machine type, traffic volume, and request characteristics.

It's possible to choose your own draft and target models as long as they use the same tokenizer and are imported into Vertex Model Registry.

While speculative decoding is great for improving TPOT, there are some caveats to note:

  - The draft model will consume some of the HBM for its weight, KV cache etc. which will increase the HBM usage
  - Time-to-First-Token (TTFT) will increase slightly due to the extra prefill for the draft model.

In the following section, you will try out speculative decoding with vLLM.

### Try out Speculative Decoding with vLLM

    # @title Deploy the model to vLLM with Speculative Decoding
    
    # @markdown This section uploads prebuilt Llama target model and draft model to Model Registry and deploys it to a Agent Platform Endpoint. It takes 15 minutes to 1 hour to finish depending on the size of the model.
    
    # @markdown NVIDIA_A100_80GB is used for demonstration, plase make sure you have quota.
    
    # @markdown Set the model to deploy.
    
    import time
    from typing import Tuple
    
    import google.auth
    import requests
    
    # @markdown Pre-verified `target_model_name`s are `Meta-Llama-3.1-8B-Instruct`, `Meta-Llama-3.1-70B-Instruct`, `Llama-3.3-70B-Instruct`.
    # @markdown Supported speculation methods are `draft_model` and `ngram`.
    # @markdown If using draft model speculation, the corresponding `draft_model_name` is `Llama-3.2-1B-Instruct`.
    
    # The pre-built serving docker images.
    VLLM_DOCKER_URI = "us-docker.pkg.dev/vertex-ai/vertex-vision-model-garden-dockers/pytorch-vllm-serve:20250116_0916_RC00"
    
    target_model_name = "Meta-Llama-3.1-8B-Instruct"  # @param {"type":"string","placeholder":"Meta-Llama-3.1-8B-Instruct"}
    draft_model_name = "Llama-3.2-1B-Instruct"  # @param {"type":"string","placeholder":"Llama-3.2-1B-Instruct"}
    speculative_token_count = 3  # @param {"type":"integer"}
    spec_method = "draft_model"  # @param ["draft_model", "ngram"] {isTemplate:true}
    
    
    def format_model_id(base_model_name: str) -> Tuple[str, str]:
        if "3.3" in base_model_name:
            model_id = os.path.join(VERTEX_AI_MODEL_GARDEN_LLAMA_3_3, base_model_name)
            hf_model_id = "meta-llama/" + base_model_name
        elif "3.2" in base_model_name:
            model_id = os.path.join(VERTEX_AI_MODEL_GARDEN_LLAMA_3_2, base_model_name)
            hf_model_id = "meta-llama/" + base_model_name
        elif "3.1" in base_model_name:
            model_id = os.path.join(VERTEX_AI_MODEL_GARDEN_LLAMA_3_1, base_model_name)
            hf_model_id = "meta-llama/" + base_model_name
        else:
            raise ValueError(f"Unsupported base model name: {base_model_name}.")
        return model_id, hf_model_id
    
    
    target_model_id, hf_model_id = format_model_id(target_model_name)
    draft_model_id, _ = format_model_id(draft_model_name)
    
    if "8b" in target_model_name.lower():
        accelerator_type = "NVIDIA_A100_80GB"
        machine_type = "a2-ultragpu-1g"
        accelerator_count = 1
    elif "70b" in target_model_name.lower():
        accelerator_type = "NVIDIA_A100_80GB"
        machine_type = "a2-ultragpu-4g"
        accelerator_count = 4
    else:
        raise ValueError(f"Recommended GPU setting not found for: {target_model_name}.")
    
    common_util.check_quota(
        project_id=PROJECT_ID,
        region=REGION,
        accelerator_type=accelerator_type,
        accelerator_count=accelerator_count,
        is_for_training=False,
    )
    
    gpu_memory_utilization = 0.85
    max_model_len = 131072  # Maximum context length.
    use_dedicated_endpoint = False
    
    
    def poll_operation(op_name: str) -> bool:
        creds, _ = google.auth.default()
        auth_req = google.auth.transport.requests.Request()
        creds.refresh(auth_req)
        headers = {
            "Authorization": f"Bearer {creds.token}",
        }
        get_resp = requests.get(
            f"https://{REGION}-aiplatform.googleapis.com/v1beta1/{op_name}",
            headers=headers,
        )
        opjs = get_resp.json()
        if "error" in opjs:
            raise ValueError(f"Operation failed: {opjs['error']}")
        return opjs.get("done", False)
    
    
    def poll_and_wait(op_name: str, total_wait: int, interval: int = 60):
        waited = 0
        while not poll_operation(op_name):
            if waited > total_wait:
                raise TimeoutError("Operation timed out")
            print(
                f"\rStill waiting for operation... Waited time in second: {waited:<6}",
                end="",
                flush=True,
            )
            waited += interval
            time.sleep(interval)
    
    
    def deploy_model_vllm_speculative_decoding(
        model_name: str,
        model_id: str,
        service_account: str,
        base_model_id: str = None,
        machine_type: str = "g2-standard-8",
        accelerator_type: str = "NVIDIA_L4",
        accelerator_count: int = 1,
        gpu_memory_utilization: float = 0.9,
        max_model_len: int = 4096,
        dtype: str = "auto",
        enable_trust_remote_code: bool = False,
        enforce_eager: bool = False,
        enable_chunked_prefill: bool = False,
        use_dedicated_endpoint: bool = False,
        max_num_seqs: int = 256,
        model_type: str = None,
        enable_speculative_decoding: bool = False,
        speculation_method: str = "draft_model",
        draft_model_name: str = None,
        draft_model_id: str = None,
        speculative_token_count: int = 3,
        ngram_size: int = 3,
    ) -> Tuple[aiplatform.Model, aiplatform.Endpoint]:
        """Deploys trained models with vLLM into Agent Platform."""
        endpoint = aiplatform.Endpoint.create(
            display_name=f"{model_name}-endpoint",
            dedicated_endpoint_enabled=use_dedicated_endpoint,
        )
    
        if not base_model_id:
            base_model_id = model_id
    
        # See https://docs.vllm.ai/en/latest/models/engine_args.html for a list of possible arguments with descriptions.
        vllm_args = [
            "python",
            "-m",
            "vllm.entrypoints.api_server",
            "--host=0.0.0.0",
            "--port=8080",
            f"--model={model_id}",
            f"--tensor-parallel-size={accelerator_count}",
            "--swap-space=16",
            f"--gpu-memory-utilization={gpu_memory_utilization}",
            f"--max-model-len={max_model_len}",
            f"--dtype={dtype}",
            f"--max-num-seqs={max_num_seqs}",
            "--disable-log-stats",
        ]
    
        if enable_trust_remote_code:
            vllm_args.append("--trust-remote-code")
    
        if enforce_eager:
            vllm_args.append("--enforce-eager")
    
        if enable_chunked_prefill:
            vllm_args.append("--enable-chunked-prefill")
    
        if model_type:
            vllm_args.append(f"--model-type={model_type}")
    
        env_vars = {
            "MODEL_ID": base_model_id,
            "DEPLOY_SOURCE": "notebook",
        }
    
        # HF_TOKEN is not a compulsory field and may not be defined.
        try:
            if HF_TOKEN:
                env_vars["HF_TOKEN"] = HF_TOKEN
        except NameError:
            pass
    
        draft_model = None
        draft_resource_name = draft_model_id
        if speculation_method == "draft_model":
            print("Uploading draft model...")
            drafter_vllm_args = [
                "python",
                "-m",
                "vllm.entrypoints.api_server",
                "--host=0.0.0.0",
                "--port=8080",
                f"--model={draft_model_id}",
                f"--tensor-parallel-size={accelerator_count}",
                "--swap-space=16",
                f"--gpu-memory-utilization={gpu_memory_utilization}",
                f"--max-model-len={max_model_len}",
                f"--dtype={dtype}",
                f"--max-num-seqs={max_num_seqs}",
                "--disable-log-stats",
            ]
            draft_model = aiplatform.Model.upload(
                display_name=draft_model_name,
                serving_container_image_uri=VLLM_DOCKER_URI,
                serving_container_args=drafter_vllm_args,
                serving_container_ports=[8080],
                serving_container_predict_route="/generate",
                serving_container_health_route="/ping",
                serving_container_shared_memory_size_mb=(16 * 1024),
                serving_container_deployment_timeout=7200,
            )
            draft_resource_name = draft_model.resource_name
    
        print("Uploading target model...")
        model = aiplatform.Model.upload(
            display_name=model_name,
            serving_container_image_uri=VLLM_DOCKER_URI,
            serving_container_args=vllm_args,
            serving_container_ports=[8080],
            serving_container_predict_route="/generate",
            serving_container_health_route="/ping",
            serving_container_environment_variables=env_vars,
            serving_container_shared_memory_size_mb=(16 * 1024),
            serving_container_deployment_timeout=7200,
        )
    
        print(
            f"Deploying {model_name} on {machine_type} with"
            f" {accelerator_count} {accelerator_type} GPU(s)."
        )
    
        creds, _ = google.auth.default()
        auth_req = google.auth.transport.requests.Request()
        creds.refresh(auth_req)
    
        url = f"https://{REGION}-aiplatform.googleapis.com/v1beta1/projects/{PROJECT_ID}/locations/{REGION}/endpoints/{endpoint.name}:deployModel"
        headers = {
            "Content-Type": "application/json",
            "Authorization": f"Bearer {creds.token}",
        }
        data = {
            "deployedModel": {
                "model": model.resource_name,
                "displayName": model_name,
                "dedicatedResources": {
                    "machineSpec": {
                        "machineType": machine_type,
                        "acceleratorType": accelerator_type,
                        "acceleratorCount": accelerator_count,
                    },
                    "minReplicaCount": 1,
                    "maxReplicaCount": 1,
                },
                "serviceAccount": service_account,
                "systemLabels": {
                    "NOTEBOOK_NAME": "model_garden_advanced_features",
                },
            },
        }
        if enable_speculative_decoding:
            if speculation_method == "ngram":
                data["deployedModel"]["speculativeDecodingSpec"] = {
                    "speculativeTokenCount": speculative_token_count,
                    "ngramSpeculation": {"ngramSize": ngram_size},
                }
            elif speculation_method == "draft_model":
                data["deployedModel"]["speculativeDecodingSpec"] = {
                    "speculativeTokenCount": speculative_token_count,
                    "draftModelSpeculation": {
                        "draftModel": draft_resource_name,
                    },
                }
            else:
                raise ValueError(f"Unsupported speculation method: {speculation_method}.")
        response = requests.post(url, headers=headers, json=data)
        print(f"Deploy Model response: {response.json()}")
        if response.status_code != 200 or "name" not in response.json():
            raise ValueError(f"Failed to deploy model: {response.text}")
        poll_and_wait(response.json()["name"], 3600)
        return model, draft_model, endpoint
    
    
    (
        models["vllm_gpu_target"],
        draft_model,
        endpoints["vllm_gpu_spec"],
    ) = deploy_model_vllm_speculative_decoding(
        model_name=common_util.get_job_name_with_datetime(
            prefix="llama-spec-decoding-target"
        ),
        model_id=target_model_id,
        base_model_id=hf_model_id,
        service_account=SERVICE_ACCOUNT,
        machine_type=machine_type,
        accelerator_type=accelerator_type,
        accelerator_count=accelerator_count,
        gpu_memory_utilization=gpu_memory_utilization,
        max_model_len=max_model_len,
        enforce_eager=False,
        enable_chunked_prefill=True,
        use_dedicated_endpoint=use_dedicated_endpoint,
        enable_speculative_decoding=True,
        speculation_method=spec_method,
        speculative_token_count=speculative_token_count,
        draft_model_id=draft_model_id,
        draft_model_name=common_util.get_job_name_with_datetime(
            prefix="llama-spec-decoding-draft"
        ),
        ngram_size=3,
    )
    if draft_model:
        models["vllm_gpu_draft"] = draft_model
    # @markdown Click "Show Code" to see more details.

    # @title Query the model and check TPOT
    
    import time
    
    import google.auth
    import openai
    
    user_message = "Tell me a long story about cat"  # @param {type: "string"}
    max_tokens = 50  # @param {type: "integer"}
    temperature = 1.0  # @param {type: "number"}
    
    # @markdown Now we can send a request. We will use the OpenAI SDK to send requests to the endpoint, and calculate the TTFT and TPOT so that you can compare with the model without speculative decoding.
    
    
    creds, _ = google.auth.default()
    auth_req = google.auth.transport.requests.Request()
    creds.refresh(auth_req)
    
    if use_dedicated_endpoint:
        DEDICATED_ENDPOINT_DNS = endpoints[
            "vllm_gpu_spec"
        ].gca_resource.dedicated_endpoint_dns
    ENDPOINT_RESOURCE_NAME = endpoints["vllm_gpu_spec"].resource_name
    
    BASE_URL = (
        f"https://{REGION}-aiplatform.googleapis.com/v1beta1/{ENDPOINT_RESOURCE_NAME}"
    )
    try:
        if use_dedicated_endpoint:
            BASE_URL = f"https://{DEDICATED_ENDPOINT_DNS}/v1beta1/{ENDPOINT_RESOURCE_NAME}"
    except NameError:
        pass
    
    client = openai.OpenAI(base_url=BASE_URL, api_key=creds.token)
    
    ttft = None
    start_time = time.time()
    end_time = None
    usage = None
    contents = []
    
    response = client.chat.completions.create(
        model="",
        messages=[{"role": "user", "content": user_message}],
        temperature=temperature,
        max_tokens=max_tokens,
        stream=True,
        stream_options={"include_usage": True},
    )
    
    for chunk in response:
        if ttft is None:
            ttft = time.time() - start_time
        if chunk.usage is not None:
            usage = chunk.usage
            end_time = time.time()
            continue
        contents.append(chunk.choices[0].delta.content)
    
    print(
        f"Model response: {''.join(contents)}\nTTFT: {ttft}, TPOT:"
        f" {(end_time - start_time - ttft)/(usage.completion_tokens - 1)}"
    )
    
    # @markdown Click "Show Code" to see more details.

## Clean up resources

### Delete the models and endpoints

    # @markdown  Delete the experiment models and endpoints to recycle the resources
    # @markdown  and avoid unnecessary continuous charges that may incur.
    
    # Undeploy model and delete endpoint.
    for endpoint in endpoints.values():
        try:
            endpoint.delete(force=True)
        except google.api_core.exceptions.NotFound:
            pass
    
    # Delete models.
    for model in models.values():
        try:
            model.delete()
        except google.api_core.exceptions.NotFound:
            pass
    
    delete_bucket = False  # @param {type:"boolean"}
    if delete_bucket:
        ! gsutil -m rm -r $BUCKET_NAME
