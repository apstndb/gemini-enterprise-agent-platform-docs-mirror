---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SessionEvent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SessionEvent
title: SessionEvent
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An event represents a message from either the user or agent.

Fields

`name` `string`

Identifier. The resource name of the event. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sessions/{session}/events/{event}` .

`author` `string`

Required. The name of the agent that sent the event, or user.

`content` ` object ( Content  ` )

Optional. Content of the event provided by the author.

`invocationId` `string`

Required. The invocation id of the event, multiple events can have the same invocation id.

`actions` ` object ( EventActions  ` )

Optional. Actions executed by the agent.

`timestamp` ` string ( Timestamp  ` format)

Required. timestamp when the event was created on client side.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`errorCode` `string`

Optional. Error code if the response is an error. code varies by model.

`errorMessage` `string`

Optional. Error message if the response is an error.

`eventMetadata` ` object ( EventMetadata  ` )

Optional. metadata relating to this event.

`rawEvent` ` object ( Struct  ` format)

Optional. Weakly typed raw event data in proto struct format.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;author&quot;: string,&quot;content&quot;: {object (Content)},&quot;invocationId&quot;: string,&quot;actions&quot;: {object (EventActions)},&quot;timestamp&quot;: string,&quot;errorCode&quot;: string,&quot;errorMessage&quot;: string,&quot;eventMetadata&quot;: {object (EventMetadata)},&quot;rawEvent&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

## EventActions

Actions are parts of events that are executed by the agent.

Fields

`skipSummarization` `boolean`

Optional. If true, it won't call model to summarize function response. Only used for functionResponse event.

`stateDelta` ` object ( Struct  ` format)

Optional. Indicates that the event is updating the state with the given delta.

`artifactDelta` `map (key: string, value: integer)`

Optional. Indicates that the event is updating an artifact. key is the filename, value is the version.

`escalate` `boolean`

Optional. The agent is escalating to a higher level agent.

`requestedAuthConfigs` ` object ( Struct  ` format)

Optional. Will only be set by a tool response indicating tool request euc. Struct key is the function call id since one function call response (from model) could correspond to multiple function calls. Struct value is the required auth config, which can be another struct.

`transferAgent` `string`

Optional. If set, the event transfers to the specified agent.

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
  &quot;skipSummarization&quot;: boolean,
  &quot;stateDelta&quot;: {
    object
  },
  &quot;artifactDelta&quot;: {
    string: integer,
    ...
  },
  &quot;escalate&quot;: boolean,
  &quot;requestedAuthConfigs&quot;: {
    object
  },
  &quot;transferAgent&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## EventMetadata

metadata relating to a LLM response event.

Fields

`groundingMetadata` ` object ( GroundingMetadata  ` )

Optional. metadata returned to client when grounding is enabled.

`partial` `boolean`

Optional. Indicates whether the text content is part of a unfinished text stream. Only used for streaming mode and when the content is plain text.

`turnComplete` `boolean`

Optional. Indicates whether the response from the model is complete. Only used for streaming mode.

`interrupted` `boolean`

Optional. Flag indicating that LLM was interrupted when generating the content. Usually it's due to user interruption during a bidi streaming.

`longRunningToolIds[]` `string`

Optional. Set of ids of the long running function calls. Agent client will know from this field about which function call is long running. Only valid for function call event.

`branch` `string`

Optional. The branch of the event. The format is like agent\_1.agent\_2.agent\_3, where agent\_1 is the parent of agent\_2, and agent\_2 is the parent of agent\_3. Branch is used when multiple child agents shouldn't see their siblings' conversation history.

`customMetadata` ` object ( Struct  ` format)

The custom metadata of the LlmResponse.

`inputTranscription` ` object ( Transcription  ` )

Optional. Audio transcription of user input.

`outputTranscription` ` object ( Transcription  ` )

Optional. Audio transcription of model output.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;groundingMetadata&quot;: {object (GroundingMetadata)},&quot;partial&quot;: boolean,&quot;turnComplete&quot;: boolean,&quot;interrupted&quot;: boolean,&quot;longRunningToolIds&quot;: [string],&quot;branch&quot;: string,&quot;customMetadata&quot;: {object},&quot;inputTranscription&quot;: {object (Transcription)},&quot;outputTranscription&quot;: {object (Transcription)}}</code></pre></td>
</tr>
</tbody>
</table>

## Transcription

Audio transcription in Server Content.

Fields

`text` `string`

Optional. Transcription text.

`finished` `boolean`

Optional. The bool indicates the end of the transcription.

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
  &quot;finished&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
