---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo
title: Standard PayGo
description: Learn about Standard pay-as-you-go, a consumption option for Gemini Enterprise Agent Platform that uses spend-based usage tiers to set prioritized throughput thresholds.
data_source: docs.cloud.google.com
---

Standard pay-as-you-go (Standard PayGo) is a consumption option for using Gemini Enterprise Agent Platform's suite of generative AI models, including the Gemini model family.

Standard PayGo lets you pay only for the resources that you consume, without requiring upfront financial commitments. To help scale workloads on shared capacity, Standard PayGo incorporates a usage tier system. Agent Platform dynamically adjusts your organization's prioritized throughput threshold based on its total spend on eligible Agent Platform services over a rolling 30-day period. As your organization's spend grows, it's automatically promoted to higher tiers with higher prioritized throughput thresholds within the shared capacity pool. Standard PayGo runs on shared resources and doesn't reserve dedicated capacity or provide assured throughput during periods of high contention. For workloads requiring more consistent performance than Standard PayGo, consider [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo) . For dedicated and assured capacity, see [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput) .

## Usage tiers and throughput

Each Standard PayGo usage tier defines an organization-level prioritized throughput threshold, measured in tokens per minute (TPM). Requests up to your tier's TPM threshold receive prioritized access to shared capacity ahead of excess burst traffic, though throughput and availability still depend on real-time demand across the shared pool and aren't assured. The throughput thresholds apply to requests sent to the `global` endpoint. Using the `global` endpoint is a best practice because it provides access to a worldwide pool of throughput capacity and dynamically routes your requests to the location with the most availability.

