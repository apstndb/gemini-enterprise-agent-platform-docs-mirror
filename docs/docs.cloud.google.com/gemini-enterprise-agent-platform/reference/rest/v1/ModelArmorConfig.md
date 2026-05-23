---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelArmorConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelArmorConfig
title: ModelArmorConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration for Model Armor.

Model Armor is a Google Cloud service that provides safety and security filtering for prompts and responses. It helps protect your AI applications from risks such as harmful content, sensitive data leakage, and prompt injection attacks.

Fields

`promptTemplateName` `string`

Optional. The resource name of the Model Armor template to use for prompt screening.

A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the user's prompt for safety and security risks before it is sent to the model.

The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .

`responseTemplateName` `string`

Optional. The resource name of the Model Armor template to use for response screening.

A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the model's response for safety and security risks before it is returned to the user.

The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .

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
  &quot;promptTemplateName&quot;: string,
  &quot;responseTemplateName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
