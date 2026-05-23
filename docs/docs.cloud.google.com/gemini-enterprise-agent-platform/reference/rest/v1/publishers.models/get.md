---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/publishers.models/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/publishers.models/get
title: 'Method: models.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : publishers.models.get

Gets a Model Garden publisher model.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}`

### Query parameters

`languageCode` `string`

Optional. The IETF BCP-47 language code representing the language in which the publisher model's text information should be written in.

`view` ` enum ( PublisherModelView  ` )

Optional. PublisherModel view specifying which fields to read.

`isHuggingFaceModel` `boolean`

Optional. Boolean indicates whether the requested model is a Hugging Face model.

`huggingFaceToken` `string`

Optional. token used to access Hugging Face gated models.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  PublisherModel  ` .

## PublisherModelView

View enumeration of PublisherModel.

Enums

`PUBLISHER_MODEL_VIEW_UNSPECIFIED`

The default / unset value. The API will default to the BASIC view.

`PUBLISHER_MODEL_VIEW_BASIC`

Include basic metadata about the publisher model, but not the full contents.

`PUBLISHER_MODEL_VIEW_FULL`

Include everything.

`PUBLISHER_MODEL_VERSION_VIEW_BASIC`

Include: VersionId, ModelVersionExternalName, and SupportedActions.
