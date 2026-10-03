---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions
title: 'REST Resource: projects.locations.reasoningEngines.sessions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Session

A session contains a set of actions between users and Vertex agents.

Fields

`name` `string`

Identifier. The resource name of the session. Format: 'projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sessions/{session}'.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when the session was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when the session was updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`displayName` `string`

Optional. The display name of the session.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Sessions.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`sessionState` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Session specific memory which stores key conversation points.

`userId` `string`

Required. Immutable. String id provided by the user

`expiration` `Union type`

The expiration of the session. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`expireTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Optional. timestamp of when this session is considered expired. This is *always* provided on output, regardless of what was sent on input. The minimum value is 24 hours from the time of creation.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Input only. The TTL for this session. The minimum value is 24 hours.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "updateTime": string,
  "displayName": string,
  "labels": {
    string: string,
    ...
  },
  "sessionState": {
    object
  },
  "userId": string,

  // expiration
  "expireTime": string,
  "ttl": string
  // Union type
}
```

| Methods                                                                                                                                                         |                                                                                                                                                                                             |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`appendEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions/appendEvent) | Appends an event to a given session.                                                                                                                                                        |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions/create)           | Creates a new [`Session`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions#Session) .                     |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions/delete)           | Deletes details of the specific [`Session`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions#Session) .   |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions/get)                 | Gets details of the specific [`Session`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions#Session) .      |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions/list)               | Lists [`Sessions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions#Session) in a given reasoning engine. |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions/patch)             | Updates the specific [`Session`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions#Session) .              |
