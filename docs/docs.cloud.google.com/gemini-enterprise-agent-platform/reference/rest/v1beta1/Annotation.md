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

The type of annotation. `type` can be only one of the following:

`urlCitation` ` object ( UrlCitation  ` )

NOTE: We use these instead of the Citation message for historical reasons. A URL citation annotation.

`fileCitation` ` object ( FileCitation  ` )

A file citation annotation.

`placeCitation` ` object ( PlaceCitation  ` )

A place citation annotation.

`wordInfo` ` object ( WordInfo  ` )

word-level ASR annotation with timing and speaker info.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;startIndex&quot;: integer,&quot;endIndex&quot;: integer,// type&quot;urlCitation&quot;: {object (UrlCitation)},&quot;fileCitation&quot;: {object (FileCitation)},&quot;placeCitation&quot;: {object (PlaceCitation)},&quot;wordInfo&quot;: {object (WordInfo)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## UrlCitation

A URL citation annotation.

Fields

`url` `string`

The URL.

`title` `string`

The title of the URL.

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
  &quot;url&quot;: string,
  &quot;title&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## FileCitation

A file citation annotation.

Fields

`documentUri` `string`

The URI of the file.

`fileName` `string`

The name of the file.

`source` `string`

Source attributed for a portion of the text.

`customMetadata` ` object ( Struct  ` )

user provided metadata about the retrieved context.

`pageNumber` `integer`

Page number of the cited document, if applicable.

`mediaId` `string`

Media id in-case of image citations, if applicable.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;documentUri&quot;: string,&quot;fileName&quot;: string,&quot;source&quot;: string,&quot;customMetadata&quot;: {object (Struct)},&quot;pageNumber&quot;: integer,&quot;mediaId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## PlaceCitation

A place citation annotation.

Fields

`placeId` `string`

The id of the place, in `places/{placeId}` format.

`name` `string`

title of the place.

`url` `string`

URI reference of the place.

`reviewSnippets[]` ` object ( ReviewSnippet  ` )

Snippets of reviews that are used to generate answers about the features of a given place in Google Maps.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;placeId&quot;: string,&quot;name&quot;: string,&quot;url&quot;: string,&quot;reviewSnippets&quot;: [{object (ReviewSnippet)}]}</code></pre></td>
</tr>
</tbody>
</table>

## WordInfo

word-level ASR annotation for transcription output. Carries the word text, optional timing, and optional speaker attribution.

Fields

`text` `string`

The transcribed word.

`startOffset` ` string ( Duration  ` format)

Start offset in time of the word relative to the start of the audio. Present when timestampGranularities contains "word".

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset` ` string ( Duration  ` format)

End offset in time of the word relative to the start of the audio. Present when timestampGranularities contains "word".

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`speaker` `string`

Optional. Speaker label for this word (e.g. "spk\_1", "spk\_2"). Present when diarizationMode is set in TranscriptionConfig.

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
  &quot;text&quot;: string,
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string,
  &quot;speaker&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
