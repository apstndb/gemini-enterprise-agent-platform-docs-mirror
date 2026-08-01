---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction
title: Interaction
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response for InteractionService.CreateInteraction.

Fields

`id` `string`

Required. Output only. A unique identifier for the interaction completion.

`status` ` enum ( Status  ` )

Required. Output only. The status of the interaction.

`created` `string`

Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`updated` `string`

Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

` role (deprecated)  ` `string`

> This item is deprecated\!

Output only. The role of the interaction.

` outputs[] (deprecated)  ` ` object ( Content  ` )

> This item is deprecated\!

Output only. Responses from the model.

`systemInstruction` `string`

System instruction for the interaction.

`tools[]` ` object ( Tool  ` )

A list of tool declarations the model may call during interaction.

`usage` ` object ( Usage  ` )

Output only. Statistics on the interaction request's token usage.

` responseModalities[] (deprecated)  ` ` enum ( ResponseModality  ` )

> This item is deprecated\!

The requested modalities of the response (TEXT, IMAGE, AUDIO).

` responseMimeType (deprecated)  ` `string`

> This item is deprecated\!

The mime type of the response. This is required if responseFormat is set.

`previousInteractionId` `string`

The id of the previous interaction, if any.

`environmentId` `string`

Output only. The environment id for the interaction. Only populated if environment config is set in the request.

`steps[]` ` object ( Step  ` )

Required. Output only. The steps that make up the interaction.

`safety_settings[]` ` object ( SafetySetting  ` )

Safety settings for the interaction.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`input` `Union type`

The input for the interaction. `input` can be only one of the following:

` contentList (deprecated)  ` ` object ( ContentList  ` )

> This item is deprecated\!

The inputs for the interaction.

`stringContent` `string`

A string input for the interaction, it will be processed as a single text input.

` turnList (deprecated)  ` ` object ( TurnList  ` )

> This item is deprecated\!

The turns for the interaction.

`stepList` ` object ( StepList  ` )

Input only. The steps for the interaction.

`content` ` object ( Content  ` )

The content for the interaction.

`response_format_config` `Union type`

`response_format_config` can be only one of the following:

` responseFormat (deprecated)  ` ` object ( Value  ` )

> This item is deprecated\!

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field.

`responseFormatList` ` object ( ResponseFormatList  ` )

`responseFormatSingleton` ` object ( ResponseFormat  ` )

`request_type` `Union type`

The request type for the interaction. `request_type` can be only one of the following:

`modelInteraction` ` object ( ModelInteraction  ` )

Interaction for generating the completion using models.

`agentInteraction` ` object ( AgentInteraction  ` )

Interaction for generating the completion using agents.

`environment` `Union type`

The environment configuration for the interaction. `environment` can be only one of the following:

`envId` `string`

The environment id for the interaction. Can be 'remote' for default environment.

`remoteEnvironment` ` object ( EnvironmentConfig  ` )

`localEnvironment` ` object ( LocalEnvironmentConfig  ` )

The agent's environment lives on the client connection: its built-in environment operations (filesystem ops and running commands) are yielded to the client to execute, instead of running in a server-managed sandbox. Mutually exclusive with `remoteEnvironment` . (Independent of any client-declared function tools, which are always executed on the client regardless of this field.)

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;status&quot;: enum (Status),&quot;created&quot;: string,&quot;updated&quot;: string,&quot;role&quot;: string,&quot;outputs&quot;: [{object (Content)}],&quot;systemInstruction&quot;: string,&quot;tools&quot;: [{object (Tool)}],&quot;usage&quot;: {object (Usage)},&quot;responseModalities&quot;: [enum (ResponseModality)],&quot;responseMimeType&quot;: string,&quot;previousInteractionId&quot;: string,&quot;environmentId&quot;: string,&quot;steps&quot;: [{object (Step)}],&quot;safety_settings&quot;: [{object (SafetySetting)}],&quot;labels&quot;: {string: string,...},// input&quot;contentList&quot;: {object (ContentList)},&quot;stringContent&quot;: string,&quot;turnList&quot;: {object (TurnList)},&quot;stepList&quot;: {object (StepList)},&quot;content&quot;: {object (Content)}// Union type// response_format_config&quot;responseFormat&quot;: {object (Value)},&quot;responseFormatList&quot;: {object (ResponseFormatList)},&quot;responseFormatSingleton&quot;: {object (ResponseFormat)}// Union type// request_type&quot;modelInteraction&quot;: {object (ModelInteraction)},&quot;agentInteraction&quot;: {object (AgentInteraction)}// Union type// environment&quot;envId&quot;: string,&quot;remoteEnvironment&quot;: {object (EnvironmentConfig)},&quot;localEnvironment&quot;: {object (LocalEnvironmentConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TurnList

> This item is deprecated\!

A list of Turns.

Fields

