---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BatchMigrateResourcesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BatchMigrateResourcesResponse
title: BatchMigrateResourcesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  MigrationService.BatchMigrateResources  ` .

Fields

`migrateResourceResponses[]` ` object ( MigrateResourceResponse  ` )

Successfully migrated resources.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;migrateResourceResponses&quot;: [{object (MigrateResourceResponse)}]}</code></pre></td>
</tr>
</tbody>
</table>

## MigrateResourceResponse

Describes a successfully migrated resource.

Fields

`migratableResource` ` object ( MigratableResource  ` )

Before migration, the identifier in ml.googleapis.com, automl.googleapis.com or datalabeling.googleapis.com.

`migrated_resource` `Union type`

After migration, the resource name in Agent Platform. `migrated_resource` can be only one of the following:

`dataset` `string`

Migrated Dataset's resource name.

`model` `string`

Migrated Model's resource name.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;migratableResource&quot;: {object (MigratableResource)},// migrated_resource&quot;dataset&quot;: string,&quot;model&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>
