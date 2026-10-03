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

`status` `enum ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Status)` )`

Required. Output only. The status of the interaction.

`created` `string`

Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`updated` `string`

Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`systemInstruction` `string`

System instruction for the interaction.

`tools[]` `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Tool)` )`

A list of tool declarations the model may call during interaction.

`usage` `object ( `[`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage)` )`

Output only. Statistics on the interaction request's token usage.

`responseModalities[] `**`(deprecated)`** `enum ( `[`ResponseModality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ResponseModality)` )`

> This item is deprecated!

The requested modalities of the response (TEXT, IMAGE, AUDIO).

`responseMimeType `**`(deprecated)`** `string`

> This item is deprecated!

The mime type of the response. This is required if responseFormat is set.

`previousInteractionId` `string`

The id of the previous interaction, if any.

`environmentId` `string`

Output only. The environment id for the interaction. Only populated if environment config is set in the request.

`steps[]` `object ( `[`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step)` )`

Required. Output only. The steps that make up the interaction, when included in the response.

`safetySettings[]` `object ( `[`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#SafetySetting)` )`

Safety settings for the interaction.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata for the request.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`errors[]` `object ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Error)` )`

Output only. Diagnostic faults / platform errors recorded on the interaction.

`input` `Union type`

The input for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`contentList `**`(deprecated)`** `object ( `[`ContentList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ContentList)` )`

> This item is deprecated!

The inputs for the interaction.

`stringContent` `string`

A string input for the interaction, it will be processed as a single text input.

`turnList `**`(deprecated)`** `object ( ``TurnList`` )`

> This item is deprecated!

The turns for the interaction.

`stepList` `object ( `[`StepList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#StepList)` )`

Input only. The steps for the interaction.

`content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content)` )`

The content for the interaction.

End of mutually exclusive fields.

`response_format_config` `Union type`

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`responseFormat `**`(deprecated)`** `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

> This item is deprecated!

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field.

`responseFormatList` `object ( `[`ResponseFormatList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ResponseFormatList)` )`

`responseFormatSingleton` `object ( `[`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ResponseFormat)` )`

End of mutually exclusive fields.

`request_type` `Union type`

The request type for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`modelInteraction` `object ( `[`ModelInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ModelInteraction)` )`

Interaction for generating the completion using models.

`agentInteraction` `object ( `[`AgentInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AgentInteraction)` )`

Interaction for generating the completion using agents.

End of mutually exclusive fields.

`environment` `Union type`

The environment configuration for the interaction. Can be an object specifying remote environment sources or a string referencing an existing environment ID. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`envId` `string`

The environment id for the interaction. Can be 'remote' for default environment.

`remoteEnvironment` `object ( `[`EnvironmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#EnvironmentConfig)` )`

`localEnvironment` `object ( `[`LocalEnvironmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#LocalEnvironmentConfig)` )`

The agent's environment lives on the client connection: its built-in environment operations (filesystem ops and running commands) are yielded to the client to execute, instead of running in a server-managed sandbox. Mutually exclusive with `remoteEnvironment` . (Independent of any client-declared function tools, which are always executed on the client regardless of this field.)

End of mutually exclusive fields.

**JSON representation**

```
{
  "id": string,
  "status": enum (Status),
  "created": string,
  "updated": string,
  "systemInstruction": string,
  "tools": [
    {
      object (Tool)
    }
  ],
  "usage": {
    object (Usage)
  },
  "responseModalities": [
    enum (ResponseModality)
  ],
  "responseMimeType": string,
  "previousInteractionId": string,
  "environmentId": string,
  "steps": [
    {
      object (Step)
    }
  ],
  "safetySettings": [
    {
      object (SafetySetting)
    }
  ],
  "labels": {
    string: string,
    ...
  },
  "errors": [
    {
      object (Error)
    }
  ],

  // input
  "contentList": {
    object (ContentList)
  },
  "stringContent": string,
  "turnList": {
    object (TurnList)
  },
  "stepList": {
    object (StepList)
  },
  "content": {
    object (Content)
  }
  // Union type

  // response_format_config
  "responseFormat": {
    object (Value)
  },
  "responseFormatList": {
    object (ResponseFormatList)
  },
  "responseFormatSingleton": {
    object (ResponseFormat)
  }
  // Union type

  // request_type
  "modelInteraction": {
    object (ModelInteraction)
  },
  "agentInteraction": {
    object (AgentInteraction)
  }
  // Union type

  // environment
  "envId": string,
  "remoteEnvironment": {
    object (EnvironmentConfig)
  },
  "localEnvironment": {
    object (LocalEnvironmentConfig)
  }
  // Union type
}
```

## StepList

A list of Steps.

Fields

`steps[]` `object ( `[`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step)` )`

The steps of the list.

**JSON representation**

```
{
  "steps": [
    {
      object (Step)
    }
  ]
}
```

## ResponseFormatList

Fields

`responseFormats[]` `object ( `[`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ResponseFormat)` )`

**JSON representation**

```
{
  "responseFormats": [
    {
      object (ResponseFormat)
    }
  ]
}
```

## ResponseFormat

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`audio` `object ( `[`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AudioResponseFormat)` )`

`text` `object ( `[`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#TextResponseFormat)` )`

`image` `object ( `[`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ImageResponseFormat)` )`

`video` `object ( `[`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#VideoResponseFormat)` )`

`structValue` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

Multi-discriminator values is already enabled in GAOS

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "audio": {
    object (AudioResponseFormat)
  },
  "text": {
    object (TextResponseFormat)
  },
  "image": {
    object (ImageResponseFormat)
  },
  "video": {
    object (VideoResponseFormat)
  },
  "structValue": {
    object (Struct)
  }
  // Union type
}
```

## AudioResponseFormat

Configuration for audio output format.

Fields

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#MimeType)` )`

The MIME type of the audio output.

`delivery` `enum ( `[`Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Delivery)` )`

The delivery mode for the audio output.

`sampleRate` `integer`

Sample rate in Hz.

`bitRate` `integer`

Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "delivery": enum (Delivery),
  "sampleRate": integer,
  "bitRate": integer
}
```

## MimeType

Supported MIME types for audio output.

| Enums              |                                      |
|--------------------|--------------------------------------|
| `TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `TYPE_MP3`         | MP3 audio format.                    |
| `TYPE_OGG_OPUS`    | OGG Opus audio format.               |
| `TYPE_L16`         | Raw PCM (L16) audio format.          |
| `TYPE_WAV`         | WAV audio format.                    |
| `TYPE_ALAW`        | A-law audio format.                  |
| `TYPE_MULAW`       | Mu-law audio format.                 |

## Delivery

Delivery mode for audio output.

| Enums                  |                                                |
|------------------------|------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.           |
| `INLINE`               | Audio data is returned inline in the response. |
| `URI`                  | Audio data is returned as a URI.               |

## TextResponseFormat

Configuration for text output format.

Fields

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#MimeType_1)` )`

The MIME type of the text output.

`schema` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

The JSON schema that the output should conform to. Only applicable when mimeType is application/json.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "schema": {
    object (Struct)
  }
}
```

