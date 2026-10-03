---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchMigrateResourcesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchMigrateResourcesResponse
title: BatchMigrateResourcesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`MigrationService.BatchMigrateResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.migratableResources/batchMigrate#google.cloud.aiplatform.v1beta1.MigrationService.BatchMigrateResources) .

Fields

`migrateResourceResponses[]` `object ( `[`MigrateResourceResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchMigrateResourcesResponse#MigrateResourceResponse)` )`

Successfully migrated resources.

**JSON representation**

```
{
  "migrateResourceResponses": [
    {
      object (MigrateResourceResponse)
    }
  ]
}
```

## MigrateResourceResponse

Describes a successfully migrated resource.

Fields

`migratableResource` `object ( `[`MigratableResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.migratableResources/search#MigratableResource)` )`

Before migration, the identifier in ml.googleapis.com, automl.googleapis.com or datalabeling.googleapis.com.

`migrated_resource` `Union type`

After migration, the resource name in Agent Platform. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`dataset` `string`

Migrated Dataset's resource name.

`model` `string`

Migrated Model's resource name.

End of mutually exclusive fields.

**JSON representation**

```
{
  "migratableResource": {
    object (MigratableResource)
  },

  // migrated_resource
  "dataset": string,
  "model": string
  // Union type
}
```
