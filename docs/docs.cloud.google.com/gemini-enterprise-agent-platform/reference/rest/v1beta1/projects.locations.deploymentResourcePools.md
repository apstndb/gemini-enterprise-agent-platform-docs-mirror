---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools
title: 'REST Resource: projects.locations.deploymentResourcePools'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: DeploymentResourcePool

A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources.

Fields

`name` `string`

Immutable. The resource name of the DeploymentResourcePool. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deploymentResourcePool}`

`dedicatedResources` `object ( `[`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources)` )`

Required. The underlying DedicatedResources that the DeploymentResourcePool uses.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key spec for a DeploymentResourcePool. If set, this DeploymentResourcePool will be secured by this key. endpoints and the DeploymentResourcePool they deploy in need to have the same EncryptionSpec.

`serviceAccount` `string`

The service account that the DeploymentResourcePool's container(s) run as. Specify the email address of the service account. If this service account is not specified, the container(s) run as a service account that doesn't have access to the resource project.

Users deploying the Models to this DeploymentResourcePool must have the `iam.serviceAccounts.actAs` permission on this service account.

`disableContainerLogging` `boolean`

If the DeploymentResourcePool is deployed with custom-trained Models or AutoML Tabular Models, the container(s) of the DeploymentResourcePool will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

user can disable container logging by setting this flag to true.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this DeploymentResourcePool was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "dedicatedResources": {
    object (DedicatedResources)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "serviceAccount": string,
  "disableContainerLogging": boolean,
  "createTime": string,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

| Methods                                                                                                                                                                       |                                                                             |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/create)                           | Create a DeploymentResourcePool.                                            |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/delete)                           | Delete a DeploymentResourcePool.                                            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/get)                                 | Get a DeploymentResourcePool.                                               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/list)                               | List DeploymentResourcePools in a location.                                 |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/patch)                             | Update a DeploymentResourcePool.                                            |
| [`queryDeployedModels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/queryDeployedModels) | List DeployedModels that have been deployed on this DeploymentResourcePool. |