## MimeType

Supported MIME types for text output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `TYPE_UNSPECIFIED`      | Default value. This value is unused. |
| `TYPE_APPLICATION_JSON` | JSON output format.                  |
| `TYPE_TEXT_PLAIN`       | Plain text output format.            |

## ImageResponseFormat

Configuration for image output format.

Fields

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#MimeType_2)` )`

The MIME type of the image output.

`delivery` `enum ( `[`Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Delivery_1)` )`

The delivery mode for the image output.

`aspectRatio` `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AspectRatio)` )`

The aspect ratio for the image output.

`imageSize` `enum ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ImageSize)` )`

The size of the image output.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "delivery": enum (Delivery),
  "aspectRatio": enum (AspectRatio),
  "imageSize": enum (ImageSize)
}
```

## MimeType

Supported MIME types for image output.

| Enums              |                                      |
|--------------------|--------------------------------------|
| `TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `TYPE_JPEG`        | JPEG image format.                   |

## Delivery

Delivery mode for image output.

| Enums                  |                                                |
|------------------------|------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.           |
| `INLINE`               | Image data is returned inline in the response. |
| `URI`                  | Image data is returned as a URI.               |

## AspectRatio

Supported aspect ratios for image output.

| Enums                             |                                      |
|-----------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`        | Default value. This value is unused. |
| `ASPECT_RATIO_ONE_BY_ONE`         | 1:1 aspect ratio.                    |
| `ASPECT_RATIO_TWO_BY_THREE`       | 2:3 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_TWO`       | 3:2 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_FOUR`      | 3:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_THREE`      | 4:3 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_FIVE`       | 4:5 aspect ratio.                    |
| `ASPECT_RATIO_FIVE_BY_FOUR`       | 5:4 aspect ratio.                    |
| `ASPECT_RATIO_NINE_BY_SIXTEEN`    | 9:16 aspect ratio.                   |
| `ASPECT_RATIO_SIXTEEN_BY_NINE`    | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_TWENTY_ONE_BY_NINE` | 21:9 aspect ratio.                   |
| `ASPECT_RATIO_ONE_BY_EIGHT`       | 1:8 aspect ratio.                    |
| `ASPECT_RATIO_EIGHT_BY_ONE`       | 8:1 aspect ratio.                    |
| `ASPECT_RATIO_ONE_BY_FOUR`        | 1:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_ONE`        | 4:1 aspect ratio.                    |

## ImageSize

Supported image sizes for image output.

| Enums                    |                                      |
|--------------------------|--------------------------------------|
| `IMAGE_SIZE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_SIZE_FIVE_TWELVE` | 512px image size.                    |
| `IMAGE_SIZE_ONE_K`       | 1K image size.                       |
| `IMAGE_SIZE_TWO_K`       | 2K image size.                       |
| `IMAGE_SIZE_FOUR_K`      | 4K image size.                       |

## VideoResponseFormat

Configuration for video output format.

Fields

`delivery` `enum ( `[`Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Delivery_2)` )`

The delivery mode for the video output.

`gcsUri` `string`

The Cloud Storage URI to store the video output. Required for Vertex if delivery mode is URI.

`aspectRatio` `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AspectRatio_1)` )`

The aspect ratio for the video output.

