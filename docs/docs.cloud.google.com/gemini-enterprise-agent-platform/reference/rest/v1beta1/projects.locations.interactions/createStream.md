---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactions/createStream
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactions/createStream
title: 'Method: interactions.createStream'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.interactions.createStream

Creates an interaction and streams the response.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /projects /* /locations /* /interactions:createStream`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Request body

The request body contains data with the following structure:

Fields

`stream` `boolean`

Input only. Whether the interaction will be streamed.

`store` `boolean`

Input only. Whether to store the response and request for later retrieval.

`interaction.contentList (deprecated) .contents[].text.text` `string`

Required. The text content.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.documentUri` `string`

The URI of the file.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.fileName` `string`

The name of the file.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.source` `string`

Source attributed for a portion of the text.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].name` `string`

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.pageNumber` `integer`

Page number of the cited document, if applicable.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.mediaId` `string`

Media id in-case of image citations, if applicable.

`interaction.contentList (deprecated) .contents[].text.annotations[].startIndex` `integer`

Start of segment of the response that is attributed to this source.

Index indicates the start of the segment, measured in bytes.

`interaction.contentList (deprecated) .contents[].text.annotations[].endIndex` `integer`

End of the attributed segment, exclusive.

`interaction.contentList (deprecated) .contents[].image.mimeTypeString` `string`

Flexible MIME type string of the image, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.contentList (deprecated) .contents[].image.resolution` ` enum ( MediaResolution  ` )

The resolution of the media.

`interaction.contentList (deprecated) .contents[].audio.mimeTypeString` `string`

Flexible MIME type string of the audio, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.contentList (deprecated) .contents[].audio.channels` `integer`

The number of audio channels.

`interaction.contentList (deprecated) .contents[].audio.sampleRate` `integer`

The sample rate of the audio.

`interaction.contentList (deprecated) .contents[].document.mimeTypeString` `string`

Flexible MIME type string of the document, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.contentList (deprecated) .contents[].video.mimeTypeString` `string`

Flexible MIME type string of the video, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`interaction.contentList (deprecated) .contents[].video.resolution` ` enum ( MediaResolution  ` )

The resolution of the media.

`interaction.contentList (deprecated) .contents[].video.name` `string`

A user-defined name for this content block. Can be referenced by the model in the final response.

`interaction.stepList.steps[].text (deprecated) .text` `string`

`interaction.stepList.steps[].image (deprecated) .mimeTypeString` `string`

`interaction.stepList.steps[].image (deprecated) .resolution` ` enum ( MediaResolution  ` )

`interaction.stepList.steps[].audio (deprecated) .mimeTypeString` `string`

`interaction.stepList.steps[].audio (deprecated) .rate` `integer`

`interaction.stepList.steps[].audio (deprecated) .channels` `integer`

`interaction.stepList.steps[].audio (deprecated) .sampleRate` `integer`

`interaction.stepList.steps[].document (deprecated) .mimeTypeString` `string`

`interaction.stepList.steps[].video (deprecated) .mimeTypeString` `string`

`interaction.stepList.steps[].video (deprecated) .resolution` ` enum ( MediaResolution  ` )

`interaction.stepList.steps[].video (deprecated) .name` `string`

`interaction.id` `string`

Required. Output only. A unique identifier for the interaction completion.

`interaction.status` ` enum ( Status  ` )

Required. Output only. The status of the interaction.

`interaction.created` `string`

Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`interaction.updated` `string`

Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

` interaction.role (deprecated)  ` `string`

Output only. The role of the interaction.

` interaction.outputs[] (deprecated)  ` ` object ( Content  ` )

Output only. Responses from the model.

`interaction.tools[]` ` object ( Tool  ` )

A list of tool declarations the model may call during interaction.

`interaction.usage` ` object ( Usage  ` )

Output only. Statistics on the interaction request's token usage.

` interaction.responseModalities[] (deprecated)  ` ` enum ( ResponseModality  ` )

The requested modalities of the response (TEXT, IMAGE, AUDIO).

` interaction.responseMimeType (deprecated)  ` `string`

The mime type of the response. This is required if responseFormat is set.

`interaction.previousInteractionId` `string`

The id of the previous interaction, if any.

`interaction.environmentId` `string`

Output only. The environment id for the interaction. Only populated if environment config is set in the request.

`interaction.steps[]` ` object ( Step  ` )

Required. Output only. The steps that make up the interaction.

`interaction.safetySettings[]` ` object ( SafetySetting  ` )

Safety settings for the interaction.

`interaction.labels` `map (key: string, value: string)`

The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`interaction.errors[]` ` object ( Error  ` )

Output only. Diagnostic faults / platform errors recorded on the interaction.

`background` `boolean`

Input only. Whether to run the model interaction in the background.

`system_instruction_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.systemInstruction` `string`

System instruction for the interaction.

End of mutually exclusive fields.

`type` `Union type`

The type of annotation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].text.annotations[].urlCitation` ` object ( UrlCitation  ` )

NOTE: We use these instead of the Citation message for historical reasons. A URL citation annotation.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation` ` object ( FileCitation  ` )

A file citation annotation.

`interaction.contentList (deprecated) .contents[].text.annotations[].placeCitation` ` object ( PlaceCitation  ` )

A place citation annotation.

`interaction.contentList (deprecated) .contents[].text.annotations[].wordInfo` ` object ( WordInfo  ` )

word-level ASR annotation with timing and speaker info.

End of mutually exclusive fields.

`kind` `Union type`

The kind of value. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.nullValue` `null`

Represents a null value.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.numberValue` `number`

Represents a double value.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.stringValue` `string`

Represents a string value.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.boolValue` `boolean`

Represents a boolean value.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.structValue` ` object ( Struct  ` )

Represents a structured value.

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.listValue` ` object ( ListValue  ` )

Represents a repeated `value` .

`interaction.contentList (deprecated) .contents[].text.annotations[].fileCitation.customMetadata.fields[].value.contentValue` ` object ( Content  ` )

Represents rich content (text, image, etc.).

End of mutually exclusive fields.

`data_or_uri` `Union type`

The image content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].image.data` `string ( bytes format)`

The image content.

A base64-encoded string.

`interaction.contentList (deprecated) .contents[].image.uri` `string`

The URI of the image.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The audio content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].audio.data` `string ( bytes format)`

The audio content.

A base64-encoded string.

`interaction.contentList (deprecated) .contents[].audio.uri` `string`

The URI of the audio.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The document content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].document.data` `string ( bytes format)`

The document content.

A base64-encoded string.

`interaction.contentList (deprecated) .contents[].document.uri` `string`

The URI of the document.

End of mutually exclusive fields.

`data_or_uri` `Union type`

The video content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].video.data` `string ( bytes format)`

The video content.

A base64-encoded string.

`interaction.contentList (deprecated) .contents[].video.uri` `string`

The URI of the video.

End of mutually exclusive fields.

`processing` `Union type`

How the model processes this video for understanding. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].video.processingType` ` enum ( Processing  ` )

`interaction.contentList (deprecated) .contents[].video.processingConfig` ` object ( MediaProcessing  ` )

End of mutually exclusive fields.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.contentList (deprecated) .contents[].text` ` object ( TextContent  ` )

`interaction.contentList (deprecated) .contents[].image` ` object ( ImageContent  ` )

`interaction.contentList (deprecated) .contents[].audio` ` object ( AudioContent  ` )

`interaction.contentList (deprecated) .contents[].document` ` object ( DocumentContent  ` )

`interaction.contentList (deprecated) .contents[].video` ` object ( VideoContent  ` )

` interaction.contentList (deprecated) .contents[].thought (deprecated)  ` ` object ( ThoughtContent  ` )

` interaction.contentList (deprecated) .contents[].toolCall (deprecated)  ` ` object ( ToolCallContent  ` )

` interaction.contentList (deprecated) .contents[].toolResult (deprecated)  ` ` object ( ToolResultContent  ` )

End of mutually exclusive fields.

`input` `Union type`

The input for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

` interaction.contentList (deprecated)  ` ` object ( ContentList  ` )

The inputs for the interaction.

`interaction.stringContent` `string`

A string input for the interaction, it will be processed as a single text input.

` interaction.turnList (deprecated)  ` `object ( TurnList` )

The turns for the interaction.

`interaction.stepList` ` object ( StepList  ` )

Input only. The steps for the interaction.

`interaction.content` ` object ( Content  ` )

The content for the interaction.

End of mutually exclusive fields.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought` ` object ( ThoughtStep  ` )

`interaction.stepList.steps[].toolCall` ` object ( ToolCallStep  ` )

`interaction.stepList.steps[].toolResult` ` object ( ToolResultStep  ` )

`interaction.stepList.steps[].userInput` ` object ( UserInputStep  ` )

DO NOT USE -- These are for 3P JSON only

`interaction.stepList.steps[].modelOutput` ` object ( ModelOutputStep  ` )

` interaction.stepList.steps[].text (deprecated)  ` `object ( LegacyTextContent` )

` interaction.stepList.steps[].image (deprecated)  ` `object ( LegacyImageContent` )

` interaction.stepList.steps[].audio (deprecated)  ` `object ( LegacyAudioContent` )

` interaction.stepList.steps[].document (deprecated)  ` `object ( LegacyDocumentContent` )

` interaction.stepList.steps[].video (deprecated)  ` `object ( LegacyVideoContent` )

End of mutually exclusive fields.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].image (deprecated) .data` `string ( bytes format)`

A base64-encoded string.

`interaction.stepList.steps[].image (deprecated) .uri` `string`

End of mutually exclusive fields.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].audio (deprecated) .data` `string ( bytes format)`

A base64-encoded string.

`interaction.stepList.steps[].audio (deprecated) .uri` `string`

End of mutually exclusive fields.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].document (deprecated) .data` `string ( bytes format)`

A base64-encoded string.

`interaction.stepList.steps[].document (deprecated) .uri` `string`

End of mutually exclusive fields.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].video (deprecated) .data` `string ( bytes format)`

A base64-encoded string.

`interaction.stepList.steps[].video (deprecated) .uri` `string`

End of mutually exclusive fields.

`processing` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].video (deprecated) .processingType` ` enum ( Processing  ` )

`interaction.stepList.steps[].video (deprecated) .processingConfig` ` object ( MediaProcessing  ` )

End of mutually exclusive fields.

`response_format_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

` interaction.responseFormat (deprecated)  ` ` object ( Value  ` )

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field.

`interaction.responseFormatList` ` object ( ResponseFormatList  ` )

`interaction.responseFormatSingleton` ` object ( ResponseFormat  ` )

End of mutually exclusive fields.

`request_type` `Union type`

The request type for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.modelInteraction` ` object ( ModelInteraction  ` )

Interaction for generating the completion using models.

`interaction.agentInteraction` ` object ( AgentInteraction  ` )

Interaction for generating the completion using agents.

End of mutually exclusive fields.

`environment` `Union type`

The environment configuration for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.envId` `string`

The environment id for the interaction. Can be 'remote' for default environment.

`interaction.remoteEnvironment` ` object ( EnvironmentConfig  ` )

`interaction.localEnvironment` ` object ( LocalEnvironmentConfig  ` )

The agent's environment lives on the client connection: its built-in environment operations (filesystem ops and running commands) are yielded to the client to execute, instead of running in a server-managed sandbox. Mutually exclusive with `remoteEnvironment` . (Independent of any client-declared function tools, which are always executed on the client regardless of this field.)

End of mutually exclusive fields.

### Response body

If successful, the response body contains a stream of `  InteractionStreamingEvent  ` instances.
