---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features/list
title: 'Method: features.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.features.list

Lists Features in a given FeatureGroup.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /features`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list Features. Format for entityType as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` Format for featureGroup as parent: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

### Query parameters

`filter` `string`

Lists the Features that match the filter expression. The following filters are supported:

  - `valueType` : Supports = and \!= comparisons.
  - `createTime` : Supports =, \!=, \<, \>, \>=, and \<= comparisons. Values must be in RFC 3339 format.
  - `updateTime` : Supports =, \!=, \<, \>, \>=, and \<= comparisons. Values must be in RFC 3339 format.
  - `labels` : Supports key-value equality as well as key presence.

Examples:

  - `valueType = DOUBLE` --\> Features whose type is DOUBLE.
  - `createTime > \"2020-01-31T15:30:00.000000Z\" OR updateTime > \"2020-01-31T15:30:00.000000Z\"` --\> EntityTypes created or updated after 2020-01-31T15:30:00.000000Z.
  - `labels.active = yes AND labels.env = prod` --\> Features having both (active: yes) and (env: prod) labels.
  - `labels.env: *` --\> Any feature which has a label with 'env' as the key.

`pageSize` `integer`

The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 1000 Features will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000.

`pageToken` `string`

A page token, received from a previous `  FeaturestoreService.ListFeatures  ` call or `  FeatureRegistryService.ListFeatures  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  FeaturestoreService.ListFeatures  ` or `  FeatureRegistryService.ListFeatures  ` must match the call that provided the page token.

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

  - `featureId`
  - `valueType` (Not supported for FeatureRegistry feature)
  - `createTime`
  - `updateTime`

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`latestStatsCount` `integer`

Only applicable for Agent Platform feature Store (Legacy). If set, return the most recent `  ListFeaturesRequest.latest_stats_count  ` of stats for each feature in response. Valid value is \[0, 10\]. If number of stats exists \< `  ListFeaturesRequest.latest_stats_count  ` , return all existing stats.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListFeaturesResponse  ` .
