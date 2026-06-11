---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/migrate-code
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/migrate-code
title: Migrate from OpenAI SDK to Google Gen AI SDK
description: Learn how to migrate your code from using the OpenAI SDK to using Google Gen AI SDKs for Gemini models in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page explains how to migrate code designed for the OpenAI SDK to the Google Gen AI SDK to utilize Gemini models on Gemini Enterprise Agent Platform.

> **Note:** If you prefer to continue using OpenAI libraries without rewriting your code, see [Using OpenAI libraries with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview) .

## Migration Overview

The following notebook demonstrates a practical migration from the `openai` library to the `google-genai` library:

> To see an example of migrating from OpenAI SDK to Google GenAI SDK, run the "Migrate OpenAI SDK code to Google GenAI SDK code" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/migration/migrate_from_openai_to_gemini.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fmigration%2Fmigrate_from_openai_to_gemini.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fmigration%2Fmigrate_from_openai_to_gemini.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/migration/migrate_from_openai_to_gemini.ipynb)

### API & Syntax Mapping

The following table compares the core components, methods, and parameters of the OpenAI SDK with the Google Gen AI SDK.

| Feature                   | OpenAI SDK ( `openai` )                           | Google Gen AI SDK ( `google-genai` )                         |
| :------------------------ | :------------------------------------------------ | :----------------------------------------------------------- |
| **Client Initialization** | `client = OpenAI(api_key=...)`                    | `client = genai.Client(vertexai=True, ...)`                  |
| **Generation Method**     | `client.chat.completions.create`                  | `client.models.generate_content`                             |
| **Streaming Method**      | `stream=True` (parameter)                         | `client.models.generate_content_stream` (method)             |
| **User Input**            | `messages=[{"role": "user", "content": "..."}]`   | `contents="..."` (str) or `contents=[...]` (list)            |
| **System Instructions**   | `messages=[{"role": "system", "content": "..."}]` | `config=types.GenerateContentConfig(system_instruction=...)` |
| **Response Access**       | `response.choices[0].message.content`             | `response.text`                                              |
| **Chat History**          | Manual list management ( `messages.append` )      | `client.chats.create()` (Stateful object)                    |
| **Max Tokens**            | `max_tokens`                                      | `max_output_tokens` (inside `config` )                       |
| **Temperature**           | `temperature`                                     | `temperature` (inside `config` )                             |
| **JSON Mode**             | `response_format={"type": "json_object"}`         | `response_mime_type="application/json"` (inside `config` )   |

### Installation and Setup

Uninstall the OpenAI library and install the Google Gen AI SDK.

    pip install google-genai

### 2\. Authentication & Initialization

While OpenAI uses an API Key, Agent Platform uses [Identity and Access Management (IAM) credentials (Application Default Credentials)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) . You must explicitly define your Project ID and Location.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>OpenAI SDK</th>
<th>Google Gen AI SDK</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>from openai import OpenAI
import os

# Relies on OPENAI_API_KEY environment variable
client = OpenAI()
        </code></pre></td>
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>from google import genai

# Use vertexai=True to use Agent Platform
client = genai.Client(
    vertexai=True,
    project=&#39;your-project-id&#39;,
    location=&#39;us-central1&#39;
)
        </code></pre></td>
</tr>
</tbody>
</table>

**Tip:** You can also set environment variables to initialize the client without arguments, similar to how the OpenAI client reads the API key from the environment.

Set `GOOGLE_GENAI_USE_ENTERPRISE` , `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` , as shown:

    export GOOGLE_GENAI_USE_ENTERPRISE=true
    export GOOGLE_CLOUD_PROJECT='your-project-id'
    export GOOGLE_CLOUD_LOCATION='global'

Once configured, you can initialize the client without passing parameters:

    from google import genai
    
    client = genai.Client()

### Code Examples

The following code samples show the differences between the OpenAI SDK and Google Gen AI SDK for common tasks.

#### Single-turn text generation

The following code samples show how to generate text. Note that in the Google Gen AI SDK, system instructions are handled as a configuration parameter rather than a message role in the input list.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>OpenAI SDK</th>
<th>Google Gen AI SDK</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>response = client.chat.completions.create(
    model=&quot;gpt-4&quot;,
    messages=[
        {&quot;role&quot;: &quot;system&quot;, &quot;content&quot;: &quot;You are a helpful assistant.&quot;},
        {&quot;role&quot;: &quot;user&quot;, &quot;content&quot;: &quot;Explain quantum physics.&quot;}
    ]
)
print(response.choices[0].message.content)
        </code></pre></td>
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>from google.genai import types

