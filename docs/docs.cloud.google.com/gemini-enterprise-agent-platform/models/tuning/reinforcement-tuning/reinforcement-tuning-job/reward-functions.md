---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions
title: Reward functions for reinforcement learning fine-tuning
description: Reward functions for reinforcement learning fine-tuning of Gemini models, including string matching, autorater, code execution, and Cloud Run rewards.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

A reward function numerically scores each model response during reinforcement learning fine-tuning. The reward signal is what reinforcement learning optimizes against, so its quality directly determines tuning quality. All rewards are clipped to the range `[-1, 1]` ; any value outside that range is clipped.

This page describes each supported reward type, recommended practices for designing rewards, and how to validate a reward configuration before you launch a tuning job. Reinforcement learning fine-tuning supports the following reward types:

  - [String matching reward](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions#string-matching-reward)
  - [Gemini-based autorater reward](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions#gemini-based-autorater-reward)
  - [Code execution reward](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions#code-execution-reward)
  - [Fully customizable reward through Cloud Run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions#cloud-run-reward)

You can also combine any of these four with per-scorer weights using a **composite reward** .

## Known restrictions

The following timeouts apply per reward type:

| Reward type            | Timeout                                                   |
| ---------------------- | --------------------------------------------------------- |
| String matching        | No strict timeout                                         |
| Code execution         | 100 seconds for every `evaluate` method call              |
| Gemini-based autorater | 1 minute timeout while waiting for an LLM rating response |
| Cloud Run              | 5 minute timeout for every trigger                        |

## String matching reward

API spec: [`ReinforcementTuningStringMatchRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningStringMatchRewardScorer)

The string matching reward is a convenient configuration for evaluating model-generated responses against known ground truths. It is particularly useful for tasks like math questions, where each question has a known ground-truth answer.

Because the model might output chain-of-thought reasoning or other words before reaching the final answer that you want to compare against the ground truth, the string matching scorer supports a parser function that processes the model-generated output using a regular expression extraction. You then define how to compare the regex-extracted model response against your ground truth. The ground truth is supplied through a field in `references` , which you populate in each example when you create your training and validation files.

For the configuration schema, see the `ReinforcementTuningStringMatchRewardScorer` API spec. For details on the `references` field, see the [Tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset#the-references-field) page.

## Gemini-based autorater reward

API spec: [`ReinforcementTuningAutoraterScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningAutoraterScorer)

The Gemini-based autorater reward is a convenient configuration for evaluating model-generated responses against LLM-as-a-judge feedback. For example, you might want a model to output responses in a certain tone where the tone is decided by an autorater (LLM-as-a-judge).

This reward supports two patterns:

  - The autorater can directly output a numeric score that is used as the reinforcement learning feedback.
  - The autorater can output a judgement that is parsed and compared against predefined patterns.

The autorater is also allowed to output its chain-of-thought reasoning, so you can parse a section of the response in the same way as the string matching reward. For example, an autorater can output `blahblahblah <answer>Yes</answer>` or `blahblahblah <answer>No</answer>` , and you can create a parsing function to extract the autorater response between `<answer>` and `</answer>` . You can then compare the autorater output against a predefined expression that maps `Yes` to a `+1` score and any unmatched value (such as `No` ) to a `-1` score.

The following example autorater configuration filters to get the text between `<answer>` tags and maps `Yes` to `+1` and any other value to `-1` :

    {
      "autoraterResponseParseConfig": {
        "parseType": "REGEX_EXTRACT",
        "regexExtractExpression": "<answer>(.*?)</answer>"
      },
      "exactMatchScorer": {
        "expression": "Yes",
        "correctAnswerReward": 1.0,
        "wrongAnswerReward": -1.0
      }
    }

## Code execution reward

API spec: [`ReinforcementTuningCodeExecutionRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCodeExecutionRewardScorer)

The code execution reward configuration lets you provide user-defined Python code to evaluate model responses without setting up a Cloud Run service. Implement an `evaluate` function with the following signature:

    def evaluate(example: dict[str, Any], response: dict[str, Any]) -> float:
      ...

The function receives:

  - `example` : A [`ReinforcementTuningExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample) in ProtoJSON format (that is, the same format as one line in the training or validation dataset, except that the keys must be in camel case). System instructions ( `example.get("systemInstruction")` ) and references ( `example.get("references")` ) are also included in `example` , provided that they are set in the training or validation dataset.
  - `response` : A [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content) in ProtoJSON format (that is, keys must be in camel case), which is the same as the online prediction response for Gemini models.

The function must return a float, which is then clipped to the range `[-1, 1]` .

Example implementation:

    def evaluate(example, response) -> float:
      response_str = response.get("parts", [])[0]["text"]
      references = example.get("references", {})
    
      if response_str == references.get("concise_answer"):
        return 1.0
      return -1.0

### Supported libraries

In addition to the Python Standard Library, the following Python libraries are available inside the code-execution sandbox:

  - `cv2`
  - `matplotlib`
  - `mpmath`
  - `numpy`
  - `pandas`
  - `seaborn`
  - `sklearn`
  - `statsmodels`
  - `sympy`

### Timeouts and resource limits

Each `evaluate` call has a 100-second timeout. Timed-out calls are retried several times. If the call continues to time out after several retries, the sample is dropped from reward calculation.

We strongly recommend testing your code with the `ValidateReinforcementTuningReward` API (see [Validate a reward configuration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions#validate-a-reward-configuration) ) and aim for code execution to finish well under 100 seconds for best performance.

The code execution environment provides 1 CPU and 1GB of memory per invocation.

## Fully customizable reward through Cloud Run

API spec: [`ReinforcementTuningCloudRunRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCloudRunRewardScorer)

The Cloud Run reward configuration lets you implement fully customizable scoring logic. Your Cloud Run service must implement the following HTTP contract.

**HTTP method:** `POST`

**Request body** ( `application/json` ):

    {
      "example": { "object(RLFTExample)" },
      "response": { "object(Content)" },
      "metadata": {
        "step": int,
        "tuningJobId": int64
      }
    }

`example` is a `ReinforcementTuningExample` in ProtoJSON format, and `response` is a `Content` in ProtoJSON format.

**Response body** ( `application/json` ):

    {
      "reward": float,
      "...": {}
    }

### Example request

    {
      "example": {
        "contents": [
          {
            "role": "user",
            "parts": [
              { "text": "What is the capital of France?" }
            ]
          }
        ],
        "references": {
          "answer": "Paris"
        }
      },
      "response": {
        "parts": [
          { "text": "London" }
        ]
      },
      "metadata": {
        "step": 1,
        "tuningJobId": 123456789
      }
    }

### Example response

    {
      "reward": -1.0
    }

### Set up IAM permissions

  - You need the `roles/run.admin` permission on your Cloud Run service in order to grant additional IAM permissions to it.
  - The Gemini Enterprise Agent Platform Secure Fine Tuning Service Agent ( `service-PROJECT_NUMBER@gcp-sa-vertex-tune.iam.gserviceaccount.com` ) must be granted permission (for example, by granting `roles/run.invoker` in IAM) to invoke your Cloud Run service.

### Timeouts and retries

A maximum of **300 seconds** is allowed for the Cloud Run service to process each reward calculation request. On request errors, the service retries with exponential backoff (for example, after 2, 4, 8, 16, and 32 seconds) before giving up. If no valid response is returned after exhausting all retries, the reward is marked as `NaN` .

## Reward design recommendations

The following sections describe best practices for designing reward functions that produce well-calibrated signals for reinforcement learning fine-tuning.

### Reward scale

Every single reward must be on the scale of `[-1, 1]` . Reward values outside this range are clipped.

### What makes a good reward

  - **Aligned with the desired outcome** and well-calibrated with human preference.
  - **Clear and consistent.** For example, it is difficult for the model to learn effectively from a high-variance autorater reward.
  - **Robust to invalid outputs.** For example, the reward should be able to return a low value rather than crash and return `NaN` when invalid outputs are generated by the model, so the tuning job knows those are bad generations to optimize away from. If more than 80% of your reward invocations are errored (RPC error, returning `NaN` ), the tuning job is stopped automatically.
  - **Designed to prevent reward hacking.** Avoid configurations where the model can exploit loopholes to achieve a high reward without genuinely good performance.

## Validate a reward configuration

API spec: [`ValidateReinforcementTuningReward`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward)

Tuning jobs can be expensive, and rewards are crucial to making your tuning job effective. We recommend validating your reward configuration before launching a tuning job:

  - Use the `ValidateReinforcementTuningReward` API to check the validity and robustness of your reward. Small errors — such as parsing errors, unhandled edge cases, or invalid code snippets — can invalidate your reward and your tuning.
  - Perform an evaluation with the customized reward on a sample of your dataset. Reinforcement learning can't learn well when the reward is either too hard (rewards are almost always `0` ) or too straightforward (rewards are almost always `1` ) for the dataset.

The `ValidateReinforcementTuningReward` API expects a `sampleResponse` (of type `Content` , usually obtained from a Gemini model output), an `RLFTExample` , and one of `singleRewardConfig` or `compositeRewardConfig` . If the returned result contains an error or `NaN` , then there is something wrong with the reward setup that you need to address before running the actual tuning job.

    curl -i -X POST \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      "https://us-central1-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/us-central1/tuningJobs:validateReinforcementTuningReward" \
      -d @validate_reward_request.json

Replace PROJECT\_ID with your Google Cloud project ID.

## What's next

  - [Prepare a tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) and populate the `references` field for your reward function.
  - [Configure hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) .
  - [Monitor job status and metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) , including per-reward metrics for composite rewards.
  - Follow the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) to create your first reinforcement learning fine-tuning job.