Multi-region endpoints (such as `us` and `eu` on `aiplatform.us.rep.googleapis.com` and `aiplatform.eu.rep.googleapis.com` ) constrain machine learning processing to specific jurisdictional boundaries. Although multi-region endpoints pool capacity across multiple data centers within that geography, they operate from separate regional capacity pools and don't share the `global` endpoint's worldwide throughput capacity. Single-region endpoints (for example, `us-central1` or `us-east5` ) are restricted to a single data center cluster and have the lowest capacity headroom. If your workloads aren't subject to strict data residency requirements, use the `global` endpoint to use your tier's full prioritized throughput threshold and maximize headroom. For more information about configuring multi-region endpoints, see [Multi-region endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations#multi-region-endpoints) .

Your traffic isn't strictly capped at your tier's TPM threshold. When spare shared capacity is available, Agent Platform serves traffic that exceeds this threshold opportunistically. During periods of high demand across Agent Platform, excess burst traffic is throttled before traffic within tier thresholds, and all shared-pool traffic can experience higher latency or `429` errors. To minimize throttling, smooth your traffic as evenly as possible throughout each minute and avoid sending requests in sharp, second-level spikes. High instantaneous traffic can lead to throttling even if your average per-minute usage is within your tier's TPM threshold.

The following tiers are available in Standard PayGo:

| Model family                           | Tier        | Customer spend (30 days)                     | Traffic TPM (org-level) |
|----------------------------------------|-------------|----------------------------------------------|-------------------------|
| **Gemini Pro models**                  | Tier 1      | \$10 - \$250                                 | 500,000                 |
|                                        | Tier 2      | \$250 - \$2,000                              | 1,000,000               |
|                                        | Tier 3      | \$2,000 - \$50,000                           | 2,000,000               |
|                                        | Tier 4      | \> \$50,000                                  | 10,000,000              |
|                                        | Custom Tier | Contact your sales team for more information |                         |
| **Gemini Flash and Flash-Lite models** | Tier 1      | \$10 - \$250                                 | 2,000,000               |
|                                        | Tier 2      | \$250 - \$2,000                              | 4,000,000               |
|                                        | Tier 3      | \$2,000 - \$50,000                           | 10,000,000              |
|                                        | Tier 4      | \> \$50,000                                  | 50,000,000              |
|                                        | Custom Tier | Contact your sales team for more information |                         |

The throughput threshold shown for a model family applies independently to each model within that family. For example, an organization in Tier 3 has a prioritized throughput threshold of 10,000,000 TPM for Gemini 3.5 Flash. Usage against one model's threshold doesn't affect the throughput for other models. There's no separate requests-per-minute (RPM) limit for each tier. Gemini requests with multimodal inputs are subject to the corresponding [system rate limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#multimodal-input-quotas) .

> **Note:** For mission-critical workloads that require a strict Service Level Agreement (SLA) and can't tolerate performance variation or throttling, use [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput) . Provisioned Throughput provides assured capacity with consistent performance and reliability.

## How usage tiers work

Your usage tier is automatically determined by your organization's total spend on eligible Agent Platform services over a rolling 30-day period. As your organization's spending increases, the system promotes you to a higher tier with higher prioritized throughput thresholds.

### Spend calculation

This calculation includes a wide range of services, from predictions on all Gemini model families to Agent Platform CPU, GPU, and TPU instances, and also commitment-based SKUs, such as Provisioned Throughput.

#### Click to learn more about the SKUs included in spend calculation.

The following table lists the categories of [Google Cloud SKUs](https://cloud.google.com/skus) that are included in the calculation of the total spend.

| Category                   | Description of included SKUs                                                                                                                                                                                              |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Gemini Models**          | All Gemini model families (such as 2.0, 2.5, and 3.0 in Pro, Flash, and Lite versions) for predictions across all modalities (Text, Image, Audio, Video), including batch, long-context, tuned, and "thinking" variations |
| **Gemini Model Features**  | All related Gemini SKUs for features like Caching, Caching Storage, and Priority Tiers, across all modalities and model versions                                                                                          |
| **Agent Platform CPU**     | Online and Batch Predictions on all CPU-based instance families (such as C2, C3, E2, N1, N2, and their variants)                                                                                                          |
| **Agent Platform GPU**     | Online and Batch Predictions on all NVIDIA GPU-accelerated instances (such as A100, H100, H200, B200, L4, T4, V100, and RTX series)                                                                                       |
| **Agent Platform TPU**     | Online and Batch Predictions on all TPU-based instances (such as TPU-v5e and v6e)                                                                                                                                         |
| **Management & Fees**      | All "Management fee" SKUs associated with various Agent Platform prediction instances                                                                                                                                     |
| **Provisioned Throughput** | All commitment-based SKUs for Provisioned Throughput                                                                                                                                                                      |
| **Other Services**         | Specialized services such as "LLM Grounding for Gemini... with Google Search tool"                                                                                                                                        |

### Verify usage tier

To verify the usage tier for your organization, go to the Agent Platform Dashboard on the Google Cloud console. To view the usage tier on the dashboard, you need the [Agent Platform Viewer role](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.viewer) ( `roles/aiplatform.viewer` ) on the project and the [Billing Account Viewer role](https://docs.cloud.google.com/billing/docs/how-to/billing-access) ( `roles/billing.viewer` ) on the billing account.

### Verify spend

To review your Agent Platform spend, go to Cloud Billing on the Google Cloud console. Spend is aggregated at the organization level.

## Resource Exhausted (429) errors

If you receive a `429` error, it doesn't indicate that you've hit a fixed quota. It indicates temporary high contention for a specific shared resource. Implement an exponential backoff retry strategy to handle these errors because availability in this dynamic environment can change quickly.

In addition to a retry strategy, evaluate your endpoint choice:

- **`global` endpoint (recommended)** : The `global` endpoint dynamically routes requests across Google's worldwide fleet of data centers, pooling global throughput capacity and smoothing localized spikes. This provides the highest availability and significantly reduces the likelihood of `429` errors.
- **Multi-region endpoints (such as `us` and `eu` )** : Multi-region endpoints pool capacity across multiple data centers within a specific geographical boundary. Although they offer greater capacity than a single region, they don't access worldwide capacity. If your application uses a multi-region endpoint and experiences `429` errors during peak periods, evaluate whether your data governance policies allow routing non-sensitive or general workloads to the `global` endpoint, or consider [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo) or [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput) .
- **Single-region endpoints (such as `us-central1` )** : Single-region endpoints are constrained to a specific cluster location and have the highest likelihood of experiencing `429` errors under load contention. Avoid pinning high-throughput Standard PayGo workloads to single-region endpoints unless required for colocation with latency-sensitive compute resources.

For best results, combine the use of the `global` endpoint with traffic smoothing. Avoid sending requests in sharp, second-level spikes, because high instantaneous traffic can lead to throttling, even if your average per-minute usage is within your tier's prioritized throughput threshold. Distributing your API calls more evenly helps the system manage your load predictably and improves overall performance. For additional information about how to handle Resource Exhaustion errors, see [Build Resilient LLM Applications and Reduce 429 Errors](https://cloud.google.com/blog/products/ai-machine-learning/reduce-429-errors-on-vertex-ai) and [Error code 429](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/error-code-429) .

## Supported models

The following [generally available (GA)](https://cloud.google.com/products#product-launch-stages) Gemini models and any corresponding [supervised fine-tuned](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-supervised-tuning) models support [Standard PayGo with Usage Tiers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo#usage-tiers-and-throughput) :

#### Click to expand supported models

- [Gemini 3.8 Flash Cyber](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-cyber)
- [Gemini 3.8 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash)
- [Gemini 3.7 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash)
- [Gemini 3.6 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash)
- [Gemini 3.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite)
- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
- [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

The following [GA](https://cloud.google.com/products#product-launch-stages) Gemini models also support Standard PayGo, but the usage tiers don't apply to these models:

- [Gemini Nano Banana 2.1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/nano-banana-2-1)
- [Gemini 3.1 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)
- [Gemini 3.1 Flash-Lite Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite-image)
- [Gemini 3 Pro Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)
- [Gemini 2.5 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-image)

These tiers don't apply to preview models. Refer to the specific official documentation of each model for the most accurate and up-to-date information.

### Monitor throughput and performance

To monitor your organization's real-time token consumption, go to the Metrics Explorer in Cloud Monitoring.

For more information about monitoring model endpoint traffic, see [Monitor models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-observability) .

Usage tiers apply at an organization level. For information about setting your observability scope to chart throughput across multiple projects in your organization, see [Configure observability scopes for multi-project queries](https://docs.cloud.google.com/stackdriver/docs/observability/scopes) .

## What's next

Resource

### [Agent Platform quotas and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Quotas and limits related to Agent Platform, excluding product-specific limitations.

Overview

### [Google Cloud quotas](https://docs.cloud.google.com/docs/quotas/overview)

Learn about how Google Cloud restricts how much of a resource your Google Cloud project can use, and how quotas apply to a range of resource types, including hardware, software, and network components.
