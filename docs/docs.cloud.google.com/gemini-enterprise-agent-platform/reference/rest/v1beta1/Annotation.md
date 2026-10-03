---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation
title: Annotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Citation information for model-generated content.

Fields

`startIndex` `integer`

Start of segment of the response that is attributed to this source.

Index indicates the start of the segment, measured in bytes.

`endIndex` `integer`

End of the attributed segment, exclusive.

`type` `Union type`

The type of annotation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`urlCitation` `object ( `[`UrlCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation#UrlCitation)` )`

NOTE: We use these instead of the Citation message for historical reasons. A URL citation annotation.

`fileCitation` `object ( `[`FileCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation#FileCitation)` )`

A file citation annotation.

`placeCitation` `object ( `[`PlaceCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation#PlaceCitation)` )`

A place citation annotation.

`wordInfo` `object ( `[`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation#WordInfo)` )`

word-level ASR annotation with timing and speaker info.

End of mutually exclusive fields.

**JSON representation**

```
{
  "startIndex": integer,
  "endIndex": integer,

  // type
  "urlCitation": {
    object (UrlCitation)
  },
  "fileCitation": {
    object (FileCitation)
  },
  "placeCitation": {
    object (PlaceCitation)
  },
  "wordInfo": {
    object (WordInfo)
  }
  // Union type
}
```

## UrlCitation

A URL citation annotation.

Fields

`url` `string`

The URL.

`title` `string`

The title of the URL.

**JSON representation**

```
{
  "url": string,
  "title": string
}
```

## FileCitation

A file citation annotation.

Fields

`documentUri` `string`

The URI of the file.

`fileName` `string`

The name of the file.

`source` `string`

Source attributed for a portion of the text.

`customMetadata` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

user provided metadata about the retrieved context.

`pageNumber` `integer`

Page number of the cited document, if applicable.

`mediaId` `string`

Media id in-case of image citations, if applicable.

**JSON representation**

```
{
  "documentUri": string,
  "fileName": string,
  "source": string,
  "customMetadata": {
    object (Struct)
  },
  "pageNumber": integer,
  "mediaId": string
}
```

## PlaceCitation

A place citation annotation.

Fields

`placeId` `string`

The id of the place, in `places/{placeId}` format.

`name` `string`

title of the place.

`url` `string`

URI reference of the place.

`reviewSnippets[]` `object ( `[`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReviewSnippet)` )`

Snippets of reviews that are used to generate answers about the features of a given place in Google Maps.

**JSON representation**

```
{
  "placeId": string,
  "name": string,
  "url": string,
  "reviewSnippets": [
    {
      object (ReviewSnippet)
    }
  ]
}
```

## WordInfo

word-level ASR annotation for transcription output. Carries the word text, optional timing, and optional speaker attribution.

Fields

`text` `string`

The transcribed word.

`startOffset` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Start offset in time of the word relative to the start of the audio. Present when timestampGranularities contains "word".

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

End offset in time of the word relative to the start of the audio. Present when timestampGranularities contains "word".

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`speaker` `string`

Optional. Speaker label for this word (e.g. "spk_1", "spk_2"). Present when diarizationMode is set in TranscriptionConfig.

**JSON representation**

```
{
  "text": string,
  "startOffset": string,
  "endOffset": string,
  "speaker": string
}
```
