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

`interaction.modelInteraction.model` `string`

The name of the `Model` used for generating the completion.

`interaction.modelInteraction.generationConfig.temperature` `number`

Controls the randomness of the output.

`interaction.modelInteraction.generationConfig.topP` `number`

The maximum cumulative probability of tokens to consider when sampling.

`interaction.modelInteraction.generationConfig.seed` `integer`

Seed used in decoding for reproducibility.

`interaction.modelInteraction.generationConfig.stopSequences[]` `string`

A list of character sequences that will stop output interaction.

`interaction.modelInteraction.generationConfig.thinkingLevel` ` enum ( ThinkingLevel  ` )

The level of thought tokens that the model should generate.

`interaction.modelInteraction.generationConfig.thinkingSummaries` ` enum ( ThinkingSummaries  ` )

Whether to include thought summaries in the response.

`interaction.modelInteraction.generationConfig.maxOutputTokens` `integer`

The maximum number of tokens to include in the response.

` interaction.modelInteraction.generationConfig.imageConfig (deprecated)  ` ` object ( ImageConfig  ` )

Configuration for image interaction.

`interaction.modelInteraction.generationConfig.videoConfig` ` object ( VideoConfig  ` )

Configuration for video generation.

`interaction.modelInteraction.generationConfig.transcriptionConfig` ` object ( TranscriptionConfig  ` )

Optional. Configuration for speech recognition (transcription). If present, ASR is enabled.

`interaction.id` `string`

Required. Output only. A unique identifier for the interaction completion.

`interaction.status` ` enum ( Status  ` )

Required. Output only. The status of the interaction.

`interaction.created` `string`

Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`interaction.updated` `string`

Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

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

`interaction.safetySettings[]` ` object ( SafetySetting  ` )

Safety settings for the interaction.

`interaction.labels` `map (key: string, value: string)`

The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`interaction.errors[]` ` object ( Error  ` )

Output only. Diagnostic faults / platform errors recorded on the interaction.

`background` `boolean`

Input only. Whether to run the model interaction in the background.

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

`response_format_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

` interaction.responseFormat (deprecated)  ` ` object ( Value  ` )

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field.

`interaction.responseFormatList` ` object ( ResponseFormatList  ` )

`interaction.responseFormatSingleton` ` object ( ResponseFormat  ` )

End of mutually exclusive fields.

`tool_choice` `Union type`

The tool choice configuration. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.modelInteraction.generationConfig.toolChoiceMode` ` enum ( ToolChoiceType  ` )

The mode of the tool choice.

`interaction.modelInteraction.generationConfig.toolChoiceConfig` ` object ( ToolChoiceConfig  ` )

The config for the tool choice.

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
