---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/removeDatapoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/removeDatapoints
title: 'Method: indexes.removeDatapoints'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexes.removeDatapoints

Remove Datapoints from an Index.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{index}:removeDatapoints`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`index` `string`

Required. The name of the Index resource to be updated. Format: `projects/{project}/locations/{location}/indexes/{index}`

### Request body

The request body contains data with the following structure:

Fields

`datapointIds[]` `string`

A list of datapoint ids to be deleted.

### Response body

If successful, the response body is empty.
