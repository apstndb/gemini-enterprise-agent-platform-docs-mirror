---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate
title: 'Method: migratableResources.batchMigrate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.migratableResources.batchMigrate

Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Agent Platform.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /migratableResources:batchMigrate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The location of the migrated resource will live in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`migrateResourceRequests[]` `object ( `[`MigrateResourceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate#MigrateResourceRequest)` )`

Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch.

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

## MigrateResourceRequest

Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Agent Platform.

Fields

`request` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`migrateMlEngineModelVersionConfig` `object ( `[`MigrateMlEngineModelVersionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate#MigrateMlEngineModelVersionConfig)` )`

Config for migrating version in ml.googleapis.com to Agent Platform's Model.

`migrateAutomlModelConfig` `object ( `[`MigrateAutomlModelConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate#MigrateAutomlModelConfig)` )`

Config for migrating Model in automl.googleapis.com to Agent Platform's Model.

`migrateAutomlDatasetConfig` `object ( `[`MigrateAutomlDatasetConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate#MigrateAutomlDatasetConfig)` )`

Config for migrating Dataset in automl.googleapis.com to Agent Platform's Dataset.

`migrateDataLabelingDatasetConfig `**`(deprecated)`** `object ( `[`MigrateDataLabelingDatasetConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate#MigrateDataLabelingDatasetConfig)` )`

> This item is deprecated!

Deprecated: data labeling service is shut down. Config for migrating Dataset in datalabeling.googleapis.com to Agent Platform's Dataset.

End of mutually exclusive fields.

**JSON representation**

```
{

  // request
  "migrateMlEngineModelVersionConfig": {
    object (MigrateMlEngineModelVersionConfig)
  },
  "migrateAutomlModelConfig": {
    object (MigrateAutomlModelConfig)
  },
  "migrateAutomlDatasetConfig": {
    object (MigrateAutomlDatasetConfig)
  },
  "migrateDataLabelingDatasetConfig": {
    object (MigrateDataLabelingDatasetConfig)
  }
  // Union type
}
```

## MigrateMlEngineModelVersionConfig

Config for migrating version in ml.googleapis.com to Agent Platform's Model.

Fields

`endpoint` `string`

Required. The ml.googleapis.com endpoint that this model version should be migrated from. Example values:

- ml.googleapis.com

- us-centrall-ml.googleapis.com

- europe-west4-ml.googleapis.com

- asia-east1-ml.googleapis.com

`modelVersion` `string`

Required. Full resource name of ml engine model version. Format: `projects/{project}/models/{model}/versions/{version}` .

`modelDisplayName` `string`

Required. Display name of the model in Agent Platform. System will pick a display name if unspecified.

**JSON representation**

```
{
  "endpoint": string,
  "modelVersion": string,
  "modelDisplayName": string
}
```

## MigrateAutomlModelConfig

Config for migrating Model in automl.googleapis.com to Agent Platform's Model.

Fields

`model` `string`

Required. Full resource name of automl Model. Format: `projects/{project}/locations/{location}/models/{model}` .

`modelDisplayName` `string`

Optional. Display name of the model in Agent Platform. System will pick a display name if unspecified.

**JSON representation**

```
{
  "model": string,
  "modelDisplayName": string
}
```

## MigrateAutomlDatasetConfig

Config for migrating Dataset in automl.googleapis.com to Agent Platform's Dataset.

Fields

`dataset` `string`

Required. Full resource name of automl Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}` .

`datasetDisplayName` `string`

Required. Display name of the Dataset in Agent Platform. System will pick a display name if unspecified.

**JSON representation**

```
{
  "dataset": string,
  "datasetDisplayName": string
}
```

## MigrateDataLabelingDatasetConfig

Config for migrating Dataset in datalabeling.googleapis.com to Agent Platform's Dataset.

Fields

`dataset` `string`

Required. Full resource name of data labeling Dataset. Format: `projects/{project}/datasets/{dataset}` .

`datasetDisplayName` `string`

Optional. Display name of the Dataset in Agent Platform. System will pick a display name if unspecified.

`migrateDataLabelingAnnotatedDatasetConfigs[]` `object ( `[`MigrateDataLabelingAnnotatedDatasetConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate#MigrateDataLabelingAnnotatedDatasetConfig)` )`

Optional. Configs for migrating AnnotatedDataset in datalabeling.googleapis.com to Agent Platform's SavedQuery. The specified AnnotatedDatasets have to belong to the datalabeling Dataset.

**JSON representation**

```
{
  "dataset": string,
  "datasetDisplayName": string,
  "migrateDataLabelingAnnotatedDatasetConfigs": [
    {
      object (MigrateDataLabelingAnnotatedDatasetConfig)
    }
  ]
}
```

## MigrateDataLabelingAnnotatedDatasetConfig

Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Agent Platform's SavedQuery.

Fields

`annotatedDataset` `string`

Required. Full resource name of data labeling AnnotatedDataset. Format: `projects/{project}/datasets/{dataset}/annotatedDatasets/{annotatedDataset}` .

**JSON representation**

```
{
  "annotatedDataset": string
}
```
