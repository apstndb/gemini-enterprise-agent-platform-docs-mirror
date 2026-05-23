---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModalityTokenCount
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModalityTokenCount
title: ModalityTokenCount
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a breakdown of token usage by modality.

This message is used in \[CountTokensResponse\]\[google.cloud.aiplatform.master.CountTokensResponse\] and `  GenerateContentResponse.UsageMetadata  ` to provide a detailed view of how many tokens are used by each modality (e.g., text, image, video) in a request. This is particularly useful for multimodal models, allowing you to track and manage token consumption for billing and quota purposes.

Fields

`modality` ` enum ( Modality  ` )

The modality that this token count applies to.

`tokenCount` `integer`

The number of tokens counted for this modality.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modality&quot;: enum (Modality),&quot;tokenCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## Modality

The modality of a `Part` of a `Content` message. A modality is the type of media, such as an image or a video. It is used to categorize the content of a `Part` for token counting purposes.

Enums

`MODALITY_UNSPECIFIED`

When a modality is not specified, it is treated as `TEXT` .

`TEXT`

The `Part` contains plain text.

`IMAGE`

The `Part` contains an image.

`VIDEO`

The `Part` contains a video.

`AUDIO`

The `Part` contains audio.

`DOCUMENT`

The `Part` contains a document, such as a PDF.
