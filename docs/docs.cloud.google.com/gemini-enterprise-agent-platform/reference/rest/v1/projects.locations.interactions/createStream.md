---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.interactions/createStream
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.interactions/createStream
title: 'Method: interactions.createStream'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.interactions.createStream

Creates an interaction and streams the response.

### Endpoint

post `https: / /{service-endpoint} /v1 /projects /* /locations /* /interactions:createStream`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Request body

The request body contains data with the following structure:

Fields

`stream` `boolean`

Input only. Whether the interaction will be streamed.

`store` `boolean`

Input only. Whether to store the response and request for later retrieval.

`interaction.stepList.steps[].thought.signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`interaction.stepList.steps[].thought.summary[].text.text` `string`

Required. The text content.

`interaction.stepList.steps[].thought.summary[].text.annotations[].urlCitation.url` `string`

The URL.

`interaction.stepList.steps[].thought.summary[].text.annotations[].urlCitation.title` `string`

The title of the URL.

`interaction.stepList.steps[].thought.summary[].text.annotations[].startIndex` `integer`

Start of segment of the response that is attributed to this source.

Index indicates the start of the segment, measured in bytes.

`interaction.stepList.steps[].thought.summary[].text.annotations[].endIndex` `integer`

End of the attributed segment, exclusive.

`interaction.stepList.steps[].thought.summary[].image.mimeTypeString` `string`

Flexible MIME type string of the image, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.stepList.steps[].thought.summary[].image.resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MediaResolution)` )`

The resolution of the media.

`interaction.stepList.steps[].thought.summary[].audio.mimeTypeString` `string`

Flexible MIME type string of the audio, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.stepList.steps[].thought.summary[].audio.channels` `integer`

The number of audio channels.

`interaction.stepList.steps[].thought.summary[].audio.sampleRate` `integer`

The sample rate of the audio.

`interaction.stepList.steps[].thought.summary[].document.mimeTypeString` `string`

Flexible MIME type string of the document, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.stepList.steps[].thought.summary[].video.mimeTypeString` `string`

Flexible MIME type string of the video, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.stepList.steps[].thought.summary[].video.resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MediaResolution)` )`

The resolution of the media.

`interaction.stepList.steps[].thought.summary[].video.name` `string`

A user-defined name for this content block. Can be referenced by the model in the final response.

`interaction.stepList.steps[].toolCall.functionCall.name` `string`

Required. The name of the tool to call.

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].name` `string`

`interaction.stepList.steps[].toolCall.id` `string`

Required. A unique id for this specific tool call.

`interaction.stepList.steps[].toolCall.signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`interaction.id` `string`

Required. Output only. A unique identifier for the interaction completion.

`interaction.status` `enum ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Status)` )`

Required. Output only. The status of the interaction.

`interaction.created` `string`

Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`interaction.updated` `string`

Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`interaction.systemInstruction` `string`

System instruction for the interaction.

`interaction.tools[]` `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#Tool)` )`

A list of tool declarations the model may call during interaction.

`interaction.usage` `object ( `[`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Usage)` )`

Output only. Statistics on the interaction request's token usage.

`interaction.previousInteractionId` `string`

The id of the previous interaction, if any.

`interaction.environmentId` `string`

Output only. The environment id for the interaction. Only populated if environment config is set in the request.

`interaction.steps[]` `object ( `[`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step)` )`

Required. Output only. The steps that make up the interaction, when included in the response.

`interaction.safetySettings[]` `object ( `[`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#SafetySetting)` )`

Safety settings for the interaction.

`interaction.labels` `map (key: string, value: string)`

The labels with user-defined metadata for the request.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`interaction.errors[]` `object ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Error)` )`

Output only. Diagnostic faults / platform errors recorded on the interaction.

`background` `boolean`

Input only. Whether to run the model interaction in the background.

`input` `Union type`

The input for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stringContent` `string`

A string input for the interaction, it will be processed as a single text input.

`interaction.stepList` `object ( `[`StepList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#StepList)` )`

Input only. The steps for the interaction.

`interaction.content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

The content for the interaction.

End of mutually exclusive fields.

`type` `Union type`

