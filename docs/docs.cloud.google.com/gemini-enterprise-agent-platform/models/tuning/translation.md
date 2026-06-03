---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/translation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/translation
title: About supervised fine-tuning for Translation LLM models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Supervised fine-tuning is a good option when you have a translation task with available labeled text data. It's particularly effective for domain-specific applications where the translation significantly differs from the general data the large model was originally trained on.

Supervised fine-tuning adapts model behavior with a labeled dataset. This process adjusts the model's weights to minimize the difference between its inferences and the actual labels.

## Supported models

The following Translation LLM models support supervised tuning:

  - `translation-llm-002`

## Limitations

  - Maximum input and output tokens:
      - Serving: 1,000 (\~4000 characters)
  - Validation dataset size: 1024 examples
  - Training dataset file size: Up to 1GB for JSONL
  - Training example length: 1,000 (\~4000 characters)
  - Adapter size:
      - `Translation LLM V2` : Supported value is only 4. Using any other values (e.g., 1 or 8) will result in failure.

## Use cases for using supervised fine-tuning

General pretrained translation model works well when the text to be translated is based on general commonplace text structures that the model learned from. If you want a model to learn something niche or domain-specific that deviates from general translation, then you might want to consider tuning that model. For example, you can use model tuning to teach the model the following:

  - Specific content of an industry domain with jargon or style
  - Specific structures or formats for generating output.
  - Specific behaviors such as when to provide a terse or verbose output.
  - Specific customized outputs for specific types of inputs.

## Configure a tuning job region

User data, such as the transformed dataset and the tuned model, is stored in the tuning job region. The only supported region is `us-central1` .

  - If you use the Vertex AI SDK, you can specify the region at initialization. For example:
    
        import vertexai
        vertexai.init(project='myproject', location='us-central1')

  - If you create a supervised fine-tuning job by sending a POST request using the [`tuningJobs.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/create) method, then you use the URL to specify the region where the tuning job runs. For example, in the following URL, you specify a region by replacing both instances of `TUNING_JOB_REGION` with the region where the job runs.
    
    ``` 
     https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs
    ```

  - If you use the [Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/supervised-tuning/use#create_a_text_model_supervised_tuning_job) , you can select the region name in the **Region** drop down field on the **Model details** page. This is the same page where you select the base model and a tuned model name.

## Quota

Quota is enforced on the number of concurrent tuning jobs. Every project comes with a default quota to run at least one tuning job. This is a global quota, shared across all available regions and supported models. If you want to run more jobs concurrently, you need to [request additional quota](https://docs.cloud.google.com/docs/quota_detail/view_manage#requesting_higher_quota) for `Global concurrent tuning jobs` .

## Pricing

You are billed for tuning based on [pricing for Translation Model tuning](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#model-tuning) .

You are also billed for related services, such as Cloud Storage and Translation LLM Prediction.

Learn about [Translation LLM pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#translation-text) , [Cloud Storage pricing](http://cloud.google.com/storage/pricing) .

## What's next

  - Prepare a [supervised fine-tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/translation/prepare-data) .
