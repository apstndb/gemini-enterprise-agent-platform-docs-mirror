---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-model-tuning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-model-tuning
title: Supervised and distillation fine-tuning for open models
description: Learn how to use supervised fine-tuning with open models.
data_source: docs.cloud.google.com
---

> To see an example of supervised fine-tuning an open model, run the "Fine-tuning a Llama model on the MetaMathQA" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/open-models/fine-tuning/get_started_with_oss_tuning_on_vertexai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fopen-models%2Ffine-tuning%2Fget_started_with_oss_tuning_on_vertexai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fopen-models%2Ffine-tuning%2Fget_started_with_oss_tuning_on_vertexai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/open-models/fine-tuning/get_started_with_oss_tuning_on_vertexai.ipynb)

This page describes how to perform [supervised and distillation fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models) on open models such as Llama 3.1. Unless stated otherwise, the instructions on this page apply to both supervised fine-tuning and distillation fine-tuning. Distillation lets you tune a smaller student model using the outputs of a larger teacher model.

## Supported tuning modes

  - **Supervised fine-tuning:**
      - [Full fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models#tuning-approaches)
      - Low-Rank Adaptation (LoRA): LoRA is a [parameter-efficient tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models#tuning-approaches) mode that only adjust subset of parameters. It's more cost efficient and require less training data than full fine-tuning. On the other hand, full fine-tuning has higher quality potential by adjusting all parameters.
  - **Distillation fine-tuning:** Distillation fine-tuning uses the GenAI SDK, where you specify a teacher model to generate responses that are then used to tune a smaller student model.

### Recommended use cases for distillation fine-tuning

Distillation fine-tuning is most effective when the teacher model is substantially more capable than the student on the target task. It is recommended for transferring complex, multi-step **reasoning** capabilities from a larger teacher to a smaller student, including:

  - Math and quantitative reasoning
  - Scientific, medical, and other domain-specific question answering that requires step-by-step reasoning
  - Other tasks where a strong teacher model with "thinking" or chain-of-thought behavior consistently produces higher-quality responses than the student.

Distillation provides smaller gains on tasks where the student model already performs close to the teacher, or on short-form retrieval tasks where the teacher's reasoning trace does not add value.

## Supported models

#### Supervised fine-tuning supported models

  - Gemma 3 1B IT ( `google/gemma3@gemma-3-1b-it` )
  - Gemma 3 4B IT ( `google/gemma3@gemma-3-4b-it` )
  - Gemma 3 12B IT ( `google/gemma3@gemma-3-12b-it` )
  - Gemma 3 27B IT ( `google/gemma3@gemma-3-27b-it` )
  - Medgemma 1.5 4B IT ( `google/medgemma@medgemma-4b-it` )
  - Llama 3.1 8B ( `meta/llama3_1@llama-3.1-8b` )
  - Llama 3.1 8B Instruct ( `meta/llama3_1@llama-3.1-8b-instruct` )
  - Llama 3.2 1B Instruct ( `meta/llama3-2@llama-3.2-1b-instruct` )
  - Llama 3.2 3B Instruct ( `meta/llama3-2@llama-3.2-3b-instruct` )
  - Llama 3.3 70B Instruct ( `meta/llama3-3@llama-3.3-70b-instruct` )
  - Qwen 3 4B ( `qwen/qwen3@qwen3-4b` )
  - Qwen 3 8B ( `qwen/qwen3@qwen3-8b` )
  - Qwen 3 14B ( `qwen/qwen3@qwen3-14b` )
  - Qwen 3 32B ( `qwen/qwen3@qwen3-32b` )
  - Llama 4 Scout 17B 16E Instruct ( `meta/llama4@llama-4-scout-17b-16e-instruct` )

#### Distillation tuning supported models

Supported teacher models:

  - DeepSeek R1 0528 MaaS ( `deepseek-ai/deepseek-r1-0528-maas` )
  - DeepSeek V3.2 MaaS ( `deepseek-ai/deepseek-v3.2-maas` )
  - Qwen 3 Next 80B A3B Thinking MaaS ( `qwen/qwen3-next-80b-a3b-thinking-maas` )

Supported student models:

  - Qwen 3 4B ( `qwen/qwen3@qwen3-4b` )
  - Qwen 3 8B ( `qwen/qwen3@qwen3-8b` )
  - Qwen 3 14B ( `qwen/qwen3@qwen3-14b` )
  - Qwen 3 32B ( `qwen/qwen3@qwen3-32b` )
  - Gemma 3 1B IT ( `google/gemma3@gemma-3-1b-it` )
  - Gemma 3 4B IT ( `google/gemma3@gemma-3-4b-it` )
  - Gemma 3 12B IT ( `google/gemma3@gemma-3-12b-it` )
  - Gemma 3 27B IT ( `google/gemma3@gemma-3-27b-it` )

## Supported regions

  - Iowa ( `us-central1` )
  - Netherlands ( `europe-west4` )
  - Oregon ( `us-west1` )
  - Columbus ( `us-east5` )
  - Singapore ( `asia-southeast1` )

## Limitations

Model

Specification

Value

Gemma 3 1B IT

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Gemma 3 4B IT

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Gemma 3 12B IT

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Gemma 3 27B IT

Tuning modes

Parameter-efficient fine-tuning  
Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Medgemma 1.5 4B IT

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Llama 3.1 8B

Tuning modes

Parameter-efficient fine-tuning  
Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Llama 3.1 8B Instruct

Tuning modes

Parameter-efficient fine-tuning  
Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Llama 3.2 1B Instruct

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Llama 3.2 3B Instruct

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Llama 3.3 70B Instruct

Tuning modes

Parameter-efficient fine-tuning  
Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Llama 4 Scout 17B 16E Instruct

Tuning modes

Parameter-efficient fine-tuning

Maximum sequence length

2048

Modalities

Text  
Images <sup>\*</sup>  
  
<sup>\*</sup> Mixed datasets of both text-only and image examples are not supported. If there is at least one image example in the dataset, all text-only examples will be filtered out.

Qwen 3 4B

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Qwen 3 8B

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Qwen 3 14B

Tuning modes

Full fine-tuning

Maximum sequence length

8192

Modalities

Text

Qwen 3 32B

Tuning modes

Parameter-efficient fine-tuning  
Full fine-tuning

Maximum sequence length

8192

Modalities

Text

## Before you begin

Install the SDK and import the libraries for your tuning method.

### Supervised fine-tuning

[Install and initialize the Vertex AI SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk) , then import the following libraries:

    import os
    import time
    import uuid
    import vertexai
    
    vertexai.init(project=PROJECT_ID, location=REGION)
    
    from google.cloud import aiplatform
    from vertexai.tuning import sft, SourceModel

### Distillation tuning

Install the following SDK:

    pip install google-genai

Then import the following libraries:

    import os
    import time
    import uuid
    
    from google import genai
    from google.genai import types
    client = genai.Client(vertexai=True, project=PROJECT_ID, location=REGION)

## Prepare dataset for tuning

> Before starting the knowledge distillation, you can run [the knowledge distillation feasibility notebook](https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_oss_distillation_feasibility.ipynb) in Colab Enterprise to see if your dataset is a good candidate for the teacher-student model pair.

A training dataset is required for tuning. You are recommended to prepare an optional validation dataset if you'd like to evaluate your tuned model's performance.

> **Note:** For distillation tuning, the training dataset can contain prompts only — the teacher model generates the completions. However, the validation dataset must contain both prompts and ground-truth completions, because it is consumed during student model tuning to evaluate quality on held-out examples.

Your dataset must be in one of the following supported JSON Lines (JSONL) formats, where each line contains a single tuning example.

Upload your JSONL files to Cloud Storage.

### Text-only datasets

### Prompt completion

    {"prompt": "<prompt text>", "completion": "<ideal generated text>"}

### Turn based chat format

    {"messages": [
      {"content": "You are a chatbot that helps with scientific literature and generates state-of-the-art abstracts from articles.",
        "role": "system"},
      {"content": "Summarize the paper in one paragraph.",
        "role": "user"},
      {"content": " Here is a one paragraph summary of the paper:\n\nThe paper describes PaLM, ...",
        "role": "assistant"}
    ]}

### GenerateContent

> **Note:** The GenerateContent dataset format applies to supervised fine-tuning only.

    {
    "systemInstruction": {
      "parts": [{ "text": "You are a chatbot that helps with scientific literature and generates state-of-the-art abstracts from articles." }]},
    "contents": [
      {"role": "user",
        "parts": [{ "text": "Summarize the paper in one paragraph." }]},
      {"role": "assistant",
        "parts": [{ "text": "Here is a one paragraph summary of the paper:\n\nThe paper describes PaLM, ..." }]}
    ]}

### Multimodal datasets

> **Note:** Multimodal datasets apply to supervised fine-tuning only.

> **Note:** OpenAI Prompt Completion and Gemini Enterprise Agent Platform Text Bison are text-only dataset formats, and as a result, multimodal tuning with some models may not support these two formats. Refer to [model-specific documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-model-tuning#limitations) for more information.

### Turn based chat format

    {"messages": [
      {"role": "user", "content": [
        {"type": "text", "text": "You are a chatbot that helps with scientific literature and generates state-of-the-art abstracts from articles."},
        {"type": "image_url", "image_url": {
          "url": "gs://your-gcs-bucket/your-image.jpeg",
          "detail": "low"}}]
      },
      {"role": "assistant", "content": [
        {"type": "text", "text": "Here is a one paragraph summary of the paper:\n\nThe paper describes PaLM, ..."}]
      },
      {"role": "user", "content": [
        {"type": "text", "text": "You are a chatbot that helps with scientific literature and generates state-of-the-art abstracts from articles."},
        {"type": "image_url", "image_url": {
          "url": "data:image/jpeg;base64,<base64 image>",
          "detail": "low"}}]
      },
      {"role": "assistant", "content": [
        {"type": "text", "text": "Here is a one paragraph summary of the paper:\n\nThe paper describes PaLM, ..."}]
      },
    ]}

### GenerateContent

    {
    "systemInstruction": {
      "parts": [{ "text": "You are a chatbot that helps with scientific literature and generates state-of-the-art abstracts from articles." }]},
    "contents": [
      {"role": "user",
        "parts": [
          {"text": "You are a chatbot that helps with scientific literature and generates state-of-the-art abstracts from articles." },
          {"file_data": {
            "mime_type": "image/jpeg", "file_uri": "gs://your-gcs-bucket/your-image.jpeg"}}]
      },
      {"role": "assistant",
        "parts": [{ "text": "Here is a one paragraph summary of the paper:\n\nThe paper describes PaLM, ..." }]}
    ]}

Supported formats include JPEG, PNG, WEBP, and Base64-encoded images.

Note that if your images are stored under a different Cloud Storage bucket from your JSONL files, make sure that you have granted the Storage Object User ( `roles/storage.objectUser` ) IAM role on both buckets for these two service accounts:

  - `service- PROJECT_NUMBER @gcp-sa-vertex-moss-ft.iam.gserviceaccount.com`
  - `service- PROJECT_NUMBER @gcp-sa-aiplatform.iam.gserviceaccount.com`

## Create tuning job

You can tune from:

  - A [supported base model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-model-tuning#supported-models) , such as Llama 3.1

  - A model that has the same architecture as one of the supported base models. This could be either a custom model checkpoint from a repository such as Hugging Face or a previously tuned model from a Gemini Enterprise Agent Platform tuning job. This lets you continue tuning a model that has already been tuned.

### Cloud Console (Supervised)

1.  You can initiate fine tuning in the following ways:
    
      - Go the model card and click **Fine tune** and choose **Managed tuning** .
    
    or
    
      - Go to the **Tuning** page and click **Create tuned model** .

2.  Fill out the parameters and click **Start tuning** .

This starts a tuning job, which you can see in the Tuning page under the **Managed tuning** tab.

Once the tuning job has finished, you can view the information about the tuned model in the **Details** tab.

### Agent Platform SDK (Supervised)

Replace the parameter values with your own and then run the following code to create a tuning job:

    sft_tuning_job = sft.train(
        source_model=SourceModel(
          base_model="meta/llama3_1@llama-3.1-8b",
          # Optional, folder that is either a custom model checkpoint or previously tuned model
          custom_base_model="gs://{STORAGE-URI}",
        ),
        tuning_mode="FULL", # FULL or PEFT_ADAPTER
        epochs=3,
        train_dataset="gs://{STORAGE-URI}", # JSONL file
        validation_dataset="gs://{STORAGE-URI}", # JSONL file
        output_uri="gs://{STORAGE-URI}",
    )

### GenAI SDK (Distillation)

Replace the parameter values with your own and then run the following code to create a distillation tuning job:

    tuning_job = client.tunings.tune(
        base_model="qwen/qwen3@qwen3-4b",
        training_dataset=types.TuningDataset(
            gcs_uri="gs://{STORAGE-URI}"
        ),
        config=types.CreateTuningJobConfig(
            method="DISTILLATION",
            base_teacher_model="qwen/qwen3-next-80b-a3b-thinking-maas",
            epoch_count=3,
            validation_dataset=types.TuningValidationDataset(
                gcs_uri="gs://{STORAGE-URI}"
            ),
            output_uri="gs://{STORAGE-URI}",
        ),
    )

## Tuned model artifacts

When the tuning job finishes, the model artifacts for the tuned model are stored in your Cloud Storage output directory.

    gs://<output_dir>/
        # (Distillation tuning only) The labeled dataset from teacher model's inference
        -> distillation_labelled_dataset.jsonl
    
    gs://<output_dir>/postprocess/node-0/checkpoints/
        # Final checkpoint
        -> final/
            -> model-00001-of-000xx.safetensors
            -> model-000yy-of-000xx.safetensors
    
        # Intermediate checkpoints
        -> checkpoint-M/
            -> model-00001-of-000xx.safetensors
            -> model-000yy-of-000xx.safetensors
        …
        -> checkpoint-N/
            -> model-00001-of-000xx.safetensors
            -> model-000yy-of-000xx.safetensors

  - A maximum of 10 checkpoints are stored.
  - If the number of epochs (E) is less than 10, then exactly E checkpoints are stored (one for each epoch).
  - Intermediate checkpoints from range M to N are ordered. Note that intermediate checkpoints are not always consecutively numbered. For example, checkpoints may be numbered 1, 3, 5, 10 rather than 1, 2, 3, 4.

## Deploy tuned model

You can deploy the tuned model to a [Gemini Enterprise Agent Platform endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) . You can also export the tuned model from Cloud Storage and deploy it elsewhere.

To deploy the tuned model to a Gemini Enterprise Agent Platform endpoint:

### Cloud Console

1.  Go to the **Model Garden** page and click **Deploy model with custom weights** .

2.  Fill out the parameters and click **Deploy** .

### Agent Platform SDK for Python

Deploy a [`G2 machine`](https://docs.cloud.google.com/compute/docs/gpus#l4-gpus) using a [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) :

    from vertexai.preview import model_garden
    
    MODEL_ARTIFACTS_STORAGE_URI = "gs://{STORAGE-URI}/postprocess/node-0/checkpoints/final"
    
    model = model_garden.CustomModel(
        gcs_uri=MODEL_ARTIFACTS_STORAGE_URI,
    )
    
    # deploy the model to an endpoint using GPUs. Cost will incur for the deployment
    endpoint = model.deploy(
      machine_type="g2-standard-12",
      accelerator_type="NVIDIA_L4",
      accelerator_count=1,
    )

## Get an inference

Once deployment succeeds, you can send requests to the endpoint with text prompts. Note that the first few prompts will take longer to execute.

    # Loads the deployed endpoint
    endpoint = aiplatform.Endpoint("projects/{PROJECT_ID}/locations/{REGION}/endpoints/{endpoint_name}")
    
    prompt = "Summarize the following article. Article: Preparing a perfect risotto requires patience and attention to detail. Begin by heating butter in a large, heavy-bottomed pot over medium heat. Add finely chopped onions and minced garlic to the pot, and cook until they're soft and translucent, about 5 minutes. Next, add Arborio rice to the pot and cook, stirring constantly, until the grains are coated with the butter and begin to toast slightly. Pour in a splash of white wine and cook until it's absorbed. From there, gradually add hot chicken or vegetable broth to the rice, stirring frequently, until the risotto is creamy and the rice is tender with a slight bite.. Summary:"
    
    # Define input to the prediction call
    instances = [
        {
            "prompt": "What is a car?",
            "max_tokens": 200,
            "temperature": 1.0,
            "top_p": 1.0,
            "top_k": 1,
            "raw_response": True,
        },
    ]
    
    # Request the prediction
    response = endpoint.predict(
        instances=instances
    )
    
    for prediction in response.predictions:
        print(prediction)

For more details on getting inferences from a deployed model, see [Get an online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#response-examples) .

Notice that managed open models use the [`chat.completions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints.chat/completions) method instead of the [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) method used by deployed models. For more information on getting inferences from managed models, see [Make a call to a Llama model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/use-llama#unary) .

## Limits and quotas

Quota is enforced on the number of concurrent tuning jobs. Every project comes with a default quota to run at least one tuning job. This is a global quota, shared across all available regions and supported models. If you want to run more jobs concurrently, you need to [request additional quota](https://docs.cloud.google.com/docs/quota_detail/view_manage#requesting_higher_quota) for `Global concurrent managed OSS model fine-tuning jobs per project` .

In addition to the tuning job quota, distillation fine-tuning uses the teacher model, and your project must have sufficient quota for the specified teacher model. Open models provided as a service (MaaS) use [dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo) . When a tuning job calls a teacher model, it consumes from the project's shared quota for that model. For more information on quotas for managed open models, see [Gemini Enterprise Agent Platform managed models for MaaS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/use-open-models) .

## Pricing

You are billed for tuning based on [pricing for Model tuning](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#model-tuning) . The number of training tokens is calculated by multiplying the number of tokens in your training dataset by the number of epochs. For distillation tuning, you are also billed for the API calls made to the teacher model to generate responses, based on [pricing for managed models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) .

You are also billed for related services, such as Cloud Storage and Gemini Enterprise Agent Platform Prediction.

Learn about [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) , [Cloud Storage pricing](http://cloud.google.com/storage/pricing) , and use the [Pricing Calculator](https://cloud.google.com/products/calculator/) to generate a cost estimate based on your projected usage.

## What's next

  - [Evaluate the tuned model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/evaluation-overview)
