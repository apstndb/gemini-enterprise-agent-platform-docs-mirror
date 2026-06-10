---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelConfig
title: PublisherModelConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This message contains configs of a publisher model.

Fields

`loggingConfig` ` object ( PredictRequestResponseLoggingConfig  ` )

Optional. The prediction request/response logging config.

`dataSharingEnabledProvider` ` enum ( ModelProvider  ` )

Optional. The model provider (publisher) for which the customer has enabled data sharing. For publisher models that are configured to require data sharing, a prediction request is only allowed when the model's publisher matches this provider. Otherwise, the request is rejected.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;loggingConfig&quot;: {object (PredictRequestResponseLoggingConfig)},&quot;dataSharingEnabledProvider&quot;: enum (ModelProvider)}</code></pre></td>
</tr>
</tbody>
</table>

## ModelProvider

A model provider (publisher) that prediction data may be shared with.

Enums

`MODEL_PROVIDER_UNSPECIFIED`

Unspecified model provider.

`ANTHROPIC`

Anthropic.
