---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/mergeVersionAliases
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/mergeVersionAliases
title: 'Method: models.mergeVersionAliases'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.mergeVersionAliases

Merges a set of aliases for a Model version.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:mergeVersionAliases`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the model version to merge aliases, with a version id explicitly included.

Example: `projects/{project}/locations/{location}/models/{model}@1234`

### Request body

The request body contains data with the following structure:

Fields

`versionAliases[]` `string`

Required. The set of version aliases to merge. The alias should be at most 128 characters, and match `[a-z][a-zA-Z0-9-]{0,126}[a-z-0-9]` . Add the `-` prefix to an alias means removing that alias from the version. `-` is NOT counted in the 128 characters. Example: `-golden` means removing the `golden` alias from the version.

There is NO ordering in aliases, which means 1) The aliases returned from models.get API might not have the exactly same order from this models.mergeVersionAliases API. 2) Adding and deleting the same alias in the request is not recommended, and the 2 operations will be cancelled out.

### Response body

If successful, the response body contains an instance of `  Model  ` .
