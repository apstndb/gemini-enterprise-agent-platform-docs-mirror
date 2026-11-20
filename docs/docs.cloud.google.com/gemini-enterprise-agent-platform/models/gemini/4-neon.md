---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-neon
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-neon
title: Gemini 4 Neon
description: Learn about Gemini 4 Neon, built for high-performance coding, multi-step reasoning, and low-latency agentic workflows in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Gemini 4 Neon delivers high-performance coding, multi-step reasoning, and multimodal understanding at low latency for agentic enterprise workflows. Gemini 4 Neon is a Google Frontier Model subject to Section 34 of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) (for details, see [Abuse monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring#google-frontier-models) ).

Neon differs from earlier Gemini models in the following ways:

- **Unified input and output token limit and long decodes** : Neon shares a unified 1,048,576-token limit across input and output tokens on the [`GenerateContent` API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference) , the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) , and the [OpenAI compatibility Chat Completions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/openai) . Output tokens include thinking, function calls, and the final response, and a single foreground segment generates up to 65,536 output tokens. On the Interactions API and `GenerateContent` ( `v1beta1` ), long decodes extend output up to 1,048,576 tokens minus your input tokens. The Google Gen AI SDK and Agent Studio follow `continuation_token` automatically across segments ( `v1beta1` by default). You can also run `background=true` on the Interactions API or pass `continuation_token` in a custom loop. For details, see the [developer's guide to Gemini 4 Neon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-neon#long-decodes) .

- **Thinking levels** : Neon supports [thinking levels](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking) `LOW` , `MEDIUM` , `HIGH` (default), and `XHIGH` . Setting `thinking_budget` or `thinking_level="MINIMAL"` returns an HTTP `400` validation error.

- **Sampling parameters** : Custom values for [sampling parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters) ( `temperature` , `top_p` , and `top_k` ) are ignored.

- **Context caching** : Neon supports [implicit caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview) only (4,096-token minimum), with durable caching enabled by default. Explicit context caching isn't supported. Starting on January 12, 2027, Gemini 4 Hydrogen and later models support cache control features with TTL configuration. You choose what to cache and how long cached content stays valid through TTL configuration. Cache writes are billed at 1.25x the standard input token price by default, and longer retention costs more. For details, see [Gemini 4 pricing](https://cloud.google.com/model-garden/pricing#gemini-4) .

- **Office and OpenDocument file inputs** : In addition to PDF ( `application/pdf` ) and plain text ( `text/plain` ), Neon accepts Microsoft Office ( `.docx` , `.dotx` , `.doc` , `.pptx` , `.ppt` , `.xlsx` , `.xls` ) and OpenDocument ( `.odt` , `.odp` , `.ods` ) files inline or from Cloud Storage on both the [`GenerateContent` API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference) and the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) , including inside multimodal `FunctionResponse` parts.

> **Note:** To maintain platform reliability, capacity, and security, Gemini 4 Neon is available to verified enterprise customers in select regions.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/chat?model=gemini-4-neon) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/chat?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-4-neon) [Developer guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-neon) [Pricing](https://cloud.google.com/model-garden/pricing)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<th><code>gemini-4-neon</code></th>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<th>description
Text<br />
Input and output
photo
Image<br />
Input only
mic
Audio<br />
Input only
videocam
Video<br />
Input only</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Context window</th>
<td>1,048,576</td>
</tr>
<tr class="even">
<th>Maximum output tokens</th>
<th>1,048,576</th>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Implicit context caching<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Tools</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a><br />
Google Search, Google Maps, Agent Search, Parallel Web Search, Exa Web Search, Web Grounding for Enterprise<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>APIs</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo with Usage Tiers, Priority PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier">Deferred tier</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Input size limit</th>
<th><ul>
<li>GenerateContent API: 500 MiB compressed</li>
<li>Interactions API: 256 MiB compressed (synchronous or streaming); 9.75 MiB uncompressed (deferred, when background and store are true)</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Interactions API URI limit</th>
<th>Up to 100 distinct Cloud Storage ( <code>gs://</code> ) URIs per request across all modalities on the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> , including URIs carried forward from earlier turns using <code>previous_interaction_id</code> . <code>generateContent</code> supports <code>gs://</code> URIs up to the per-modality model item limits (up to 6,500 combined multimodal files when including plain-text files).</th>
<td></td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<th><strong>Image</strong></th>
<td><ul>
<li>Maximum images per prompt: 3,000 (images and documents combined)</li>
<li>Maximum inline part size (GenerateContent API): 256 MB</li>
<li>Maximum file size per file from Cloud Storage: 2 GiB minus 500 KiB</li>
<li>Maximum file size per file from public HTTP or HTTPS URLs: 15 MiB</li>
<li>Maximum file size per file for direct local uploads in the console: 7 MiB inline (up to 50 MiB staged to Cloud Storage)</li>
<li>Maximum file size per file for Google Drive imports in the console: 7 MB (10 MB total)</li>
<li>Default resolution tokens: 1,120</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/heic</code> , <code>image/heif</code></li>
</ul></td>
</tr>
<tr class="even">
<th><strong>Text</strong></th>
<th><ul>
<li>Maximum number of files per prompt: 3,000 documents (shared with images; up to 6,500 total files when including plain text)</li>
<li>Maximum number of pages per file: 3,000</li>
<li>Maximum inline part size (GenerateContent API): 256 MB</li>
<li>Maximum file size per file from Cloud Storage: 2 GiB minus 500 KiB</li>
<li>Maximum file size per file from public HTTP or HTTPS URLs: 15 MiB</li>
<li>Maximum file size per file for direct local uploads in the console: 7 MiB inline (up to 50 MiB staged to Cloud Storage)</li>
<li>Maximum file size per file for Google Drive imports in the console: 7 MB (10 MB total)</li>
<li>Default resolution tokens: 560</li>
<li>OCR for scanned PDFs: Not used by default</li>
<li>Supported MIME types:
<code>application/pdf</code> , <code>text/plain</code> , <code>application/msword</code> , <code>application/vnd.openxmlformats-officedocument.wordprocessingml.document</code> , <code>application/vnd.openxmlformats-officedocument.wordprocessingml.template</code> , <code>application/vnd.oasis.opendocument.text</code> , <code>application/vnd.ms-powerpoint</code> , <code>application/vnd.openxmlformats-officedocument.presentationml.presentation</code> , <code>application/vnd.oasis.opendocument.presentation</code> , <code>application/vnd.ms-excel</code> , <code>application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</code> , <code>application/vnd.oasis.opendocument.spreadsheet</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Video</strong></th>
<th><ul>
<li>Maximum video length (with audio): Approximately 45 minutes</li>
<li>Maximum video length (without audio): Approximately 1 hour</li>
<li>Maximum number of videos per prompt: 10</li>
<li>Maximum inline part size (GenerateContent API): 256 MB</li>
<li>Maximum file size per file from Cloud Storage: 2 GiB minus 500 KiB</li>
<li>Maximum file size per file from public HTTP or HTTPS URLs: 15 MiB</li>
<li>Default resolution tokens per frame: 70</li>
<li>Supported MIME types:
<code>video/x-flv</code> , <code>video/quicktime</code> , <code>video/mpeg</code> , <code>video/mpegs</code> , <code>video/mpg</code> , <code>video/mp4</code> , <code>video/webm</code> , <code>video/wmv</code> , <code>video/3gpp</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Audio</strong></th>
<th><ul>
<li>Maximum audio length per prompt: Approximately 8.4 hours, or up to 1 million tokens</li>
<li>Maximum number of audio files per prompt: 1,000</li>
<li>Maximum inline part size (GenerateContent API): 256 MB</li>
<li>Maximum file size per file from Cloud Storage: 2 GiB minus 500 KiB</li>
<li>Maximum file size per file from public HTTP or HTTPS URLs: 15 MiB</li>
<li>Speech understanding for: Audio summarization, transcription, and translation</li>
<li>Supported MIME types:
<code>audio/x-aac</code> , <code>audio/flac</code> , <code>audio/mp3</code> , <code>audio/m4a</code> , <code>audio/mpeg</code> , <code>audio/mpga</code> , <code>audio/mp4</code> , <code>audio/ogg</code> , <code>audio/pcm</code> , <code>audio/wav</code> , <code>audio/webm</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Parameter defaults</strong></th>
<th><ul>
<li>Temperature: 1.0 (fixed; custom values ignored)</li>
<li>topP: 0.95 (fixed; custom values ignored)</li>
<li>topK: 64 (fixed; custom values ignored)</li>
<li>candidateCount: 1 (fixed)</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency">ML processing</a></strong></p></th>
<th><ul>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models">Provisioned Throughput</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo">Priority PayGo</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Knowledge cutoff date</th>
<th>March 2026</th>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-4-neon</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: November 18, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Security controls</th>
<th><strong>Online prediction</strong></th>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="even">
<th><strong>Batch inference</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Context caching</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<th></th>
<td></td>
</tr>
</tbody>
</table>
