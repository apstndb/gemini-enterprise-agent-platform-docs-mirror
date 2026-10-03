---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints
title: 'REST Resource: projects.locations.indexEndpoints'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: IndexEndpoint

Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes.

Fields

`name` `string`

Output only. The resource name of the IndexEndpoint.

`displayName` `string`

Required. The display name of the IndexEndpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the IndexEndpoint.

`deployedIndexes[]` `object ( `[`DeployedIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#DeployedIndex)` )`

Output only. The indexes deployed in this endpoint.

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your IndexEndpoints.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this IndexEndpoint was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this IndexEndpoint was last updated. This timestamp is not updated when the endpoint's DeployedIndexes are updated, e.g. due to updates of the original Indexes they are the deployments of.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`network` `string`

Optional. The full name of the Google Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the IndexEndpoint should be peered.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

[`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.network) and [`privateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.private_service_connect_config) are mutually exclusive.

[Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) : `projects/{project}/global/networks/{network}` . Where {project} is a project number, as in '12345', and {network} is network name.

`enablePrivateServiceConnect `**`(deprecated)`** `boolean`

> This item is deprecated!

Optional. Deprecated: If true, expose the IndexEndpoint via private service connect.

Only one of the fields, [`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.network) or [`enablePrivateServiceConnect`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.enable_private_service_connect) , can be set.

