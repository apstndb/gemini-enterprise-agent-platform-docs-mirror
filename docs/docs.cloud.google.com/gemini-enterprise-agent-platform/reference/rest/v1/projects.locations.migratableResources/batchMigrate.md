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

`migrateResourceRequests[]` ` object ( MigrateResourceRequest  ` )

Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## MigrateResourceRequest

Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Agent Platform.

Fields

`request` `Union type`

`request` can be only one of the following:

`migrateMlEngineModelVersionConfig` ` object ( MigrateMlEngineModelVersionConfig  ` )

Config for migrating version in ml.googleapis.com to Agent Platform's Model.

`migrateAutomlModelConfig` ` object ( MigrateAutomlModelConfig  ` )

Config for migrating Model in automl.googleapis.com to Agent Platform's Model.

`migrateAutomlDatasetConfig` ` object ( MigrateAutomlDatasetConfig  ` )

Config for migrating Dataset in automl.googleapis.com to Agent Platform's Dataset.

` migrateDataLabelingDatasetConfig (deprecated)  ` ` object ( MigrateDataLabelingDatasetConfig  ` )

> This item is deprecated\!

Deprecated: data labeling service is shut down. Config for migrating Dataset in datalabeling.googleapis.com to Agent Platform's Dataset.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// request&quot;migrateMlEngineModelVersionConfig&quot;: {object (MigrateMlEngineModelVersionConfig)},&quot;migrateAutomlModelConfig&quot;: {object (MigrateAutomlModelConfig)},&quot;migrateAutomlDatasetConfig&quot;: {object (MigrateAutomlDatasetConfig)},&quot;migrateDataLabelingDatasetConfig&quot;: {object (MigrateDataLabelingDatasetConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

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
  &quot;endpoint&quot;: string,
  &quot;modelVersion&quot;: string,
  &quot;modelDisplayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## MigrateAutomlModelConfig

Config for migrating Model in automl.googleapis.com to Agent Platform's Model.

Fields

`model` `string`

Required. Full resource name of automl Model. Format: `projects/{project}/locations/{location}/models/{model}` .

`modelDisplayName` `string`

Optional. Display name of the model in Agent Platform. System will pick a display name if unspecified.

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
  &quot;model&quot;: string,
  &quot;modelDisplayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## MigrateAutomlDatasetConfig

Config for migrating Dataset in automl.googleapis.com to Agent Platform's Dataset.

Fields

`dataset` `string`

Required. Full resource name of automl Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}` .

`datasetDisplayName` `string`

Required. Display name of the Dataset in Agent Platform. System will pick a display name if unspecified.

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
  &quot;dataset&quot;: string,
  &quot;datasetDisplayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## MigrateDataLabelingDatasetConfig

Config for migrating Dataset in datalabeling.googleapis.com to Agent Platform's Dataset.

Fields

`dataset` `string`

Required. Full resource name of data labeling Dataset. Format: `projects/{project}/datasets/{dataset}` .

`datasetDisplayName` `string`

Optional. Display name of the Dataset in Agent Platform. System will pick a display name if unspecified.

`migrateDataLabelingAnnotatedDatasetConfigs[]` ` object ( MigrateDataLabelingAnnotatedDatasetConfig  ` )

Optional. Configs for migrating AnnotatedDataset in datalabeling.googleapis.com to Agent Platform's SavedQuery. The specified AnnotatedDatasets have to belong to the datalabeling Dataset.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataset&quot;: string,&quot;datasetDisplayName&quot;: string,&quot;migrateDataLabelingAnnotatedDatasetConfigs&quot;: [{object (MigrateDataLabelingAnnotatedDatasetConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

## MigrateDataLabelingAnnotatedDatasetConfig

Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Agent Platform's SavedQuery.

Fields

`annotatedDataset` `string`

Required. Full resource name of data labeling AnnotatedDataset. Format: `projects/{project}/datasets/{dataset}/annotatedDatasets/{annotatedDataset}` .

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
  &quot;annotatedDataset&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
