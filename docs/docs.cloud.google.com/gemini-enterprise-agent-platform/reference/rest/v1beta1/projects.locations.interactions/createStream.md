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

`interaction.stepList.steps[].text (deprecated) .text` `string`

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

`interaction.systemInstruction` `string`

System instruction for the interaction.

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

`interaction.safety_settings[]` ` object ( SafetySetting  ` )

Safety settings for the interaction.

`interaction.labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`background` `boolean`

Input only. Whether to run the model interaction in the background.

`type` `Union type`

`type` can be only one of the following:

`interaction.contentList (deprecated) .contents[].text` ` object ( TextContent  ` )

`interaction.contentList (deprecated) .contents[].image` ` object ( ImageContent  ` )

`interaction.contentList (deprecated) .contents[].audio` ` object ( AudioContent  ` )

`interaction.contentList (deprecated) .contents[].document` ` object ( DocumentContent  ` )

`interaction.contentList (deprecated) .contents[].video` ` object ( VideoContent  ` )

` interaction.contentList (deprecated) .contents[].thought (deprecated)  ` ` object ( ThoughtContent  ` )

` interaction.contentList (deprecated) .contents[].toolCall (deprecated)  ` ` object ( ToolCallContent  ` )

` interaction.contentList (deprecated) .contents[].toolResult (deprecated)  ` ` object ( ToolResultContent  ` )

`input` `Union type`

The input for the interaction. `input` can be only one of the following:

` interaction.contentList (deprecated)  ` ` object ( ContentList  ` )

The inputs for the interaction.

`interaction.stringContent` `string`

A string input for the interaction, it will be processed as a single text input.

` interaction.turnList (deprecated)  ` ` object ( TurnList  ` )

The turns for the interaction.

`interaction.stepList` ` object ( StepList  ` )

Input only. The steps for the interaction.

`interaction.content` ` object ( Content  ` )

The content for the interaction.

`type` `Union type`

`type` can be only one of the following:

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

`response_format_config` `Union type`

`response_format_config` can be only one of the following:

` interaction.responseFormat (deprecated)  ` ` object ( Value  ` )

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field.

`interaction.responseFormatList` ` object ( ResponseFormatList  ` )

`interaction.responseFormatSingleton` ` object ( ResponseFormat  ` )

`request_type` `Union type`

The request type for the interaction. `request_type` can be only one of the following:

`interaction.modelInteraction` ` object ( ModelInteraction  ` )

Interaction for generating the completion using models.

`interaction.agentInteraction` ` object ( AgentInteraction  ` )

Interaction for generating the completion using agents.

`environment` `Union type`

The environment configuration for the interaction. `environment` can be only one of the following:

`interaction.envId` `string`

The environment id for the interaction. Can be 'remote' for default environment.

`interaction.remoteEnvironment` ` object ( EnvironmentConfig  ` )

`interaction.localEnvironment` ` object ( LocalEnvironmentConfig  ` )

The agent's environment lives on the client connection: its built-in environment operations (filesystem ops and running commands) are yielded to the client to execute, instead of running in a server-managed sandbox. Mutually exclusive with `remoteEnvironment` . (Independent of any client-declared function tools, which are always executed on the client regardless of this field.)

### Response body

If successful, the response body contains a stream of `  InteractionStreamingEvent  ` instances.
