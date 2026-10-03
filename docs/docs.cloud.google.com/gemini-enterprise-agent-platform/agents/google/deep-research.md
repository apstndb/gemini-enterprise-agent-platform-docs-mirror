---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/google/deep-research
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/google/deep-research
title: Gemini Deep Research Agent
description: Learn about the Gemini Deep Research Agent, our advanced agent for deep research.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The Gemini Deep Research Agent is a managed AI agent designed to plan, execute, and synthesize complex, multi-step research workflows. Powered by Gemini, the agent navigates diverse information landscapes including the public web and private enterprise data to generate comprehensive, cited reports that accelerate informed decision-making.

For more information on how to get started using Deep Research, see [Use the Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Agent ID</th>
<td><code>deep-research-preview-04-2026</code></td>
<td></td>
</tr>
<tr class="even">
<th>Supported APIs</th>
<td><ul>
<li>Interactions API</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , PDF</li>
<li>Outputs:
Text , Images</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 1,048,576</li>
<li>Maximum output tokens: 65,536</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search">Grounding with Google Search</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/web-grounding-enterprise">Grounding with Enterprise Web Search</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-vertex-ai-search">Grounding with Agent Search</a></li>
<li><a href="https://ai.google.dev/gemini-api/docs/interactions/deep-research#mcp-servers">Grounding on remote MCP servers</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thought summaries</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Implicit context caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search#inline-citations">Citations</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking level</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Explicit context caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></li>
</ul>
Not supported</td>
<td></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Consumption options</a> for more information.</th>
<td></td>
<td></td>
</tr>
<tr class="even">
<th>Technical specifications</th>
<td></td>
<td></td>
</tr>
<tr class="odd">
<th><strong>Documents</strong> description</th>
<td><ul>
<li>Maximum number of files per prompt: 3,000</li>
<li>Maximum number of pages per file: 3,000</li>
<li>Maximum file size per file for the API or Cloud Storage imports: 50 MB (application/pdf) or 7 MB (text/plain)</li>
<li>Maximum file size per file for direct uploads through the console: 7 MB</li>
<li>Default resolution tokens: 560</li>
<li>OCR for scanned PDFs: Not used by default</li>
<li>Supported MIME types:
<code>application/pdf</code> , <code>text/plain</code></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td><p>Agent availability</p></td>
<td>Global
<ul>
<li>global</li>
</ul></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations">Agent locations</a> for more information.</th>
<td></td>
<td></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>January 2025</td>
<td></td>
</tr>
<tr class="odd">
<th>Quota name</th>
<td>Stateful Gen AI Interaction Creation requests per minute</td>
<td></td>
</tr>
<tr class="even">
<th>Billing label</th>
<td><code>is_deep_research</code></td>
<td></td>
</tr>
<tr class="odd">
<th>Supported languages</th>
<td>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#expandable-1">Supported languages</a> .</td>
<td></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
<td></td>
</tr>
</tbody>
</table>
