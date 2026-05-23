---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/upload
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/upload
title: 'Method: models.upload'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.upload

Uploads a Model artifact into Agent Platform.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /models:upload`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location into which to upload the Model. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`parentModel` `string`

Optional. The resource name of the model into which to upload the version. Only specify this field when uploading a new version.

`modelId` `string`

Optional. The id to use for the uploaded Model, which will become the final component of the model resource name.

This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number or hyphen.

`model` ` object ( Model  ` )

Required. The Model to create.

`serviceAccount` `string`

Optional. The user-provided custom service account to use to do the model upload. If empty, [Agent Platform service Agent](https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) will be used to access resources needed to upload the model. This account must belong to the target project where the model is uploaded to, i.e., the project specified in the `parent` field of this request and have necessary read permissions (to Google Cloud Storage, Artifact Registry, etc.).

### Response body

If successful, the response body contains an instance of `  Operation  ` .