`turns[]` ` object ( Turn  ` )

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;turns&quot;: [{object (Turn)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Turn

> This item is deprecated\!

Fields

`role` `string`

The originator of this turn. Must be user for input or model for model output.

`content` `Union type`

`content` can be only one of the following:

`contentList` ` object ( ContentList  ` )

The content of the turn. An array of Content objects.

`contentString` `string`

The content of the turn. A single string.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;role&quot;: string,// content&quot;contentList&quot;: {object (ContentList)},&quot;contentString&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## StepList

A list of Steps.

Fields

`steps[]` ` object ( Step  ` )

The steps of the list.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;steps&quot;: [{object (Step)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ResponseFormatList

Fields

`responseFormats[]` ` object ( ResponseFormat  ` )

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;responseFormats&quot;: [{object (ResponseFormat)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ResponseFormat

Fields

`type` `Union type`

`type` can be only one of the following:

`audio` ` object ( AudioResponseFormat  ` )

`text` ` object ( TextResponseFormat  ` )

`image` ` object ( ImageResponseFormat  ` )

`video` ` object ( VideoResponseFormat  ` )

`structValue` ` object ( Struct  ` )

Multi-discriminator values is already enabled in GAOS

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;audio&quot;: {object (AudioResponseFormat)},&quot;text&quot;: {object (TextResponseFormat)},&quot;image&quot;: {object (ImageResponseFormat)},&quot;video&quot;: {object (VideoResponseFormat)},&quot;structValue&quot;: {object (Struct)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AudioResponseFormat

Configuration for audio output format.

Fields

`mimeType` ` enum ( MimeType  ` )

The MIME type of the audio output.

`delivery` ` enum ( Delivery  ` )

The delivery mode for the audio output.

`sampleRate` `integer`

Sample rate in Hz.

`bitRate` `integer`

Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;delivery&quot;: enum (Delivery),&quot;sampleRate&quot;: integer,&quot;bitRate&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## MimeType

Supported MIME types for audio output.

Enums

`TYPE_UNSPECIFIED`

Default value. This value is unused.

`TYPE_MP3`

MP3 audio format.

`TYPE_OGG_OPUS`

OGG Opus audio format.

`TYPE_L16`

Raw PCM (L16) audio format.

`TYPE_WAV`

WAV audio format.

`TYPE_ALAW`

A-law audio format.

`TYPE_MULAW`

Mu-law audio format.

## Delivery

Delivery mode for audio output.

Enums

`DELIVERY_UNSPECIFIED`

Default value. This value is unused.

`INLINE`

Audio data is returned inline in the response.

`URI`

Audio data is returned as a URI.

## TextResponseFormat

Configuration for text output format.

Fields

`mimeType` ` enum ( MimeType  ` )

The MIME type of the text output.

`schema` ` object ( Struct  ` )

The JSON schema that the output should conform to. Only applicable when mimeType is application/json.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;schema&quot;: {object (Struct)}}</code></pre></td>
</tr>
</tbody>
</table>

## MimeType

Supported MIME types for text output.

Enums

`TYPE_UNSPECIFIED`

Default value. This value is unused.

`TYPE_APPLICATION_JSON`

JSON output format.

`TYPE_TEXT_PLAIN`

Plain text output format.

## ImageResponseFormat

Configuration for image output format.

Fields

`mimeType` ` enum ( MimeType  ` )

The MIME type of the image output.

`delivery` ` enum ( Delivery  ` )

The delivery mode for the image output.

`aspectRatio` ` enum ( AspectRatio  ` )

The aspect ratio for the image output.

`imageSize` ` enum ( ImageSize  ` )

The size of the image output.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;delivery&quot;: enum (Delivery),&quot;aspectRatio&quot;: enum (AspectRatio),&quot;imageSize&quot;: enum (ImageSize)}</code></pre></td>
</tr>
</tbody>
</table>

## MimeType

Supported MIME types for image output.

Enums

`TYPE_UNSPECIFIED`

Default value. This value is unused.

`TYPE_JPEG`

JPEG image format.

## Delivery

Delivery mode for image output.

Enums

`DELIVERY_UNSPECIFIED`

Default value. This value is unused.

`INLINE`

Image data is returned inline in the response.

`URI`

Image data is returned as a URI.

## AspectRatio

Supported aspect ratios for image output.

Enums

`ASPECT_RATIO_UNSPECIFIED`

Default value. This value is unused.

`ASPECT_RATIO_ONE_BY_ONE`

1:1 aspect ratio.

`ASPECT_RATIO_TWO_BY_THREE`

2:3 aspect ratio.

`ASPECT_RATIO_THREE_BY_TWO`

3:2 aspect ratio.

`ASPECT_RATIO_THREE_BY_FOUR`

3:4 aspect ratio.

`ASPECT_RATIO_FOUR_BY_THREE`

4:3 aspect ratio.

`ASPECT_RATIO_FOUR_BY_FIVE`

4:5 aspect ratio.

`ASPECT_RATIO_FIVE_BY_FOUR`

5:4 aspect ratio.

`ASPECT_RATIO_NINE_BY_SIXTEEN`

9:16 aspect ratio.

`ASPECT_RATIO_SIXTEEN_BY_NINE`

16:9 aspect ratio.

`ASPECT_RATIO_TWENTY_ONE_BY_NINE`

21:9 aspect ratio.

