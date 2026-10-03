---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview
title: Using OpenAI libraries with Gemini Enterprise Agent Platform
description: Learn how to use OpenAI libraries with Gemini Enterprise Agent Platform through the Chat Completions API.
data_source: docs.cloud.google.com
---

> To see an example of using the Chat Completions API, run the "Call Gemini with the OpenAI Library" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/chat-completions/intro_chat_completions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fchat-completions%2Fintro_chat_completions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fchat-completions%2Fintro_chat_completions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/chat-completions/intro_chat_completions_api.ipynb)

The Chat Completions API works as an Open AI-compatible endpoint, designed to make it easier to interface with Gemini on Gemini Enterprise Agent Platform by using the OpenAI libraries for Python and REST. If you're already using the OpenAI libraries, you can use this API as a low-cost way to switch between calling OpenAI models and Agent Platform hosted models to compare output, cost, and scalability, without changing your existing code. If you aren't already using the OpenAI libraries, we recommend that you [use the Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) . To migrate your existing OpenAI SDK code to use the Google Gen AI SDK, see [Migrate from OpenAI SDK to Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/migrate-code) .

## Supported models

The Chat Completions API supports both Gemini models and select self-deployed models from Model Garden.

### Gemini models

The following models provide support for the Chat Completions API:

#### Click to expand supported models

