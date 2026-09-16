---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start-console
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start-console
title: 'Quick start: Reinforcement learning fine-tuning using the Google Cloud console'
description: Quick start guide for creating, monitoring, and running inference on a reinforcement learning fine-tuned Gemini model by using the {{dynamic_data.site_values.cloud_name_short}} console.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

This page walks you through the end-to-end workflow for reinforcement learning fine-tuning of Gemini models in the Google Cloud console: creating a tuning job, checking its status, retrieving the tuned-model endpoint, and running inference against it. To complete these tasks by using the Agent Platform API, see the [API quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) .

Before you begin, see [About reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning) for an overview of the feature, supported models, and supported regions.

## Create a reinforcement learning fine-tuning job

To create a reinforcement learning fine-tuning job by using the Google Cloud console, perform the following steps:

1.  In the Google Cloud console, go to the **Models \> Tuning** page.

2.  Click **Create tuned model** .

3.  In the **Model details** section, configure the following:
    
    1.  Under **Tuning method** , select **Reinforcement learning fine tuning** .
    2.  In the **Tuned model name** field, enter a name for your tuned model (for example, `my-rl-tuned-model` ).
    3.  Under **Base model** , select **Tune a foundation model** .
    4.  In the **Base model** drop-down list, select the model to tune (for example, `gemini-3.5-flash` ).
    5.  In the **Region** drop-down list, select the region where the tuning job runs (for example, `us-central1 (Iowa)` ). The resulting tuned model is served from the `us` multi-region endpoint. For the full list of supported tuning and serving regions, see the [Supported models and regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning#supported_models_and_regions) section.
    6.  Optional: Expand **Advanced options** to customize hyperparameters:
          - **Number of epochs** : The number of training epochs (for example, `15` ).
          - **Learning rate multiplier** : The multiplier to scale the learning rate (for example, `1.0` ).
          - **Adapter size** : The adapter size for parameter-efficient tuning (for example, `16` ).
          - **Samples per prompt** : The number of candidate responses the model generates per prompt during training (for example, `16` ).
          - **Thinking level** : The thinking level for reasoning models (for example, `HIGH` ).
          - **Batch size** : The number of training examples per batch (for example, `32` ).
          - **Checkpoint interval** : The frequency in steps at which intermediate checkpoints are saved (for example, `5` ).
          - **Max output token** : The maximum number of output tokens generated per sample (for example, `32768` ).
          - **Evaluate interval** : The frequency in steps at which evaluation runs against the validation dataset (for example, `5` ).
    7.  Click **Continue** .

4.  In the **Reward configuration** section, configure one or more reward functions to score model responses during training:
    
    1.  In the **Reward name** field, enter a unique name for the reward function (for example, `my_reward_function_name` ). Emitted metrics in the monitoring view are prefixed with this name.
    
    2.  In the **Reward type** drop-down list, select the scorer type:
        
          - **String match reward** : Evaluates generated text against references by using exact matching or regular expressions.
          - **LLM based reward** : Uses a Gemini model as an autorater to score responses based on an evaluation prompt.
          - **Python function based reward** : Executes custom Python code in a secure sandbox to evaluate responses.
          - **Fully customizable reward via Cloud Run** : Calls an external HTTP endpoint hosted on Cloud Run to evaluate responses.
    
    3.  Configure the settings for your selected reward type. For example, for a Cloud Run reward:
        
          - In the **Cloud Run URI** field, enter the HTTPS URI of your deployed service (for example, `https://my.cloud.run.uri` ).
          - In the **Parse type** field, select `IDENTITY` .
        
        Alternatively, for a string match reward:
        
          - In the **Parse type** field, select `REGEX_EXTRACT` or `IDENTITY` . If you select `REGEX_EXTRACT` , enter the regular expression in **Regex extract expression** (for example, `\text{(.*)}` ).
          - In the **Wrong answer reward** field, enter the penalty for an incorrect response (for example, `-1` ).
          - In the **Correct answer reward** field, enter the score for a correct response (for example, `1` ).
          - Under **String match expression type** , select **String match** or **JSON match** .
          - In the **Match operation** drop-down list, select the match logic (for example, **Exact match** ).
          - In the **Expression** field, enter the reference expression (for example, `references.reference` ).
    
    4.  In the **Reward weight** field, enter the relative weight for this reward function (for example, `1` ).
    
    5.  Click **Done** .
    
    6.  Optional: To define a composite reward, click **+ Add another reward** and configure additional reward functions. You can add up to 16 reward functions and assign relative weights to each.
    
    7.  Click **Continue** .

5.  In the **Test reward (Optional)** section, validate your reward configuration before starting the tuning job:
    
    1.  In the **Training Example** field, enter a sample JSON object containing `contents` and `references` .
    2.  In the **Sample model response** field, enter a candidate response, or click **Generate from Training Example** to generate a sample response by using the base model.
    3.  Click **Test** .
    4.  Verify that the evaluation succeeds and check the computed score. If using composite rewards, click **See individual reward information** to inspect the per-reward score breakdown.
    5.  Click **Continue** .

6.  Under **Tuning dataset** , specify your dataset files stored in Cloud Storage:
    
    1.  In the **Training dataset** field, enter the Cloud Storage URI of your training dataset JSONL file (for example, `gs://path/to/my/training_dataset.jsonl` ).
    2.  In the **Validation dataset** field, enter the Cloud Storage URI of your validation dataset JSONL file (for example, `gs://path/to/my/eval_dataset.jsonl` ).
    3.  Click **Start tuning** .

## Check the reinforcement learning fine-tuning job status

After you click **Start tuning** , the console redirects to the [**Models \> Tuning**](https://console.cloud.google.com/agent-platform/tuning) page. The tuning jobs table displays your newly created job near the top of the list with the following details:

  - **Model name** : The display name you specified for the tuned model.
  - **Status** : The current state of the tuning job (such as **Pending** , **Running** , or **Succeeded** ).
  - **Method** : `Reinforcement Learning` .
  - **Base model** : The foundation or pre-tuned model.
  - **Region** : The location where the tuning job is running.

Click the model name to open the tuning job details page. The page provides the following tabs:

  - **Monitor** : Surfaces tuning progress and interactive metrics charts:
      - **Tuning progress** : Shows whether the job is running or completed.
      - **Combined charts** : When a validation dataset is provided, training and validation curves (such as `/train_mean_reward` and `/eval_mean_reward` ) are plotted together on the same charts.
      - **Collapsible chart groups** : Metric charts are organized into groups, including general tuning metrics (mean reward, generation token length, thinking token length, sampling latency, and reward latency) and per-reward metrics prefixed by `${reward_name}` .
      - **Checkpoint annotations** : Intermediate checkpoints saved during tuning are annotated directly on the charts along the training timeline.
      - **Filter bar** : Use the filter bar to search metrics by name or filter by category ( `Show Category` ). When filtered, the filter bar remains sticky at the top of the view.
      - **Checkpoints table** : Lists saved intermediate checkpoints with step numbers and metric values. Use the column selector to choose which columns to display.
  - **Dataset** : Displays dataset details, sample conversations, and reference values.
  - **Details** : Summarizes the job configuration, including the base model, tuning method, hyperparameters, and reward configurations. Click **View details** on a reward configuration card to view non-default parameter values.

For the full list of emitted metrics and how to interpret them, see the [Metrics and monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) page.

### Training time

Training time is affected by the following factors:

  - **Training and validation dataset size** : For details, see [Tuning dataset for reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) .
  - **Hyperparameters** : Includes `samplesPerPrompt` , batch size, epoch count, and learning rate multiplier. For details, see [Hyperparameters for reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) .

Depending on your setup, a Gemini reinforcement learning fine-tuning job can run for hours to days.

## Get the tuned-model endpoint

After the tuning job reaches **Succeeded** , the model checkpoint is deployed to an endpoint. You can view and manage the deployed tuned model directly in the Google Cloud console:

1.  In the header of the tuning job details page, click **View model details** . The **Model Registry** page opens with details for the tuned model.
2.  On the model details page, find the **Deploy & test** tab to view the deployed endpoint resource path (in the format `projects/{PROJECT_ID}/locations/{LOCATION}/endpoints/{ENDPOINT_ID}` ).
3.  Alternatively, on the **Monitor** tab of the tuning job details page, locate the **Checkpoints** table to inspect intermediate checkpoints. You can deploy and evaluate individual checkpoints independently.

If the tuning job ran in `us-central1` , the tuned model is served from the `us` multi-region endpoint.

## Run inference on the tuned model

You can test and run inference on the tuned model directly in the Google Cloud console, do the following:

1.  In the header of the tuning job details page, click **Test** .
    
    Agent Studio opens with your tuned model pre-selected.

2.  In the prompt field, enter an input prompt (for example, `"Why is the sky blue?"` or a question from your target domain).

3.  Click **Run** (or **Send** ) to generate a response.

4.  Review the generated output to evaluate how well the model adheres to your desired reasoning style, formatting, and reward objectives.

## What's next

  - Learn more about [reinforcement learning fine-tuning jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job) .
  - Explore supported [reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) .
  - Configure [hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) for reinforcement learning.
  - Learn how to track [metrics and monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) .
  - Try the [API quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) to create tuning jobs programmatically.