`ASPECT_RATIO_ONE_BY_EIGHT`

1:8 aspect ratio.

`ASPECT_RATIO_EIGHT_BY_ONE`

8:1 aspect ratio.

`ASPECT_RATIO_ONE_BY_FOUR`

1:4 aspect ratio.

`ASPECT_RATIO_FOUR_BY_ONE`

4:1 aspect ratio.

## ImageSize

Supported image sizes for image output.

Enums

`IMAGE_SIZE_UNSPECIFIED`

Default value. This value is unused.

`IMAGE_SIZE_FIVE_TWELVE`

512px image size.

`IMAGE_SIZE_ONE_K`

1K image size.

`IMAGE_SIZE_TWO_K`

2K image size.

`IMAGE_SIZE_FOUR_K`

4K image size.

## VideoResponseFormat

Configuration for video output format.

Fields

`delivery` ` enum ( Delivery  ` )

The delivery mode for the video output.

`gcsUri` `string`

The Cloud Storage URI to store the video output. Required for Vertex if delivery mode is URI.

`aspectRatio` ` enum ( AspectRatio  ` )

The aspect ratio for the video output.

`duration` ` string ( Duration  ` format)

The duration for the video output.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (Delivery),&quot;gcsUri&quot;: string,&quot;aspectRatio&quot;: enum (AspectRatio),&quot;duration&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## Delivery

Delivery mode for video output.

Enums

`DELIVERY_UNSPECIFIED`

Default value. This value is unused.

`INLINE`

Video data is returned inline in the response.

`URI`

Video data is returned as a URI.

## AspectRatio

Supported aspect ratios for video output.

Enums

`ASPECT_RATIO_UNSPECIFIED`

Default value. This value is unused.

`ASPECT_RATIO_SIXTEEN_BY_NINE`

16:9 aspect ratio.

`ASPECT_RATIO_NINE_BY_SIXTEEN`

9:16 aspect ratio.

## ModelInteraction

Interaction for generating the completion using models.

Fields

`model` `string`

The name of the `Model` used for generating the completion.

`generationConfig` ` object ( GenerationConfig  ` )

Input only. Configuration parameters for the model interaction.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;model&quot;: string,&quot;generationConfig&quot;: {object (GenerationConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## GenerationConfig

Configuration parameters for model interactions.

Fields

`temperature` `number`

Controls the randomness of the output.

`topP` `number`

The maximum cumulative probability of tokens to consider when sampling.

`seed` `integer`

Seed used in decoding for reproducibility.

`stopSequences[]` `string`

A list of character sequences that will stop output interaction.

`thinkingLevel` ` enum ( ThinkingLevel  ` )

The level of thought tokens that the model should generate.

`thinkingSummaries` ` enum ( ThinkingSummaries  ` )

Whether to include thought summaries in the response.

`maxOutputTokens` `integer`

The maximum number of tokens to include in the response.

`speechConfig[]` ` object ( SpeechConfig  ` )

Configuration for speech interaction.

` imageConfig (deprecated)  ` ` object ( ImageConfig  ` )

> This item is deprecated\!

Configuration for image interaction.

`videoConfig` ` object ( VideoConfig  ` )

Configuration for video generation.

`transcriptionConfig` ` object ( TranscriptionConfig  ` )

Optional. Configuration for speech recognition (transcription). If present, ASR is enabled.

`tool_choice` `Union type`

The tool choice configuration. `tool_choice` can be only one of the following:

`toolChoiceMode` ` enum ( ToolChoiceType  ` )

The mode of the tool choice.

`toolChoiceConfig` ` object ( ToolChoiceConfig  ` )

The config for the tool choice.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;temperature&quot;: number,&quot;topP&quot;: number,&quot;seed&quot;: integer,&quot;stopSequences&quot;: [string],&quot;thinkingLevel&quot;: enum (ThinkingLevel),&quot;thinkingSummaries&quot;: enum (ThinkingSummaries),&quot;maxOutputTokens&quot;: integer,&quot;speechConfig&quot;: [{object (SpeechConfig)}],&quot;imageConfig&quot;: {object (ImageConfig)},&quot;videoConfig&quot;: {object (VideoConfig)},&quot;transcriptionConfig&quot;: {object (TranscriptionConfig)},// tool_choice&quot;toolChoiceMode&quot;: enum (ToolChoiceType),&quot;toolChoiceConfig&quot;: {object (ToolChoiceConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ToolChoiceType

The type of tool choice.

Enums

`TOOL_CHOICE_TYPE_UNSPECIFIED`

Default value. This value is unused.

`AUTO`

Auto tool choice.

`ANY`

Any tool choice.

`NONE`

No tool choice.

`VALIDATED`

Validated tool choice.

## ToolChoiceConfig

The tool choice configuration containing allowed tools.

Fields

`allowedTools` ` object ( AllowedTools  ` )

The allowed tools.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;allowedTools&quot;: {object (AllowedTools)}}</code></pre></td>
</tr>
</tbody>
</table>

## AllowedTools

The configuration for allowed tools.

Fields

`mode` ` enum ( ToolChoiceType  ` )

The mode of the tool choice.

