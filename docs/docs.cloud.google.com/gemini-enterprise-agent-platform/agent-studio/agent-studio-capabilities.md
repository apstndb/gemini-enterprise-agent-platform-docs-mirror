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

| **Role**      | **Description**                                                                                                                                            |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Administrator | Responsible for Google Cloud setup that interacts with agents using technical language to connect Agent Platform with the Google Cloud ecosystem.          |
| Builder       | Includes the ML developers and App developers, who use the developer tools. Agents use developer-specific language with a scope limited to Agent Platform. |

## Features and experiences

This section describes Agent Studio capabilities.

### Onboarding and administrative

The onboarding and administrative features let you access and set up your environment.

| **Feature**              | **Description**                                                                                                                                                                              |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Access to API key        | You can access your API key quickly.                                                                                                                                                         |
| Left navigation redesign | The left menu includes a Floating Action Button (FAB) that lets you open different playgrounds, view recent sessions, and access other options.                                              |
| Getting started menu     | A menu for new users with steps to properly activate their accounts, which include trying a prompt, adding a collaborator, and getting an API key.                                           |
| New experience opt-in    | A dialog that prompts existing users to try the latest signin and can revert to their earlier UI in settings.                                                                                |
| Settings menu            | A settings menu that includes options to switch between the previous and latest UI, change the appearance to use the light or dark system, generate and access API keys, and manage billing. |

### Studio discovery and development

The studio discovery and development features enhance the developer workflow.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Feature</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Interactive canvas view</td>
<td>A canvas that illustrates the artifact to be retrieved for development, which includes a preview and a code view.</td>
</tr>
<tr class="even">
<td>Minimap</td>
<td>A summarized history of prompt and response headers that can be turned off.</td>
</tr>
<tr class="odd">
<td>Slash commands</td>
<td>Keyboard shortcuts for developers, which include the following commands:<br />

<ul>
<li><strong><code dir="ltr" translate="no">/ask</code></strong> : You can get Google Cloud and general help.</li>
<li><strong><code dir="ltr" translate="no">/clear</code></strong> : You can clear the current conversation.</li>
<li><strong><code dir="ltr" translate="no">/compare</code></strong> : You can see how changes impact a response.</li>
<li><strong><code dir="ltr" translate="no">/model</code></strong> : You can manage your model selection.</li>
<li><strong><code dir="ltr" translate="no">/prompt</code></strong> : You can manage and modify prompts.</li>
</ul></td>
</tr>
<tr class="even">
<td>Side-by-side comparison</td>
<td>An updated comparison feature for models, system instructions, and prompts, which lets you compare multiple prompts and your responses simultaneously.</td>
</tr>
<tr class="odd">
<td>Upload large files</td>
<td>The ability to upload local or Cloud Storage files up to 20 MB.</td>
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
<td>In-App help tool</td>
<td>An in-app help tool accessible through the <code dir="ltr" translate="no">/ask</code> command or the prompt field.</td>
</tr>
<tr class="even">
<td>Prompt gallery</td>
<td>An updated prompt gallery with app samples.</td>
</tr>
</tbody>
</table>

### Built-in tools and capabilities

This section lists the built-in tools and capabilities within Agent Studio that automate a significant portion of the work for developers. Agent Studio integrates with Google Cloud, which provides an effortless experience that's collaborative and agentic.

| **Feature**                 | **Description**                                                                                                                                               |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Natural language refinement | For prompt refinement, you can describe how you want to change your prompt using natural language, and the system automatically optimizes the prompt for you. |
| Optimize system instruction | You can use a one-click feature that asks Gemini to automatically optimize a system instruction based on the prompt.                                          |
| Refine prompt response      | You can use the `/prompt` command to provide feedback and to create a well-formatted revised prompt.                                                          |
| Help-me-write tool          | You can use the `/prompt` command and a described intent to create a well-formatted prompt, system instruction, and to recommend a model.                     |

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
