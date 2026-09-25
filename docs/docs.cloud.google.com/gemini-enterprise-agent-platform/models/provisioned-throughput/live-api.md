---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/live-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/live-api
title: Provisioned Throughput for Gemini Live API
description: Learn how to use Provisioned Throughput for Gemini Live API.
data_source: docs.cloud.google.com
---

This section explains how Provisioned Throughput works with the Gemini Live API for token counting and quota enforcement.

The Gemini Live API enables low-latency multimodal interactions using session memory to retain context across turns. For additional capabilities and session limits, see the [Gemini Live API reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live) .

Each session must be dedicated entirely to either Provisioned Throughput or PayGo; mid-session spillover is not supported. If you exceed your Provisioned Throughput quota during an active session, the system allows temporary bursting to avoid errors, registering the overage against your overall quota. To avoid unexpected usage spikes, purchase sufficient GSUs to support your peak demand.

Spillover is supported between sessions. When starting a session, the system evaluates the request header and verifies Provisioned Throughput quota availability. If quota is insufficient, the new session defaults to PayGo.

Because session memory carries over previous turn outputs as inputs for subsequent requests, Provisioned Throughput calculates quota based on both new incoming tokens and accumulated session tokens. As a result, total processed tokens per request will increase as the session progresses until the predefined session limit is reached. The session state, including the session memory, are available as long as the session is live.

Be sure to account for session memory tokens when estimating your required Provisioned Throughput. Note that output video avatar tokens aren't included within the session memory. Historical PayGo traffic patterns can serve as a helpful baseline for calculating your GSU needs.

