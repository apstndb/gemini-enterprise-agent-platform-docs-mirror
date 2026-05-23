---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews.featureViewSyncs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews.featureViewSyncs
title: 'REST Resource: projects.locations.featureOnlineStores.featureViews.featureViewSyncs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeatureViewSync

FeatureViewSync is a representation of sync operation which copies data from data source to feature View in Online Store.

Fields

`name` `string`

Identifier. name of the FeatureViewSync. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}/featureViewSyncs/{featureViewSync}`

`createTime` ` string ( Timestamp  ` format)

Output only. time when this FeatureViewSync is created. Creation of a FeatureViewSync means that the job is pending / waiting for sufficient resources but may not have started the actual data transfer yet.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`runTime` ` object ( Interval  ` )

Output only. time when this FeatureViewSync is finished.

`finalStatus` ` object ( Status  ` )

Output only. Final status of the FeatureViewSync.

`syncSummary` ` object ( SyncSummary  ` )

Output only. Summary of the sync job.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;runTime&quot;: {object (Interval)},&quot;finalStatus&quot;: {object (Status)},&quot;syncSummary&quot;: {object (SyncSummary)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## SyncSummary

Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.

Fields

`rowSynced` `string ( int64 format)`

Output only. Total number of rows synced.

`totalSlot` `string ( int64 format)`

Output only. BigQuery slot milliseconds consumed for the sync job.

`systemWatermarkTime` ` string ( Timestamp  ` format)

Lower bound of the system time watermark for the sync job. This is only set for continuously syncing feature views.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;rowSynced&quot;: string,
  &quot;totalSlot&quot;: string,
  &quot;systemWatermarkTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            get           `

Gets details of a single FeatureViewSync.

### `            list           `

Lists FeatureViewSyncs in a given FeatureView.
