---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/HarmCategory
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/HarmCategory
title: HarmCategory
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Harm categories that can be detected in user input and model responses.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>HARM_CATEGORY_UNSPECIFIED</code></td>
<td>Default value. This value is unused.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_HATE_SPEECH</code></td>
<td>Content that promotes violence or incites hatred against individuals or groups based on certain attributes.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_DANGEROUS_CONTENT</code></td>
<td>Content that promotes, facilitates, or enables dangerous activities.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_HARASSMENT</code></td>
<td>Abusive, threatening, or content intended to bully, torment, or ridicule.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_SEXUALLY_EXPLICIT</code></td>
<td>Content that contains sexually explicit material.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_CIVIC_INTEGRITY</code></td>
<td><p>Deprecated: Election filter is not longer supported. The harm category is civic integrity.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_IMAGE_HATE</code></td>
<td>Images that contain hate speech.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_IMAGE_DANGEROUS_CONTENT</code></td>
<td>Images that contain dangerous content.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_IMAGE_HARASSMENT</code></td>
<td>Images that contain harassment.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_IMAGE_SEXUALLY_EXPLICIT</code></td>
<td>Images that contain sexually explicit content.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_JAILBREAK</code></td>
<td>Prompts designed to bypass safety filters.</td>
</tr>
</tbody>
</table>
