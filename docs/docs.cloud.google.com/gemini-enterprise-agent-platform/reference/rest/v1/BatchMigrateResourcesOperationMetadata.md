---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BatchMigrateResourcesOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BatchMigrateResourcesOperationMetadata
title: BatchMigrateResourcesOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for `  MigrationService.BatchMigrateResources  ` .

Fields

`genericMetadata` ` object ( GenericOperationMetadata  ` )

The common part of the operation metadata.

`partialResults[]` ` object ( PartialResult  ` )

Partial results that reflect the latest migration operation progress.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;genericMetadata&quot;: {object (GenericOperationMetadata)},&quot;partialResults&quot;: [{object (PartialResult)}]}</code></pre></td>
</tr>
</tbody>
</table>

## PartialResult

Represents a partial result in batch migration operation for one `  MigrateResourceRequest  ` .

Fields

`request` ` object ( MigrateResourceRequest  ` )

It's the same as the value in `  BatchMigrateResourcesRequest.migrate_resource_requests  ` .

`result` `Union type`

If the resource's migration is ongoing, none of the result will be set. If the resource's migration is finished, either error or one of the migrated resource name will be filled. `result` can be only one of the following:

`error` ` object ( Status  ` )

The error result of the migration request in case of failure.

`model` `string`

Migrated model resource name.

`dataset` `string`

Migrated dataset resource name.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;request&quot;: {object (MigrateResourceRequest)},// result&quot;error&quot;: {object (Status)},&quot;model&quot;: string,&quot;dataset&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>
