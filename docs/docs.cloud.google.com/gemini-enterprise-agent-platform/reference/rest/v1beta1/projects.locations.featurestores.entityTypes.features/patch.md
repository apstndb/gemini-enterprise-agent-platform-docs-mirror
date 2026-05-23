---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes.features/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes.features/patch
title: 'Method: features.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.features.patch

Updates the parameters of a single feature.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{feature.name}`  

`PATCH https://{service-endpoint}/v1beta1/{feature.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`feature.name` `string`

Immutable. name of the feature. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}/features/{feature}` `projects/{project}/locations/{location}/featureGroups/{featureGroup}/features/{feature}`

The last part feature is assigned by the client. The feature can be up to 64 characters long and can consist only of ASCII Latin letters A-Z and a-z, underscore(\_), and ASCII digits 0-9 starting with a letter. The value will be unique given an entity type.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the updateMask to `*` to override all fields.

Updatable fields:

  - `description`
  - `labels`
  - `disableMonitoring` (Not supported for FeatureRegistryService feature)
  - `pointOfContact` (Not supported for FeaturestoreService FeatureStore)

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Feature  ` .

### Response body

If successful, the response body contains an instance of `  Feature  ` .
