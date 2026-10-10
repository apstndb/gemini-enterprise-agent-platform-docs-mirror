---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api
title: Gemini 2.5 Flash with Gemini Live API
description: Learn about Gemini 2.5 Flash with Gemini Live API, featuring cutting-edge audio functionality.
data_source: docs.cloud.google.com
---

Gemini 2.5 Flash with Gemini Live API native audio features our cutting-edge native audio functionality for [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) . In addition to the standard Gemini Live API features, this model includes:

- **Enhanced audio quality:** Experience dramatically improved audio quality that feels like speaking with a person.
- **Enhanced voice quality and adaptability:** Gemini Live API native audio provides richer, more natural voice interactions with [30 HD voices](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd#voice_options) in [24 languages](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd#language_availability) .
- **Introducing [Proactive Audio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-gemini-capabilities#use-proactive-audio) :** (Preview) When Proactive Audio is enabled, the model only responds when it's relevant. The model generates text transcripts and audio responses proactively only for queries directed to the device, and does not respond to non-device directed queries.
- **Introducing Affective Dialog:** Models using Gemini Live API native audio can understand and respond appropriately to users' emotional expressions for more nuanced conversations.
- **Improved barge-in:** Interrupt Gemini more naturally and reliably, even in loud and noisy environments.
- **Robust function calling:** We've improved the triggering rate, allowing Gemini to successfully execute the functions you define to support your use cases.
- **Accurate transcription:** The accuracy of audio-to-text transcription has been significantly enhanced. For even better results, you can provide language hints to guide the model toward the correct language. For more information, see [Enable audio transcription for the session](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#enable-audio-transcription) .
- **Seamless multilingual support:** Speak to Gemini in multiple languages, and it will effortlessly switch between them without any pre-configuration. Language is no longer a barrier.

For more information on Gemini Live API, see:

- Our [standalone Gemini Live API documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) .
- Our [Gemini Live API supported audio formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api#supported-audio-formats) .
- Our [Gemini Live API concurrent session limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#max-concurrent-sessions) .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal-live?model=gemini-live-2.5-flash-native-audio) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<th><code>gemini-live-2.5-flash-native-audio</code></th>
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
Input and output
videocam
Video<br />
Input only</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Context window</th>
<td>128K</td>
</tr>
<tr class="even">
<th>Maximum output tokens</th>
<th>64K</th>
<td></td>
</tr>
<tr class="odd">
<th>Maximum concurrent sessions</th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#maximum_concurrent_sessions">1000</a></th>
<td></td>
</tr>
<tr class="even">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a> preview Preview feature<br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Tools</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a><br />
Google Search<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a> preview Preview feature<br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>APIs</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Technical specifications</th>
<th><strong>Image</strong> photo</th>
<td><ul>
<li>Maximum images per prompt: 3,000</li>
<li>Maximum file size per file for inline data or direct uploads through the console: 7 MB</li>
<li>Maximum file size per file from Google Cloud Storage: 30 MB</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/heic</code> , <code>image/heif</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><strong>Video</strong> videocam</th>
<th><ul>
<li>Standard resolution: 768 x 768</li>
<li>Supported MIME types:
<code>video/x-flv</code> , <code>video/quicktime</code> , <code>video/mpeg</code> , <code>video/mpegs</code> , <code>video/mpg</code> , <code>video/mp4</code> , <code>video/webm</code> , <code>video/wmv</code> , <code>video/3gpp</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Audio</strong> mic</th>
<th><ul>
<li>Maximum conversation length: Default 10 minutes that can <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#session-extension">be extended.</a></li>
<li>Required audio input format: Raw 16-bit PCM audio at 16kHz, little-endian</li>
<li>Required audio output format: Raw 16-bit PCM audio at 24kHz, little-endian</li>
<li>Supported MIME types:
<code>audio/x-aac</code> , <code>audio/flac</code> , <code>audio/mp3</code> , <code>audio/m4a</code> , <code>audio/mpeg</code> , <code>audio/mpga</code> , <code>audio/mp4</code> , <code>audio/ogg</code> , <code>audio/pcm</code> , <code>audio/wav</code> , <code>audio/webm</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Parameter defaults</strong> tune</th>
<th><ul>
<li>Start of speech sensitivity: Low</li>
<li>End of speech sensitivity: High</li>
<li>Prefix padding: 0</li>
<li>Max context size: 128K</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>United States: <code>us-central1</code> , <code>us-east1</code> , <code>us-east4</code> , <code>us-east5</code> , <code>us-south1</code> , <code>us-west1</code> , <code>us-west4</code></li>
<li>Europe: <code>europe-central2</code> , <code>europe-north1</code> , <code>europe-southwest1</code> , <code>europe-west1</code> , <code>europe-west4</code> , <code>europe-west8</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Versions</th>
<th><ul>
<li><code>gemini-live-2.5-flash-native-audio</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: December 12, 2025</li>
<li>Retirement date <sup><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api#retirement-date">†</a></sup> : December 13, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Security controls</th>
<th><strong>Online prediction</strong></th>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<th></th>
<td></td>
</tr>
</tbody>
</table>

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .
