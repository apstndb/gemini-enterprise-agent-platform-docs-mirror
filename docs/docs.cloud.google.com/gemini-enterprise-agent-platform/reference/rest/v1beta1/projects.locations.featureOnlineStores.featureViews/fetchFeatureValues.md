---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/fetchFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/fetchFeatureValues
title: 'Method: featureViews.fetchFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.fetchFeatureValues

Fetch feature values under a FeatureView.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{featureView}:fetchFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView` `string`

Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Request body

The request body contains data with the following structure:

Fields

`dataKey` ` object ( FeatureViewDataKey  ` )

Optional. The request key to fetch feature values for.

`dataFormat` ` enum ( FeatureViewDataFormat  ` )

Optional. Response data format. If not set, `  FeatureViewDataFormat.KEY_VALUE  ` will be used.

` format (deprecated)  ` ` enum ( Format  ` )

Specify response data format. If not set, keyvalue format will be used. Deprecated. Use `  FetchFeatureValuesRequest.data_format  ` .

`entity_id` `Union type`

Entity ID to fetch feature values for. Deprecated. Use `  FetchFeatureValuesRequest.data_key  ` . `entity_id` can be only one of the following:

` id (deprecated)  ` `string`

Simple id. The whole string will be used as is to identify Entity to fetch feature values for.

### Response body

If successful, the response body contains an instance of `  FetchFeatureValuesResponse  ` .

## Format

> This item is deprecated\!

Format of the response data.

Enums

`FORMAT_UNSPECIFIED`

Not set. Will be treated as the keyvalue format.

`KEY_VALUE`

Return response data in key-value format.

`PROTO_STRUCT`

Return response data in proto Struct format.
