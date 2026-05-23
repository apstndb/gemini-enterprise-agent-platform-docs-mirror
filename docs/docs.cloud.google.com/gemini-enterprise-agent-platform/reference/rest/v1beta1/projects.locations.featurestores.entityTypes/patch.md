---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/patch
title: 'Method: entityTypes.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.patch

Updates the parameters of a single EntityType.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{entityType.name}`  

`PATCH https://{service-endpoint}/v1beta1/{entityType.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType.name` `string`

Immutable. name of the EntityType. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`

The last part entityType is assigned by the client. The entityType can be up to 64 characters long and can consist only of ASCII Latin letters A-Z and a-z and underscore(\_), and ASCII digits 0-9 starting with a letter. The value will be unique given a featurestore.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the updateMask to `*` to override all fields.

Updatable fields:

  - `description`
  - `labels`
  - `monitoringConfig.snapshot_analysis.disabled`
  - `monitoringConfig.snapshot_analysis.monitoring_interval_days`
  - `monitoringConfig.snapshot_analysis.staleness_days`
  - `monitoringConfig.import_features_analysis.state`
  - `monitoringConfig.import_features_analysis.anomaly_detection_baseline`
  - `monitoringConfig.numerical_threshold_config.value`
  - `monitoringConfig.categorical_threshold_config.value`
  - `offlineStorageTtlDays`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  EntityType  ` .

### Response body

If successful, the response body contains an instance of `  EntityType  ` .
