---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchMigrateResourcesOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchMigrateResourcesOperationMetadata
title: BatchMigrateResourcesOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`MigrationService.BatchMigrateResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.migratableResources/batchMigrate#google.cloud.aiplatform.v1beta1.MigrationService.BatchMigrateResources) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

The common part of the operation metadata.

`partialResults[]` `object ( `[`PartialResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchMigrateResourcesOperationMetadata#PartialResult)` )`

Partial results that reflect the latest migration operation progress.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "partialResults": [
    {
      object (PartialResult)
    }
  ]
}
```

## PartialResult

Represents a partial result in batch migration operation for one [`MigrateResourceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.migratableResources/batchMigrate#MigrateResourceRequest) .

Fields

`request` `object ( `[`MigrateResourceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.migratableResources/batchMigrate#MigrateResourceRequest)` )`

It's the same as the value in [`BatchMigrateResourcesRequest.migrate_resource_requests`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.migratableResources/batchMigrate#body.request_body.FIELDS.migrate_resource_requests) .

`result` `Union type`

If the resource's migration is ongoing, none of the result will be set. If the resource's migration is finished, either error or one of the migrated resource name will be filled. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

The error result of the migration request in case of failure.

`model` `string`

Migrated model resource name.

`dataset` `string`

Migrated dataset resource name.

End of mutually exclusive fields.

**JSON representation**

```
{
  "request": {
    object (MigrateResourceRequest)
  },

  // result
  "error": {
    object (Status)
  },
  "model": string,
  "dataset": string
  // Union type
}
```
