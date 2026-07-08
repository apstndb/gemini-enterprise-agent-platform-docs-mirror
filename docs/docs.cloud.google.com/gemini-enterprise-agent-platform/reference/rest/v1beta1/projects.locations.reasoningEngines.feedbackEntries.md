---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.feedbackEntries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.feedbackEntries
title: 'REST Resource: projects.locations.reasoningEngines.feedbackEntries'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeedbackEntry

FeedbackEntry is a resource that represents a user's feedback on a conversation with an agent.

Fields

`name` `string`

Identifier. The resource name. Assigned by the server on create.

Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/feedbackEntries/{feedbackEntry}`

`sessionId` `string`

Required. The id of the session that the feedback relates to.

`eventId` `string`

Required. The id of the event within the session that the feedback relates to.

`feedbackType` ` enum ( FeedbackType  ` )

Required. The coarse-grained type of feedback provided by the user. Must be set to a value other than `FEEDBACK_TYPE_UNSPECIFIED` .

`feedbackLabels[]` `string`

`feedbackText` `string`

Optional. Qualitative free-form comments provided by the user.

`userId` `string`

Optional. A caller-supplied identifier for the user who provided the feedback. The semantics of this field (for example whether it is an opaque token, a hashed value, or a user-visible identifier) are determined by the calling application.

`source` `string`

Optional. The surface that the feedback originated from.

`customMetadata` `map (key: string, value: string)`

Optional. Additional key-value metadata associated with the feedback.

`createTime` ` string ( Timestamp  ` format)

Output only. The time at which the entry was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. The time at which the entry was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;sessionId&quot;: string,&quot;eventId&quot;: string,&quot;feedbackType&quot;: enum (FeedbackType),&quot;feedbackLabels&quot;: [string],&quot;feedbackText&quot;: string,&quot;userId&quot;: string,&quot;source&quot;: string,&quot;customMetadata&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## FeedbackType

The coarse-grained type of feedback provided by the user.

The enum is not frozen; additional values may be added in the future, so clients should treat unknown values gracefully.

Enums

`FEEDBACK_TYPE_UNSPECIFIED`

This is the default value meaning the type has not been set.

`THUMBS_UP`

Indicates positive feedback.

`THUMBS_DOWN`

Indicates negative feedback.

## Methods

### `            create           `

Creates a new FeedbackEntry.

### `            delete           `

Deletes a FeedbackEntry and its associated FeedbackContext.

### `            get           `

Retrieves a single FeedbackEntry by its resource name.

### `            getFeedbackContext           `

Retrieves the FeedbackContext associated with a FeedbackEntry.

### `            list           `

Lists FeedbackEntries in a ReasoningEngine.

### `            patch           `

Updates an existing FeedbackEntry.

### `            updateFeedbackContext           `

Updates the FeedbackContext associated with a FeedbackEntry.
