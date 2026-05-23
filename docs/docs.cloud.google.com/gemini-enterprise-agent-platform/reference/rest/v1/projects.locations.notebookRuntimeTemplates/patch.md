---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimeTemplates/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimeTemplates/patch
title: 'Method: notebookRuntimeTemplates.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookRuntimeTemplates.patch

Updates a NotebookRuntimeTemplate.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{notebookRuntimeTemplate.name}`  

`PATCH https://{service-endpoint}/v1/{notebookRuntimeTemplate.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`notebookRuntimeTemplate.name` `string`

The resource name of the NotebookRuntimeTemplate.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource. For the `FieldMask` definition, see `  google.protobuf.FieldMask  ` . Input format: `{paths: "${updated_field}"}` Updatable fields:

  - `encryptionSpec.kms_key_name`
  - `displayName`
  - `softwareConfig.post_startup_script_config.post_startup_script`
  - `softwareConfig.post_startup_script_config.post_startup_script_url`
  - `softwareConfig.post_startup_script_config.post_startup_script_behavior`
  - `softwareConfig.env`
  - `softwareConfig.colab_image.release_name`
  - `softwareConfig.custom_container_config.image_uri`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  NotebookRuntimeTemplate  ` .

### Response body

If successful, the response body contains an instance of `  NotebookRuntimeTemplate  ` .
