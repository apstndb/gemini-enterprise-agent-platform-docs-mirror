---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/streamingReadFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/streamingReadFeatureValues
title: 'Method: entityTypes.streamingReadFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.streamingReadFeatureValues

Reads feature values for multiple entities. Depending on their size, data for different entities may be broken up across multiple responses.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{entityType}:streamingReadFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType` `string`

Required. The resource name of the entities' type. value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` . For example, for a machine learning model predicting user clicks on a website, an EntityType id could be `user` .

### Request body

The request body contains data with the following structure:

Fields

`entityIds[]` `string`

Required. IDs of entities to read feature values of. The maximum number of IDs is 100. For example, for a machine learning model predicting user clicks on a website, an entity id could be `user_123` .

`featureSelector` ` object ( FeatureSelector  ` )

Required. Selector choosing Features of the target EntityType. feature IDs will be deduplicated.

### Response body

If successful, the response body contains a stream of `  ReadFeatureValuesResponse  ` instances.
