---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig
title: RagEngineConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Config for RagEngine.

Fields

`name` `string`

Identifier. The name of the RagEngineConfig. Format: `projects/{project}/locations/{location}/ragEngineConfig`

`ragManagedDbConfig` ` object ( RagManagedDbConfig  ` )

The config of the RagManagedDb used by RagEngine.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;ragManagedDbConfig&quot;: {object (RagManagedDbConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RagManagedDbConfig

Configuration message for RagManagedDb used by RagEngine.

Fields

`tier` `Union type`

The tier of the RagManagedDb. `tier` can be only one of the following:

` scaled (deprecated)  ` ` object ( Scaled  ` )

> This item is deprecated\!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Scaled tier.

` basic (deprecated)  ` ` object ( Basic  ` )

> This item is deprecated\!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Basic tier.

` unprovisioned (deprecated)  ` ` object ( Unprovisioned  ` )

> This item is deprecated\!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Unprovisioned tier.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// tier&quot;scaled&quot;: {object (Scaled)},&quot;basic&quot;: {object (Basic)},&quot;unprovisioned&quot;: {object (Unprovisioned)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Scaled

This type has no fields.

Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

## Basic

This type has no fields.

Basic tier is a cost-effective and low compute tier suitable for the following cases: \* Experimenting with RagManagedDb. \* Small data size. \* Latency insensitive workload. \* Only using RAG Engine with external vector DBs.

NOTE: This is the default tier under Spanner mode if not explicitly chosen.

## Unprovisioned

This type has no fields.

Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.
