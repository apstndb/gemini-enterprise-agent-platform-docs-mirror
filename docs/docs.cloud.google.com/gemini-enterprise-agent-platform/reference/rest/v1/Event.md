---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Event
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Event
title: Event
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An edge describing the relationship between an Artifact and an Execution in a lineage graph.

Fields

`artifact` `string`

Required. The relative resource name of the Artifact in the Event.

`execution` `string`

Output only. The relative resource name of the Execution in the Event.

`eventTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time the Event occurred.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`type` `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Event#Type)` )`

Required. The type of the Event.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to annotate events.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Event (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

**JSON representation**

```
{
  "artifact": string,
  "execution": string,
  "eventTime": string,
  "type": enum (Type),
  "labels": {
    string: string,
    ...
  }
}
```

## Type

Describes whether an Event's Artifact is the Execution's input or output.

| Enums              |                                                       |
|--------------------|-------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Unspecified whether input or output of the Execution. |
| `INPUT`            | An input of the Execution.                            |
| `OUTPUT`           | An output of the Execution.                           |