- [Gemini 3.8 Flash Cyber](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-cyber)
- [Gemini 3.8 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash)
- [Gemini 3.7 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash)
- [Gemini 3.6 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash)
- [Gemini 3.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite)
- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro) preview
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 3 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash) preview
- [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

### Self-deployed models from Model Garden

The [Hugging Face Text Generation Interface (HF TGI)](https://huggingface.co/docs/text-generation-inference/en/index) and [Agent Platform Model Garden prebuilt vLLM](http://us-docker.pkg.dev/vertex-ai/vertex-vision-model-garden-dockers/pytorch-vllm-serve) containers support the Chat Completions API. However, not every model deployed to these containers supports the Chat Completions API. The following table includes the most popular supported models by container:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>HF TGI</p></th>
<th><p>vLLM</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><a href="https://huggingface.co/google/gemma-2-9b-it"><code>gemma-2-9b-it</code></a></li>
<li><a href="https://huggingface.co/google/gemma-2-27b-it"><code>gemma-2-27b-it</code></a></li>
<li><a href="https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct"><code>Meta-Llama-3.1-8B-Instruct</code></a></li>
<li><a href="https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct"><code>Meta-Llama-3-8B-Instruct</code></a></li>
<li><a href="https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.3"><code>Mistral-7B-Instruct-v0.3</code></a></li>
<li><a href="https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407"><code>Mistral-Nemo-Instruct-2407</code></a></li>
</ul></td>
<td><ul>
<li><a href="https://console.cloud.google.com/agent-platform/publishers/google/model-garden/335">Gemma</a></li>
<li><a href="https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama2">Llama 2</a></li>
<li><a href="https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama3">Llama 3</a></li>
<li><a href="https://console.cloud.google.com/agent-platform/publishers/mistral-ai/model-garden/mistral-7b">Mistral-7B</a></li>
<li><a href="https://console.cloud.google.com/agent-platform/publishers/mistralai/model-garden/mistral-nemo">Mistral Nemo</a></li>
</ul></td>
</tr>
</tbody>
</table>

## Supported parameters

For Google models, the Chat Completions API supports the following OpenAI parameters. For a description of each parameter, see OpenAI's documentation on [Creating chat completions](https://platform.openai.com/docs/api-reference/chat/create) . Parameter support for third-party models varies by model. To see which parameters are supported, consult the model's documentation.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>messages</code></td>
<td><ul>
<li><code>System message</code></li>
<li><code>User message</code> : The <code>text</code> and <code>image_url</code> types are supported. The <code>image_url</code> type supports images stored in a Cloud Storage URI or a base64 encoding in the form <code>"data:&lt;MIME-TYPE&gt;;base64,&lt;BASE64-ENCODED-BYTES&gt;"</code> . To learn how to create a Cloud Storage bucket and upload a file to it, see <a href="https://docs.cloud.google.com/storage/docs/discover-object-storage-console">Discover object storage</a> .</li>
<li><code>Assistant message</code></li>
<li><code>Tool message</code></li>
<li><code>Function message</code> : This field is deprecated, but supported for backwards compatibility.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>model</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>detail</code></td>
<td>For models older than Gemini 3, the <code>detail</code> field must be consistent across all messages and contents (it is request-level). For Gemini 3 and onwards, this corresponds to a part-level `media_resolution`. For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerationConfig#MediaResolution">Media Resolution</a> .</td>
</tr>
<tr class="even">
<td><code>max_completion_tokens</code></td>
<td>Alias for <code>max_tokens</code> .</td>
</tr>
<tr class="odd">
<td><code>modalities</code></td>
<td>Supports <code>audio</code> , <code>image</code> , and <code>text</code> .</td>
</tr>
<tr class="even">
<td><code>max_tokens</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>n</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>frequency_penalty</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>presence_penalty</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>reasoning_effort</code></td>
<td>Configures how much time and how many tokens are used on a response.
<ul>
<li><code>low</code> : 1024</li>
<li><code>medium</code> : 8192</li>
<li><code>high</code> : 24576</li>
</ul>
As no thoughts are included in the response, only one of <code>reasoning_effort</code> or <code>extra_body.google.thinking_config</code> may be specified.</td>
</tr>
<tr class="odd">
<td><code>response_format</code></td>
<td><ul>
<li><code>json_object</code> : Interpreted as passing "application/json" to the Gemini API.</li>
<li><code>json_schema</code> . <a href="https://platform.openai.com/docs/guides/structured-outputs#recursive-schemas-are-supported">Fully recursive schemas</a> are not supported. <code>additional_properties</code> is supported.</li>
<li><code>text</code> : Interpreted as passing "text/plain" to the Gemini API.</li>
<li>Any other MIME type is passed as is to the model, such as passing "application/json" directly.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>seed</code></td>
<td>Corresponds to <code>GenerationConfig.seed</code> .</td>
</tr>
<tr class="odd">
<td><code>stop</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>stream</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>temperature</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>top_p</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>tools</code></td>
<td><ul>
<li><code>type</code></li>
<li><code>function</code>
<ul>
<li><code>name</code></li>
<li><code>description</code></li>
<li><code>parameters</code> : Specify parameters by using the <a href="https://spec.openapis.org/oas/v3.0.3#openapi-specification">OpenAPI specification</a> . This differs from the OpenAI parameters field, which is described as a JSON Schema object. To learn about keyword differences between OpenAPI and JSON Schema, see the <a href="https://swagger.io/docs/specification/data-models/keywords/">OpenAPI guide</a> .</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><code>tool_choice</code></td>
<td><ul>
<li><code>none</code></li>
<li><code>auto</code></li>
<li><code>required</code> : Corresponds to the mode <code>ANY</code> in the <code>FunctionCallingConfig</code> .</li>
<li><code>validated</code> : Corresponds to the mode <code>VALIDATED</code> in the <code>FunctionCallingConfig</code> . This is Google-specific.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>web_search_options</code></td>
<td>Corresponds to the <code>GoogleSearch</code> tool. No sub-options are supported.</td>
</tr>
<tr class="even">
<td><code>function_call</code></td>
<td>This field is deprecated, but supported for backwards compatibility.</td>
</tr>
<tr class="odd">
<td><code>functions</code></td>
<td>This field is deprecated, but supported for backwards compatibility.</td>
</tr>
</tbody>
</table>

If you pass any unsupported parameter, it is ignored.

### Multimodal input parameters

The Chat Completions API supports select multimodal inputs.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><code>input_audio</code></td>
<td><ul>
<li><code>data:</code> Any URI or valid blob format. We support all blob types, including image, audio, and video. Anything supported by <code>GenerateContent</code> is supported (HTTP, Cloud Storage, etc.).</li>
<li><code>format:</code> OpenAI supports both <code>wav</code> (audio/wav) and <code>mp3</code> (audio/mp3). Using Gemini, all valid MIME types are supported.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>image_url</code></td>
<td><ul>
<li><code>data:</code> Like <code>input_audio</code> , any URI or valid blob format is supported.<br />
Note that <code>image_url</code> as a URL will default to the image/* MIME-type and <code>image_url</code> as blob data can be used as any multimodal input.</li>
<li><code>detail:</code> Similar to <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-understanding#supported_models">media resolution</a> , this determines the maximum tokens per image for the request. Note that while OpenAI's field is per-image, Gemini enforces the same detail across the request, and passing multiple detail types in one request will throw an error.</li>
</ul></td>
</tr>
</tbody>
</table>

In general, the `data` parameter can be a URI or a combination of MIME type and base64 encoded bytes in the form `"data:<MIME-TYPE>;base64,<BASE64-ENCODED-BYTES>"` . For a full list of MIME types, see [`GenerateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/generateContent) . For more information on OpenAI's base64 encoding, see [their documentation](https://platform.openai.com/docs/guides/images-vision#giving-a-model-images-as-input) .

For usage, see our [multimodal input examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/examples#multimodal-requests) .

### Gemini-specific parameters

There are several features supported by Gemini that are not available in OpenAI models. These features can still be passed in as parameters, but must be contained within an `extra_content` or `extra_body` or they will be ignored.

### `extra_body` features

Include a `google` field to contain any Gemini-specific `extra_body` features.

```
{
  ...,
  "extra_body": {
     "google": {
       ...,
       // Add extra_body features here.
     }
   }
}
```

|                                  |                                                                                                                                                                                                                                                                                                                                                    |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `safety_settings`                | This corresponds to the Gemini [`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SafetySetting) .                                                                                                                                                                                                 |
| `cached_content`                 | This corresponds to the Gemini [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.models/generateContent)` .cached_content` field.                                                                                                                                 |
| `thinking_config`                | This corresponds to the Gemini [`GenerationConfig.ThinkingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerationConfig#ThinkingConfig) .                                                                                                                                                             |
| `thought_tag_marker`             | Used to separate a model's thoughts from its responses for models with Thinking available. If not specified, no tags will be returned around the model's thoughts. If present, subsequent queries will strip the thought tags and mark the thoughts appropriately for context. This helps preserve the appropriate context for subsequent queries. |
| `stream_function_call_arguments` | Streams function call arguments back as segments of JSON. For more information, see [Streaming function call arguments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling#streaming-fc) .                                                                                                               |
| `tools`                          | Specify tools similar to \`GenerateContent\`. For more information, see [`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#Tool) .                                                                                                                                                  |
| `media_resolution`               | Specify a request-level media resolution similar to \`GenerateContent\`. For more information, see [`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerationConfig#MediaResolution) .                                                                                                        |

### `extra_content` features

`extra_content` lets you specify Gemini-specific content that shouldn't be ignored.

Include a `google` field to contain any Gemini-specific `extra_content` features.

```
{
  ...,
  "extra_content": {
     "google": {
       ...,
       // Add extra_content features here.
     }
   }
}
```

|                     |                                                                                                                                                                                                                                                                                                                                                                                                                           |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `thought`           | This field explicitly marks if a field is a thought and takes precedence over `thought_tag_marker` . It helps distinguish between different steps in a thought process, especially in tool use scenarios where intermediate steps might be mistaken for final answers. By tagging specific parts of the input as thoughts, you can guide the model to treat them as internal reasoning rather than user-facing responses. |
| `thought_signature` | A bytes field that provides a thought signature to validate against thoughts returned by the model. This field is distinct from `thought` , which is a boolean field. For more information, see [Thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/thought-signatures) .                                                                                                 |
| `parts`             | Specific to a Tool message to pass multi-modal function response parts back to the model. For more information, see [`FunctionResponsePart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#FunctionResponsePart) and [Multimodal function response](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling#mm-fr) .                      |

## What's next

- Learn more about [authentication and credentialing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) with the OpenAI-compatible syntax.
- See examples of calling the [Chat Completions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/examples) with the OpenAI-compatible syntax.
- See examples of calling the [Inference API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/generateContent) with the OpenAI-compatible syntax.
- See examples of calling the [Function Calling API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling#examples) with OpenAI-compatible syntax.
- Learn more about the [Gemini API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models) .
- Learn more about [migrating to the latest Gemini models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate) .
- To migrate your existing OpenAI SDK code to use the Google Gen AI SDK, see [Migrate from OpenAI SDK to Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/migrate-code) .
