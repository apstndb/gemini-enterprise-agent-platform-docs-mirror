---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.feedbackEntries/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.feedbackEntries/list
title: 'Method: feedbackEntries.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.feedbackEntries.list

Lists FeedbackEntries in a ReasoningEngine.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /feedbackEntries`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine from which to list FeedbackEntries.

Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`pageSize` `integer`

Optional. The maximum number of FeedbackEntries to return per page.

`pageToken` `string`

Optional. A page token, received from a previous feedbackEntries.list call.

`filter` `string`

Optional. Standard list filter.

Supported fields:

  - `sessionId`
  - `userId`
  - `feedbackType`
  - `feedbackLabels` : Supports the HAS operator ( `:` ). For example: `feedbackLabels:"inaccurate"` .
  - `createTime`
  - `updateTime`

Example: `feedbackType="THUMBS_DOWN" AND feedbackLabels:"hallucination"` .

`orderBy` `string`

Optional. A comma-separated list of fields to order results by, sorted in ascending order by default. Append `desc` after a field name to sort that field in descending order.

Supported fields:

  - `createTime`
  - `updateTime`

Example: `createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for feedbackEntries.list.

If successful, the response body contains data with the following structure:

Fields

`feedbackEntries[]` ` object ( FeedbackEntry  ` )

The page of FeedbackEntries matching the request.

`nextPageToken` `string`

A token to retrieve the next page. Absence of this field indicates there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;feedbackEntries&quot;: [{object (FeedbackEntry)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
