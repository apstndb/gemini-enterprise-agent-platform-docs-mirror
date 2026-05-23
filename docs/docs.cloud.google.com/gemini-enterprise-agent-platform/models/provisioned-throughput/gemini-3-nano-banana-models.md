---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/gemini-3-nano-banana-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/gemini-3-nano-banana-models
title: Provisioned Throughput for Gemini 3 Image models
description: Learn how Provisioned Throughput works for Gemini 3 Image models, including quota enforcement behavior and minimum GSU purchases.
data_source: docs.cloud.google.com
---

This section explains how Provisioned Throughput works for Gemini 3 Image (also known as Nano Banana) models, including quota enforcement behavior and minimum GSU purchase increment.

For [Gemini 3 Image models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation) , the [quota enforcement windows](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/use-provisioned-throughput#pt-quota-enforcement-period) vary based on the number of GSUs you purchase for the model, and are subject to change. The following sections list quota enforcement windows for different GSU sizes.

## Gemini 3.1 Flash Image Preview

The following are the quota enforcement windows for different GSU sizes for Gemini 3.1 Flash Image Preview:

  - 1 GSU: 435 seconds
  - 2 GSUs: 220 seconds
  - 3 GSUs: 145 seconds
  - 4 GSUs: 110 seconds
  - 5-14 GSUs: 100 seconds
  - 15-17 GSUs: 30 seconds
  - 18-21 GSUs: 25 seconds
  - 22-28 GSUs: 20 seconds
  - 29-42 GSUs: 15 seconds
  - 43-99 GSUs: 10 seconds
  - 100+ GSUs: 5 seconds

## Gemini 3 Pro Image Preview

The following are the quota enforcement windows for different GSU sizes for Gemini 3 Pro Image Preview:

  - 1 GSU: 1,230 seconds
  - 2 GSUs: 615 seconds
  - 3 GSUs: 410 seconds
  - 4 GSUs: 310 seconds
  - 5 GSUs: 245 seconds
  - 6 GSUs: 205 seconds
  - 7-12 GSUs: 175 seconds
  - 13 - 24 GSUs: 100 seconds
  - 25 - 30 GSUs: 50 seconds
  - 31 - 40 GSUs: 40 seconds
  - 41 - 61 GSUs: 30 seconds
  - 62 - 122 GSUs: 20 seconds
  - 123 - 244 GSUs: 10 seconds
  - 245+ GSUs: 5 seconds

The listed values aren't connected to the request latency. The time to process your request isn't the same as the quota enforcement window.

Enforcement windows are larger at smaller GSU amounts to ensure that smaller requests are processed successfully within the window. As the amount of GSUs for a model increases, longer window times are not required to process a request. If you need to process outputs on Gemini 3 Image more frequently using Provisioned Throughput, we recommend that you increase the amount of GSUs purchased and check the corresponding enforcement window.

For example, consider a situation where you purchased 1 GSU of Gemini 3.1 Flash Image Preview and have a workload that requires generating a single image with 4K resolution. In this case, you can usually generate this single image within seconds and the traffic is processed as Provisioned Throughput. However, if you wanted to generate another image of the same size, you need to wait until the quota enforcement window ends (435 seconds for 1 GSU). The time of this enforcement window is determined by the Gemini Enterprise Agent Platform clock time and not when the request is made.

We recommend using the estimation tool on the [Provisioned Throughput page](https://console.cloud.google.com/agent-platform/provisioned-throughput/price-estimate) to estimate the number of GSUs required for your workload. For more information about using the estimation tool, see [Purchase a Provisioned Throughput order](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput#place-an-order) .

## What's next

  - [Purchase standard Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput#place-an-order)