`tools[]` `string`

The names of the allowed tools.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mode&quot;: enum (ToolChoiceType),&quot;tools&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## ThinkingLevel

The level of thought tokens that the model should generate.

Enums

`THINKING_LEVEL_UNSPECIFIED`

Default value. This value is unused.

`THINKING_LEVEL_MINIMAL`

Little to no thinking.

`THINKING_LEVEL_LOW`

Low thinking level.

`THINKING_LEVEL_MEDIUM`

Medium thinking level.

`THINKING_LEVEL_HIGH`

High thinking level.

## ThinkingSummaries

Whether to include thought summaries in the response.

Enums

`THINKING_SUMMARIES_UNSPECIFIED`

Default value. This value is unused.

`THINKING_SUMMARIES_AUTO`

Auto thinking summaries.

`THINKING_SUMMARIES_NONE`

No thinking summaries.

## SpeechConfig

The configuration for speech interaction.

Fields

`voice` `string`

The voice of the speaker.

`language` `string`

The language of the speech.

`speaker` `string`

The speaker's name, it should match the speaker name given in the prompt.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;voice&quot;: string,
  &quot;language&quot;: string,
  &quot;speaker&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ImageConfig

The configuration for image interaction.

Fields

`aspectRatio` `string`

The aspect ratio of the image to generate. Supported aspect ratios: 1:1, 2:3, 3:2, 3:4, 4:3, 9:16, 16:9, 21:9.

If not specified, the model will choose a default aspect ratio based on any reference images provided.

`imageSize` `string`

Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;aspectRatio&quot;: string,
  &quot;imageSize&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## VideoConfig

Configuration options for video generation.

Fields

`task` ` enum ( Task  ` )

Optional task mode for video generation. If not specified, the model automatically determines the appropriate mode based on the provided text prompt and input media.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;task&quot;: enum (Task)}</code></pre></td>
</tr>
</tbody>
</table>

## Task

Supported video generation tasks.

Enums

`TASK_UNSPECIFIED`

Unspecified task. The task is inferred from the input prompt and media.

`TEXT_TO_VIDEO`

Generates video solely from a text prompt.

`IMAGE_TO_VIDEO`

Generates video from one or two source images. The first image defines the starting frame, and the optional second image defines the ending frame.

`REFERENCE_TO_VIDEO`

Generates video using reference media (such as images, audio, or video).

`EDIT`

Modifies an existing input video.

## TranscriptionConfig

Configuration for speech recognition (transcription).

Fields

`timestampGranularities[]` `string`

Optional. The granularity of timestamps to include in the transcription output. Supported values: "word". If empty, no timestamps are generated.

`diarizationMode` `string`

Optional. Configures speaker diarization. Supported values: "speaker".

`languageCodes[]` `string`

Optional. BCP-47 language codes providing hints about the languages present in the audio. If omitted or empty, defaults to automatic language detection.

` adaptationPhrases[] (deprecated)  ` `string`

> This item is deprecated\!

Optional. A list of phrases to bias the ASR model towards.

`customVocabulary[]` `string`

Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;timestampGranularities&quot;: [
    string
  ],
  &quot;diarizationMode&quot;: string,
  &quot;languageCodes&quot;: [
    string
  ],
  &quot;adaptationPhrases&quot;: [
    string
  ],
  &quot;customVocabulary&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## AgentInteraction

Interaction for generating the completion using agents.

Fields

`agent` `string`

The name of the `Agent` used for generating the completion.

`agent_config` `Union type`

Parameters for the agent interaction. `agent_config` can be only one of the following:

`dynamicConfig` ` object ( DynamicAgentConfig  ` )

`deepResearchConfig` ` object ( DeepResearchAgentConfig  ` )

`codeMenderConfig` ` object ( CodeMenderAgentConfig  ` )

`antigravityConfig` ` object ( AntigravityAgentConfig  ` )

Antigravity agent configuration. This configuration is session-level settings that are passed to the agent runtime on a per-request basis.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agent&quot;: string,// agent_config&quot;dynamicConfig&quot;: {object (DynamicAgentConfig)},&quot;deepResearchConfig&quot;: {object (DeepResearchAgentConfig)},&quot;codeMenderConfig&quot;: {object (CodeMenderAgentConfig)},&quot;antigravityConfig&quot;: {object (AntigravityAgentConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DynamicAgentConfig

Configuration for dynamic agents.

Fields

`config` ` object ( Struct  ` )

For agents that are not supported statically in the API definition.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;config&quot;: {object (Struct)}}</code></pre></td>
</tr>
</tbody>
</table>

## DeepResearchAgentConfig

Configuration for the Deep Research agent.

Fields

`thinkingSummaries` ` enum ( ThinkingSummaries  ` )

Whether to include thought summaries in the response.

`visualization` ` enum ( VisualizationMode  ` )

Whether to include visualizations in the response.

`collaborativePlanning` `boolean`

Enables human-in-the-loop planning for the Deep Research agent. If set to true, the Deep Research agent will provide a research plan in its response. The agent will then proceed only if the user confirms the plan in the next turn.

