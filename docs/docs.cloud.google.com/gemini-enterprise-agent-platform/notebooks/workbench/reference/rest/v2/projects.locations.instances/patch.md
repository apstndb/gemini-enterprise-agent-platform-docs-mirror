---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch
title: 'Method: projects.locations.instances.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

instances.patch updates an Instance.

### HTTP request

`PATCH https://notebooks.googleapis.com/v2/{instance.name}`

### Path parameters

Parameters

`instance.name`

`string`

Output only. Identifier. The name of this notebook instance. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

### Query parameters

Parameters

`updateMask`

` string ( FieldMask  ` format)

Required. Mask used to update an instance. Updatable fields:

  - `labels`
  - `gceSetup.min_cpu_platform`
  - `gceSetup.metadata`
  - `gceSetup.machine_type`
  - `gceSetup.accelerator_configs`
  - `gceSetup.accelerator_configs.type`
  - `gceSetup.accelerator_configs.core_count`
  - `gceSetup.gpu_driver_config`
  - `gceSetup.gpu_driver_config.enable_gpu_driver`
  - `gceSetup.gpu_driver_config.custom_gpu_driver_path`
  - `gceSetup.shielded_instance_config`
  - `gceSetup.shielded_instance_config.enable_secure_boot`
  - `gceSetup.shielded_instance_config.enable_vtpm`
  - `gceSetup.shielded_instance_config.enable_integrity_monitoring`
  - `gceSetup.reservation_affinity`
  - `gceSetup.reservation_affinity.consume_reservation_type`
  - `gceSetup.reservation_affinity.key`
  - `gceSetup.reservation_affinity.values`
  - `gceSetup.tags`
  - `gceSetup.container_image`
  - `gceSetup.container_image.repository`
  - `gceSetup.container_image.tag`
  - `gceSetup.disable_public_ip`
  - `disableProxyAccess`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`requestId`

`string`

Optional. Idempotent request UUID.

### Request body

The request body contains an instance of `  Instance  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
