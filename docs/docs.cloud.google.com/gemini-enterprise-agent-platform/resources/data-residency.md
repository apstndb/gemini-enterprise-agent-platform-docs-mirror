---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency
title: Data residency
description: Review data residency commitments and ML processing locations for Agent Platform. See location details for Google, partner, and open models.
data_source: docs.cloud.google.com
---

Data stored at rest in the customer selected location remains at rest in that [location](https://cloud.google.com/about/locations) , independent of the Agent Platform endpoint called by that customer's request.

## ML processing

Machine learning (ML) processing for Agent Platform services occurs within the specific [region or multi-region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) where the request is made. For instructions on how to connect to endpoints, see [Specify an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations#specify-an-endpoint) .

For any regional endpoint not explicitly listed in the following tables, such as those in the Middle East, there is no guarantee that ML processing occurs at a specific location. These endpoints support older models that don't offer ML processing guarantees.

### Google Cloud model support

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
<td>Anthropic's Claude Haiku 4.5</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Opus 4</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Opus 4.1</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Opus 4.5</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Opus 4.8</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Opus 4.7</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Opus 4.6</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Sonnet 4</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude Sonnet 4.5</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude Sonnet 4.6</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude 3.5 Haiku (deprecated)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Anthropic's Claude 3 Haiku (deprecated)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Anthropic's Claude 3.7 Sonnet (deprecated)</td>
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