`duration` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The duration for the video output.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`resolution` `enum ( `[`Resolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Resolution)` )`

The video output resolution. Defaults to 720p.

**JSON representation**

```
{
  "delivery": enum (Delivery),
  "gcsUri": string,
  "aspectRatio": enum (AspectRatio),
  "duration": string,
  "resolution": enum (Resolution)
}
```

## Delivery

Delivery mode for video output.

| Enums                  |                                                |
|------------------------|------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.           |
| `INLINE`               | Video data is returned inline in the response. |
| `URI`                  | Video data is returned as a URI.               |

## AspectRatio

Supported aspect ratios for video output.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`     | Default value. This value is unused. |
| `ASPECT_RATIO_SIXTEEN_BY_NINE` | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_NINE_BY_SIXTEEN` | 9:16 aspect ratio.                   |

## Resolution

Supported resolutions for video output.

| Enums                       |                                      |
|-----------------------------|--------------------------------------|
| `RESOLUTION_UNSPECIFIED`    | Default value. This value is unused. |
| `RESOLUTION_THREE_SIXTY_P`  | 360p resolution.                     |
| `RESOLUTION_SEVEN_TWENTY_P` | 720p resolution.                     |
| `RESOLUTION_TEN_EIGHTY_P`   | 1080p resolution.                    |
| `RESOLUTION_FOUR_K`         | 4K resolution.                       |

## ModelInteraction

Interaction for generating the completion using models.

Fields

`model` `string`

The name of the `Model` used for generating the completion.

`generationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#GenerationConfig)` )`

Input only. Configuration parameters for the model interaction.

**JSON representation**

```
{
  "model": string,
  "generationConfig": {
    object (GenerationConfig)
  }
}
```

## GenerationConfig

Configuration parameters for model interactions.

Fields

`temperature `**`(deprecated)`** `number`

> This item is deprecated!

Controls the randomness of the output.

`topP `**`(deprecated)`** `number`

> This item is deprecated!

The maximum cumulative probability of tokens to consider when sampling.

`seed` `integer`

Seed used in decoding for reproducibility.

`stopSequences[]` `string`

A list of character sequences that will stop output interaction.

`thinkingLevel` `enum ( `[`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ThinkingLevel)` )`

The level of thought tokens that the model should generate.

`thinkingSummaries` `enum ( `[`ThinkingSummaries`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ThinkingSummaries)` )`

Whether to include thought summaries in the response.

`maxOutputTokens` `integer`

The maximum number of tokens to include in the response.

`imageConfig `**`(deprecated)`** `object ( `[`ImageConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ImageConfig)` )`

> This item is deprecated!

Configuration for image interaction.

