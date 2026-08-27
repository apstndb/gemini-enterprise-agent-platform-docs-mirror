---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/agent-studio-capabilities
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/agent-studio-capabilities
title: Agent Studio capabilities
description: Learn about the capabilities of Agent Studio for discovering models, prompt engineering, and collaborative development within Agent Platform.
data_source: docs.cloud.google.com
---

Agent Studio provides a collaborative workspace for discovering models, refining system instructions, and optimizing prompts. With built-in tools for natural language refinement and side-by-side comparison, you can efficiently prototype and test generative AI solutions.

This page outlines the key features implemented within Agent Studio that facilitate transforming innovative ideas into generative AI solutions, for example, solutions that benefit customer service and support, content creation, healthcare, financial services, and software development.

## Roles

You can control which Google Cloud services that users can access through Agent Studio by assigning the following roles:

| Role          | Description                                                                                                                                                |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Administrator | Responsible for Google Cloud setup that interacts with agents using technical language to connect Agent Platform with the Google Cloud ecosystem.          |
| Builder       | Includes the ML developers and App developers, who use the developer tools. Agents use developer-specific language with a scope limited to Agent Platform. |

## Features and experiences

This section describes Agent Studio capabilities.

### Navigation and playgrounds

Agent Studio opens on the prompt workspace, where you write prompts, adjust model settings, and compare responses. The left navigation gives you the following destinations:

| Destination           | Description                                                                                                                                                                                                                                          |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| New                   | Opens a new playground. See the following table for the available playgrounds.                                                                                                                                                                       |
| Agents (preview)      | The list of agents you have designed. From here you can open an existing agent or create one. For more information, see [Design agents in Agent Studio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents) . |
| App builder (preview) | A workspace for generating a web application from a description, and for editing and deploying the generated code.                                                                                                                                   |
| Gallery               | Sample prompts, apps, and agents that you can open and run. Filter the samples by task, media type, or feature.                                                                                                                                      |
| Documentation         | Opens the Agent Platform documentation in a new tab.                                                                                                                                                                                                 |

> **Preview**
> 
> These features are subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To start fresh work, click **New** in the left navigation and choose a playground. Each playground is tuned for one kind of model output:

| Playground | Description                                                                                                                                                                                                                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Chat       | Multi-turn text and multimodal prompting. Supports the full set of model settings, grounding options, and built-in tools.                                                                                                                                                                        |
| Image      | Image generation and editing. For more information, see [Generate images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation) .                                                                                                                 |
| Video      | Video generation. For more information, see [Video generation overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/overview) .                                                                                                                                  |
| Music      | Music generation. For more information, see [Music generation overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/overview) .                                                                                                                                  |
| Speech     | Speech generation and transcription. For more information, see [Text-to-speech](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/speech/text-to-speech) and [Speech-to-text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/speech/speech-to-text) . |
| Live API   | Low-latency, bidirectional voice and video interaction. For more information, see [Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) .                                                                                                                   |

The Image, Video, Music, and Speech playgrounds are collectively known as Agent Media Studio.

### Onboarding and administrative

The onboarding and administrative features let you access and set up your environment.

| Feature              | Description                                                                                                                                                                                  |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Get API key          | You can access your API key quickly.                                                                                                                                                         |
| Getting started menu | A menu for new users with steps to properly activate their accounts, which include trying a prompt, adding a collaborator, and getting an API key.                                           |
| Settings menu        | A settings menu that includes options to switch between the previous and latest UI, change the appearance to use the light or dark system, generate and access API keys, and manage billing. |

### Studio discovery and development

The studio discovery and development features enhance the developer workflow.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Interactive canvas view</td>
<td>A canvas that illustrates the artifact to be retrieved for development, which includes a setting/preview pane and a code view.</td>
</tr>
<tr class="even">
<td>Minimap</td>
<td>A summarized history of prompt and response headers that can be turned off.</td>
</tr>
<tr class="odd">
<td>Slash commands</td>
<td>Type <code dir="ltr" translate="no">/</code> in the prompt field to open the command menu. The commands are grouped as follows.<br />
<strong>Prompt development:</strong>
<ul>
<li><strong><code dir="ltr" translate="no">/model [describe]</code></strong> : Change the model.</li>
<li><strong><code dir="ltr" translate="no">/prompt [describe]</code></strong> : Improve your prompt. Use <code dir="ltr" translate="no">/prompt -generate           DESCRIPTION         </code> to generate a prompt and system instructions from an intent, or <code dir="ltr" translate="no">/prompt -refine           INSTRUCTIONS         </code> to revise the current prompt from your feedback.</li>
<li><strong><code dir="ltr" translate="no">/si</code></strong> : Optimize system instructions. Use <code dir="ltr" translate="no">/si -optimize</code> to rewrite the current system instructions.</li>
</ul>
<strong>Test and deploy:</strong>
<ul>
<li><strong><code dir="ltr" translate="no">/compare</code></strong> : Compare settings and instructions side by side.</li>
<li><strong><code dir="ltr" translate="no">/evaluate [optional guideline]</code></strong> : Get metrics for the last prompt and response.</li>
<li><strong><code dir="ltr" translate="no">/build [describe]</code></strong> : Describe an app to build.</li>
</ul>
<strong>Actions:</strong>
<ul>
<li><strong><code dir="ltr" translate="no">/clear</code></strong> : Clear the current conversation.</li>
</ul></td>
</tr>
<tr class="even">
<td>Side-by-side comparison</td>
<td>An updated comparison feature for models, system instructions, and prompts, which lets you compare multiple prompts and your responses simultaneously.</td>
</tr>
<tr class="odd">
<td>Upload large files</td>
<td>The ability to upload local or Cloud Storage files up to 50 MB.</td>
</tr>
<tr class="even">
<td>Generate code files</td>
<td>A feature that generates application code files, which are then accessible in the canvas pane.</td>
</tr>
<tr class="odd">
<td>Download code files</td>
<td>The ability to download generated code files as a zip file.</td>
</tr>
<tr class="even">
<td>Undo or Redo</td>
<td>Undo or redo functionality is available for actions like model settings and prompt changes.</td>
</tr>
<tr class="odd">
<td>Gallery</td>
<td>A gallery of sample prompts, apps, and agents. Filter the samples by task, media type, or feature.</td>
</tr>
</tbody>
</table>

