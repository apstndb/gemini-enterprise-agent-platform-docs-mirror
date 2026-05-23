---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagEngineConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagEngineConfig
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

` enterprise (deprecated)  ` ` object ( Enterprise  ` )

> This item is deprecated\!

Sets the RagManagedDb to the Enterprise tier.

` scaled (deprecated)  ` ` object ( Scaled  ` )

> This item is deprecated\!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Scaled tier.

` basic (deprecated)  ` ` object ( Basic  ` )

> This item is deprecated\!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Basic tier.

` unprovisioned (deprecated)  ` ` object ( Unprovisioned  ` )

> This item is deprecated\!

Deprecated: Use `mode` instead to set the tier under Spanner. Sets the RagManagedDb to the Unprovisioned tier.

`mode` `Union type`

The choice of backend for your RagEngine. `mode` can be only one of the following:

`serverless` ` object ( Serverless  ` )

Sets the backend to be the serverless mode offered by RAG Engine.

`spanner` ` object ( Spanner  ` )

Sets the RAG Engine backend to be RagManagedDb, built on top of Spanner.

NOTE: This is the default mode (w/ Basic Tier) if not explicitly chosen.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// tier&quot;enterprise&quot;: {object (Enterprise)},&quot;scaled&quot;: {object (Scaled)},&quot;basic&quot;: {object (Basic)},&quot;unprovisioned&quot;: {object (Unprovisioned)}// Union type// mode&quot;serverless&quot;: {object (Serverless)},&quot;spanner&quot;: {object (Spanner)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Enterprise

This type has no fields.

> This item is deprecated\!

Enterprise tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

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

## Serverless

This type has no fields.

message to configure the serverless mode offered by RAG Engine.

## Spanner

message to configure the Spanner database used by RagManagedDb.

Fields

`tier` `Union type`

The tier of the RagManagedDb, built on top of Spanner. `tier` can be only one of the following:

`scaled` ` object ( Scaled  ` )

Sets the RagManagedDb to the Scaled tier.

`basic` ` object ( Basic  ` )

Sets the RagManagedDb to the Basic tier. This is the default tier for Spanner mode if not explicitly chosen.

`unprovisioned` ` object ( Unprovisioned  ` )

Sets the RagManagedDb to the Unprovisioned tier.

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