[Quota enforcement windows](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/use-provisioned-throughput#pt-quota-enforcement-period) vary based on the number of GSUs you purchase for the model and are subject to change.

## Gemini 3.8 Live API

### Quota enforcement windows

The following are the quota enforcement windows for different GSU sizes for the Gemini 3.8 Live API model:

  - 1-9 GSUs: 45 seconds
  - 10+ GSUs: 5 seconds

The listed values are independent of the request latency. The time to process your request isn't the same as the quota enforcement window. Note that a minimum of 10 GSUs must be purchased for Provisioned Throughput to be able to process this model's video avatar-related requests. If less than 10 GSUs are purchased, the entire video avatar-based session will spill over to PayGo.

Enforcement windows are larger at smaller GSU amounts to ensure that smaller requests are processed successfully within the window. As the number of GSUs for a model increases, longer window times aren't required to process a request. If you need to process outputs more frequently using Provisioned Throughput, we recommend that you increase the amount of GSUs purchased and check the corresponding enforcement window. Enforcement windows are dependent on backend algorithms and subject to change.

### Estimating GSU requirements

Let's walk through an example of a potential workload and understand how the [estimation tool](https://console.cloud.google.com/agent-platform/provisioned-throughput/price-estimate) would provide a recommendation for this model, which also informs how requests are processed and burndown rates are applied. A user is planning to use the Live API for a chatbot where 10 concurrent sessions are expected, and the duration is 5 minutes (300 seconds). There are an expected 30 conversation turns per session, and the user specifies a maximum session context window of 6,000 trigger tokens. The shape of the requests are captured below:

| Field                                     | Example Value |
| :---------------------------------------- | :------------ |
| Expected number of concurrent sessions    | 10            |
| Expected duration (seconds)               | 300           |
| Average number of turns per session       | 30            |
| Maximum context length (trigger tokens)   | 6,000         |
| Average input text tokens per turn        | 20            |
| Average input audio tokens per turn       | 200           |
| Average input image/video tokens per turn | 50            |
| Average output text tokens per turn       | 100           |
| Average output audio tokens per turn      | 200           |
| Is output video avatar enabled?           | Yes           |

**Input tokens per turn:**

Calculate the sumproduct of input modalities and their respective burndown rates:

  - Average input text tokens per turn \* Input text burndown rate = 20 \* 1 = 20

  - Average input audio tokens per turn \* Input audio burndown rate = 200 \* 4 = 800

  - Average input image/video tokens per turn \* Input image burndown rate = 50 \* 1.4 = 70

Burndown-adjusted input tokens total per turn = 20 + 800 + 70 = **890**

**Output tokens per turn:**

Calculate the sumproduct of output modalities and their respective burndown rates. Note that output video avatar tokens represents a fixed 6,192 tokens per 25 audio tokens:

  - Average output text tokens per turn \* Output text burndown rate = 100 \* 6 = 600

  - Average audio tokens per turn \* Output audio burndown rate = 200 \* 16 = 3,200

  - Is output video avatar enabled? Yes, so multiply audio token output by (6,192/25) and apply output video avatar token burndown rate: 200 \* (6,192/25) \* 1.4 = 69,350

Burndown-adjusted output tokens total per turn = 600 + 3,200 + 69,350 = **73,150**

**Context window tokens per turn:**

The context window accumulates raw input and output tokens (excluding output video avatar tokens) in each turn until it reaches the maximum context window length and stops increasing. Tokens are counted towards the context window limit as raw tokens (without applying burndown rates). However, when the context window is fed into the next turn's input requests as session memory, the tokens in the context window must apply the corresponding input burndown rates based on their modality.

Add the total raw tokens in each session without accounting for burndown rates.

  - Average input text tokens per turn + average input audio tokens per turn + average input image/video tokens per turn + average output text tokens per turn + average output audio tokens per turn = 20 + 200 + 50 + 100 + 200 = 570

Then calculate the ratio of each raw token count to the total. We can ignore video avatar output tokens as part of the context window calculation.

  - Input text ratio = 20/570 = 0.035
  - Input audio ratio = 200/570 = 0.351
  - Input image/video ratio = 50/570 = 0.088
  - Output text ratio = 100/570 = 0.175
  - Output audio ratio = 200/570 = 0.351

Then calculate the sumproduct of the ratios, maximum context length, and the burndown rates as if they were all input modalities.

  - Input text ratio \* maximum context length \* input text burndown = 0.035 \* 6,000 \* 1 = 210

  - Input audio ratio \* maximum context length \* input audio burndown = 0.351 \* 6,000 \* 4 = 8,424

  - Input image/video ratio \* maximum context length \* input image/video burndown = 0.088 \* 6,000 \* 1.4 = 739

  - Output text ratio \* maximum context length \* input text burndown = 0.175 \* 6,000 \* 1 = 1,050

  - Output audio ratio \* maximum context length \* input audio burndown = 0.351 \* 6,000 \* 4 = 8,424

At the maximum context window limit of 6,000 raw tokens, the total burndown-adjusted context window tokens processed per turn is 210 + 8,424 + 739 + 1,050 + 8,424 = 18,847.

**GSU calculation:**

(input tokens per turn + output tokens per turn + context window tokens per turn) \* average \# of turns per session \* expected number of concurrent sessions \* (1/expected duration) \* (1 GSU / 1,350 TPS) = (890 + 73,150 + 18,847) \* 30 \* 10 \* (1/300) \* (1/1,350) = 68.8, rounded up gives **69 GSUs** .

### Request processing

Let's walk through an example of how requests are processed with regards to Provisioned Throughput for this model. Let's assume there are 3 requests.

**Request \#1 details - input audio & video, output audio**

  - Duration: 10 seconds
  - Tokens sent (audio): 10 seconds x 25 tokens/second = 250 tokens
  - Tokens sent (video): 10 seconds x 258 tokens/frame per second = 2,580 tokens
  - Output audio tokens received based on nature of request: 100 tokens
  - Updated session memory = 250 + 2,580 + 100 = **2,930 tokens**

**Request \#2 details - input audio with session memory, output audio**

  - Duration: 40 seconds
  - Tokens sent (audio): 40 seconds x 25 tokens/second = 1,000 tokens
  - Session memory after Request \#1 = 2,930 tokens
  - Total input tokens sent: tokens sent in this request + session memory from Request \#1 = 1,000 + 2,930 = **3,930 tokens**
  - Output audio tokens received based on nature of request: **200 tokens**
  - Updated session memory = 3,930 + 200 = **4,130 tokens**

**Request \#3 details - input audio & video with session memory, output avatar video & audio**

  - Duration: 10 seconds
  - Tokens sent (audio): 10 seconds x 25 tokens/second = 250 tokens
  - Tokens sent (video): 10 seconds x 258 tokens/frame per second = 2,580 tokens
  - Session memory after Request \#2 = 4,130 tokens
  - Total input tokens sent: tokens sent in this request + session memory from Request \#2 = 250 + 2,580 + 4,130 = **6,960 tokens**
  - Output video avatar tokens received based on nature of request: **61,920 tokens**
  - Output audio tokens received based on nature of request: **250 tokens**
  - Updated session memory = 6,960 + 250 = **7,210 tokens**

**Understanding tokens processed**

  - Request \#1 processes only the input and output tokens from the ongoing request, since there are no additional tokens in session memory. All processed tokens now make up the session memory.

  - Request \#2 processes the input and output tokens from the ongoing request while also including the session memory from Request \#1. All session memory tokens apply the burndown rate of a corresponding input token.

  - Request \#3 processes the input and output tokens from the ongoing request while also including the session memory from Request \#2. All session memory tokens apply the burndown rate of a corresponding input token.

If Request \#3 took exactly 1 second to process after it was sent, the burndown-adjusted tokens applied to the Provisioned Throughput quota for this model would be as follows:

  - Input audio tokens \* input audio burndown rate = 250 \* 4 = 1,000

  - Input video tokens \* input video burndown rate = 2,580 \* 1.4 = 3,612

  - Session memory audio \* input audio burndown rate = (250 + 100 + 1,000 + 200) \* 4 = 6,200

  - Session memory video \* input video burndown rate = 2,580 \* 1.4 = 3,612

  - Output video avatar tokens \* output video avatar burndown rate = 61,920 \* 1.4 = 86,688

  - Output audio tokens \* output audio burndown rate = 250 \* 16 = 4,000

Adding the total provides **105,112 burndown-adjusted tokens** .

## Gemini 2.5 Flash Live API Native Audio

### Request processing

**Request \#1 details - input audio & video, output audio**

  - Duration: 10 seconds
  - Tokens sent (audio): 10 seconds x 25 tokens/second = 250 tokens
  - Tokens sent (video): 10 seconds x 258 tokens/frame per second = 2,580 tokens
  - Output audio tokens received based on nature of request: 100 tokens
  - Updated session memory = 250 + 2,580 + 100 = **2,930 tokens**

**Request \#2 details - input audio with session memory, output audio**

  - Duration: 40 seconds

  - Tokens sent (audio): 40 seconds x 25 tokens/second = 1,000 tokens

  - Session memory after Request \#1 = 2,930 tokens

  - Total input tokens sent: tokens sent in this request + session memory from Request \#1 = 1,000 + 2,930 = **3,930 tokens**

  - Output audio tokens received based on nature of request: **200 tokens**

  - Updated session memory = 3,930 + 200 = **4,130 tokens**

**Understanding tokens processed**

  - Request \#1 processes only the input and output tokens from the ongoing request, since there are no additional tokens in session memory. All processed tokens now make up the session memory.

  - Request \#2 processes the input and output tokens from the ongoing request while also including the session memory from Request \#1. All session memory tokens apply the burndown rate of a corresponding input token.

If Request \#2 took exactly 1 second to process after it was sent, the burndown-adjusted tokens applied to the Provisioned Throughput quota for this model would be as follows:

  - Input audio tokens \* input audio burndown rate = 1,000 \* 6 = 6,000
  - Session memory audio \* input audio burndown rate = (250 + 100) \* 6 = 2,100
  - Session memory video \* input video burndown rate = 2,580 \* 6 = 15,480
  - Output audio tokens \* output audio burndown rate = 200 \* 24 = 4,800

Adding the total provides **28,380 burndown-adjusted tokens** .

## What's next

  - [Purchase Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput) .