`privateServiceConnectConfig` `object ( `[`PrivateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PrivateServiceConnectConfig)` )`

Optional. Configuration for private service connect.

[`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.network) and [`privateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.private_service_connect_config) are mutually exclusive.

`publicEndpointEnabled` `boolean`

Optional. If true, the deployed index will be accessible through public endpoint.

`publicEndpointDomainName` `string`

Output only. If [`publicEndpointEnabled`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.public_endpoint_enabled) is true, this field will be populated with the domain name to use for this index endpoint.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Immutable. Customer-managed encryption key spec for an IndexEndpoint. If set, this IndexEndpoint and all sub-resources of this IndexEndpoint will be secured by this key.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "deployedIndexes": [
    {
      object (DeployedIndex)
    }
  ],
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "network": string,
  "enablePrivateServiceConnect": boolean,
  "privateServiceConnectConfig": {
    object (PrivateServiceConnectConfig)
  },
  "publicEndpointEnabled": boolean,
  "publicEndpointDomainName": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

## DeployedIndex

A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.

Fields

`id` `string`

Required. The user specified id of the DeployedIndex. The id can be up to 128 characters long and must start with a letter and only contain letters, numbers, and underscores. The id must be unique within the project it is created in.

`index` `string`

Required. The name of the Index this is the deployment of. We may refer to this Index as the DeployedIndex's "original" Index.

`displayName` `string`

The display name of the DeployedIndex. If not provided upon creation, the Index's displayName is used.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when the DeployedIndex was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`privateEndpoints` `object ( `[`IndexPrivateEndpoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexPrivateEndpoints)` )`

Output only. Provides paths for users to send requests directly to the deployed index services running on Cloud via private services access. This field is populated if [`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#IndexEndpoint.FIELDS.network) is configured.

`indexSyncTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. The DeployedIndex may depend on various data on its original Index. Additionally when certain changes to the original Index are being done (e.g. when what the Index contains is being changed) the DeployedIndex may be asynchronously updated in the background to reflect these changes. If this timestamp's value is at least the [`Index.update_time`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes#Index.FIELDS.update_time) of the original Index, it means that this DeployedIndex and the original Index are in sync. If this timestamp is older, then to see which updates this DeployedIndex already contains (and which it does not), one must [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.operations/list#google.longrunning.Operations.ListOperations) the operations that are running on the original Index. Only the successfully completed Operations with [`updateTime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata#FIELDS.update_time) equal or before this sync time are contained in this DeployedIndex.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`automaticResources` `object ( `[`AutomaticResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/AutomaticResources)` )`

Optional. A description of resources that the DeployedIndex uses, which to large degree are decided by Agent Platform, and optionally allows only a modest additional configuration. If minReplicaCount is not set, the default value is 2 (we don't provide SLA when minReplicaCount=1). If maxReplicaCount is not set, the default value is minReplicaCount. The max allowed replica count is 1000.

`dedicatedResources` `object ( `[`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DedicatedResources)` )`

Optional. A description of resources that are dedicated to the DeployedIndex, and that need a higher degree of manual configuration. The field minReplicaCount must be set to a value strictly greater than 0, or else validation will fail. We don't provide SLA when minReplicaCount=1. If maxReplicaCount is not set, the default value is minReplicaCount. The max allowed replica count is 1000.

Available machine types for SMALL shard: e2-standard-2 and all machine types available for MEDIUM and LARGE shard.

Available machine types for MEDIUM shard: e2-standard-16 and all machine types available for LARGE shard.

Available machine types for LARGE shard: e2-highmem-16, n2d-standard-32.

n1-standard-16 and n1-standard-32 are still available, but we recommend e2-standard-16 and e2-highmem-16 for cost efficiency.

`enableAccessLogging` `boolean`

Optional. If true, private endpoint's access logs are sent to Cloud Logging.

These logs are like standard server access logs, containing information like timestamp and latency for each MatchRequest.

Note that logs may incur a cost, especially if the deployed index receives a high queries per second rate (QPS). Estimate your costs before enabling this option.

`enableDatapointUpsertLogging` `boolean`

Optional. If true, logs to Cloud Logging errors relating to datapoint upserts.

Under normal operation conditions, these log entries should be very rare. However, if incompatible datapoint updates are being uploaded to an index, a high volume of log entries may be generated in a short period of time.

Note that logs may incur a cost, especially if the deployed index receives a high volume of datapoint upserts. Estimate your costs before enabling this option.

`deployedIndexAuthConfig` `object ( `[`DeployedIndexAuthConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#DeployedIndexAuthConfig)` )`

Optional. If set, the authentication is enabled for the private endpoint.

`reservedIpRanges[]` `string`

Optional. A list of reserved ip ranges under the VPC network that can be used for this DeployedIndex.

If set, we will deploy the index within the provided ip ranges. Otherwise, the index might be deployed to any ip ranges under the provided VPC network.

The value should be the name of the address ( <https://cloud.google.com/compute/docs/reference/rest/v1/addresses> ) Example: \['vertex-ai-ip-range'\].

For more information about subnets and network IP ranges, please see <https://cloud.google.com/vpc/docs/subnets#manually_created_subnet_ip_ranges> .

`deploymentGroup` `string`

Optional. The deployment group can be no longer than 64 characters (eg: 'test', 'prod'). If not set, we will use the 'default' deployment group.

Creating `deployment_groups` with `reservedIpRanges` is a recommended practice when the peered network has multiple peering ranges. This creates your deployments from predictable IP spaces for easier traffic administration. Also, one deploymentGroup (except 'default') can only be used with the same reservedIpRanges which means if the deploymentGroup has been used with reservedIpRanges: \[a, b, c\], using it with \[a, b\] or \[d, e\] is disallowed.

Note: we only support up to 5 deployment groups(not including 'default').

`deploymentTier` `enum ( `[`DeploymentTier`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#DeploymentTier)` )`

Optional. The deployment tier that the index is deployed to. DEPLOYMENT_TIER_UNSPECIFIED will use a system-chosen default tier.

`pscAutomationConfigs[]` `object ( `[`PSCAutomationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PSCAutomationConfig)` )`

Optional. If set for PSC deployed index, PSC connection will be automatically created after deployment is done and the endpoint information is populated in privateEndpoints.psc_automated_endpoints.

**JSON representation**

```
{
  "id": string,
  "index": string,
  "displayName": string,
  "createTime": string,
  "privateEndpoints": {
    object (IndexPrivateEndpoints)
  },
  "indexSyncTime": string,
  "automaticResources": {
    object (AutomaticResources)
  },
  "dedicatedResources": {
    object (DedicatedResources)
  },
  "enableAccessLogging": boolean,
  "enableDatapointUpsertLogging": boolean,
  "deployedIndexAuthConfig": {
    object (DeployedIndexAuthConfig)
  },
  "reservedIpRanges": [
    string
  ],
  "deploymentGroup": string,
  "deploymentTier": enum (DeploymentTier),
  "pscAutomationConfigs": [
    {
      object (PSCAutomationConfig)
    }
  ]
}
```

## IndexPrivateEndpoints

IndexPrivateEndpoints proto is used to provide paths for users to send requests via private endpoints (e.g. private service access, private service connect). To send request via private service access, use matchGrpcAddress. To send request via private service connect, use serviceAttachment.

Fields

`matchGrpcAddress` `string`

Output only. The ip address used to send match gRPC requests.

`serviceAttachment` `string`

Output only. The name of the service attachment resource. Populated if private service connect is enabled.

`pscAutomatedEndpoints[]` `object ( `[`PscAutomatedEndpoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#PscAutomatedEndpoints)` )`

Output only. PscAutomatedEndpoints is populated if private service connect is enabled if PscAutomatedConfig is set.

**JSON representation**

```
{
  "matchGrpcAddress": string,
  "serviceAttachment": string,
  "pscAutomatedEndpoints": [
    {
      object (PscAutomatedEndpoints)
    }
  ]
}
```

## PscAutomatedEndpoints

PscAutomatedEndpoints defines the output of the forwarding rule automatically created by each PscAutomationConfig.

Fields

`projectId` `string`

Corresponding projectId in pscAutomationConfigs

`network` `string`

Corresponding network in pscAutomationConfigs.

`matchAddress` `string`

ip Address created by the automated forwarding rule.

**JSON representation**

```
{
  "projectId": string,
  "network": string,
  "matchAddress": string
}
```

## DeployedIndexAuthConfig

Used to set up the auth on the DeployedIndex's private endpoint.

Fields

`authProvider` `object ( `[`AuthProvider`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints#AuthProvider)` )`

Defines the authentication provider that the DeployedIndex uses.

**JSON representation**

```
{
  "authProvider": {
    object (AuthProvider)
  }
}
```

## AuthProvider

Configuration for an authentication provider, including support for [JSON Web token (JWT)](https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32) .

Fields

`audiences[]` `string`

The list of JWT [audiences](https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32#section-4.1.3) . that are allowed to access. A JWT containing any of these audiences will be accepted.

`allowedIssuers[]` `string`

A list of allowed JWT issuers. Each entry must be a valid Google service account, in the following format:

`service-account-name@project-id.iam.gserviceaccount.com`

**JSON representation**

```
{
  "audiences": [
    string
  ],
  "allowedIssuers": [
    string
  ]
}
```

## DeploymentTier

Tiers encapsulate serving time attributes like latency and throughput.

| Enums                         |                          |
|-------------------------------|--------------------------|
| `DEPLOYMENT_TIER_UNSPECIFIED` | Default deployment tier. |
| `STORAGE`                     | Optimized for costs.     |

| Methods                                                                                                                                                         |                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/create)                           | Creates an IndexEndpoint.                                                                                         |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/delete)                           | Deletes an IndexEndpoint.                                                                                         |
| [`deployIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/deployIndex)                 | Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it.                                     |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/get)                                 | Gets an IndexEndpoint.                                                                                            |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/list)                               | Lists IndexEndpoints in a Location.                                                                               |
| [`mutateDeployedIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/mutateDeployedIndex) | Update an existing DeployedIndex under an IndexEndpoint.                                                          |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/patch)                             | Updates an IndexEndpoint.                                                                                         |
| [`undeployIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/undeployIndex)             | Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using. |