response = client.models.generate_content(
    model=&quot;gemini-2.5-flash&quot;,
    contents=&quot;Explain quantum physics.&quot;,
    config=types.GenerateContentConfig(
        system_instruction=&quot;You are a helpful assistant.&quot;
    )
)
print(response.text)
        </code></pre></td>
</tr>
</tbody>
</table>

#### Text generation with parameters

The following code samples show the differences in defining configuration parameters. In the Google Gen AI SDK, parameters like `temperature` , `max_output_tokens` (previously `max_tokens` ), and JSON formatting are grouped into a `GenerateContentConfig` object.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>OpenAI SDK</th>
<th>Google Gen AI SDK</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>response = client.chat.completions.create(
    model=&quot;gpt-4&quot;,
    messages=[
        {&quot;role&quot;: &quot;user&quot;, &quot;content&quot;: &quot;List 3 types of apples in JSON.&quot;}
    ],
    temperature=0.7,
    max_tokens=1000,
    response_format={&quot;type&quot;: &quot;json_object&quot;}
)

print(response.choices[0].message.content)
        </code></pre></td>
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>from google.genai import types

config = types.GenerateContentConfig(
    temperature=0.7,
    max_output_tokens=1000,
    response_mime_type=&quot;application/json&quot;
)

response = client.models.generate_content(
    model=&quot;gemini-2.5-flash&quot;,
    contents=&quot;List 3 types of apples in JSON.&quot;,
    config=config
)

print(response.text)
        </code></pre></td>
</tr>
</tbody>
</table>

#### Chat (Multi-turn)

The following code samples show the differences in managing chat history. Google Gen AI SDK simplifies this by providing a stateful `chat` object, whereas OpenAI requires manually appending messages to a list.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>OpenAI SDK</th>
<th>Google Gen AI SDK</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code># You must manually manage the list state
messages = [{&quot;role&quot;: &quot;user&quot;, &quot;content&quot;: &quot;Hi&quot;}]

response = client.chat.completions.create(
    model=&quot;gpt-4&quot;,
    messages=messages
)

# Append the response to history manually
messages.append(response.choices[0].message)
messages.append({&quot;role&quot;: &quot;user&quot;, &quot;content&quot;: &quot;Next question&quot;})

response2 = client.chat.completions.create(
    model=&quot;gpt-4&quot;,
    messages=messages
)
print(response2.choices[0].message.content)
        </code></pre></td>
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code># The SDK manages history for you
chat = client.chats.create(
    model=&quot;gemini-2.5-flash&quot;,
    config=types.GenerateContentConfig(
        system_instruction=&quot;You are a helpful assistant.&quot;
    )
)

response1 = chat.send_message(&quot;Hi&quot;)
print(response1.text)

# History is retained automatically in the chat object
response2 = chat.send_message(&quot;Next question&quot;)
print(response2.text)
        </code></pre></td>
</tr>
</tbody>
</table>

#### Streaming

The following code samples show the differences in streaming responses. Google Gen AI SDK uses a specific method ( `generate_content_stream` ) rather than a boolean flag.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>OpenAI SDK</th>
<th>Google Gen AI SDK</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>stream = client.chat.completions.create(
    model=&quot;gpt-4&quot;,
    messages=[{&quot;role&quot;: &quot;user&quot;, &quot;content&quot;: &quot;Write a story.&quot;}],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end=&quot;&quot;)
        </code></pre></td>
<td><code dir="ltr" translate="no"></code>
<pre dir="ltr" data-is-upgraded="" data-syntax="Python" translate="no"><code>stream = client.models.generate_content_stream(
    model=&quot;gemini-2.5-flash&quot;,
    contents=&quot;Write a story.&quot;
)

for chunk in stream:
    print(chunk.text, end=&quot;&quot;)
        </code></pre></td>
</tr>
</tbody>
</table>

## What's next

  - Learn how to [Use OpenAI libraries with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview) .
  - See code examples for [OpenAI compatibility](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/openai) .
  - Get started with [Google Gen AI SDK quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/quickstart-multimodal) .
