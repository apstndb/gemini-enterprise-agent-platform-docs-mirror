---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/mutateDeployedModel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/mutateDeployedModel
title: 'Method: endpoints.mutateDeployedModel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.mutateDeployedModel

Updates an existing deployed model. Updatable fields include `minReplicaCount` , `maxReplicaCount` , `requiredReplicaCount` , `autoscalingMetricSpecs` , `disableContainerLogging` (v1 only), and `enableContainerLogging` (v1beta1 only).

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:mutateDeployedModel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`deployedModel` `object ( `[`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints#DeployedModel)` )`

Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated:

- `minReplicaCount` in either [`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources) or [`AutomaticResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutomaticResources)
- `maxReplicaCount` in either [`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources) or [`AutomaticResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutomaticResources)
- `requiredReplicaCount` in [`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources)
- [`autoscalingMetricSpecs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources#FIELDS.autoscaling_metric_specs)
- `disableContainerLogging` (v1 only)
- `enableContainerLogging` (v1beta1 only)
- `scaleToZeroSpec` in [`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources) (v1beta1 only)
- `initialReplicaCount` in [`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources) (v1beta1 only)

`updateMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Required. The update mask applies to the resource. See [`google.protobuf.FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .
