---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/copy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/copy
title: 'Method: models.copy'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.copy

Copies an already existing Agent Platform Model into the specified Location. The source Model must exist in the same Project. When copying custom Models, the users themselves are responsible for `  Model.metadata  ` content to be region-agnostic, as well as making sure that any resources (e.g. files) it depends on remain accessible.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /models:copy`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location into which to copy the Model. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`sourceModel` `string`

Required. The resource name of the Model to copy. That Model must be in the same Project. Format: `projects/{project}/locations/{location}/models/{model}`

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key options. If this is set, then the Model copy will be encrypted with the provided encryption key.

`customServiceAccount` `string`

Optional. The user-provided custom service account to use to do the copy model. If empty, [Agent Platform service Agent](https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) will be used to access resources needed to upload the model. This account must belong to the destination project where the model is copied to, i.e., the project specified in the `parent` field of this request and have the Agent Platform service Agent role in the source project.

Requires the user copying the Model to have the `iam.serviceAccounts.actAs` permission on this service account.

`destination_model` `Union type`

If both fields are unset, a new Model will be created with a generated ID. `destination_model` can be only one of the following:

`modelId` `string`

Optional. Copy sourceModel into a new Model with this id. The id will become the final component of the model resource name.

This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number or hyphen.

`parentModel` `string`

Optional. Specify this field to copy sourceModel into this existing Model as a new version. Format: `projects/{project}/locations/{location}/models/{model}`

### Response body

If successful, the response body contains an instance of `  Operation  ` .