`videoConfig` `object ( `[`VideoConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#VideoConfig)` )`

Configuration for video generation.

`transcriptionConfig` `object ( `[`TranscriptionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#TranscriptionConfig)` )`

Optional. Configuration for speech recognition (transcription). If present, ASR is enabled.

`tool_choice` `Union type`

The tool choice configuration. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`toolChoiceMode` `enum ( `[`ToolChoiceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ToolChoiceType)` )`

The mode of the tool choice.

`toolChoiceConfig` `object ( `[`ToolChoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ToolChoiceConfig)` )`

The config for the tool choice.

End of mutually exclusive fields.

**JSON representation**

```
{
  "temperature": number,
  "topP": number,
  "seed": integer,
  "stopSequences": [
    string
  ],
  "thinkingLevel": enum (ThinkingLevel),
  "thinkingSummaries": enum (ThinkingSummaries),
  "maxOutputTokens": integer,
  "imageConfig": {
    object (ImageConfig)
  },
  "videoConfig": {
    object (VideoConfig)
  },
  "transcriptionConfig": {
    object (TranscriptionConfig)
  },

  // tool_choice
  "toolChoiceMode": enum (ToolChoiceType),
  "toolChoiceConfig": {
    object (ToolChoiceConfig)
  }
  // Union type
}
```

## ToolChoiceType

The type of tool choice.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `TOOL_CHOICE_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `AUTO`                         | Auto tool choice.                    |
| `ANY`                          | Any tool choice.                     |
| `NONE`                         | No tool choice.                      |
| `VALIDATED`                    | Validated tool choice.               |

## ToolChoiceConfig

The tool choice configuration containing allowed tools.

Fields

`allowedTools` `object ( `[`AllowedTools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AllowedTools)` )`

The allowed tools.

**JSON representation**

```
{
  "allowedTools": {
    object (AllowedTools)
  }
}
```

## AllowedTools

The configuration for allowed tools.

Fields

`mode` `enum ( `[`ToolChoiceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ToolChoiceType)` )`

The mode of the tool choice.

`tools[]` `string`

The names of the allowed tools.

**JSON representation**

```
{
  "mode": enum (ToolChoiceType),
  "tools": [
    string
  ]
}
```

## ThinkingLevel

The level of thought tokens that the model should generate.

| Enums                        |                                      |
|------------------------------|--------------------------------------|
| `THINKING_LEVEL_UNSPECIFIED` | Default value. This value is unused. |
| `THINKING_LEVEL_MINIMAL`     | Little to no thinking.               |
| `THINKING_LEVEL_LOW`         | Low thinking level.                  |
| `THINKING_LEVEL_MEDIUM`      | Medium thinking level.               |
| `THINKING_LEVEL_HIGH`        | High thinking level.                 |

## ThinkingSummaries

Whether to include thought summaries in the response.

| Enums                            |                                      |
|----------------------------------|--------------------------------------|
| `THINKING_SUMMARIES_UNSPECIFIED` | Default value. This value is unused. |
| `THINKING_SUMMARIES_AUTO`        | Auto thinking summaries.             |
| `THINKING_SUMMARIES_NONE`        | No thinking summaries.               |

## ImageConfig

> This item is deprecated!

The configuration for image interaction.

Fields

`aspectRatio` `string`

The aspect ratio of the image to generate. Supported aspect ratios: 1:1, 2:3, 3:2, 3:4, 4:3, 9:16, 16:9, 21:9.

If not specified, the model will choose a default aspect ratio based on any reference images provided.

`imageSize` `string`

Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

**JSON representation**

```
{
  "aspectRatio": string,
  "imageSize": string
}
```

## VideoConfig

Configuration options for video generation.

Fields

`task` `enum ( `[`Task`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Task)` )`

Optional task mode for video generation. If not specified, the model automatically determines the appropriate mode based on the provided text prompt and input media.

**JSON representation**

```
{
  "task": enum (Task)
}
```

## Task

Supported video generation tasks.

| Enums                |                                                                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `TASK_UNSPECIFIED`   | Unspecified task. The task is inferred from the input prompt and media.                                                                            |
| `TEXT_TO_VIDEO`      | Generates video solely from a text prompt.                                                                                                         |
| `IMAGE_TO_VIDEO`     | Generates video from one or two source images. The first image defines the starting frame, and the optional second image defines the ending frame. |
| `REFERENCE_TO_VIDEO` | Generates video using reference media (such as images, audio, or video).                                                                           |
| `EDIT`               | Modifies an existing input video.                                                                                                                  |
| `EXTEND`             | Extends an existing input video.                                                                                                                   |

## TranscriptionConfig

Configuration for speech recognition (transcription).

Fields

`languageCodes[]` `string`

Optional. BCP-47 language codes providing hints about the languages present in the audio. If omitted or empty, defaults to automatic language detection.

`customVocabulary[]` `string`

Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.

`timestampGranularities[] `**`(deprecated)`** `string`

> This item is deprecated!

Optional. The granularity of timestamps to include in the transcription output. Supported values: "word". If empty, no timestamps are generated.

`diarizationMode `**`(deprecated)`** `string`

> This item is deprecated!

Optional. Configures speaker diarization. Supported values: "speaker".

`adaptationPhrases[] `**`(deprecated)`** `string`

> This item is deprecated!

Optional. A list of phrases to bias the ASR model towards.

**JSON representation**

```
{
  "languageCodes": [
    string
  ],
  "customVocabulary": [
    string
  ],
  "timestampGranularities": [
    string
  ],
  "diarizationMode": string,
  "adaptationPhrases": [
    string
  ]
}
```

## AgentInteraction

Interaction for generating the completion using agents.

Fields

`agent` `string`

The name of the `Agent` used for generating the completion.

`agent_config` `Union type`

Configuration parameters for the agent interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`dynamicConfig` `object ( `[`DynamicAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#DynamicAgentConfig)` )`

`deepResearchConfig` `object ( `[`DeepResearchAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#DeepResearchAgentConfig)` )`

`codeMenderConfig` `object ( `[`CodeMenderAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#CodeMenderAgentConfig)` )`

`antigravityConfig` `object ( `[`AntigravityAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AntigravityAgentConfig)` )`

Antigravity agent configuration. This configuration is session-level settings that are passed to the agent runtime on a per-request basis.

End of mutually exclusive fields.

**JSON representation**

```
{
  "agent": string,

  // agent_config
  "dynamicConfig": {
    object (DynamicAgentConfig)
  },
  "deepResearchConfig": {
    object (DeepResearchAgentConfig)
  },
  "codeMenderConfig": {
    object (CodeMenderAgentConfig)
  },
  "antigravityConfig": {
    object (AntigravityAgentConfig)
  }
  // Union type
}
```

## DynamicAgentConfig

Configuration for dynamic agents.

Fields

`config` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

For agents that are not supported statically in the API definition.

**JSON representation**

```
{
  "config": {
    object (Struct)
  }
}
```

## DeepResearchAgentConfig

Configuration for the Deep Research agent.

Fields

`thinkingSummaries` `enum ( `[`ThinkingSummaries`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ThinkingSummaries)` )`

Whether to include thought summaries in the response.

`visualization` `enum ( `[`VisualizationMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#VisualizationMode)` )`

Whether to include visualizations in the response.

`collaborativePlanning` `boolean`

Enables human-in-the-loop planning for the Deep Research agent. If set to true, the Deep Research agent will provide a research plan in its response. The agent will then proceed only if the user confirms the plan in the next turn.

`enableBigqueryTool` `boolean`

Enables bigquery tool for the Deep Research agent.

**JSON representation**

```
{
  "thinkingSummaries": enum (ThinkingSummaries),
  "visualization": enum (VisualizationMode),
  "collaborativePlanning": boolean,
  "enableBigqueryTool": boolean
}
```

## VisualizationMode

Enum for visualization mode. Eventually we will support an interactive mode where the user can choose whether to include HTML visualizations in the response.

| Enums         |                                                       |
|---------------|-------------------------------------------------------|
| `UNSPECIFIED` | The default visualization mode. Will default to AUTO. |
| `OFF`         | Do not include visualizations.                        |
| `AUTO`        | Automatically include visualizations.                 |

## CodeMenderAgentConfig

Configuration for the CodeMender agent.

Fields

`sessionId` `string`

Parameter for grouping multiple interactions that belong to the same CodeMender session.

`sessionConfig` `object ( `[`SessionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#SessionConfig)` )`

Optional session-specific configurations to override default agent behavior.

`model` `string`

The name of the model to use for the CodeMender agent. One CodeMender session will only use one model.

`request` `Union type`

CodeMender's request type. Set exactly one of find_request/fix_request only on the first round to start a session; on subsequent rounds (e.g. submitting tool results), leave this unset and identify the session via session_id. This oneof is intentionally not a subtype_source discriminator so it can be omitted on resume rounds. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`findRequest` `object ( `[`FindRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#FindRequest)` )`

Parameters for finding vulnerabilities.

`fixRequest` `object ( `[`FixRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#FixRequest)` )`

Parameters for fixing vulnerabilities.

End of mutually exclusive fields.

**JSON representation**

```
{
  "sessionId": string,
  "sessionConfig": {
    object (SessionConfig)
  },
  "model": string,

  // request
  "findRequest": {
    object (FindRequest)
  },
  "fixRequest": {
    object (FixRequest)
  }
  // Union type
}
```

## FindRequest

Request parameters specific to FIND sessions, used for discovering vulnerabilities in a codebase.

Fields

`sourceFiles[]` `object ( `[`FileContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#FileContent)` )`

A list of source files to provide as context for the scan.

`findingId` `string`

The identifier of a specific finding to verify. This is primarily used in VERIFY mode to focus the agent's execution-based validation on a single vulnerability.

`description` `string`

Additional context or custom instructions provided by the user to guide the vulnerability analysis.

`mode` `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Mode)` )`

The mode of the find session.

**JSON representation**

```
{
  "sourceFiles": [
    {
      object (FileContent)
    }
  ],
  "findingId": string,
  "description": string,
  "mode": enum (Mode)
}
```

## FileContent

Content of a single file in the codebase.

Fields

`path` `string`

The relative path of the file from the project root.

`content` `string`

The UTF-8 encoded text content of the file.

**JSON representation**

```
{
  "path": string,
  "content": string
}
```

## Mode

Defines the depth and thoroughness of the find session.

| Enums              |                                                             |
|--------------------|-------------------------------------------------------------|
| `MODE_UNSPECIFIED` | Default value. This value is unused.                        |
| `MODE_SCAN`        | Fast scan using only the initial classifier.                |
| `MODE_VERIFY`      | Performs classification followed by detailed investigation. |

## FixRequest

Request parameters specific to FIX sessions, used for generating and validating security patches.

Fields

`sourceFiles[]` `object ( `[`FileContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#FileContent)` )`

A list of source files providing context for the remediation. These files are typically the ones containing the identified vulnerability.

`findingId` `string`

The identifier of the specific security finding to be remediated. This id maps to a previously discovered vulnerability.

`description` `string`

Additional context or custom instructions provided by the user to guide the patch generation process.

**JSON representation**

```
{
  "sourceFiles": [
    {
      object (FileContent)
    }
  ],
  "findingId": string,
  "description": string
}
```

## SessionConfig

The configuration of CodeMender sessions.

Fields

`maxRounds` `integer`

The maximum number of interaction rounds the agent is allowed to perform before reaching a timeout.

**JSON representation**

```
{
  "maxRounds": integer
}
```

## AntigravityAgentConfig

Configuration for the Antigravity agent runtime. Provides server-side control over the agent's execution environment and tool configuration.

Fields

`maxTotalTokens` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Max total tokens for the agent run.

`model_config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`model` `string`

The model to use for agent reasoning.

End of mutually exclusive fields.

**JSON representation**

```
{
  "maxTotalTokens": string,

  // model_config
  "model": string
  // Union type
}
```

## EnvironmentConfig

Configuration for a custom environment.

Fields

`sources[]` `object ( `[`Source`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Source)` )`

`environmentId` `string`

Optional. The environment id for the interaction. If specified, the request will update the existing environment instead of creating a new one.

`network` `Union type`

Network configuration for the environment. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`networkAllowlist` `object ( `[`EnvironmentNetworkEgressAllowlist`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#EnvironmentNetworkEgressAllowlist)` )`

Allow only specific domains.

`networkMode` `enum ( `[`NetworkMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#NetworkMode)` )`

Network egress mode.

End of mutually exclusive fields.

**JSON representation**

```
{
  "sources": [
    {
      object (Source)
    }
  ],
  "environmentId": string,

  // network
  "networkAllowlist": {
    object (EnvironmentNetworkEgressAllowlist)
  },
  "networkMode": enum (NetworkMode)
  // Union type
}
```

## EnvironmentNetworkEgressAllowlist

Network egress configuration for the environment.

Fields

`allowlist[]` `object ( `[`EgressRule`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#EgressRule)` )`

List of allowed domains and their configurations.

**JSON representation**

```
{
  "allowlist": [
    {
      object (EgressRule)
    }
  ]
}
```

## EgressRule

A single domain allowlist rule with optional header injection.

Fields

`domain` `string`

domain to allow outbound requests to. Supports wildcards (e.g. '\*.googleapis.com'). Use '\*' to allow all domains.

`transform` `map (key: string, value: string)`

headers to inject into requests matching this rule. Key: header name (e.g., "Authorization"). value: header value (e.g., "Bearer your-token").

**JSON representation**

```
{
  "domain": string,
  "transform": {
    string: string,
    ...
  }
}
```

## NetworkMode

Network egress mode for non-allowlist configurations.

| Enums                      |                                |
|----------------------------|--------------------------------|
| `NETWORK_MODE_UNSPECIFIED` | Default value. Unused.         |
| `DISABLED`                 | All network egress is blocked. |

## Source

A source to be mounted into the environment.

Fields

`type` `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Type)` )`

`source` `string`

The source of the environment. For Cloud Storage, this is the Cloud Storage path. For GitHub, this is the GitHub path.

`target` `string`

Where the source should appear in the environment.

`content` `string`

The inline content if `type` is `INLINE` .

`encoding` `string`

Optional encoding for inline content (e.g. `base64` ).

**JSON representation**

```
{
  "type": enum (Type),
  "source": string,
  "target": string,
  "content": string,
  "encoding": string
}
```

## Type

| Enums              |                                                                                                                                                                                                                                                                                                         |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` |                                                                                                                                                                                                                                                                                                         |
| `GCS`              | A Cloud Storage bucket.                                                                                                                                                                                                                                                                                 |
| `INLINE`           | Inline content.                                                                                                                                                                                                                                                                                         |
| `REPOSITORY`       | A generic repository. The protocol prefix in the source URL identifies the provider (e.g., github://, gcs://).                                                                                                                                                                                          |
| `SKILL_REGISTRY`   | A skill resource from the Skill Registry service. Skill: projects/{project}/locations/{location}/skills/{skill} SkillRevision: projects/{project}/locations/{location}/skills/{skill}/revisions/{revision} Support mounting all skills under a project: projects/{project}/locations/{location}/skills. |

## LocalEnvironmentConfig

This type has no fields.

Configuration for an environment that lives on the client connection rather than in a server-managed sandbox.

When set (via Interaction.local_environment), the agent's filesystem and shell are treated as living on the client: the agent's built-in environment operations (e.g. reading/listing/editing files and running commands) are suspended on the server and yielded back to the client to execute, with their results returned on a subsequent turn. This is mutually exclusive with a server-managed `EnvironmentConfig` (remoteEnvironment), since the environment is either on the client or in a server sandbox, never both.

This governs only the agent's built-in environment. client-declared function tools are always executed on the client regardless of this field.

## Tool

A tool that can be used by the model.

Fields

`type` `Union type`

The tool to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`function` `object ( `[`Function`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Function)` )`

A function that can be used by the model.

`codeExecution` `object ( `[`CodeExecution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#CodeExecution)` )`

A tool that can be used by the model to execute code.

`urlContext` `object ( `[`UrlContext`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#UrlContext)` )`

A tool that can be used by the model to fetch URL context.

`computerUse` `object ( `[`ComputerUse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ComputerUse)` )`

Tool to support the model interacting directly with the computer.

`mcpServer` `object ( `[`McpServer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#McpServer)` )`

A MCPServer is a server that can be called by the model to perform actions.

`googleSearch` `object ( `[`GoogleSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#GoogleSearch)` )`

A tool that can be used by the model to search Google.

`fileSearch` `object ( `[`FileSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#FileSearch)` )`

A tool that can be used by the model to search files.

`googleMaps` `object ( `[`GoogleMaps`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#GoogleMaps)` )`

A tool that can be used by the model to search Google Maps.

`retrieval` `object ( `[`Retrieval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Retrieval)` )`

A tool that can be used by the model to retrieve files.

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "function": {
    object (Function)
  },
  "codeExecution": {
    object (CodeExecution)
  },
  "urlContext": {
    object (UrlContext)
  },
  "computerUse": {
    object (ComputerUse)
  },
  "mcpServer": {
    object (McpServer)
  },
  "googleSearch": {
    object (GoogleSearch)
  },
  "fileSearch": {
    object (FileSearch)
  },
  "googleMaps": {
    object (GoogleMaps)
  },
  "retrieval": {
    object (Retrieval)
  }
  // Union type
}
```

## Function

A tool that can be used by the model.

Fields

`name` `string`

The name of the function.

`description` `string`

A description of the function.

`parameters` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

The JSON Schema for the function's parameters.

**JSON representation**

```
{
  "name": string,
  "description": string,
  "parameters": {
    object (Value)
  }
}
```

## CodeExecution

This type has no fields.

A tool that can be used by the model to execute code.

## UrlContext

This type has no fields.

A tool that can be used by the model to fetch URL context.

## ComputerUse

A tool that can be used by the model to interact with the computer.

Fields

`environment` `enum ( `[`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Environment)` )`

The environment being operated.

`excludedPredefinedFunctions[]` `string`

The list of predefined functions that are excluded from the model call.

`enablePromptInjectionDetection` `boolean`

Whether enable the prompt injection detection check on computer-use request.

`disabledSafetyPolicies[]` `enum ( `[`SafetyPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#SafetyPolicy)` )`

Optional. disabled safety policies for computer use.

**JSON representation**

```
{
  "environment": enum (Environment),
  "excludedPredefinedFunctions": [
    string
  ],
  "enablePromptInjectionDetection": boolean,
  "disabledSafetyPolicies": [
    enum (SafetyPolicy)
  ]
}
```

## Environment

Represents the environment being operated, such as a web browser.

| Enums                     |                                    |
|---------------------------|------------------------------------|
| `ENVIRONMENT_UNSPECIFIED` | Defaults to browser.               |
| `BROWSER`                 | Operates in a web browser.         |
| `MOBILE`                  | Operates in a mobile environment.  |
| `DESKTOP`                 | Operates in a desktop environment. |

## SafetyPolicy

| Enums                         |                                                                 |
|-------------------------------|-----------------------------------------------------------------|
| `SAFETY_POLICY_UNSPECIFIED`   | Unspecified safety policy.                                      |
| `FINANCIAL_TRANSACTIONS`      | Safety policy for financial transactions.                       |
| `SENSITIVE_DATA_MODIFICATION` | Safety policy for sensitive data modification.                  |
| `COMMUNICATION_TOOL`          | Safety policy for communication tools (e.g. Gmail, Chat, Meet). |
| `ACCOUNT_CREATION`            | Safety policy for account creation.                             |
| `DATA_MODIFICATION`           | Safety policy for data modification.                            |
| `USER_CONSENT_MANAGEMENT`     | Safety policy for user consent management.                      |
| `LEGAL_TERMS_AND_AGREEMENTS`  | Safety policy for legal terms and agreements.                   |

## McpServer

A MCPServer is a server that can be called by the model to perform actions.

Fields

`name` `string`

The name of the MCPServer.

`headers` `map (key: string, value: string)`

Optional: Fields for authentication headers, timeouts, etc., if needed.

`allowedTools[]` `object ( `[`AllowedTools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#AllowedTools)` )`

The allowed tools.

`transport` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`url` `string`

The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "headers": {
    string: string,
    ...
  },
  "allowedTools": [
    {
      object (AllowedTools)
    }
  ],

  // transport
  "url": string
  // Union type
}
```

## GoogleSearch

A tool that can be used by the model to search Google.

Fields

`searchTypes[]` `enum ( `[`SearchType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchType)` )`

The types of search grounding to enable.

**JSON representation**

```
{
  "searchTypes": [
    enum (SearchType)
  ]
}
```

## FileSearch

A tool that can be used by the model to search files.

Fields

`fileSearchStoreNames[]` `string`

The file search store names to search.

`topK` `integer`

The number of semantic retrieval chunks to retrieve.

`metadataFilter` `string`

metadata filter to apply to the semantic retrieval documents and chunks.

**JSON representation**

```
{
  "fileSearchStoreNames": [
    string
  ],
  "topK": integer,
  "metadataFilter": string
}
```

## GoogleMaps

A tool that can be used by the model to call Google Maps.

Fields

`enableWidget` `boolean`

Whether to return a widget context token in the tool call result of the response.

`latitude` `number`

The latitude of the user's location.

`longitude` `number`

The longitude of the user's location.

**JSON representation**

```
{
  "enableWidget": boolean,
  "latitude": number,
  "longitude": number
}
```

## Retrieval

A tool that can be used by the model to retrieve files.

Fields

`retrievalTypes[]` `enum ( `[`RetrievalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrievalType)` )`

The types of file retrieval to enable.

`vertexAiSearchConfig` `object ( `[`VertexAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#VertexAISearchConfig)` )`

Used to specify configuration for VertexAISearch.

`exaAiSearchConfig` `object ( `[`ExaAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ExaAISearchConfig)` )`

Used to specify configuration for ExaAISearch.

`parallelAiSearchConfig` `object ( `[`ParallelAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#ParallelAISearchConfig)` )`

Used to specify configuration for ParallelAISearch.

`ragStoreConfig` `object ( `[`RagStoreConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#RagStoreConfig)` )`

Used to specify configuration for RagStore.

**JSON representation**

```
{
  "retrievalTypes": [
    enum (RetrievalType)
  ],
  "vertexAiSearchConfig": {
    object (VertexAISearchConfig)
  },
  "exaAiSearchConfig": {
    object (ExaAISearchConfig)
  },
  "parallelAiSearchConfig": {
    object (ParallelAISearchConfig)
  },
  "ragStoreConfig": {
    object (RagStoreConfig)
  }
}
```

## VertexAISearchConfig

Used to specify configuration for VertexAISearch.

Fields

`engine` `string`

Optional. Used to specify Agent Platform Search engine.

`datastores[]` `string`

Optional. Used to specify Agent Platform Search datastores.

**JSON representation**

```
{
  "engine": string,
  "datastores": [
    string
  ]
}
```

## ExaAISearchConfig

Used to specify configuration for ExaAISearch.

Fields

`apiKey` `string`

Required. The API key for ExaAiSearch.

`customConfig` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. This field can be used to pass any parameter from the Exa.ai Search API.

**JSON representation**

```
{
  "apiKey": string,
  "customConfig": {
    object
  }
}
```

## ParallelAISearchConfig

Used to specify configuration for ParallelAISearch.

Fields

`apiKey` `string`

Optional. The API key for ParallelAiSearch.

`customConfig` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Custom configs for ParallelAiSearch.

**JSON representation**

```
{
  "apiKey": string,
  "customConfig": {
    object
  }
}
```

## RagStoreConfig

Use to specify configuration for RAG Store.

Fields

`ragResources[]` `object ( `[`RagResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#RagResource)` )`

Optional. The representation of the rag source.

`similarityTopK `**`(deprecated)`** `integer`

> This item is deprecated!

Optional. Number of top k results to return from the selected corpora.

`vectorDistanceThreshold `**`(deprecated)`** `number`

> This item is deprecated!

Optional. Only return results with vector distance smaller than the threshold.

`ragRetrievalConfig` `object ( `[`RagRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#RagRetrievalConfig)` )`

Optional. The retrieval config for the Rag query.

**JSON representation**

```
{
  "ragResources": [
    {
      object (RagResource)
    }
  ],
  "similarityTopK": integer,
  "vectorDistanceThreshold": number,
  "ragRetrievalConfig": {
    object (RagRetrievalConfig)
  }
}
```

## RagResource

The definition of the Rag resource.

Fields

`ragCorpus` `string`

Optional. RagCorpora resource name.

`ragFileIds[]` `string`

Optional. ragFileId. The files should be in the same ragCorpus set in ragCorpus field.

**JSON representation**

```
{
  "ragCorpus": string,
  "ragFileIds": [
    string
  ]
}
```

## RagRetrievalConfig

Specifies the context retrieval config.

Fields

`topK` `integer`

Optional. The number of contexts to retrieve.

`hybridSearch` `object ( `[`HybridSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#HybridSearch)` )`

Optional. Config for Hybrid Search.

`filter` `object ( `[`Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Filter)` )`

Optional. Config for filters.

`ranking` `object ( `[`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#Ranking)` )`

Optional. Config for ranking and reranking.

**JSON representation**

```
{
  "topK": integer,
  "hybridSearch": {
    object (HybridSearch)
  },
  "filter": {
    object (Filter)
  },
  "ranking": {
    object (Ranking)
  }
}
```

## HybridSearch

Config for Hybrid Search.

Fields

`alpha` `number`

Optional. Alpha value controls the weight between dense and sparse vector search results.

**JSON representation**

```
{
  "alpha": number
}
```

## Filter

Config for filters.

Fields

`metadataFilter` `string`

Optional. String for metadata filtering.

`vector_db_threshold` `Union type`

Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vectorDistanceThreshold` `number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vectorSimilarityThreshold` `number`

Optional. Only returns contexts with vector similarity larger than the threshold.

End of mutually exclusive fields.

**JSON representation**

```
{
  "metadataFilter": string,

  // vector_db_threshold
  "vectorDistanceThreshold": number,
  "vectorSimilarityThreshold": number
  // Union type
}
```

## Ranking

Config for ranking and reranking.

Fields

`ranking_config` `Union type`

Config options for ranking. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`rankService` `object ( `[`RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#RankService)` )`

Config for Rank service.

End of mutually exclusive fields.

**JSON representation**

```
{

  // ranking_config
  "rankService": {
    object (RankService)
  }
  // Union type
}
```

## RankService

Config for Rank service.

Fields

`modelName` `string`

Optional. The model name of the rank service.

**JSON representation**

```
{
  "modelName": string
}
```

## SafetySetting

A safety setting that affects the safety-blocking behavior.

A `SafetySetting` consists of a harm `category` and a `threshold` for that category.

Fields

`type` `enum ( `[`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#HarmCategory)` )`

Required. The type of harm category to be blocked.

`threshold` `enum ( `[`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#HarmBlockThreshold)` )`

Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked.

`method` `enum ( `[`HarmBlockMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction#HarmBlockMethod)` )`

Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.

**JSON representation**

```
{
  "type": enum (HarmCategory),
  "threshold": enum (HarmBlockThreshold),
  "method": enum (HarmBlockMethod)
}
```

## HarmCategory

Harm categories that can be detected in user input and model responses.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>HARM_CATEGORY_UNSPECIFIED</code></td>
<td>Default value. This value is unused.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_HATE_SPEECH</code></td>
<td>Content that promotes violence or incites hatred against individuals or groups based on certain attributes.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_DANGEROUS_CONTENT</code></td>
<td>Content that promotes, facilitates, or enables dangerous activities.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_HARASSMENT</code></td>
<td>Abusive, threatening, or content intended to bully, torment, or ridicule.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_SEXUALLY_EXPLICIT</code></td>
<td>Content that contains sexually explicit material.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_CIVIC_INTEGRITY</code></td>
<td><p>Deprecated: Election filter is not longer supported. The harm category is civic integrity.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_IMAGE_HATE</code></td>
<td>Images that contain hate speech.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_IMAGE_DANGEROUS_CONTENT</code></td>
<td>Images that contain dangerous content.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_IMAGE_HARASSMENT</code></td>
<td>Images that contain harassment.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_IMAGE_SEXUALLY_EXPLICIT</code></td>
<td>Images that contain sexually explicit content.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_JAILBREAK</code></td>
<td>Prompts designed to bypass safety filters.</td>
</tr>
</tbody>
</table>

## HarmBlockThreshold

Thresholds for blocking content based on harm probability.

| Enums                              |                                                               |
|------------------------------------|---------------------------------------------------------------|
| `HARM_BLOCK_THRESHOLD_UNSPECIFIED` | The harm block threshold is unspecified.                      |
| `BLOCK_LOW_AND_ABOVE`              | Block content with a low harm probability or higher.          |
| `BLOCK_MEDIUM_AND_ABOVE`           | Block content with a medium harm probability or higher.       |
| `BLOCK_ONLY_HIGH`                  | Block content with a high harm probability.                   |
| `BLOCK_NONE`                       | Do not block any content, regardless of its harm probability. |
| `OFF`                              | Turn off the safety filter entirely.                          |

## HarmBlockMethod

The method for blocking content.

| Enums                           |                                                                  |
|---------------------------------|------------------------------------------------------------------|
| `HARM_BLOCK_METHOD_UNSPECIFIED` | The harm block method is unspecified.                            |
| `SEVERITY`                      | The harm block method uses both probability and severity scores. |
| `PROBABILITY`                   | The harm block method uses the probability score.                |
