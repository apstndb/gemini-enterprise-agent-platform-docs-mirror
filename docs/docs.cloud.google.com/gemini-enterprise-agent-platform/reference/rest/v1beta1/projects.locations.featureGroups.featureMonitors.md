---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors
title: 'REST Resource: projects.locations.featureGroups.featureMonitors'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeatureMonitor

Agent Platform feature Monitor.

Fields

`name` `string`

Identifier. name of the FeatureMonitor. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}`

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this FeatureMonitor was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this FeatureMonitor was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your FeatureMonitor.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureMonitor(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`description` `string`

Optional. description of the FeatureMonitor.

`scheduleConfig` ` object ( ScheduleConfig  ` )

Required. Schedule config for the FeatureMonitor.

`featureSelectionConfig` ` object ( FeatureSelectionConfig  ` )

Required. feature selection config for the FeatureMonitor.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;description&quot;: string,&quot;scheduleConfig&quot;: {object (ScheduleConfig)},&quot;featureSelectionConfig&quot;: {object (FeatureSelectionConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ScheduleConfig

Schedule configuration for the FeatureMonitor.

Fields

`cron` `string`

Cron schedule ( <https://en.wikipedia.org/wiki/Cron> ) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON\_TZ=${IANA\_TIME\_ZONE}" or "TZ=${IANA\_TIME\_ZONE}". The ${IANA\_TIME\_ZONE} may only be a valid string from IANA time zone database. For example, "CRON\_TZ=America/New\_York 1 \* \* \* \*", or "TZ=America/New\_York 1 \* \* \* \*".

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
  &quot;cron&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a new FeatureMonitor in a given project, location and FeatureGroup.

### `            delete           `

Deletes a single FeatureMonitor.

### `            get           `

Gets details of a single FeatureMonitor.

### `            list           `

Lists FeatureGroups in a given project and location.

### `            patch           `

Updates the parameters of a single FeatureMonitor.