`enableBigqueryTool` `boolean`

Enables bigquery tool for the Deep Research agent.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;thinkingSummaries&quot;: enum (ThinkingSummaries),&quot;visualization&quot;: enum (VisualizationMode),&quot;collaborativePlanning&quot;: boolean,&quot;enableBigqueryTool&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## VisualizationMode

Enum for visualization mode. Eventually we will support an interactive mode where the user can choose whether to include HTML visualizations in the response.

Enums

`UNSPECIFIED`

The default visualization mode. Will default to AUTO.

`OFF`

Do not include visualizations.

`AUTO`

Automatically include visualizations.

## CodeMenderAgentConfig

Configuration for the CodeMender agent.

Fields

`session_id` `string`

Parameter for grouping multiple interactions that belong to the same CodeMender session.

`session_config` ` object ( SessionConfig  ` )

Optional session-specific configurations to override default agent behavior.

`model` `string`

The name of the model to use for the CodeMender agent. One CodeMender session will only use one model.

`request` `Union type`

CodeMender's request type. Set exactly one of find\_request/fix\_request only on the first round to start a session; on subsequent rounds (e.g. submitting tool results), leave this unset and identify the session via session\_id. This oneof is intentionally not a subtype\_source discriminator so it can be omitted on resume rounds. `request` can be only one of the following:

`find_request` ` object ( FindRequest  ` )

Parameters for finding vulnerabilities.

`fix_request` ` object ( FixRequest  ` )

Parameters for fixing vulnerabilities.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;session_id&quot;: string,&quot;session_config&quot;: {object (SessionConfig)},&quot;model&quot;: string,// request&quot;find_request&quot;: {object (FindRequest)},&quot;fix_request&quot;: {object (FixRequest)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FindRequest

Request parameters specific to FIND sessions, used for discovering vulnerabilities in a codebase.

Fields

`source_files[]` ` object ( FileContent  ` )

A list of source files to provide as context for the scan.

`finding_id` `string`

The identifier of a specific finding to verify. This is primarily used in VERIFY mode to focus the agent's execution-based validation on a single vulnerability.

`description` `string`

Additional context or custom instructions provided by the user to guide the vulnerability analysis.

`mode` ` enum ( Mode  ` )

The mode of the find session.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;source_files&quot;: [{object (FileContent)}],&quot;finding_id&quot;: string,&quot;description&quot;: string,&quot;mode&quot;: enum (Mode)}</code></pre></td>
</tr>
</tbody>
</table>

## FileContent

Content of a single file in the codebase.

Fields

`path` `string`

The relative path of the file from the project root.

`content` `string`

The UTF-8 encoded text content of the file.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;path&quot;: string,
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Mode

Defines the depth and thoroughness of the find session.

Enums

`MODE_UNSPECIFIED`

Default value. This value is unused.

`MODE_SCAN`

Fast scan using only the initial classifier.

`MODE_VERIFY`

Performs classification followed by detailed investigation.

## FixRequest

Request parameters specific to FIX sessions, used for generating and validating security patches.

Fields

`source_files[]` ` object ( FileContent  ` )

A list of source files providing context for the remediation. These files are typically the ones containing the identified vulnerability.

`finding_id` `string`

The identifier of the specific security finding to be remediated. This id maps to a previously discovered vulnerability.

`description` `string`

Additional context or custom instructions provided by the user to guide the patch generation process.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;source_files&quot;: [{object (FileContent)}],&quot;finding_id&quot;: string,&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## SessionConfig

The configuration of CodeMender sessions.

Fields

`max_rounds` `integer`

The maximum number of interaction rounds the agent is allowed to perform before reaching a timeout.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;max_rounds&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## AntigravityAgentConfig

Configuration for the Antigravity agent runtime. Provides server-side control over the agent's execution environment and tool configuration.

Fields

`model` `string`

The model to use for agent reasoning.

`maxTotalTokens` `string ( int64 format)`

Max total tokens for the agent run.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;model&quot;: string,
  &quot;maxTotalTokens&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## EnvironmentConfig

Configuration for a custom environment.

Fields

`sources[]` ` object ( Source  ` )

`environmentId` `string`

Optional. The environment id for the interaction. If specified, the request will update the existing environment instead of creating a new one.

`network` `Union type`

Network configuration for the environment. `network` can be only one of the following:

`network_allowlist` ` object ( EnvironmentNetworkEgressAllowlist  ` )

Allow only specific domains.

`network_mode` ` enum ( NetworkMode  ` )

Network egress mode.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sources&quot;: [{object (Source)}],&quot;environmentId&quot;: string,// network&quot;network_allowlist&quot;: {object (EnvironmentNetworkEgressAllowlist)},&quot;network_mode&quot;: enum (NetworkMode)// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## EnvironmentNetworkEgressAllowlist

Network egress configuration for the environment.

Fields

`allowlist[]` ` object ( EgressRule  ` )

List of allowed domains and their configurations.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;allowlist&quot;: [{object (EgressRule)}]}</code></pre></td>
</tr>
</tbody>
</table>

## EgressRule

