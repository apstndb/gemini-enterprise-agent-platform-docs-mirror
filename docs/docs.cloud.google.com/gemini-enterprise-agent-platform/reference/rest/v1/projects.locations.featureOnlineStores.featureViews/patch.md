---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/patch
title: 'Method: featureViews.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.patch

Updates the parameters of a single FeatureView.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{featureView.name}`  

`PATCH https://{service-endpoint}/v1/{featureView.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView.name` `string`

Identifier. name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Field mask is used to specify the fields to be overwritten in the FeatureView resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the updateMask to `*` to override all fields.

Updatable fields:

  - `labels`
  - `serviceAgentType`
  - `bigQuerySource`
  - `bigQuerySource.uri`
  - `bigQuerySource.entity_id_columns`
  - `featureRegistrySource`
  - `featureRegistrySource.feature_groups`
  - `syncConfig`
  - `syncConfig.cron`
  - `optimizedConfig.automatic_resources`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  FeatureView  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
