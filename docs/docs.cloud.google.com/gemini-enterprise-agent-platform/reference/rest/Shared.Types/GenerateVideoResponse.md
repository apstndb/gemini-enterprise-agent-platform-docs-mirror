---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse
title: GenerateVideoResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Generate video response.

Fields

`generatedSamples[]` `object ( `[`Media`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#Media)` )`

The generates samples.

`raiMediaFilteredCount` `integer`

Returns if any videos were filtered due to RAI policies.

`raiMediaFilteredReasons[]` `string`

Returns rai failure reasons if any.

**JSON representation**

```
{
  "generatedSamples": [
    {
      object (Media)
    }
  ],
  "raiMediaFilteredCount": integer,
  "raiMediaFilteredReasons": [
    string
  ]
}
```

## Media

Media.

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`image` `object ( `[`Image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#Image)` )`

Image.

`video` `object ( `[`Video`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#Video)` )`

Video

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "image": {
    object (Image)
  },
  "video": {
    object (Video)
  }
  // Union type
}
```

## Image

Image.

Fields

`encoding` `string`

Image encoding, encoded as "image/png" or "image/jpg".

`imageRaiScores` `object ( `[`ImageRAIScores`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#ImageRAIScores)` )`

RAI scores for generated image.

`raiInfo` `object ( `[`RaiInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#RaiInfo)` )`

RAI info for image.

`semanticFilterResponse` `object ( `[`SemanticFilterResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#SemanticFilterResponse)` )`

Semantic filter info for image.

`text` `string`

Text/Expanded text input for imagen.

`imageSize` `object ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#ImageSize)` )`

Image size. The size of the image. Can be self reported, or computed from the image bytes.

`content` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`image` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Raw bytes.

A base64-encoded string.

`uri` `string`

Path to another storage (typically Google Cloud Storage).

End of mutually exclusive fields.

**JSON representation**

```
{
  "encoding": string,
  "imageRaiScores": {
    object (ImageRAIScores)
  },
  "raiInfo": {
    object (RaiInfo)
  },
  "semanticFilterResponse": {
    object (SemanticFilterResponse)
  },
  "text": string,
  "imageSize": {
    object (ImageSize)
  },

  // content
  "image": string,
  "uri": string
  // Union type
}
```

## ImageRAIScores

RAI scores for generated image returned.

Fields

`agileWatermarkDetectionScore` `number`

Agile watermark score for image.

**JSON representation**

```
{
  "agileWatermarkDetectionScore": number
}
```

## RaiInfo

Next id: 6

Fields

`raiCategories[]` `string`

List of rai categories' information to return

`scores[]` `number`

List of rai scores mapping to the rai categories. Rounded to 1 decimal place.

`blockedEntities[]` `string`

List of blocked entities from the blocklist if it is detected.

`modelName` `string`

The model name used to indexing into the RaiFilterConfig map. Would either be one of <imagegeneration@002-006> , imagen-3.0-... api endpoint names, or internal names used for mapping to different filter configs (genselfie, ai_watermark) than its api endpoint.

**JSON representation**

```
{
  "raiCategories": [
    string
  ],
  "scores": [
    number
  ],
  "blockedEntities": [
    string
  ],
  "modelName": string
}
```

## SemanticFilterResponse

Fields

`passedSemanticFilter` `boolean`

This response is added when semantic filter config is turned on in EditConfig. It reports if this image is passed semantic filter response. If passedSemanticFilter is false, the bounding box information will be populated for user to check what caused the semantic filter to fail.

`namedBoundingBoxes[]` `object ( `[`NamedBoundingBox`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse#NamedBoundingBox)` )`

Class labels of the bounding boxes that failed the semantic filtering. Bounding box coordinates.

**JSON representation**

```
{
  "passedSemanticFilter": boolean,
  "namedBoundingBoxes": [
    {
      object (NamedBoundingBox)
    }
  ]
}
```

## NamedBoundingBox

Fields

`x1` `number`

`x2` `number`

`y1` `number`

`y2` `number`

`classes[]` `string`

`entities[]` `string`

`scores[]` `number`

**JSON representation**

```
{
  "x1": number,
  "x2": number,
  "y1": number,
  "y2": number,
  "classes": [
    string
  ],
  "entities": [
    string
  ],
  "scores": [
    number
  ]
}
```

## ImageSize

Image size.

Fields

`width` `integer`

`height` `integer`

`channels` `integer`

**JSON representation**

```
{
  "width": integer,
  "height": integer,
  "channels": integer
}
```

## Video

Video

Fields

`encoding` `string`

Video encoding, for example "video/mp4".

`text` `string`

Text/Expanded text input for Help Me Write.

`content` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`video` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Raw bytes.

A base64-encoded string.

`uri` `string`

Path to another storage (typically Google Cloud Storage).

`encodedVideo` `string`

Base 64 encoded video bytes.

End of mutually exclusive fields.

**JSON representation**

```
{
  "encoding": string,
  "text": string,

  // content
  "video": string,
  "uri": string,
  "encodedVideo": string
  // Union type
}
```