A network egress rule that controls which external domains the environment is allowed to reach. Each rule identifies a target domain and, optionally, a set of HTTP headers to inject into every matching outbound request.

Fields

`domain` `string`

The domain pattern to match for this rule. Use an exact hostname (e.g., `github.com` ), a wildcard prefix (e.g., `*.googleapis.com` ), or `*` to match all domains.

`transform` `map (key: string, value: string)`

headers to inject into requests matching this rule. Key: header name (e.g., "Authorization"). value: header value (e.g., "Bearer your-token").

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;domain&quot;: string,
  &quot;transform&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## NetworkMode

Network egress mode for non-allowlist configurations.

Enums

`NETWORK_MODE_UNSPECIFIED`

Default value. Unused.

`DISABLED`

All network egress is blocked.

## Source

A source to be mounted into the environment.

Fields

`type` ` enum ( Type  ` )

`source` `string`

The source of the environment. For Cloud Storage, this is the Cloud Storage path. For GitHub, this is the GitHub path.

`target` `string`

Where the source should appear in the environment.

`content` `string`

The inline content if `type` is `INLINE` .

`encoding` `string`

Optional encoding for inline content (e.g. `base64` ).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;source&quot;: string,&quot;target&quot;: string,&quot;content&quot;: string,&quot;encoding&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## Type

Enums

`TYPE_UNSPECIFIED`

`GCS`

A Cloud Storage bucket.

`INLINE`

Inline content.

`REPOSITORY`

A generic repository. The protocol prefix in the source URL identifies the provider (e.g., github://, <gcs://)> .

`SKILL_REGISTRY`

A skill resource from the Skill Registry service. Skill: projects/{project}/locations/{location}/skills/{skill} SkillRevision: projects/{project}/locations/{location}/skills/{skill}/revisions/{revision} Support mounting all skills under a project: projects/{project}/locations/{location}/skills.

## LocalEnvironmentConfig

This type has no fields.

Configuration for an environment that lives on the client connection rather than in a server-managed sandbox.

When set (via Interaction.local\_environment), the agent's filesystem and shell are treated as living on the client: the agent's built-in environment operations (e.g. reading/listing/editing files and running commands) are suspended on the server and yielded back to the client to execute, with their results returned on a subsequent turn. This is mutually exclusive with a server-managed `EnvironmentConfig` (remoteEnvironment), since the environment is either on the client or in a server sandbox, never both.

This governs only the agent's built-in environment. client-declared function tools are always executed on the client regardless of this field.

## Tool

A tool that can be used by the model.

Fields

`type` `Union type`

The tool to use. `type` can be only one of the following:

`function` ` object ( Function  ` )

A function that can be used by the model.

`codeExecution` ` object ( CodeExecution  ` )

A tool that can be used by the model to execute code.

`urlContext` ` object ( UrlContext  ` )

A tool that can be used by the model to fetch URL context.

`computerUse` ` object ( ComputerUse  ` )

Tool to support the model interacting directly with the computer.

`mcpServer` ` object ( McpServer  ` )

A MCPServer is a server that can be called by the model to perform actions.

`googleSearch` ` object ( GoogleSearch  ` )

A tool that can be used by the model to search Google.

`fileSearch` ` object ( FileSearch  ` )

A tool that can be used by the model to search files.

`googleMaps` ` object ( GoogleMaps  ` )

A tool that can be used by the model to search Google Maps.

`retrieval` ` object ( Retrieval  ` )

A tool that can be used by the model to retrieve files.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;function&quot;: {object (Function)},&quot;codeExecution&quot;: {object (CodeExecution)},&quot;urlContext&quot;: {object (UrlContext)},&quot;computerUse&quot;: {object (ComputerUse)},&quot;mcpServer&quot;: {object (McpServer)},&quot;googleSearch&quot;: {object (GoogleSearch)},&quot;fileSearch&quot;: {object (FileSearch)},&quot;googleMaps&quot;: {object (GoogleMaps)},&quot;retrieval&quot;: {object (Retrieval)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Function

A tool that can be used by the model.

Fields

`name` `string`

The name of the function.

`description` `string`

A description of the function.

`parameters` ` object ( Value  ` )

The JSON Schema for the function's parameters.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;parameters&quot;: {object (Value)}}</code></pre></td>
</tr>
</tbody>
</table>

## CodeExecution

This type has no fields.

A tool that can be used by the model to execute code.

## UrlContext

This type has no fields.

A tool that can be used by the model to fetch URL context.

## ComputerUse

A tool that can be used by the model to interact with the computer.

Fields

`environment` ` enum ( Environment  ` )

The environment being operated.

`excludedPredefinedFunctions[]` `string`

The list of predefined functions that are excluded from the model call.

`enablePromptInjectionDetection` `boolean`

Whether enable the prompt injection detection check on computer-use request.

`disabledSafetyPolicies[]` ` enum ( SafetyPolicy  ` )

Optional. disabled safety policies for computer use.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;environment&quot;: enum (Environment),&quot;excludedPredefinedFunctions&quot;: [string],&quot;enablePromptInjectionDetection&quot;: boolean,&quot;disabledSafetyPolicies&quot;: [enum (SafetyPolicy)]}</code></pre></td>
</tr>
</tbody>
</table>

