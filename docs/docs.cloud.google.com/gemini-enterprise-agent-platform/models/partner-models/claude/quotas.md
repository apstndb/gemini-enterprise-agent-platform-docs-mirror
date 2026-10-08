---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas
title: Quotas for Anthropic Claude models
description: Learn how quotas for Anthropic Claude models are managed on Agent Platform.
data_source: docs.cloud.google.com
---

This page describes how Gemini Enterprise Agent Platform manages quotas for Anthropic Claude models.

## Overview

Anthropic Claude models on Agent Platform use one of the following quota systems:

- **Models launched after May 26, 2026:** [Shared lineage quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas#shared-lineage-quotas) .
- **Models launched before May 26, 2026:** [Per-model quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas#per-model-quotas) .

## Shared lineage quotas

Global and multi-regional endpoints for Anthropic Claude models launched after May 26, 2026 use shared model lineage quotas. A single quota limit is shared across **all model versions in a model lineage** for a given location.

For example, if you call Claude Opus 4.8 on Google Cloud through the global endpoint, then all requests, input tokens, and output tokens count against the same `anthropic-claude-opus` quota bucket for the global endpoint, regardless of the specific Opus version that you call.

Quotas on the global endpoint and each multi-region endpoint are independent buckets. Usage on the global endpoint doesn't consume quota on a multi-region endpoint, and similarly usage on a multi-region endpoint doesn't consume quota on the global endpoint.

The following sections describe how shared lineage quotas work for global endpoints and multi-region endpoints.

### Global endpoints

The following table describes metrics for global endpoints:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric</th>
<th>Quota dimension</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>global_online_prediction_requests_per_base_model</code></td>
<td><code>base_model</code> :
<ul>
<li><code>anthropic-claude-opus</code></li>
<li><code>anthropic-claude-sonnet</code></li>
<li><code>anthropic-claude-haiku</code></li>
<li><code>anthropic-claude-fable</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>global_online_prediction_input_tokens_per_minute_per_base_model</code></td>
<td><code>base_model</code> :
<ul>
<li><code>anthropic-claude-opus</code></li>
<li><code>anthropic-claude-sonnet</code></li>
<li><code>anthropic-claude-haiku</code></li>
<li><code>anthropic-claude-fable</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>global_online_prediction_output_tokens_per_minute_per_base_model</code></td>
<td><code>base_model</code> :
<ul>
<li><code>anthropic-claude-opus</code></li>
<li><code>anthropic-claude-sonnet</code></li>
<li><code>anthropic-claude-haiku</code></li>
<li><code>anthropic-claude-fable</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Multi-region endpoints

The following table describes the metrics for multi-region endpoints, such as `us` and `eu` :

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric</th>
<th>Quota dimension</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><var translate="no">LOCATION </var><code> _multi_region_online_prediction_requests_per_base_model</code></td>
<td><code>base_model</code> :
<ul>
<li><code>anthropic-claude-opus</code></li>
<li><code>anthropic-claude-sonnet</code></li>
<li><code>anthropic-claude-haiku</code></li>
<li><code>anthropic-claude-fable</code></li>
</ul></td>
</tr>
<tr class="even">
<td><var translate="no">LOCATION </var><code> _multi_region_online_prediction_input_tokens_per_minute_per_base_model</code></td>
<td><code>base_model</code> :
<ul>
<li><code>anthropic-claude-opus</code></li>
<li><code>anthropic-claude-sonnet</code></li>
<li><code>anthropic-claude-haiku</code></li>
<li><code>anthropic-claude-fable</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><var translate="no">LOCATION </var><code> _multi_region_online_prediction_output_tokens_per_minute_per_base_model</code></td>
<td><code>base_model</code> :
<ul>
<li><code>anthropic-claude-opus</code></li>
<li><code>anthropic-claude-sonnet</code></li>
<li><code>anthropic-claude-haiku</code></li>
<li><code>anthropic-claude-fable</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Implications for your application

- **Adding a new version of a lineage doesn't require a new quota request.** When a new version of a model lineage, such as a future Sonnet release, launches on a public endpoint, it shares the existing model lineage quota bucket. You don't need to file a separate quota increase to use the new version.

- **Mixing versions consumes the same quota bucket.** Traffic split across multiple versions of the same model lineage draws from one shared quota. Plan capacity at the lineage level, not the version level.

## View and manage your quotas

To view your current usage limits or request quota increases, go to the [Quotas and system limits](https://console.cloud.google.com/iam-admin/quotas) page in the Google Cloud console.

To filter quotas, use the **model lineage** value of `base_model` , such as `anthropic-claude-opus` .

## Per-model quotas

Anthropic Claude models launched before May 26, 2026 have quotas based on the type of endpoint used: regional, multi-region, or global. The quota is specified in queries per minute (QPM) and tokens per minute (TPM). TPM includes both input and output tokens.

To maintain overall service performance and acceptable use, the maximum quotas might vary by account and, in some cases, access might be restricted. View your project's quotas on the [Quotas & Systems Limits](https://console.cloud.google.com/quotas) page in the Google Cloud console. You must also have the following quotas available:

- **Queries Per Minute (QPM):**

  - For regional endpoints: `online_prediction_requests_per_base_model`
  - For the global endpoint: `global_online_prediction_requests_per_base_model`
  - For the US multi-region endpoint: `us_multi_region_online_prediction_requests_per_base_model`
  - For the EU multi-region endpoint: `eu_multi_region_online_prediction_requests_per_base_model`

- **Tokens Per Minute (TPM):**

  - Some models count input and output tokens together:
    - Regional: `online_prediction_tokens_per_minute_per_base_model`
    - Global: `global_online_prediction_tokens_per_minute_per_base_model`
  - Other models count input and output tokens separately:
    - **Input TPM:**
      - Regional: `online_prediction_input_tokens_per_minute_per_base_model`
      - Global: `global_online_prediction_input_tokens_per_minute_per_base_model`
      - US Multi-Region: `us_multi_region_online_prediction_input_tokens_per_minute_per_base_model`
      - EU Multi-Region: `eu_multi_region_online_prediction_input_tokens_per_minute_per_base_model`
    - **Output TPM:**
      - Regional: `online_prediction_output_tokens_per_minute_per_base_model`
      - Global: `global_online_prediction_output_tokens_per_minute_per_base_model`
      - US Multi-Region: `us_multi_region_online_prediction_output_tokens_per_minute_per_base_model`
      - EU Multi-Region: `eu_multi_region_online_prediction_output_tokens_per_minute_per_base_model`

  To see which models count input and output tokens separately, see [Quotas by model and region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas#quotas) .

### Input tokens

> **Note:** Due to a complex token estimation and refund system for Anthropic's Claude models, the token usage reported on the [Quota](https://console.cloud.google.com/quotas) page in the Google Cloud console might be inaccurate. For accurate token usage and billing information, use one of the following methods:
>
> - The [token counting API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens) .
> - The `token_count` metrics for Agent Platform in the [Metrics Explorer](https://console.cloud.google.com/monitoring/metrics-explorer) .

The following list defines the input tokens that can count towards your input TPM quota. The input tokens that each model counts can vary. To see which input tokens a model counts, see [Quotas by model and region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas#quotas) .

- **Input tokens** includes all input tokens, including cache read and cache write tokens.
- **Uncached input tokens** includes only the input tokens that weren't read from a cache (cache read tokens).
- **Cache write tokens** includes tokens that were used to create or update a cache.

### Quotas by model and region

The following table shows the default quotas and supported context length for each model in each region.

> **Important:** Machine learning (ML) processing for all available Anthropic models occurs within the US when requests are made to regionally-available APIs in the US, or within the EU when requests are made to regionally-available APIs in Europe.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Model</th>
<th>Region</th>
<th>Quotas</th>
<th>Context length</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Claude Sonnet 5.5 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,250</li>
<li>Input TPM: 12,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,250,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,250</li>
<li>Input TPM: 12,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,250,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,500</li>
<li>Input TPM: 25,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,500,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude Fable 5.1 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><code>Multi-region</code></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Sonnet 5 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,250</li>
<li>Input TPM: 12,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,250,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,250</li>
<li>Input TPM: 12,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,250,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,500</li>
<li>Input TPM: 25,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,500,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude Opus 5.5 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="odd">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,000</li>
<li>Input TPM: 20,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Opus 5 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,000</li>
<li>Input TPM: 20,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude Fable 5 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="odd">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,000</li>
<li>Input TPM: 20,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Opus 4.8 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,000</li>
<li>Input TPM: 10,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,000</li>
<li>Input TPM: 20,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude Opus 4.7 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 400</li>
<li>Input TPM: 4,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 400,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="odd">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 400</li>
<li>Input TPM: 4,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 400,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 800</li>
<li>Input TPM: 8,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 800,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Opus 4.6 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 200</li>
<li>Input TPM: 2,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 200,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 200</li>
<li>Input TPM: 2,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 200,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>asia-southeast1</code></td>
<td><ul>
<li>QPM: 200</li>
<li>Input TPM: 2,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 200,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 400</li>
<li>Input TPM: 4,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 400,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Sonnet 4.6 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 1500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 1800</li>
<li>Input TPM: 1,800,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 180,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>asia-southeast1</code></td>
<td><ul>
<li>QPM: 1500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 1500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Opus 4.5 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 200</li>
<li>Input TPM: 2,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 200,000</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 200</li>
<li>Input TPM: 2,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 200,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>asia-southeast1</code></td>
<td><ul>
<li>QPM: 200</li>
<li>Input TPM: 2,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 200,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 400</li>
<li>Input TPM: 4,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 400,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Opus 4.1 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 25</li>
<li>Input TPM: 60,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 6,000</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 25</li>
<li>Input TPM: 60,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 6,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Opus 4 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 25</li>
<li>Input TPM: 60,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 6,000</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 25</li>
<li>Input TPM: 60,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 6,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Sonnet 4.5 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>1,000,000 (beta), 200,000 (GA)</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 1,800</li>
<li>Input TPM: 1,800,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 180,000</li>
</ul></td>
<td>1,000,000 (beta), 200,000 (GA)</td>
<td></td>
</tr>
<tr class="odd">
<td><code>asia-southeast1</code></td>
<td><ul>
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>1,000,000 (beta), 200,000 (GA)</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>1,000,000 (beta), 200,000 (GA)</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Sonnet 4 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 35</li>
<li>Input TPM: 280,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 20,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 25</li>
<li>Input TPM: 180,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 20,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 35</li>
<li>Input TPM: 276,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 24,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude 3.7 Sonnet on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 55</li>
<li>TPM: 500,000 ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached</a> input and output)</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="odd">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 40</li>
<li>TPM: 300,000 ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached</a> input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 35</li>
<li>TPM: 300,000 ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached</a> input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude 3.5 Sonnet v2 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 90</li>
<li>TPM: 540,000 (input and output)</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 55</li>
<li>TPM: 330,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 25</li>
<li>TPM: 140,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude Haiku 5.5 on Google Cloud</td>
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,500</li>
<li>Input TPM: 15,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,500,000</li>
</ul></td>
<td>1,000,000</td>
</tr>
<tr class="odd">
<td><code>Multi-region</code></td>
<td><ul>
<li>QPM: 1,500</li>
<li>Input TPM: 15,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,500,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 3,000</li>
<li>Input TPM: 30,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 3,000,000</li>
</ul></td>
<td>1,000,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude Haiku 4.5 on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="even">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 1,800</li>
<li>Input TPM: 1,800,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 180,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td><code>global endpoint</code></td>
<td><ul>
<li>QPM: 2,500</li>
<li>Input TPM: 2,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 250,000</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude 3.5 Haiku on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 80</li>
<li>TPM: 350,000 (input and output)</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="odd">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 90</li>
<li>TPM: 400,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td>Claude 3.5 Sonnet on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 80</li>
<li>TPM: 350,000 (input and output)</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="odd">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 130</li>
<li>TPM: 600,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>asia-southeast1</code></td>
<td><ul>
<li>QPM: 35</li>
<li>TPM: 150,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="odd">
<td>Claude 3 Opus on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 20</li>
<li>TPM: 105,000 (input and output)</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="even">
<td>Claude 3 Haiku on Google Cloud</td>
<td><code>us-east5</code></td>
<td><ul>
<li>QPM: 245</li>
<li>TPM: 600,000 (input and output)</li>
</ul></td>
<td>200,000</td>
</tr>
<tr class="odd">
<td><code>europe-west1</code></td>
<td><ul>
<li>QPM: 75</li>
<li>TPM: 181,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
<tr class="even">
<td><code>asia-southeast1</code></td>
<td><ul>
<li>QPM: 70</li>
<li>TPM: 174,000 (input and output)</li>
</ul></td>
<td>200,000</td>
<td></td>
</tr>
</tbody>
</table>

If you want to increase any of your quotas for Agent Platform, you can use the Google Cloud console to request a quota increase. To learn more about quotas, see the [Cloud Quotas overview](https://docs.cloud.google.com/docs/quotas/overview) .
