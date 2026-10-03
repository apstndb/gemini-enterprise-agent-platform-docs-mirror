---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups
title: 'REST Resource: projects.locations.featureGroups'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeatureGroup

Agent Platform feature Group.

Fields

`name` `string`

Identifier. name of the FeatureGroup. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this FeatureGroup was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this FeatureGroup was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your FeatureGroup.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureGroup(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`description` `string`

Optional. description of the FeatureGroup.

`serviceAgentType` `enum ( `[`ServiceAgentType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups#ServiceAgentType)` )`

Optional. service agent type used during jobs under a FeatureGroup. By default, the Agent Platform service Agent is used. When using an IAM Policy to isolate this FeatureGroup within a project, a separate service account should be provisioned by setting this field to `SERVICE_AGENT_TYPE_FEATURE_GROUP` . This will generate a separate service account to access the BigQuery source table.

`serviceAccountEmail` `string`

Output only. A service Account unique to this FeatureGroup. The role bigquery.dataViewer should be granted to this service account to allow Agent Platform feature Store to access source data while running jobs under this FeatureGroup.

`source` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bigQuery` `object ( `[`BigQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups#BigQuery)` )`

Indicates that features for this group come from BigQuery Table/View. By default treats the source as a sparse time series source. The BigQuery source table or view must have at least one entity id column and a column named `feature_timestamp` .

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "description": string,
  "serviceAgentType": enum (ServiceAgentType),
  "serviceAccountEmail": string,

  // source
  "bigQuery": {
    object (BigQuery)
  }
  // Union type
}
```

## BigQuery

Input source type for BigQuery Tables and Views.

Fields

`bigQuerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQuerySource)` )`

Required. Immutable. The BigQuery source URI that points to either a BigQuery Table or View.

`entityIdColumns[]` `string`

Optional. columns to construct entityId / row keys. If not provided defaults to `entityId` .

`staticDataSource` `boolean`

Optional. Set if the data source is not a time-series.

`timeSeries` `object ( `[`TimeSeries`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups#TimeSeries)` )`

Optional. If the source is a time-series source, this can be set to control how downstream sources (ex: [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews#FeatureView) ) will treat time-series sources. If not set, will treat the source as a time-series source with `feature_timestamp` as timestamp column and no scan boundary.

`dense` `boolean`

Optional. If set, all feature values will be fetched from a single row per unique entityId including nulls. If not set, will collapse all rows for each unique entityId into a singe row with any non-null values if present, if no non-null values are present will sync null. ex: If source has schema `(entityId, feature_timestamp, f0, f1)` and the following rows: `(e1, 2020-01-01T10:00:00.123Z, 10, 15)` `(e1, 2020-02-01T10:00:00.123Z, 20, null)` If dense is set, `(e1, 20, null)` is synced to online stores. If dense is not set, `(e1, 20, 15)` is synced to online stores.

**JSON representation**

```
{
  "bigQuerySource": {
    object (BigQuerySource)
  },
  "entityIdColumns": [
    string
  ],
  "staticDataSource": boolean,
  "timeSeries": {
    object (TimeSeries)
  },
  "dense": boolean
}
```

## TimeSeries

Fields

`timestampColumn` `string`

Optional. column hosting timestamp values for a time-series source. Will be used to determine the latest `featureValues` for each entity. Optional. If not provided, column named `feature_timestamp` of type `TIMESTAMP` will be used.

**JSON representation**

```
{
  "timestampColumn": string
}
```

## ServiceAgentType

service agent type used during jobs under a FeatureGroup.

| Enums                              |                                                                                                                                                                                                                                  |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SERVICE_AGENT_TYPE_UNSPECIFIED`   | By default, the project-level Agent Platform service Agent is enabled.                                                                                                                                                           |
| `SERVICE_AGENT_TYPE_PROJECT`       | Specifies the project-level Agent Platform service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents)> .                                                                                    |
| `SERVICE_AGENT_TYPE_FEATURE_GROUP` | Enable a FeatureGroup service account to be created by Agent Platform and output in the field `serviceAccountEmail` . This service account will be used to read from the source BigQuery table during jobs under a FeatureGroup. |

| Methods                                                                                                                                                           |                                                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/create)                         | Creates a new FeatureGroup in a given project and location.      |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/delete)                         | Deletes a single FeatureGroup.                                   |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/get)                               | Gets details of a single FeatureGroup.                           |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/getIamPolicy)             | Gets the access control policy for a resource.                   |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/list)                             | Lists FeatureGroups in a given project and location.             |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/patch)                           | Updates the parameters of a single FeatureGroup.                 |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/setIamPolicy)             | Sets the access control policy on the specified resource.        |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups/testIamPermissions) | Returns permissions that a caller has on the specified resource. |