## Environment

Represents the environment being operated, such as a web browser.

Enums

`ENVIRONMENT_UNSPECIFIED`

Defaults to browser.

`BROWSER`

Operates in a web browser.

`MOBILE`

Operates in a mobile environment.

`DESKTOP`

Operates in a desktop environment.

## SafetyPolicy

Enums

`SAFETY_POLICY_UNSPECIFIED`

Unspecified safety policy.

`FINANCIAL_TRANSACTIONS`

Safety policy for financial transactions.

`SENSITIVE_DATA_MODIFICATION`

Safety policy for sensitive data modification.

`COMMUNICATION_TOOL`

Safety policy for communication tools (e.g. Gmail, Chat, Meet).

`ACCOUNT_CREATION`

Safety policy for account creation.

`DATA_MODIFICATION`

Safety policy for data modification.

`USER_CONSENT_MANAGEMENT`

Safety policy for user consent management.

`LEGAL_TERMS_AND_AGREEMENTS`

Safety policy for legal terms and agreements.

## McpServer

A MCPServer is a server that can be called by the model to perform actions.

Fields

`name` `string`

The name of the MCPServer.

`url` `string`

The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"

`headers` `map (key: string, value: string)`

Optional: Fields for authentication headers, timeouts, etc., if needed.

`allowedTools[]` ` object ( AllowedTools  ` )

The allowed tools.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;url&quot;: string,&quot;headers&quot;: {string: string,...},&quot;allowedTools&quot;: [{object (AllowedTools)}]}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleSearch

A tool that can be used by the model to search Google.

Fields

`searchTypes[]` ` enum ( SearchType  ` )

The types of search grounding to enable.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchTypes&quot;: [enum (SearchType)]}</code></pre></td>
</tr>
</tbody>
</table>

## FileSearch

A tool that can be used by the model to search files.

Fields

`fileSearchStoreNames[]` `string`

The file search store names to search.

`topK` `integer`

The number of semantic retrieval chunks to retrieve.

`metadataFilter` `string`

metadata filter to apply to the semantic retrieval documents and chunks.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fileSearchStoreNames&quot;: [
    string
  ],
  &quot;topK&quot;: integer,
  &quot;metadataFilter&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleMaps

A tool that can be used by the model to call Google Maps.

Fields

`enableWidget` `boolean`

Whether to return a widget context token in the tool call result of the response.

`latitude` `number`

The latitude of the user's location.

`longitude` `number`

The longitude of the user's location.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;enableWidget&quot;: boolean,
  &quot;latitude&quot;: number,
  &quot;longitude&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## Retrieval

A tool that can be used by the model to retrieve files.

Fields

`retrievalTypes[]` ` enum ( RetrievalType  ` )

The types of file retrieval to enable.

`vertex_ai_search_config` ` object ( VertexAISearchConfig  ` )

Used to specify configuration for VertexAISearch.

`exa_ai_search_config` ` object ( ExaAISearchConfig  ` )

Used to specify configuration for ExaAISearch.

`parallel_ai_search_config` ` object ( ParallelAISearchConfig  ` )

Used to specify configuration for ParallelAISearch.

`rag_store_config` ` object ( RagStoreConfig  ` )

Used to specify configuration for RagStore.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;retrievalTypes&quot;: [enum (RetrievalType)],&quot;vertex_ai_search_config&quot;: {object (VertexAISearchConfig)},&quot;exa_ai_search_config&quot;: {object (ExaAISearchConfig)},&quot;parallel_ai_search_config&quot;: {object (ParallelAISearchConfig)},&quot;rag_store_config&quot;: {object (RagStoreConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## VertexAISearchConfig

Used to specify configuration for VertexAISearch.

Fields

`engine` `string`

Optional. Used to specify Agent Platform Search engine.

`datastores[]` `string`

Optional. Used to specify Agent Platform Search datastores.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;engine&quot;: string,
  &quot;datastores&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## ExaAISearchConfig

Used to specify configuration for ExaAISearch.

Fields

`api_key` `string`

Required. The API key for ExaAiSearch.

`custom_config` ` object ( Struct  ` format)

Optional. This field can be used to pass any parameter from the Exa.ai Search API.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;api_key&quot;: string,
  &quot;custom_config&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## ParallelAISearchConfig

Used to specify configuration for ParallelAISearch.

Fields

`api_key` `string`

Optional. The API key for ParallelAiSearch.

`custom_config` ` object ( Struct  ` format)

Optional. Custom configs for ParallelAiSearch.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;api_key&quot;: string,
  &quot;custom_config&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## RagStoreConfig

Use to specify configuration for RAG Store.

Fields

`rag_resources[]` ` object ( RagResource  ` )

Optional. The representation of the rag source.

` similarity_top_k (deprecated)  ` `integer`

> This item is deprecated\!

Optional. Number of top k results to return from the selected corpora.

` vector_distance_threshold (deprecated)  ` `number`

> This item is deprecated\!

Optional. Only return results with vector distance smaller than the threshold.

