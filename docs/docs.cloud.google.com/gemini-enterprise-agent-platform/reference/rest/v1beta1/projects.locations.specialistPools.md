---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools
title: 'REST Resource: projects.locations.specialistPools'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SpecialistPool

SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

Fields

`name` `string`

Required. The resource name of the SpecialistPool.

`displayName` `string`

Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level.

`specialistManagersCount` `integer`

Output only. The number of managers in this SpecialistPool.

`specialistManagerEmails[]` `string`

The email addresses of the managers in the SpecialistPool.

`pendingDataLabelingJobs[]` `string`

Output only. The resource name of the pending data labeling jobs.

`specialistWorkerEmails[]` `string`

The email addresses of workers in the SpecialistPool.

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
  &quot;name&quot;: string,
  &quot;displayName&quot;: string,
  &quot;specialistManagersCount&quot;: integer,
  &quot;specialistManagerEmails&quot;: [
    string
  ],
  &quot;pendingDataLabelingJobs&quot;: [
    string
  ],
  &quot;specialistWorkerEmails&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a SpecialistPool.

### `            delete           `

Deletes a SpecialistPool as well as all Specialists in the pool.

### `            get           `

Gets a SpecialistPool.

### `            list           `

Lists SpecialistPools in a Location.

### `            patch           `

Updates a SpecialistPool.
