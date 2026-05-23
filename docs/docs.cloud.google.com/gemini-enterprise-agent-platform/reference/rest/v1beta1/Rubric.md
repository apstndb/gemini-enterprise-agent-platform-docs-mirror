---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric
title: Rubric
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

message representing a single testable criterion for evaluation. One input prompt could have multiple rubrics.

Fields

`rubricId` `string`

Unique identifier for the rubric. This id is used to refer to this rubric, e.g., in RubricVerdict.

`content` ` object ( Content  ` )

Required. The actual testable criteria for the rubric.

`type` `string`

Optional. A type designator for the rubric, which can inform how it's evaluated or interpreted by systems or users. It's recommended to use consistent, well-defined, upper snake\_case strings. Examples: "SUMMARIZATION\_QUALITY", "SAFETY\_HARMFUL\_CONTENT", "INSTRUCTION\_ADHERENCE".

`importance` ` enum ( Importance  ` )

Optional. The relative importance of this rubric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rubricId&quot;: string,&quot;content&quot;: {object (Content)},&quot;type&quot;: string,&quot;importance&quot;: enum (Importance)}</code></pre></td>
</tr>
</tbody>
</table>

## Content

Content of the rubric, defining the testable criteria.

Fields

`content_type` `Union type`

`content_type` can be only one of the following:

`property` ` object ( Property  ` )

Evaluation criteria based on a specific property.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// content_type&quot;property&quot;: {object (Property)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Property

Defines criteria based on a specific property.

Fields

`description` `string`

description of the property being evaluated. Example: "The model's response is grammatically correct."

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
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Importance

Importance level of the rubric.

Enums

`IMPORTANCE_UNSPECIFIED`

Importance is not specified.

`HIGH`

High importance.

`MEDIUM`

Medium importance.

`LOW`

Low importance.
