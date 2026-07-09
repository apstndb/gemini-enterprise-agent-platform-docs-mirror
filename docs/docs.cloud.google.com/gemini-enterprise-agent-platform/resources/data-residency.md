---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency
title: Data residency
description: Review data residency commitments and ML processing locations for Agent Platform. See location details for Google, partner, and open models.
data_source: docs.cloud.google.com
---

Data stored at rest in the customer selected location remains at rest in that [location](https://cloud.google.com/about/locations) , independent of the Agent Platform endpoint called by that customer's request.

## Where your data lives and is processed

Gemini Enterprise Agent Platform provides transparency on where your data is stored ("at rest") and where the actual model computation ("ML processing") happens.

### 1\. Data-at-rest (storage)

When you store data on Agent Platform (such as custom model weights or metadata), it remains physically stored in the specific Google Cloud location you chose. This residency is maintained regardless of which endpoint you use to call the model.

### 2\. ML processing (in-use)

*ML processing* is the method by which data is processed such that it produces model weights (tuning & training) or applies the model to the data for model inference. The geographic location of this processing is determined by your choice of endpoint:

  - **Jurisdictional multi-region endpoints** : When you use jurisdictional endpoints, ML processing stays within that specific geographical region (such as the United States or the European Union).
    
    > **Note:** The European Union multi-region ( `eu` ) endpoint strictly covers data residency within EU member states. Geographies outside the European Union political boundary, including the United Kingdom and Switzerland, are excluded from this endpoint.
    
      - **Operational efficiency (unified capacity)** : Multi-region endpoints eliminate regional resource siloes. Instead of purchasing and managing separate Provisioned Throughput allocations for individual regions (such as `us-central1` and `us-east4` ), you can deploy a single Provisioned Throughput commitment that covers your entire jurisdictional boundary (such as the United States).
    
      - **Compliance enablement** : Multi-region endpoints provide the data-in-use isolation controls required to help satisfy stringent regulatory frameworks. While multi-region endpoints serve as a foundational technical capability for complying with Department of Defense (DoD) Impact Level 5 (IL5) or International Traffic in Arms Regulations (ITAR) requirements, fully achieving compliance also requires broader customer-managed architecture, identity, and access controls.
        
        > **Important:** Models not explicitly listed as supporting US multi-regions don't meet DoD IL5 commitments. IL5 customers are responsible for restricting access to these models on Global endpoints by configuring [organizational policies](https://docs.cloud.google.com/docs/security/compliance/restrict-endpoint-usage) to block global endpoint traffic.

  - **Locational endpoints** : These endpoints (like `us-central1` , `europe-west1` ) ensure that ML processing remains entirely within the broader multi-regional or country jurisdiction associated with that region (for example, requests to us-central1 are processed within the United States).
    
    For European regions, local in-country processing varies by model type (for example, specific models may have local processing in France or Germany, while others are processed within the broader EU multi-region boundary). See the [following section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency#supported-models) for the exact ML processing commitments for each model and location.
    
      - **Compliance alignment** : While locational endpoints meet standard enterprise data governance and sovereign requirements (such as GDPR and HIPAA), workloads requiring specialized government isolation frameworks like DoD IL5 or ITAR should be deployed on jurisdictional endpoints as part of a broader compliant architecture.

  - **Global endpoints** : Global endpoints route and process data anywhere globally, without restricting it to a specific geographic region. These endpoints (like `https://aiplatform.googleapis.com` ) don't specify a region in the hostname. They are designed to maximize availability and minimize latency by terminating TLS sessions as close to the client as possible, but they don't provide regional isolation or data residency guarantees.

## Supported models

The tables in this section cover the regional support for ML processing at a per-model basis for the following model categories:

  - [Google models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency#ml-processing-google-models)
  - [Partner models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency#ml-processing-partner-models)
  - [Open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency#ml-processing-open-models)

### Google models

To learn what capabilities support data residency, see [Supported capabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/supported-capabilities) .

<table style="width:100%;">
<colgroup>
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
<col style="width: 7%" />
</colgroup>
<thead>
<tr class="header">
<th>Model</th>
<th>US multi-region</th>
<th>EU multi-region</th>
<th>Brazil<br />
(southamerica-east1)</th>
<th>Canada<br />
(northamerica-northeast1)</th>
<th>France<br />
(europe-west9)</th>
<th>Germany<br />
(europe-west3)</th>
<th>Netherlands<br />
(europe-west4)</th>
<th>United Kingdom<br />
(europe-west2)</th>
<th>Australia<br />
(australia-southeast1)</th>
<th>India<br />
(asia-south1)</th>
<th>Japan<br />
(asia-northeast1)</th>
<th>Singapore<br />
(asia-southeast1)</th>
<th>South Korea<br />
(asia-northeast3)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Gemini 3.5 Flash<br />
( <code dir="ltr" translate="no">gemini-3.5-flash</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Gemini 3.1 Flash-Lite<br />
( <code dir="ltr" translate="no">gemini-3.1-flash-lite</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Gemini 2.5 Flash Live API Native Audio<br />
( <code dir="ltr" translate="no">gemini-live-2.5-flash-native-audio</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Gemini 2.5 Flash, 128k<br />
( <code dir="ltr" translate="no">gemini-2.5-flash</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Gemini 2.5 Flash, 1M<br />
( <code dir="ltr" translate="no">gemini-2.5-flash</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Gemini 2.5 Flash Image<br />
( <code dir="ltr" translate="no">gemini-2.5-flash-image</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Gemini 2.5 Flash-Lite<br />
( <code dir="ltr" translate="no">gemini-2.5-flash-lite</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Gemini 2.5 Pro, 1M<br />
( <code dir="ltr" translate="no">gemini-2.5-pro</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Gemini 2.5 Pro, 64k<br />
( <code dir="ltr" translate="no">gemini-2.5-pro</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Tuning for Gemini 2.5 Flash<br />
( <code dir="ltr" translate="no">gemini-2.5-flash</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Tuning for Gemini 2.5 Flash-Lite<br />
( <code dir="ltr" translate="no">gemini-2.5-flash-lite</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Tuning for Gemini 2.5 Pro<br />
( <code dir="ltr" translate="no">gemini-2.5-pro</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Gemini Embedding<br />
( <code dir="ltr" translate="no">gemini-embedding-001</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Gemini Embedding 2<br />
( <code dir="ltr" translate="no">gemini-embedding-2</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Chirp 2: Transcription<br />
( <code dir="ltr" translate="no">chirp_2</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Chirp 3: Transcription<br />
( <code dir="ltr" translate="no">chirp_3</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Chirp 3: HD Voices</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Chirp 3: Instant Custom Voice</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Embeddings for Multimodal</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Embeddings for Text<br />
( <code dir="ltr" translate="no">text-embedding-004</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Embeddings for Text<br />
( <code dir="ltr" translate="no">text-embedding-005</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Embeddings for Text<br />
( <code dir="ltr" translate="no">text-multilingual-embedding-002</code> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Google Cloud partner model support

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>Model</th>
<th>US multi-region</th>
<th>EU multi-region</th>
<th>Belgium<br />
(europe-west1)</th>
<th>Netherlands<br />
(europe-west4)</th>
<th>Singapore<br />
(asia-southeast1)</th>
<th>Taiwan<br />
(asia-east1)</th>
<th>Global</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Anthropic's Claude Sonnet 5 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Fable 5 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Haiku 4.5 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Opus 4 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Opus 4.1 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Opus 4.5 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Opus 4.8 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Opus 4.7 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Opus 4.6 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Sonnet 4 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Sonnet 4.5 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Sonnet 4.6 on Google Cloud</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude 3.5 Haiku on Google Cloud (deprecated)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude 3 Haiku on Google Cloud (deprecated)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude 3.7 Sonnet on Google Cloud (deprecated)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Codestral (24.05)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Codestral 2</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Mistral Large (24.07)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Mistral Medium 3</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Mistral OCR (25.05)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Mistral Small 3.1 (25.03)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Google Cloud open model support

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Model</th>
<th>US multi-region</th>
<th>EU multi-region</th>
<th>Singapore<br />
(asia-southeast1)</th>
<th>Global</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>DeepSeek-OCR</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>DeepSeek R1 (0528)</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>DeepSeek-V3.1</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>DeepSeek-V3.2</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Gemma 4 26B A4B IT</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>GLM 4.7</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>GLM 5</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>gpt-oss 120B</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>gpt-oss 20B</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Kimi K2 Thinking</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Llama 3.3 70B (Preview)</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Llama 4 Maverick 17B-128E (Preview)</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Llama 4 Scout 17B-16E (Preview)</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>MiniMax M2</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Multilingual E5 Large</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Multilingual E5 Small</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Qwen3 235B</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Qwen3 Coder</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Qwen3-Next-80B Instruct</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Qwen3-Next-80B Thinking</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## What's next

  - Learn about [Google Cloud regions](https://docs.cloud.google.com/docs/geography-and-regions) .

  - Learn more about [security controls by feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) .

  - Learn about [Gemini Enterprise Agent Platform locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .
