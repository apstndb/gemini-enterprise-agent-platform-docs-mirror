---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails
title: 'REST Resource: projects.locations.nasJobs.nasTrialDetails'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NasTrialDetail

Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.

Fields

`name` `string`

Output only. Resource name of the NasTrialDetail.

`parameters` `string`

The parameters for the NasJob NasTrial.

`searchTrial` ` object ( NasTrial  ` )

The requested search NasTrial.

`trainTrial` ` object ( NasTrial  ` )

The train NasTrial corresponding to `  searchTrial  ` . Only populated if `  searchTrial  ` is used for training.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;parameters&quot;: string,&quot;searchTrial&quot;: {object (NasTrial)},&quot;trainTrial&quot;: {object (NasTrial)}}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            get           `

Gets a NasTrialDetail.

### `            list           `

List top NasTrialDetails of a NasJob.
