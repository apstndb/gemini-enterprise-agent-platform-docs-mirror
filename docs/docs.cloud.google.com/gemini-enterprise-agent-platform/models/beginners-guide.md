---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/beginners-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/beginners-guide
title: Generative AI beginner&#39;s guide
description: Learn about generative AI workflows in Agent Platform, available models (including Gemini), and how to start building your generative AI app.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=cZaNf2rA30k)

This beginner's guide introduces you to the core technologies of generative AI and explains how they fit together to power chatbots and applications. Generative AI (also known as *genAI* or *gen AI* ) is a field of machine learning (ML) that develops and uses ML models for generating new content.

Generative AI models are often called large language models (LLMs) because of their large size and ability to understand and generate natural language. However, depending on the data that the models are trained on, these models can understand and generate content from multiple modalities, including text, images, videos, and audio. Models that work with multiple modalities of data are called *multimodal* models.

Google provides the [Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models) family of generative AI models designed for *multimodal* use cases; capable of processing information from multiple modalities, including images, videos, and text.

## Content generation

In order for generative AI models to generate content that's useful in real-world applications, they need to have the following capabilities:

  - **Learn how to perform new tasks:**
    
    Generative AI models are designed to perform general tasks. If you want a model to perform tasks that are unique to your use case, then you need to be able to customize the model. On Gemini Enterprise Agent Platform, you can customize your model through model tuning.

  - **Access external information:**
    
    Generative AI models are trained on vast amounts of data. However, in order for these models to be useful, they need to be able to access information outside of their training data. For example, if you want to create a customer service chatbot that's powered by a generative AI model, the model needs to have access to information about the products and services that you offer. In Gemini Enterprise Agent Platform, you use the grounding and function calling features to help the model access external information.

  - **Block harmful content:**
    
    Generative AI models might generate output that you don't expect, including text that's offensive or insensitive. To maintain safety and prevent misuse, the models need safety filters to block prompts and responses that are determined to be potentially harmful. Gemini Enterprise Agent Platform has built-in safety features that promote the responsible use of our generative AI services.

### Prompt

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/prompt.svg" alt="Prompt" /></td>
<td><p>The generative AI workflow typically starts with prompting. A prompt is a natural language request sent to a generative AI model to elicit a response back. Depending on the model, a prompt can contain <em>text</em> , <em>images</em> , <em>videos</em> , <em>audio</em> , <em>documents</em> , and other modalities or even multiple modalities (multimodal).</p>
<p>Creating a prompt to get the desired response from the model is a practice called <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/introduction-prompt-design">prompt design</a> . While prompt design is a process of trial and error, there are prompt design principles and strategies that you can use to nudge the model to behave in the desired way. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/quickstart">Agent Studio</a> offers a prompt management tool to help you manage your prompts.</p></td>
</tr>
</tbody>
</table>

### Foundation models

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/model.svg" alt="Foundation models" /></td>
<td><p>Prompts are sent to a generative AI model for response generation. Gemini Enterprise Agent Platform has a variety of <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models">generative AI foundation models</a> that are accessible through a managed API, including the following:</p>
<ul>
<li><strong>Gemini API:</strong> Advanced reasoning, multiturn chat, code generation, and multimodal prompts.</li>
</ul>
<p>The models differ in size, modality, and cost. You can explore Google models, as well as open models and models from Google partners, in <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models">Model Garden</a> .</p></td>
</tr>
</tbody>
</table>

### Model customization

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/tune.svg" alt="Model customization" /></td>
<td><p>You can customize the default behavior of Google's foundation models so that they consistently generate the desired results without using complex prompts. This customization process is called <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">model tuning</a> . Model tuning helps you reduce the cost and latency of your requests by allowing you to simplify your prompts.</p>
<p>Gemini Enterprise Agent Platform also offers <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/evaluation-overview">model evaluation tools</a> to help you evaluate the performance of your tuned model. After your tuned model is production-ready, you can <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/overview">deploy it to an endpoint</a> and monitor performance like in standard MLOps workflows.</p></td>
</tr>
</tbody>
</table>

### Access external information

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/ground.svg" alt="Augmentation" /></td>
<td><p>Gemini Enterprise Agent Platform offers multiple ways to give the model access to external APIs and real-time information.</p>
<ul>
<li><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a> :</strong> Connects model responses to a source of truth, such as your own data or web search, helping to reduce hallucinations.</li>
<li><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG</a> :</strong> Connects models to external knowledge sources, such as documents and databases, to generate more accurate and informative responses.</li>
<li><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a> :</strong> Lets the model interact with external APIs to get real-time information and perform real-world tasks.</li>
</ul></td>
</tr>
</tbody>
</table>

### Citation check

|                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Citation check](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/cite.svg) | After the response is generated, Gemini Enterprise Agent Platform checks whether [citations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/configure-safety-filters#citation-filter) need to be included with the response. If a significant amount of the text in the response comes from a particular source, that source is added to the citation metadata in the response. |

### Responsible AI and safety

|                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Responsible AI and safety](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/safe.svg) | The last layer of checks that the prompt and response go through before being returned is the [safety filters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/configure-safety-filters#configurable-filters) . Gemini Enterprise Agent Platform checks both the prompt and response for how much the prompt or response belongs to a [safety category](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/configure-safety-filters#harm-categories) . If the threshold is exceeded for one or more categories, the response is blocked and Gemini Enterprise Agent Platform returns a [fallback response](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/process-blocked-responses#when-blocked) . |

### Response

|                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Response](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/icons/spark.svg) | If the prompt and response passes the safety filter checks, the response is returned. Typically, the response is returned all at once. However, with Agent Platform you can also receive responses progressively as it generates by enabling [streaming](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/send-chat-prompts-gemini#streaming-and-non-streaming-responses) . |

## Get started

Try one of these quickstarts to get started with generative AI on Agent Platform:

  - **[Generate text using the Agent Platform Gemini API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) :** Use the SDK to send requests to the Gemini API
  - **[Generate an image by using Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image) :** Generate images from a text prompt
