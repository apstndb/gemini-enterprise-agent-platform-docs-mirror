---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference
title: Generate content with the Gemini API
description: Use the Model API for Gemini in Gemini Enterprise Agent Platform to create custom applications. Review the Gemini model request body, model parameters, response body, and sample requests and responses.
data_source: docs.cloud.google.com
---

Use `generateContent` or `streamGenerateContent` to generate content with Gemini.

The Gemini model family includes models that work with multimodal prompt requests. The term multimodal indicates that you can use more than one modality, or type of input, in a prompt. Models that aren't multimodal accept prompts only with text. Modalities can include text, audio, video, and more.

## Get started

To get started generating content with Gemini, do the following:

1.  [Create a Google Cloud account](https://console.cloud.google.com/freetrial?redirectPath=/marketplace/product/google/cloudaicompanion.googleapis.com) .

2.  Review this document to learn about the Gemini model [request body](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#request) , [parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#parameters) , and [response body](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#response) . To see some sample requests, see [Examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#sample-requests) .

3.  To learn how to send a request to the Gemini API by using a programming language SDK or the REST API, see the [Gemini API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) .

## Supported models

All Gemini models support content generation.

> **Note:** Adding a lot of images to a request increases response latency.

## Parameter list

See [examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#sample-requests) for implementation details.

### Request body

```
{
  "cachedContent": string,
  "contents": [
    {
      "role": string,
      "parts": [
        {
          // Union field data can be only one of the following:
          "text": string,
          "inlineData": {
            "mimeType": string,
            "data": string
          },
          "fileData": {
            "mimeType": string,
            "fileUri": string
          },
          // End of list of possible types for union field data.

          "thought": boolean,
          "thoughtSignature": string,
          "videoMetadata": {
            "startOffset": {
              "seconds": integer,
              "nanos": integer
            },
            "endOffset": {
              "seconds": integer,
              "nanos": integer
            },
            "fps": double
          },
          "mediaProcessing": string,
          "mediaResolution": MediaResolution
        }
      ]
    }
  ],
  "systemInstruction": {
    "role": string,
    "parts": [
      {
        "text": string
      }
    ]
  },
  "tools": [
    {
      "functionDeclarations": [
        {
          "name": string,
          "description": string,
          "parameters": {
            object (OpenAPI Object Schema)
          }
        }
      ]
    }
  ],
  "safetySettings": [
    {
      "category": enum (HarmCategory),
      "threshold": enum (HarmBlockThreshold)
    }
  ],
  "generationConfig": {
    "temperature": number,
    "topP": number,
    "topK": number,
    "candidateCount": integer,
    "maxOutputTokens": integer,
    "presencePenalty": float,
    "frequencyPenalty": float,
    "stopSequences": [
      string
    ],
    "responseMimeType": string,
    "responseSchema": schema,
    "seed": integer,
    "responseLogprobs": boolean,
    "logprobs": integer,
    "audioTimestamp": boolean,
    "thinkingConfig": {
      "thinkingBudget": integer,
      "thinkingLevel": enum
    },
    "mediaProcessing": string,
    "mediaResolution": MediaResolution
  },
  "labels": {
    string: string
  }
}
```

The request body contains data with the following parameters:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>cachedContent</code></p></td>
<td><p>Optional: <code>string</code></p>
<p>The name of the cached content used as context to serve the prediction. Format: <code>projects/{project}/locations/{location}/cachedContents/{cachedContent}</code></p></td>
</tr>
<tr class="even">
<td><p><code>contents</code></p></td>
<td><p>Required: <code>Content</code></p>
<p>The content of the current conversation with the model.</p>
<p>For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history and the latest request.</p></td>
</tr>
<tr class="odd">
<td><p><code>systemInstruction</code></p></td>
<td><p>Optional: <code>Content</code></p>
<p>Instructions for the model to steer it toward better performance. For example, "Answer as concisely as possible" or "Don't use technical terms in your response".</p>
<p>The <code>text</code> strings count toward the token limit.</p>
<p>The <code>role</code> field of <code>systemInstruction</code> is ignored and doesn't affect the performance of the model.</p>
<blockquote>
<strong>Note:</strong> Only <code>text</code> should be used in <code>parts</code> and content in each <code>part</code> should be in a separate paragraph.
</blockquote></td>
</tr>
<tr class="even">
<td><p><code>tools</code></p></td>
<td><p>Optional. A piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model. See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling">Function calling</a> .</p></td>
</tr>
<tr class="odd">
<td><p><code>toolConfig</code></p></td>
<td><p>Optional. See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling">Function calling</a> .</p></td>
</tr>
<tr class="even">
<td><p><code>safetySettings</code></p></td>
<td><p>Optional: <code>SafetySetting</code></p>
<p>Per request settings for blocking unsafe content.</p>
<p>Enforced on <code>GenerateContentResponse.candidates</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code>generationConfig</code></p></td>
<td><p>Optional: <code>GenerationConfig</code></p>
<p>Generation configuration settings.</p></td>
</tr>
<tr class="even">
<td><p><code>labels</code></p></td>
<td><p>Optional: <code>string</code></p>
<p>Metadata that you can add to the API call in the format of key-value pairs.</p></td>
</tr>
</tbody>
</table>

#### `contents`

The base structured data type containing multi-part content of a message.

This class consists of two main properties: `role` and `parts` . The `role` property denotes the individual producing the content, while the `parts` property contains multiple elements, each representing a segment of data within a message.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>role</code></p></td>
<td><p><code>string</code></p>
<p>The identity of the entity that creates the message. The following values are supported:</p>
<ul>
<li><code>user</code> : This indicates that the message is sent by a real person, typically a user-generated message.</li>
<li><code>model</code> : This indicates that the message is generated by the model.</li>
</ul>
<p>The <code>model</code> value is used to insert messages from the model into the conversation during multi-turn conversations.</p></td>
</tr>
<tr class="even">
<td><p><code>parts</code></p></td>
<td><p><code>Part</code></p>
<p>A list of ordered parts that make up a single message. Different parts may have different <a href="https://www.iana.org/assignments/media-types/media-types.xml">IANA MIME types</a> .</p>
<p>For limits on the inputs, such as the maximum number of tokens or the number of images, see the model specifications on the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models">Google models</a> page.</p>
<p>To compute the number of tokens in your request, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Get token count</a> .</p></td>
</tr>
</tbody>
</table>

#### `parts`

A data type containing media that is part of a multi-part `Content` message.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>text</code></p></td>
<td><p>Optional: <code>string</code></p>
<p>A text prompt or code snippet.</p></td>
</tr>
<tr class="even">
<td><p><code>inlineData</code></p></td>
<td><p>Optional: <code>Blob</code></p>
<p>Inline data in raw bytes.</p></td>
</tr>
<tr class="odd">
<td><p><code>fileData</code></p></td>
<td><p>Optional: <code>fileData</code></p>
<p>Data stored in a file.</p></td>
</tr>
<tr class="even">
<td><p><code>functionCall</code></p></td>
<td><p>Optional: <code>FunctionCall</code> .</p>
<p>It contains a string representing the <code>FunctionDeclaration.name</code> field and a structured JSON object containing any parameters for the function call predicted by the model.</p>
<p>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling">Function calling</a> .</p></td>
</tr>
<tr class="odd">
<td><p><code>functionResponse</code></p></td>
<td><p>Optional: <code>FunctionResponse</code> .</p>
<p>The result output of a <code>FunctionCall</code> that contains a string representing the <code>FunctionDeclaration.name</code> field and a structured JSON object containing any output from the function call. It is used as context to the model.</p>
<p>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling">Function calling</a> .</p></td>
</tr>
<tr class="even">
<td><p><code>thought</code></p></td>
<td><p>Optional: <code>boolean</code></p>
<p>Indicates whether the part represents the model's thought process or reasoning.</p></td>
</tr>
<tr class="odd">
<td><p><code>thoughtSignature</code></p></td>
<td><p>Optional: <code>string (bytes format)</code></p>
<p>An opaque signature for the thought so it can be reused in subsequent requests. A base64-encoded string.</p></td>
</tr>
<tr class="even">
<td><p><code>videoMetadata</code></p></td>
<td><p>Optional: <code>VideoMetadata</code></p>
<p>For video input, the start and end offset of the video in <a href="https://protobuf.dev/reference/protobuf/google.protobuf/#duration">Duration</a> format, and the frame rate of the video . For example, to specify a 10 second clip starting at 1:00 with a frame rate of 10 frames per second, set the following:</p>
<ul>
<li><code>"startOffset": { "seconds": 60 }</code></li>
<li><code>"endOffset": { "seconds": 70 }</code></li>
<li><code>"fps": 10.0</code></li>
</ul>
<p>The metadata should only be specified while the video data is presented in <code>inlineData</code> or <code>fileData</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code>mediaProcessing</code></p></td>
<td><p>Optional: <code>string</code></p>
<p>How the model processes this media part. When set to <code>AGENTIC</code> , uses model-driven dynamic video navigation. When set to <code>STATIC</code> , uses fixed-rate frame extraction.</p>
<p>Only supported for 3.5 and higher versioned Gemini models. If set for a request using an unsupported model, falls back to <code>STATIC</code> .</p>
<p>Supported values: <code>AGENTIC</code> , <code>STATIC</code> .</p></td>
</tr>
<tr class="even">
<td><p><code>mediaResolution</code></p></td>
<td><p>Optional: <code>MediaResolution</code></p>
<p>Per-part media resolution for the input media. Controls how input media is processed. If specified, this overrides the <code>mediaResolution</code> setting in <code>generationConfig</code> . <code>LOW</code> reduces tokens per image/video, possibly losing detail but allowing longer videos in context. Supported values: <code>HIGH</code> , <code>MEDIUM</code> , <code>LOW</code> .</p></td>
</tr>
</tbody>
</table>

#### `blob`

Content blob. If possible send as text rather than raw bytes.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>mimeType</code></p></td>
<td><p><code>string</code></p>
The media type of the file specified in the <code>data</code> or <code>fileUri</code> fields. Acceptable values include the following:
<p><strong>Click to expand MIME types</strong></p>
<ul>
<li><code>application/pdf</code></li>
<li><code>audio/mpeg</code></li>
<li><code>audio/mp3</code></li>
<li><code>audio/wav</code></li>
<li><code>image/png</code></li>
<li><code>image/jpeg</code></li>
<li><code>image/webp</code></li>
<li><code>text/plain</code></li>
<li><code>video/mov</code></li>
<li><code>video/mpeg</code></li>
<li><code>video/mp4</code></li>
<li><code>video/mpg</code></li>
<li><code>video/avi</code></li>
<li><code>video/wmv</code></li>
<li><code>video/mpegps</code></li>
<li><code>video/flv</code></li>
</ul>
<p>For more information, see Gemini <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/audio-understanding#audio-requirements">audio</a> and <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#video-requirements">video</a> requirements.</p>
<p>Text files must be UTF-8 encoded. The contents of the text file count toward the token limit.</p>
<p>There is no limit on image resolution.</p></td>
</tr>
<tr class="even">
<td><p><code>data</code></p></td>
<td><p><code>bytes</code></p>
<p>The <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/tutorials/base64-encode">base64 encoding</a> of the image, PDF, or video to include inline in the prompt. When including media inline, you must also specify the media type ( <code>mimeType</code> ) of the data.</p>
<p>Size limit: 7 MB for images</p></td>
</tr>
</tbody>
</table>

#### FileData

URI or web-URL data.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>mimeType</code></p></td>
<td><p><code>string</code></p>
<p><a href="https://www.iana.org/assignments/media-types/media-types.xml">IANA MIME type</a> of the data.</p></td>
</tr>
<tr class="even">
<td><p><code>fileUri</code></p></td>
<td><p><code>string</code></p>
<p>The URI or URL of the file to include in the prompt. Acceptable values include the following:</p>
<ul>
<li><strong>Cloud Storage bucket URI:</strong> The object must either be publicly readable or reside in the same Google Cloud project that's sending the request.</li>
<li><strong>HTTP URL:</strong> The file URL must be publicly readable. You can specify one video file, one audio file, and up to 10 image files per request. Audio files, video files, and documents can't exceed 15 MB.</li>
<li><strong>YouTube video URL:</strong> The YouTube video must be either owned by the account that you used to sign in to the Google Cloud console or be public. Only one YouTube video URL is supported per request.</li>
</ul>
<p>When specifying a <code>fileURI</code> , you must also specify the media type ( <code>mimeType</code> ) of the file. If VPC Service Controls is enabled, specifying a media file URL for <code>fileURI</code> is not supported.</p></td>
</tr>
</tbody>
</table>

#### `functionCall`

A predicted `functionCall` returned from the model that contains a string representing the `functionDeclaration.name` and a structured JSON object containing the parameters and their values.

| Parameters |                                                                                                                                                                                                                    |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` The name of the function to call.                                                                                                                                                                         |
| `args`     | `Struct` The function parameters and values in JSON object format. See [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling) for parameter details. |

#### `functionResponse`

The resulting output from a `FunctionCall` that contains a string representing the `FunctionDeclaration.name` . Also contains a structured JSON object with the output from the function (and uses it as context for the model). This should contain the result of a `FunctionCall` made based on model prediction.

| Parameters |                                                       |
|------------|-------------------------------------------------------|
| `name`     | `string` The name of the function to call.            |
| `response` | `Struct` The function response in JSON object format. |

#### `videoMetadata`

Metadata describing the input video content.

| Parameters    |                                                                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startOffset` | Optional: `google.protobuf.Duration` The start offset of the video.                                                                                                                                     |
| `endOffset`   | Optional: `google.protobuf.Duration` The end offset of the video.                                                                                                                                       |
| `fps`         | Optional: `double` The frame rate of the video sent to the model. Defaults to `1.0` if not specified. The minimum accepted value is as low as, but not including, `0.0` . The maximum value is `24.0` . |

#### `safetySetting`

Safety settings.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>category</code></p></td>
<td><p>Optional: <code>HarmCategory</code></p>
The safety category to configure a threshold for. Acceptable values include the following:
<p><strong>Click to expand safety categories</strong></p>
<ul>
<li><code>HARM_CATEGORY_SEXUALLY_EXPLICIT</code></li>
<li><code>HARM_CATEGORY_HATE_SPEECH</code></li>
<li><code>HARM_CATEGORY_HARASSMENT</code></li>
<li><code>HARM_CATEGORY_DANGEROUS_CONTENT</code></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>threshold</code></p></td>
<td><p>Optional: <code>HarmBlockThreshold</code></p>
<p>The threshold for blocking responses that could belong to the specified safety category based on probability.</p>
<ul>
<li><code>OFF</code></li>
<li><code>BLOCK_NONE</code></li>
<li><code>BLOCK_LOW_AND_ABOVE</code></li>
<li><code>BLOCK_MEDIUM_AND_ABOVE</code></li>
<li><code>BLOCK_ONLY_HIGH</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>method</code></p></td>
<td><p>Optional: <code>HarmBlockMethod</code></p>
<p>Specify if the threshold is used for probability or severity score. If not specified, the threshold is used for probability score.</p></td>
</tr>
</tbody>
</table>

#### `harmCategory`

Harm categories that block content.

| Parameters                        |                                                 |
|-----------------------------------|-------------------------------------------------|
| `HARM_CATEGORY_UNSPECIFIED`       | The harm category is unspecified.               |
| `HARM_CATEGORY_HATE_SPEECH`       | The harm category is hate speech.               |
| `HARM_CATEGORY_DANGEROUS_CONTENT` | The harm category is dangerous content.         |
| `HARM_CATEGORY_HARASSMENT`        | The harm category is harassment.                |
| `HARM_CATEGORY_SEXUALLY_EXPLICIT` | The harm category is sexually explicit content. |

#### `harmBlockThreshold`

Probability thresholds levels used to block a response.

| Parameters                         |                                                      |
|------------------------------------|------------------------------------------------------|
| `HARM_BLOCK_THRESHOLD_UNSPECIFIED` | Unspecified harm block threshold.                    |
| `BLOCK_LOW_AND_ABOVE`              | Block low threshold and higher (i.e. block more).    |
| `BLOCK_MEDIUM_AND_ABOVE`           | Block medium threshold and higher.                   |
| `BLOCK_ONLY_HIGH`                  | Block only high threshold (i.e. block less).         |
| `BLOCK_NONE`                       | Block none.                                          |
| `OFF`                              | Switches off safety if all categories are turned OFF |

#### `harmBlockMethod`

A probability threshold that blocks a response based on a combination of probability and severity.

| Parameters                      |                                                                  |
|---------------------------------|------------------------------------------------------------------|
| `HARM_BLOCK_METHOD_UNSPECIFIED` | The harm block method is unspecified.                            |
| `SEVERITY`                      | The harm block method uses both probability and severity scores. |
| `PROBABILITY`                   | The harm block method uses the probability score.                |

#### `generationConfig`

Configuration settings used when generating the prompt.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>temperature</code></p></td>
<td><p>Optional: <code>float</code></p>
<p>The range of values and default value is specific for each model. See the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#temperature-ranges">temperature ranges and default values list</a> .</p>
<p>The temperature is used for sampling during response generation, which occurs when <code>topP</code> and <code>topK</code> are applied. Temperature controls the degree of randomness in token selection. Lower temperatures are good for prompts that require a less open-ended or creative response, while higher temperatures can lead to more diverse or creative results. A temperature of <code>0</code> means that the highest probability tokens are always selected. In this case, responses for a given prompt are mostly deterministic, but a small amount of variation is still possible.</p>
<p>If the model returns a response that's too generic, too short, or the model gives a fallback response, try increasing the temperature. If the model enters infinite generation, increasing the temperature to at least <code>0.1</code> may lead to improved results.</p>
<code>1.0</code> is the recommended starting value for temperature.
<ul>
<li>Range for Gemini 3 models versions 3.5 Flash and lower: <code>0.0 - 2.0</code> (default: <code>1.0</code> )</li>
</ul>
<blockquote>
<strong>Warning:</strong> For Gemini 3.6 Flash and later models, custom values for sampling parameters ( <code>temperature</code> , <code>topP</code> , and <code>topK</code> ) aren't supported and are ignored if set, and custom values for penalization parameters ( <code>frequencyPenalty</code> and <code>presencePenalty</code> ) return an error. Remove these parameters from your requests.
</blockquote>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#temperature">Content generation parameters</a> .</p></td>
</tr>
<tr class="even">
<td><p><code>topP</code></p></td>
<td><p>Optional: <code>float</code></p>
<p>If specified, nucleus sampling is used.</p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#top-p">Top-P</a> changes how the model selects tokens for output. Tokens are selected from the most (see top-K) to least probable until the sum of their probabilities equals the top-P value. For example, if tokens A, B, and C have a probability of 0.3, 0.2, and 0.1 and the top-P value is <code>0.5</code> , then the model will select either A or B as the next token by using temperature and excludes C as a candidate.</p>
<p>Specify a lower value for less random responses and a higher value for more random responses.</p>
<ul>
<li>Range: <code>0.0 - 1.0</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>topK</code></p></td>
<td><p>Optional: <code>float</code></p>
<p>Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a `topK` of 40 means the model will choose the next word from the 40 most likely words.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#top-k">Content generation parameters</a> .</p></td>
</tr>
<tr class="even">
<td><p><code>candidateCount</code></p></td>
<td><p>Optional: <code>int</code></p>
<p>The number of response variations to return. For each request, you're charged for the output tokens of all candidates, but are only charged once for the input tokens.</p>
<p>Specifying multiple candidates is a Preview feature that works with <code>generateContent</code> ( <code>streamGenerateContent</code> is not supported).</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#candidate-count">Content generation parameters</a> .</p></td>
</tr>
<tr class="odd">
<td><p><code>maxOutputTokens</code></p></td>
<td><p>Optional: int</p>
<p>Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.</p>
<p>Specify a lower value for shorter responses and a higher value for potentially longer responses.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#max-output-tokens">Content generation parameters</a> .</p></td>
</tr>
<tr class="even">
<td><p><code>stopSequences</code></p></td>
<td><p>Optional: <code>List[string]</code></p>
<p>Specifies a list of strings that tells the model to stop generating text if one of the strings is encountered in the response. If a string appears multiple times in the response, then the response is truncated where it's first encountered. The strings are case-sensitive.<br />
<br />
For example, if the following is the returned response when <code>stopSequences</code> isn't specified:<br />
<br />
<code>public static string reverse(string myString)</code><br />
<br />
Then the returned response with <code>stopSequences</code> set to <code>["Str", "reverse"]</code> is:<br />
<br />
<code>public static string</code></p>
<p>Maximum 5 items in the list.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#stop-sequences">Content generation parameters</a> .</p></td>
</tr>
<tr class="odd">
<td><p><code>presencePenalty</code></p></td>
<td><p>Optional: <code>float</code></p>
<p>Positive penalties.</p>
<p>Positive values penalize tokens that already appear in the generated text, increasing the probability of generating more diverse content.</p>
<p>The maximum value for <code>presencePenalty</code> is up to, but not including, <code>2.0</code> . Its minimum value is <code>-2.0</code> .</p></td>
</tr>
<tr class="even">
<td><p><code>frequencyPenalty</code></p></td>
<td><p>Optional: <code>float</code></p>
<p>Positive values penalize tokens that repeatedly appear in the generated text, decreasing the probability of repeating content.</p>
<p>This maximum value for <code>frequencyPenalty</code> is up to, but not including, <code>2.0</code> . Its minimum value is <code>-2.0</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code>responseMimeType</code></p></td>
<td><p>Optional: <code>string (enum)</code></p>
<p>The output response MIME type of the generated candidate text.</p>
<p>The following MIME types are supported:</p>
<ul>
<li><code>application/json</code> : JSON response in the candidates.</li>
<li><code>text/plain</code> (default): Plain text output.</li>
<li><code>text/x.enum</code> : For classification tasks, output an enum value as defined in the response schema.</li>
</ul>
<p>Specify the appropriate response type to avoid unintended behaviors. For example, if you require a JSON-formatted response, specify <code>application/json</code> and not <code>text/plain</code> .</p>
<p><code>text/plain</code> isn't supported for use with <code>responseSchema</code> .</p>
<blockquote>
<p><strong>Caution:</strong> Setting <code>responseMimeType</code> to <code>application/json</code> (JSON mode) without specifying a <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#responseSchema"><code>responseSchema</code></a> acts only as a strong hint to the model and doesn't ensure 100% valid JSON. Because JSON mode lacks strict schema enforcement, type checking, and relationship constraints, complex payloads can occasionally result in trailing characters or malformed outputs.</p>
<p>To ensure 100% valid JSON objects, requests must include <strong>both</strong> a <code>responseSchema</code> and <code>responseMimeType: "application/json"</code> . As a best practice, if your use case prevents you from pre-defining a schema, implement a client-side JSON validator with a retry mechanism.</p>
</blockquote>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/content-generation-parameters#response-mime-type">Content generation parameters</a> .</p></td>
</tr>
<tr class="even">
<td><p><code>responseSchema</code></p></td>
<td><p>Optional: <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.cachedContents#Schema">schema</a></p>
<p>The schema that generated candidate text must follow. For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Control generated output</a> .</p>
<p>To use this parameter, you must specify a supported MIME type other than <code>text/plain</code> for the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#responseMimeType"><code>responseMimeType</code></a> parameter.</p>
<p>To ensure 100% valid JSON objects, requests must include both a <code>responseSchema</code> and <code>responseMimeType</code> set to <code>application/json</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code>seed</code></p></td>
<td><p>Optional: <code>int</code></p>
<p>When seed is fixed to a specific value, the model makes a best effort to provide the same response for repeated requests. Deterministic output isn't guaranteed. Also, changing the model or parameter settings, such as the temperature, can cause variations in the response even when you use the same seed value. By default, a random seed value is used.</p></td>
</tr>
<tr class="even">
<td><p><code>responseLogprobs</code></p></td>
<td><p>Optional: <code>boolean</code></p>
<p>If true, returns the log probabilities of the tokens that were chosen by the model at each step. By default, this parameter is set to <code>false</code> .</p>
<blockquote>
<strong>Warning:</strong> The <code>responseLogprobs</code> parameter is deprecated for Gemini 3.x models and will soon be completely deprecated.
</blockquote></td>
</tr>
<tr class="odd">
<td><p><code>logprobs</code></p></td>
<td><p>Optional: <code>int</code></p>
<p>Returns the log probabilities of the top candidate tokens at each generation step. The model's chosen token might not be the same as the top candidate token at each step. Specify the number of candidates to return by using an integer value in the range of <code>1</code> - <code>20</code> .</p>
<p>You must enable <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference#responseLogprobs"><code>responseLogprobs</code></a> to use this parameter.</p>
<blockquote>
<strong>Warning:</strong> The <code>logprobs</code> parameter is deprecated for Gemini 3.x models and will soon be completely deprecated.
</blockquote></td>
</tr>
<tr class="even">
<td><p><code>audioTimestamp</code></p></td>
<td><p>Optional: <code>boolean</code></p>
<p>Enables timestamp understanding for audio-only files.</p>
<p>This is a preview feature.</p></td>
</tr>
<tr class="odd">
<td><p><code>thinkingConfig</code></p></td>
<td><p>Optional: <code>object</code></p>
<p>Configuration for the model's <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">thinking process</a> for Gemini 2.5 and higher models.</p>
<p>The <code>thinkingConfig</code> object contains the following fields:</p>
<ul>
<li><code>thinkingBudget</code> : <code>integer</code> . By default, the model automatically controls how much it thinks up to a maximum of <code>8,192</code> tokens.</li>
<li><code>thinkingLevel</code> : <code>enum</code> . Controls the amount of internal reasoning the model performs before generating a response. Higher levels may improve quality on complex tasks but increase latency and cost. Supported values are <code>MINIMAL</code> , <code>LOW</code> , <code>MEDIUM</code> , and <code>HIGH</code> (support varies by model).</li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>mediaResolution</code></p></td>
<td><p>Optional: <code>MediaResolution</code></p>
<p>Controls how input media is processed. <code>LOW</code> reduces tokens per image/video, possibly losing detail but allowing longer videos in context. Supported values: <code>HIGH</code> , <code>MEDIUM</code> , <code>LOW</code> .</p></td>
</tr>
</tbody>
</table>

### Response body

```
{
  "candidates": [
    {
      "content": {
        "parts": [
          {
            "text": string
          }
        ]
      },
      "finishReason": enum (FinishReason),
      "safetyRatings": [
        {
          "category": enum (HarmCategory),
          "probability": enum (HarmProbability),
          "blocked": boolean
        }
      ],
      "citationMetadata": {
        "citations": [
          {
            "startIndex": integer,
            "endIndex": integer,
            "uri": string,
            "title": string,
            "license": string,
            "publicationDate": {
              "year": integer,
              "month": integer,
              "day": integer
            }
          }
        ]
      },
      "avgLogprobs": double,
      "logprobsResult": {
        "topCandidates": [
          {
            "candidates": [
              {
                "token": string,
                "logProbability": float
              }
            ]
          }
        ],
        "chosenCandidates": [
          {
            "token": string,
            "logProbability": float
          }
        ]
      }
    }
  ],
  "usageMetadata": {
    "promptTokenCount": integer,
    "candidatesTokenCount": integer,
    "totalTokenCount": integer
  },
  "modelVersion": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Response element</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>modelVersion</code></td>
<td>The model and version used for generation. For example: <code>gemini-3.5-flash</code> .</td>
</tr>
<tr class="even">
<td><code>text</code></td>
<td>The generated text.</td>
</tr>
<tr class="odd">
<td><code>finishReason</code></td>
<td>The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens. Because the response uses the prompt for context, it's not possible to change the behavior of how the model stops generating tokens.<br />

<ul>
<li><code>FINISH_REASON_STOP</code> : Natural stop point of the model or provided stop sequence.</li>
<li><code>FINISH_REASON_MAX_TOKENS</code> : The maximum number of tokens as specified in the request was reached.</li>
<li><code>FINISH_REASON_SAFETY</code> : Token generation was stopped because the response was flagged for safety reasons. Note that <code>Candidate.content</code> is empty if content filters block the output.</li>
<li><code>FINISH_REASON_RECITATION</code> : The token generation was stopped because the response was flagged for unauthorized citations.</li>
<li><code>FINISH_REASON_BLOCKLIST</code> : Token generation was stopped because the response includes blocked terms.</li>
<li><code>FINISH_REASON_PROHIBITED_CONTENT</code> : Token generation was stopped because the response was flagged for prohibited content, such as child sexual abuse material (CSAM).</li>
<li><code>FINISH_REASON_IMAGE_PROHIBITED_CONTENT</code> : Token generation was stopped because the image provided in the prompt was flagged for prohibited content.</li>
<li><code>FINISH_REASON_NO_IMAGE</code> : Token generation was stopped because an image was expected in the prompt, but none was provided.</li>
<li><code>FINISH_REASON_SPII</code> : Token generation was stopped because the response was flagged for sensitive personally identifiable information (SPII).</li>
<li><code>FINISH_REASON_MALFORMED_FUNCTION_CALL</code> : Candidates were blocked because of malformed and unparsable function call.</li>
<li><code>FINISH_REASON_OTHER</code> : All other reasons that stopped the token</li>
<li><code>FINISH_REASON_UNSPECIFIED</code> : The finish reason is unspecified.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>category</code></td>
<td>The safety category to configure a threshold for. Acceptable values include the following:
<p><strong>Click to expand safety categories</strong></p>
<ul>
<li><code>HARM_CATEGORY_SEXUALLY_EXPLICIT</code></li>
<li><code>HARM_CATEGORY_HATE_SPEECH</code></li>
<li><code>HARM_CATEGORY_HARASSMENT</code></li>
<li><code>HARM_CATEGORY_DANGEROUS_CONTENT</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>probability</code></td>
<td>The harm probability levels in the content.<br />

<ul>
<li><code>HARM_PROBABILITY_UNSPECIFIED</code></li>
<li><code>NEGLIGIBLE</code></li>
<li><code>LOW</code></li>
<li><code>MEDIUM</code></li>
<li><code>HIGH</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>blocked</code></td>
<td>A boolean flag associated with a safety attribute that indicates if the model's input or output was blocked.</td>
</tr>
<tr class="odd">
<td><code>startIndex</code></td>
<td>An integer that specifies where a citation starts in the <code>content</code> . The <code>startIndex</code> is in bytes and calculated from the response encoded in UTF-8.</td>
</tr>
<tr class="even">
<td><code>endIndex</code></td>
<td>An integer that specifies where a citation ends in the <code>content</code> . The <code>endIndex</code> is in bytes and calculated from the response encoded in UTF-8.</td>
</tr>
<tr class="odd">
<td><code>url</code></td>
<td>The URL of a citation source. Examples of a URL source might be a news website or a GitHub repository.</td>
</tr>
<tr class="even">
<td><code>title</code></td>
<td>The title of a citation source. Examples of source titles might be that of a news article or a book.</td>
</tr>
<tr class="odd">
<td><code>license</code></td>
<td>The license associated with a citation.</td>
</tr>
<tr class="even">
<td><code>publicationDate</code></td>
<td>The date a citation was published. Its valid formats are <code>YYYY</code> , <code>YYYY-MM</code> , and <code>YYYY-MM-DD</code> .</td>
</tr>
<tr class="odd">
<td><code>avgLogprobs</code></td>
<td>Average log probability of the candidate.</td>
</tr>
<tr class="even">
<td><code>logprobsResult</code></td>
<td>Returns the top candidate tokens ( <code>topCandidates</code> ) and the actual chosen tokens ( <code>chosenCandidates</code> ) at each step.</td>
</tr>
<tr class="odd">
<td><code>token</code></td>
<td>Generative AI models break down text data into tokens for processing, which can be characters, words, or phrases.</td>
</tr>
<tr class="even">
<td><code>logProbability</code></td>
<td>A log probability value that indicates the model's confidence for a particular token.</td>
</tr>
<tr class="odd">
<td><code>promptTokenCount</code></td>
<td>Number of tokens in the request.</td>
</tr>
<tr class="even">
<td><code>candidatesTokenCount</code></td>
<td>Number of tokens in the response(s).</td>
</tr>
<tr class="odd">
<td><code>totalTokenCount</code></td>
<td>Number of tokens in the request and response(s).</td>
</tr>
</tbody>
</table>

> **Note:** For billing purposes, tokens consumed by document inputs to Gemini 3 and later models are counted as image tokens.

## Examples

The following examples show how to generate content using Gemini models.

### Text Generation

Generate a text response from a text input.

### Google Gen AI SDK for Python

```
from google import genai
from google.genai.types import HttpOptions

client = genai.Client(http_options=HttpOptions(api_version="v1"))
response = client.models.generate_content(
    model="gemini-3.5-flash",
    contents="How does AI work?",
)
print(response.text)
# Example response:
# Okay, let's break down how AI works. It's a broad field, so I'll focus on the ...
#
# Here's a simplified overview:
# ...
```

### Python (OpenAI)

You can call the Inference API by using the OpenAI library. For more information, see [Call Agent Platform models by using the OpenAI library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview) .

```python
from google.auth import default
import google.auth.transport.requests

import openai

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "us-central1"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
    base_url=f"https://{location}-aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
    api_key=credentials.token,
)

response = client.chat.completions.create(
    model="google/gemini-2.0-flash-001",
    messages=[{"role": "user", "content": "Why is the sky blue?"}],
)

print(response)
```

### Go

```
import (
    "context"
    "fmt"
    "io"

    "google.golang.org/genai"
)

// generateWithText shows how to generate text using a text prompt.
func generateWithText(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    resp, err := client.Models.GenerateContent(ctx,
        "gemini-2.5-flash",
        genai.Text("How does AI work?"),
        nil,
    )
    if err != nil {
        return fmt.Errorf("failed to generate content: %w", err)
    }

    respText := resp.Text()

    fmt.Fprintln(w, respText)
    // Example response:
    // That's a great question! Understanding how AI works can feel like ...
    // ...
    // **1. The Foundation: Data and Algorithms**
    // ...

    return nil
}
```

### Using multimodal prompt

Generate a text response from a multimodal input, such as text and an image.

### Google Gen AI SDK for Python

```
from google import genai
from google.genai.types import HttpOptions, Part

client = genai.Client(http_options=HttpOptions(api_version="v1"))
response = client.models.generate_content(
    model="gemini-3.5-flash",
    contents=[
        "What is shown in this image?",
        Part.from_uri(
            file_uri="gs://cloud-samples-data/generative-ai/image/scones.jpg",
            mime_type="image/jpeg",
        ),
    ],
)
print(response.text)
# Example response:
# The image shows a flat lay of blueberry scones arranged on parchment paper. There are ...
```

### Python (OpenAI)

You can call the Inference API by using the OpenAI library. For more information, see [Call Agent Platform models by using the OpenAI library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview) .

```python
from google.auth import default
import google.auth.transport.requests

import openai

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "us-central1"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
    base_url=f"https://{location}-aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
    api_key=credentials.token,
)

response = client.chat.completions.create(
    model="google/gemini-2.0-flash-001",
    messages=[
        {
            "role": "user",
            "content": [
                {"type": "text", "text": "Describe the following image:"},
                {
                    "type": "image_url",
                    "image_url": "gs://cloud-samples-data/generative-ai/image/scones.jpg",
                },
            ],
        }
    ],
)

print(response)
```

### Go

```
import (
    "context"
    "fmt"
    "io"

    genai "google.golang.org/genai"
)

// generateWithTextImage shows how to generate text using both text and image input
func generateWithTextImage(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-flash"
    contents := []*genai.Content{
        {Parts: []*genai.Part{
            {Text: "What is shown in this image?"},
            {FileData: &genai.FileData{
                // Image source: https://storage.googleapis.com/cloud-samples-data/generative-ai/image/scones.jpg
                FileURI:  "gs://cloud-samples-data/generative-ai/image/scones.jpg",
                MIMEType: "image/jpeg",
            }},
        },
            Role: genai.RoleUser},
    }

    resp, err := client.Models.GenerateContent(ctx, modelName, contents, nil)
    if err != nil {
        return fmt.Errorf("failed to generate content: %w", err)
    }

    respText := resp.Text()

    fmt.Fprintln(w, respText)

    // Example response:
    // The image shows an overhead shot of a rustic, artistic arrangement on a surface that ...

    return nil
}
```

### Streaming text response

Generate a streaming model response from a text input.

### Google Gen AI SDK for Python

```
from google import genai
from google.genai.types import HttpOptions

client = genai.Client(http_options=HttpOptions(api_version="v1"))

for chunk in client.models.generate_content_stream(
    model="gemini-3.5-flash",
    contents="Why is the sky blue?",
):
    print(chunk.text, end="")
# Example response:
# The
#  sky appears blue due to a phenomenon called **Rayleigh scattering**. Here's
#  a breakdown of why:
# ...
```

### Python (OpenAI)

You can call the Inference API by using the OpenAI library. For more information, see [Call Agent Platform models by using the OpenAI library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview) .

```python
from google.auth import default
import google.auth.transport.requests

import openai

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "us-central1"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
    base_url=f"https://{location}-aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
    api_key=credentials.token,
)

response = client.chat.completions.create(
    model="google/gemini-2.0-flash-001",
    messages=[{"role": "user", "content": "Why is the sky blue?"}],
    stream=True,
)
for chunk in response:
    print(chunk)
```

### Go

```
import (
    "context"
    "fmt"
    "io"

    genai "google.golang.org/genai"
)

// generateWithTextStream shows how to generate text stream using a text prompt.
func generateWithTextStream(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-flash"
    contents := genai.Text("Why is the sky blue?")

    for resp, err := range client.Models.GenerateContentStream(ctx, modelName, contents, nil) {
        if err != nil {
            return fmt.Errorf("failed to generate content: %w", err)
        }

        chunk := resp.Text()

        fmt.Fprintln(w, chunk)
    }

    // Example response:
    // The
    //  sky is blue
    //  because of a phenomenon called **Rayleigh scattering**. Here's the breakdown:
    // ...

    return nil
}
```

## What's next

- Learn more about [function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .
- Learn more about [grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview) .
