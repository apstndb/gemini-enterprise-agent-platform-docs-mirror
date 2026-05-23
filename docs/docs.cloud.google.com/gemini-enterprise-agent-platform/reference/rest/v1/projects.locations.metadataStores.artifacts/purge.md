---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/purge
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/purge
title: 'Method: artifacts.purge'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.artifacts.purge

Purges Artifacts.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /artifacts:purge`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The metadata store to purge Artifacts from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`

### Request body

The request body contains data with the following structure:

Fields

`filter` `string`

Required. A required filter matching the Artifacts to be purged. E.g., `updateTime <= 2020-11-19T11:30:00-04:00` .

`force` `boolean`

Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample of Artifact names that would be deleted.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
