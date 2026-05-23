---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores
title: 'REST Resource: projects.locations.featurestores'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Featurestore

Agent Platform feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values.

Fields

`name` `string`

Output only. name of the Featurestore. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Featurestore was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Featurestore was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your Featurestore.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one Featurestore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`onlineServingConfig` ` object ( OnlineServingConfig  ` )

Optional. Config for online storage resources. The field should not co-exist with the field of `OnlineStoreReplicationConfig` . If both of it and OnlineStoreReplicationConfig are unset, the feature store will not have an online store and cannot be used for online serving.

`state` ` enum ( State  ` )

Output only. state of the featurestore.

`onlineStorageTtlDays` `integer`

Optional. TTL in days for feature values that will be stored in online serving storage. The feature Store online storage periodically removes obsolete feature values older than `onlineStorageTtlDays` since the feature generation time. Note that `onlineStorageTtlDays` should be less than or equal to `offlineStorageTtlDays` for each EntityType under a featurestore. If not set, default to 4000 days

`encryptionSpec` ` object ( EncryptionSpec  ` )

Optional. Customer-managed encryption key spec for data storage. If set, both of the online and offline data storage will be secured by this key.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;onlineServingConfig&quot;: {object (OnlineServingConfig)},&quot;state&quot;: enum (State),&quot;onlineStorageTtlDays&quot;: integer,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## OnlineServingConfig

OnlineServingConfig specifies the details for provisioning online serving resources.

Fields

`fixedNodeCount` `integer`

The number of nodes for the online store. The number of nodes doesn't scale automatically, but you can manually update the number of nodes. If set to 0, the featurestore will not have an online store and cannot be used for online serving.

`scaling` ` object ( Scaling  ` )

Online serving scaling configuration. Only one of `fixedNodeCount` and `scaling` can be set. Setting one will reset the other.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;fixedNodeCount&quot;: integer,&quot;scaling&quot;: {object (Scaling)}}</code></pre></td>
</tr>
</tbody>
</table>

## Scaling

Online serving scaling configuration. If minNodeCount and maxNodeCount are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

Fields

`minNodeCount` `integer`

Required. The minimum number of nodes to scale down to. Must be greater than or equal to 1.

`maxNodeCount` `integer`

The maximum number of nodes to scale up to. Must be greater than minNodeCount, and less than or equal to 10 times of 'minNodeCount'.

`cpuUtilizationTarget` `integer`

Optional. The cpu utilization that the Autoscaler should be trying to achieve. This number is on a scale from 0 (no utilization) to 100 (total utilization), and is limited between 10 and 80. When a cluster's CPU utilization exceeds the target that you have set, Bigtable immediately adds nodes to the cluster. When CPU utilization is substantially lower than the target, Bigtable removes nodes. If not set or set to 0, default to 50.

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
  &quot;minNodeCount&quot;: integer,
  &quot;maxNodeCount&quot;: integer,
  &quot;cpuUtilizationTarget&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## State

Possible states a featurestore can have.

Enums

`STATE_UNSPECIFIED`

Default value. This value is unused.

`STABLE`

state when the featurestore configuration is not being updated and the fields reflect the current configuration of the featurestore. The featurestore is usable in this state.

`UPDATING`

The state of the featurestore configuration when it is being updated. During an update, the fields reflect either the original configuration or the updated configuration of the featurestore. For example, `onlineServingConfig.fixed_node_count` can take minutes to update. While the update is in progress, the featurestore is in the UPDATING state, and the value of `fixedNodeCount` can be the original value or the updated value, depending on the progress of the operation. Until the update completes, the actual number of nodes can still be the original value of `fixedNodeCount` . The featurestore is still usable in this state.

## Methods

### `            batchReadFeatureValues           `

Batch reads Feature values from a Featurestore.

### `            create           `

Creates a new Featurestore in a given project and location.

### `            delete           `

Deletes a single Featurestore.

### `            get           `

Gets details of a single Featurestore.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            list           `

Lists Featurestores in a given project and location.

### `            patch           `

Updates the parameters of a single Featurestore.

### `            searchFeatures           `

Searches Features matching a query in a given project.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.
