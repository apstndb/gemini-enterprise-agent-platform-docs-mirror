---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores
title: 'REST Resource: projects.locations.featureOnlineStores'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeatureOnlineStore

Agent Platform feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The feature Online Store is a top-level container.

Fields

`name` `string`

Identifier. name of the FeatureOnlineStore. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this FeatureOnlineStore was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this FeatureOnlineStore was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your FeatureOnlineStore.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#State)` )`

Output only. state of the featureOnlineStore.

`dedicatedServingEndpoint` `object ( `[`DedicatedServingEndpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#DedicatedServingEndpoint)` )`

Optional. The dedicated serving endpoint for this FeatureOnlineStore, which is different from common Vertex service endpoint.

`embeddingManagement `**`(deprecated)`** `object ( `[`EmbeddingManagement`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#EmbeddingManagement)` )`

> This item is deprecated!

Optional. Deprecated: This field is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Optional. Customer-managed encryption key spec for data storage. If set, online store will be secured by this key.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`storage_type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bigtable` `object ( `[`Bigtable`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#Bigtable)` )`

Contains settings for the Cloud Bigtable instance that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore.

`optimized` `object ( `[`Optimized`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#Optimized)` )`

Contains settings for the Optimized store that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. When choose Optimized storage type, need to set [`PrivateServiceConnectConfig.enable_private_service_connect`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PrivateServiceConnectConfig#FIELDS.enable_private_service_connect) to use private endpoint. Otherwise will use public endpoint by default.

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
  "state": enum (State),
  "dedicatedServingEndpoint": {
    object (DedicatedServingEndpoint)
  },
  "embeddingManagement": {
    object (EmbeddingManagement)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,

  // storage_type
  "bigtable": {
    object (Bigtable)
  },
  "optimized": {
    object (Optimized)
  }
  // Union type
}
```

## Bigtable

Fields

`autoScaling` `object ( `[`AutoScaling`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#AutoScaling)` )`

Required. Autoscaling config applied to Bigtable Instance.

`enableDirectBigtableAccess` `boolean`

Optional. It true, enable direct access to the Bigtable instance.

`bigtableMetadata` `object ( `[`BigtableMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores#BigtableMetadata)` )`

Output only. metadata of the Bigtable instance. Output only.

`zone` `string`

Optional. The zone where the underlying Bigtable cluster for the primary Bigtable instance will be provisioned. Only the zone must be provided. For example, only "us-central1-a" should be provided.

**JSON representation**

```
{
  "autoScaling": {
    object (AutoScaling)
  },
  "enableDirectBigtableAccess": boolean,
  "bigtableMetadata": {
    object (BigtableMetadata)
  },
  "zone": string
}
```

## AutoScaling

Fields

`minNodeCount` `integer`

Required. The minimum number of nodes to scale down to. Must be greater than or equal to 1.

`maxNodeCount` `integer`

Required. The maximum number of nodes to scale up to. Must be greater than or equal to minNodeCount, and less than or equal to 10 times of 'minNodeCount'.

`cpuUtilizationTarget` `integer`

Optional. A percentage of the cluster's CPU capacity. Can be from 10% to 80%. When a cluster's CPU utilization exceeds the target that you have set, Bigtable immediately adds nodes to the cluster. When CPU utilization is substantially lower than the target, Bigtable removes nodes. If not set will default to 50%.

**JSON representation**

```
{
  "minNodeCount": integer,
  "maxNodeCount": integer,
  "cpuUtilizationTarget": integer
}
```

## BigtableMetadata

metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

Fields

`tenantProjectId` `string`

Tenant project id.

`instanceId` `string`

The Cloud Bigtable instance id.

`tableId` `string`

The Cloud Bigtable table id.

**JSON representation**

```
{
  "tenantProjectId": string,
  "instanceId": string,
  "tableId": string
}
```

## Optimized

This type has no fields.

Optimized storage type

## State

Possible states a featureOnlineStore can have.

| Enums               |                                                                                                                                                                                                                                                                  |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Default value. This value is unused.                                                                                                                                                                                                                             |
| `STABLE`            | state when the featureOnlineStore configuration is not being updated and the fields reflect the current configuration of the featureOnlineStore. The featureOnlineStore is usable in this state.                                                                 |
| `UPDATING`          | The state of the featureOnlineStore configuration when it is being updated. During an update, the fields reflect either the original configuration or the updated configuration of the featureOnlineStore. The featureOnlineStore is still usable in this state. |

## DedicatedServingEndpoint

The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.

Fields

`publicEndpointDomainName` `string`

Output only. This field will be populated with the domain name to use for this FeatureOnlineStore

`privateServiceConnectConfig` `object ( `[`PrivateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PrivateServiceConnectConfig)` )`

Optional. Private service connect config. The private service connection is available only for Optimized storage type, not for embedding management now. If [`PrivateServiceConnectConfig.enable_private_service_connect`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PrivateServiceConnectConfig#FIELDS.enable_private_service_connect) set to true, customers will use private service connection to send request. Otherwise, the connection will set to public endpoint.

`serviceAttachment` `string`

Output only. The name of the service attachment resource. Populated if private service connect is enabled and after FeatureViewSync is created.

**JSON representation**

```
{
  "publicEndpointDomainName": string,
  "privateServiceConnectConfig": {
    object (PrivateServiceConnectConfig)
  },
  "serviceAttachment": string
}
```

## EmbeddingManagement

> This item is deprecated!

Deprecated: This sub message is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. Contains settings for embedding management.

Fields

`enabled` `boolean`

Optional. Immutable. Whether to enable embedding management in this FeatureOnlineStore. It's immutable after creation to ensure the FeatureOnlineStore availability.

**JSON representation**

```
{
  "enabled": boolean
}
```

| Methods                                                                                                                                                                 |                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/create)                         | Creates a new FeatureOnlineStore in a given project and location. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/delete)                         | Deletes a single FeatureOnlineStore.                              |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/get)                               | Gets details of a single FeatureOnlineStore.                      |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/getIamPolicy)             | Gets the access control policy for a resource.                    |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/list)                             | Lists FeatureOnlineStores in a given project and location.        |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/patch)                           | Updates the parameters of a single FeatureOnlineStore.            |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/setIamPolicy)             | Sets the access control policy on the specified resource.         |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/testIamPermissions) | Returns permissions that a caller has on the specified resource.  |
