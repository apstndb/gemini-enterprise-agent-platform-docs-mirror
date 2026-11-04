---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content
title: Content
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The content of the response.

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `object ( `[`TextContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#TextContent)` )`

`image` `object ( `[`ImageContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#ImageContent)` )`

`audio` `object ( `[`AudioContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#AudioContent)` )`

`document` `object ( `[`DocumentContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#DocumentContent)` )`

`video` `object ( `[`VideoContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#VideoContent)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "text": {
    object (TextContent)
  },
  "image": {
    object (ImageContent)
  },
  "audio": {
    object (AudioContent)
  },
  "document": {
    object (DocumentContent)
  },
  "video": {
    object (VideoContent)
  }
  // Union type
}
```

## TextContent

A text content block.

Fields

`text` `string`

Required. The text content.

`annotations[]` `object ( `[`Annotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Annotation)` )`

Citation information for model-generated content.

**JSON representation**

```
{
  "text": string,
  "annotations": [
    {
      object (Annotation)
    }
  ]
}
```

## ImageContent

An image content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the image, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MediaResolution)` )`

The resolution of the media.

`data_or_uri` `Union type`

The image content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The image content.

A base64-encoded string.

`uri` `string`

The URI of the image.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,
  "resolution": enum (MediaResolution),

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## AudioContent

An audio content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the audio, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`channels` `integer`

The number of audio channels.

`sampleRate` `integer`

The sample rate of the audio.

`data_or_uri` `Union type`

The audio content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The audio content.

A base64-encoded string.

`uri` `string`

The URI of the audio.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,
  "channels": integer,
  "sampleRate": integer,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## DocumentContent

A document content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the document, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`data_or_uri` `Union type`

The document content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The document content.

A base64-encoded string.

`uri` `string`

The URI of the document.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## VideoContent

A video content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the video, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MediaResolution)` )`

The resolution of the media.

`name` `string`

A user-defined name for this content block. Can be referenced by the model in the final response.

`data_or_uri` `Union type`

The video content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The video content.

A base64-encoded string.

`uri` `string`

The URI of the video.

End of mutually exclusive fields.

`processing` `Union type`

How the model processes this video for understanding. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`processingType` `enum ( `[`Processing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#Processing)` )`

`processingConfig` `object ( `[`MediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#MediaProcessing)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,
  "resolution": enum (MediaResolution),
  "name": string,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type

  // processing
  "processingType": enum (Processing),
  "processingConfig": {
    object (MediaProcessing)
  }
  // Union type
}
```

## Processing

How the model processes input media for understanding.

| Enums                    |                                                                                           |
|--------------------------|-------------------------------------------------------------------------------------------|
| `PROCESSING_UNSPECIFIED` | Default. uses model-specific processing (3.5 Pro+ --\> AGENTIC, older models --\> STATIC) |
| `STATIC`                 | Fixed-rate frame extraction. All frames placed in context.                                |
| `AGENTIC`                | Model-driven dynamic navigation.                                                          |

## MediaProcessing

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`static` `object ( `[`StaticMediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content#StaticMediaProcessing)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "static": {
    object (StaticMediaProcessing)
  }
  // Union type
}
```

## StaticMediaProcessing

Fields

`startOffset` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Segment start time. Specified as a decimal number of seconds followed by an 's' suffix, e.g., "10.5s". Must be non-negative.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Segment end time. Specified as a decimal number of seconds followed by an 's' suffix, e.g., "30s". Must be non-negative and greater than `startOffset` if `startOffset` is set.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`fps` `number`

Optional. Video frame-rate sampling density.

**JSON representation**

```
{
  "startOffset": string,
  "endOffset": string,
  "fps": number
}
```