The type of annotation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought.summary[].text.annotations[].urlCitation` `object ( `[`UrlCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation#UrlCitation)` )`

NOTE: We use these instead of the Citation message for historical reasons. A URL citation annotation.

`interaction.stepList.steps[].thought.summary[].text.annotations[].fileCitation` `object ( `[`FileCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation#FileCitation)` )`

A file citation annotation.

`interaction.stepList.steps[].thought.summary[].text.annotations[].placeCitation` `object ( `[`PlaceCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation#PlaceCitation)` )`

A place citation annotation.

`interaction.stepList.steps[].thought.summary[].text.annotations[].wordInfo` `object ( `[`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation#WordInfo)` )`

word-level ASR annotation with timing and speaker info.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The image content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought.summary[].image.data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The image content.

A base64-encoded string.

`interaction.stepList.steps[].thought.summary[].image.uri` `string`

The URI of the image.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The audio content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought.summary[].audio.data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The audio content.

A base64-encoded string.

`interaction.stepList.steps[].thought.summary[].audio.uri` `string`

The URI of the audio.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The document content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought.summary[].document.data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The document content.

A base64-encoded string.

`interaction.stepList.steps[].thought.summary[].document.uri` `string`

The URI of the document.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The video content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought.summary[].video.data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The video content.

A base64-encoded string.

`interaction.stepList.steps[].thought.summary[].video.uri` `string`

The URI of the video.

End of mutually exclusive fields.

`processing` `Union type`

How the model processes this video for understanding. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought.summary[].video.processingType` `enum ( `[`Processing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#Processing)` )`

`interaction.stepList.steps[].thought.summary[].video.processingConfig` `object ( `[`MediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#MediaProcessing)` )`

End of mutually exclusive fields.

`kind` `Union type`

The kind of value. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.nullValue` `null`

Represents a null value.

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.numberValue` `number`

Represents a double value.

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.stringValue` `string`

Represents a string value.

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.boolValue` `boolean`

Represents a boolean value.

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.structValue` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Struct)` )`

Represents a structured value.

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.listValue` `object ( `[`ListValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Value#ListValue)` )`

Represents a repeated `value` .

`interaction.stepList.steps[].toolCall.functionCall.arguments.fields[].value.contentValue` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Represents rich content (text, image, etc.).

End of mutually exclusive fields.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].toolCall.functionCall` `object ( `[`FunctionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#FunctionCallStep)` )`

`interaction.stepList.steps[].toolCall.codeExecutionCall` `object ( `[`CodeExecutionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#CodeExecutionCallStep)` )`

`interaction.stepList.steps[].toolCall.urlContextCall` `object ( `[`UrlContextCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#UrlContextCallStep)` )`

`interaction.stepList.steps[].toolCall.googleSearchCall` `object ( `[`GoogleSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#GoogleSearchCallStep)` )`

`interaction.stepList.steps[].toolCall.fileSearchCall` `object ( `[`FileSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#FileSearchCallStep)` )`

`interaction.stepList.steps[].toolCall.googleMapsCall` `object ( `[`GoogleMapsCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#GoogleMapsCallStep)` )`

`interaction.stepList.steps[].toolCall.retrievalCall` `object ( `[`RetrievalCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#RetrievalCallStep)` )`

End of mutually exclusive fields.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought` `object ( `[`ThoughtStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ThoughtStep)` )`

`interaction.stepList.steps[].toolCall` `object ( `[`ToolCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ToolCallStep)` )`

`interaction.stepList.steps[].toolResult` `object ( `[`ToolResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ToolResultStep)` )`

`interaction.stepList.steps[].userInput` `object ( `[`UserInputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#UserInputStep)` )`

DO NOT USE -- These are for 3P JSON only

`interaction.stepList.steps[].modelOutput` `object ( `[`ModelOutputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ModelOutputStep)` )`

End of mutually exclusive fields.

`response_format_config` `Union type`

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.responseFormatList` `object ( `[`ResponseFormatList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ResponseFormatList)` )`

`interaction.responseFormatSingleton` `object ( `[`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ResponseFormat)` )`

End of mutually exclusive fields.

`request_type` `Union type`

The request type for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.modelInteraction` `object ( `[`ModelInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ModelInteraction)` )`

Interaction for generating the completion using models.

`interaction.agentInteraction` `object ( `[`AgentInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#AgentInteraction)` )`

Interaction for generating the completion using agents.

End of mutually exclusive fields.

`environment` `Union type`

The environment configuration for the interaction. Can be an object specifying remote environment sources or a string referencing an existing environment ID. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.envId` `string`

The environment id for the interaction. Can be 'remote' for default environment.

End of mutually exclusive fields.

### Response body

If successful, the response body contains a stream of [`InteractionStreamingEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/InteractionStreamingEvent) instances.