`rag_retrieval_config` ` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the Rag query.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rag_resources&quot;: [{object (RagResource)}],&quot;similarity_top_k&quot;: integer,&quot;vector_distance_threshold&quot;: number,&quot;rag_retrieval_config&quot;: {object (RagRetrievalConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RagResource

The definition of the Rag resource.

Fields

`rag_corpus` `string`

Optional. RagCorpora resource name.

`rag_file_ids[]` `string`

Optional. ragFileId. The files should be in the same ragCorpus set in ragCorpus field.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;rag_corpus&quot;: string,
  &quot;rag_file_ids&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## RagRetrievalConfig

Specifies the context retrieval config.

Fields

`top_k` `integer`

Optional. The number of contexts to retrieve.

`hybrid_search` ` object ( HybridSearch  ` )

Optional. Config for Hybrid Search.

`filter` ` object ( Filter  ` )

Optional. Config for filters.

`ranking` ` object ( Ranking  ` )

Optional. Config for ranking and reranking.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;top_k&quot;: integer,&quot;hybrid_search&quot;: {object (HybridSearch)},&quot;filter&quot;: {object (Filter)},&quot;ranking&quot;: {object (Ranking)}}</code></pre></td>
</tr>
</tbody>
</table>

## HybridSearch

Config for Hybrid Search.

Fields

`alpha` `number`

Optional. Alpha value controls the weight between dense and sparse vector search results.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;alpha&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## Filter

Config for filters.

Fields

`metadata_filter` `string`

Optional. String for metadata filtering.

`vector_db_threshold` `Union type`

Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following:

`vector_distance_threshold` `number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vector_similarity_threshold` `number`

Optional. Only returns contexts with vector similarity larger than the threshold.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;metadata_filter&quot;: string,

  // vector_db_threshold
  &quot;vector_distance_threshold&quot;: number,
  &quot;vector_similarity_threshold&quot;: number
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Ranking

Config for ranking and reranking.

Fields

`ranking_config` `Union type`

Config options for ranking. `ranking_config` can be only one of the following:

`rank_service` ` object ( RankService  ` )

Optional. Config for Rank service.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// ranking_config&quot;rank_service&quot;: {object (RankService)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RankService

Config for Rank service.

Fields

`model_name` `string`

Optional. The model name of the rank service.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;model_name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SafetySetting

A safety setting that affects the safety-blocking behavior.

A `SafetySetting` consists of a harm `category` and a `threshold` for that category.

Fields

`type` ` enum ( HarmCategory  ` )

Required. The type of harm category to be blocked.

`threshold` ` enum ( HarmBlockThreshold  ` )

Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked.

`method` ` enum ( HarmBlockMethod  ` )

Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (HarmCategory),&quot;threshold&quot;: enum (HarmBlockThreshold),&quot;method&quot;: enum (HarmBlockMethod)}</code></pre></td>
</tr>
</tbody>
</table>

## HarmCategory

Harm categories that can be detected in user input and model responses.

Enums

`HARM_CATEGORY_UNSPECIFIED`

Default value. This value is unused.

`HARM_CATEGORY_HATE_SPEECH`

Content that promotes violence or incites hatred against individuals or groups based on certain attributes.

`HARM_CATEGORY_DANGEROUS_CONTENT`

Content that promotes, facilitates, or enables dangerous activities.

`HARM_CATEGORY_HARASSMENT`

Abusive, threatening, or content intended to bully, torment, or ridicule.

`HARM_CATEGORY_SEXUALLY_EXPLICIT`

Content that contains sexually explicit material.

`HARM_CATEGORY_CIVIC_INTEGRITY`

Deprecated: Election filter is not longer supported. The harm category is civic integrity.

> This item is deprecated\!

`HARM_CATEGORY_IMAGE_HATE`

Images that contain hate speech.

`HARM_CATEGORY_IMAGE_DANGEROUS_CONTENT`

Images that contain dangerous content.

`HARM_CATEGORY_IMAGE_HARASSMENT`

Images that contain harassment.

`HARM_CATEGORY_IMAGE_SEXUALLY_EXPLICIT`

Images that contain sexually explicit content.

`HARM_CATEGORY_JAILBREAK`

Prompts designed to bypass safety filters.

## HarmBlockThreshold

Thresholds for blocking content based on harm probability.

Enums

`HARM_BLOCK_THRESHOLD_UNSPECIFIED`

The harm block threshold is unspecified.

`BLOCK_LOW_AND_ABOVE`

Block content with a low harm probability or higher.

`BLOCK_MEDIUM_AND_ABOVE`

Block content with a medium harm probability or higher.

`BLOCK_ONLY_HIGH`

Block content with a high harm probability.

`BLOCK_NONE`

Do not block any content, regardless of its harm probability.

`OFF`

Turn off the safety filter entirely.

## HarmBlockMethod

The method for blocking content.

Enums

`HARM_BLOCK_METHOD_UNSPECIFIED`

The harm block method is unspecified.

`SEVERITY`

The harm block method uses both probability and severity scores.

`PROBABILITY`

The harm block method uses the probability score.
