---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaProcessing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaProcessing
title: MediaProcessing
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`static` `object ( `[`StaticMediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaProcessing#StaticMediaProcessing)` )`

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
