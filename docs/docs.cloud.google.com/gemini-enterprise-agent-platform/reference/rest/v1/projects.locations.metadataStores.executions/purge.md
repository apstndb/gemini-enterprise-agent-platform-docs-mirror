---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/purge
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/purge
title: 'Method: executions.purge'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.executions.purge

Purges Executions.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /executions:purge`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The metadata store to purge Executions from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`

### Request body

The request body contains data with the following structure:

Fields

`filter` `string`

Required. A required filter matching the Executions to be purged. E.g., `updateTime <= 2020-11-19T11:30:00-04:00` .

`force` `boolean`

Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample of Execution names that would be deleted.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
