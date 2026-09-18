---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/gemini-omni-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/gemini-omni-models
title: Provisioned Throughput for Gemini Omni models
description: Learn how Provisioned Throughput works for Gemini Omni models, including quota enforcement behavior and minimum GSU purchases.
data_source: docs.cloud.google.com
---

This section explains how Provisioned Throughput works for Gemini Omni models, including quota enforcement behavior and minimum generative AI scale unit (GSU) purchase increments.

For [Gemini Omni models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash) , the [quota enforcement windows](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/use-provisioned-throughput#pt-quota-enforcement-period) vary based on the number of GSUs you purchase for the model and are subject to change. The following sections list quota enforcement windows for different GSU sizes.

## Gemini Omni Flash Preview: Quota enforcement windows

The following are the quota enforcement windows for different GSU sizes for Gemini Omni Flash Preview:

  - 1-9 GSUs: 2,000 seconds
  - 10-19 GSUs: 200 seconds
  - 20-39 GSUs: 100 seconds
  - 40-66 GSUs: 50 seconds
  - 67+ GSUs: 30 seconds

The listed values are independent of the request latency. The time to process your request isn't the same as the quota enforcement window.

Enforcement windows are larger at smaller GSU amounts to ensure that smaller requests are processed successfully within the window. As the number of GSUs for a model increases, longer window times aren't required to process a request. If you need to process outputs on Omni Flash more frequently using Provisioned Throughput, we recommend that you increase the number of GSUs purchased and check the corresponding enforcement window.

For example, consider a situation where you purchased 1 GSU of Omni Flash Preview for a workload that requires generating a single 10-second 1080p video. In this case, you can usually generate this video within 60 seconds and the traffic is processed as Provisioned Throughput. However, if you want to generate another video of the same duration, you must wait until the quota enforcement window ends (2,000 seconds for 1 GSU). The time of this enforcement window is determined by the Gemini Enterprise Agent Platform clock time and not when the request is made. Enforcement windows are dependent on backend algorithms and subject to change.

We recommend setting the [duration and resolution API parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#VideoResponseFormat) when making a request. When provided, Provisioned Throughput can provide a more accurate experience. If these parameters aren't provided, Provisioned Throughput request size estimation assumes the maximum duration and resolution, which might lead to premature, avoidable spillover to pay-as-you-go and reduce the utilization of your purchased Provisioned Throughput.

## Estimating GSU requirements

We recommend using the estimation tool on the [Provisioned Throughput page](https://console.cloud.google.com/agent-platform/provisioned-throughput/price-estimate) to estimate the number of GSUs required for your workload. The tool requires your input of total input tokens and output tokens estimation for a specific frequency window. For more information about using the estimation tool, see [Place a stanard Provisioned Throughput order](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput#place-an-order) .

To estimate token counts, use the following methods:

  - **Input text tokens** : Use the SDK tokenizer or the [countTokens API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count) .
  - **Input tokens of other modalities** : Use estimates based on the assumptions in the [pricing page](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#gemini-omni) .
  - **Existing workloads** : Sum the token usage from responses generated within a specific time window.

For example, consider a workload that generates five 10-second 720p videos and five 10-second 1080p videos every 30 seconds (10 requests total). Suppose each request has 20 input text tokens, one image (1,120 tokens), and 100 response thinking tokens. The inputs for the GSU estimator are as follows:

  - **Frequency** : 30s
  - **Total input text tokens** : 20 × 10 (requests) = 200
  - **Total image tokens** : 1,120 × 10 (requests) = 11,200
  - **Total output reasoning tokens** : 100 × 10 (requests) = 1,000
  - **Total output video tokens** : 10s (duration) × 5,792 (tokens/s) × 5 videos (720p) + 10s (duration) × 8,688 (tokens/s) × 5 videos (1080p) = 724,000
  - **Estimated GSUs** : 434

## High resolution and duration scenarios

A single, large request can't be split across two enforcement windows. If one request needs more than your enforcement window holds, it's served as pay-as-you-go every time—no matter how infrequently you send it and no matter how much unused Provisioned Throughput quota might be present in subsequent windows.

This affects only 4K videos of 7 seconds or longer. At 360p, 720p, and 1080p, every supported duration fits inside one window at any purchase size, as do 4K videos of 6 seconds or shorter (assuming typical input and reasoning tokens less than 88k tokens).

If you generate 4K videos of 7 seconds or longer, compare the estimation tool's result against the following table and order whichever number is larger:

| Longest 4K video | 1–9 GSUs | 10–19 GSUs | 20–39 GSUs | 40–66 GSUs | 67+ GSUs |
| :--------------- | :------- | :--------- | :--------- | :--------- | :------- |
| 7 seconds        | 2        | 12         | 23         | 46         | 76       |
| 8 seconds        | 2        | 13         | 26         | 52         | 87       |
| 9 seconds        | 2        | 15         | 29         | 58         | 97       |
| 10 seconds       | 2        | 17         | 33         | 65         | 107      |

Read the column matching your estimated GSU count. For example, suppose you generate six 10-second 4K videos every 2,000 seconds. The estimator returns 10 GSUs, which is sufficient for average throughput. However, at 10 GSUs, the enforcement window is 200 seconds, and none of your 10-second videos fit within a single window. Spacing the six requests further apart doesn't resolve this issue. To successfully process the requests without pay-as-you-go spillover, order 17 GSUs.

These figures assume typical prompt and reasoning tokens—a text or image prompt, or a video of up to 10 seconds to edit.

## What's next

  - [Purchase Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput#place-an-order)