### Prompt settings

The **Model settings** panel next to the prompt controls how the model generates a response. The available settings depend on the model and the playground you are using.

| Setting                  | Description                                                                                                                                                                                                                                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Thinking level           | How much reasoning the model does before responding. For more information, see [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking) .                                                                                                                        |
| Output format            | The response MIME type, which lets you request structured output such as JSON. For more information, see [Control generated output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output) .                                                 |
| Grounding with Google    | Ground responses in Google Search results. Click **Customize** to configure the search behavior. For more information, see [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search) .                          |
| Grounding with partners  | Ground responses in a partner data source, such as [Elasticsearch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-elasticsearch) .                                                                                                                 |
| Grounding with your data | Ground responses in your own enterprise data using [Agent Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-vertex-ai-search) or [RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview) . |
| Function calling         | Let the model call functions that you declare. For more information, see [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .                                                                                                        |
| Code execution           | Let the model generate and run code to answer a prompt.                                                                                                                                                                                                                                            |
| URL context              | Let the model fetch and analyze URLs that appear in your prompt.                                                                                                                                                                                                                                   |
| Safety filter settings   | Thresholds that control which responses are blocked. For more information, see [Configure safety filters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/configure-safety-filters) .                                                                           |
| Output token limit       | The maximum number of tokens the model can generate in a response.                                                                                                                                                                                                                                 |
| Stop sequences           | Strings that stop generation when the model produces them.                                                                                                                                                                                                                                         |
| Seed                     | A fixed seed value, which makes responses more reproducible across requests that use the same prompt and settings.                                                                                                                                                                                 |
| Stream model responses   | Return the response incrementally as it is generated, instead of waiting for the complete response.                                                                                                                                                                                                |
| Region                   | The region that serves the request. The available regions depend on the model you select.                                                                                                                                                                                                          |

### Built-in tools and capabilities

This section lists the built-in tools and capabilities within Agent Studio that automate a significant portion of the work for developers. Agent Studio integrates with Google Cloud, which provides an effortless experience that's collaborative and agentic.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Natural language refinement</td>
<td>For prompt refinement, you can describe how you want to change your prompt using natural language, and the system automatically optimizes the prompt for you.</td>
</tr>
<tr class="even">
<td>Optimize system instruction</td>
<td>You can use a one-click feature that asks Gemini to automatically optimize a system instruction based on the prompt.</td>
</tr>
<tr class="odd">
<td>Refine prompt response</td>
<td>You can use the <code dir="ltr" translate="no">/prompt</code> command to provide feedback and to create a well-formatted revised prompt.</td>
</tr>
<tr class="even">
<td>Help-me-write tool</td>
<td>You can use the <code dir="ltr" translate="no">/prompt</code> command and a described intent to create a well-formatted prompt, system instruction, and to recommend a model.</td>
</tr>
<tr class="odd">
<td>Convert to agent (preview)</td>
<td>Turn the prompt you are working on into an agent. In the <strong>Build with code</strong> menu, click <strong>Convert to agent</strong> . The model, system instructions, prompt, and prompt variables carry over to the new agent, which you can then design and deploy. For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/design-agents">Design agents in Agent Studio</a> .<br />
<br />
The prompt or the system instructions must be non-empty before you can convert. This feature isn't available to signed-out users or to users without a billing-enabled project.</td>
</tr>
</tbody>
</table>

## What's next

Overview

### [Build overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build)

Learn how to build agents in Google Agent Platform.

Quickstart

### [Agent Studio quickstart: Send text prompts to Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/quickstart)

Learn how to send text prompts to Gemini using Agent Studio.

Guide

### [Deploy your prompt as a web application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/deploy-vais-prompt)

Follow the guide to deploy your prompt as a web application from Agent Studio.
