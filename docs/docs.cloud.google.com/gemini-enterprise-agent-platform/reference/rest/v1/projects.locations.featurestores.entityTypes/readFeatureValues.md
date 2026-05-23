---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/readFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/readFeatureValues
title: 'Method: entityTypes.readFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.readFeatureValues

Reads feature values of a specific entity of an EntityType. For reading feature values of multiple entities of an EntityType, please use entityTypes.streamingReadFeatureValues.

### Endpoint

post `https: / /{service-endpoint} /v1 /{entityType}:readFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType` `string`

Required. The resource name of the EntityType for the entity being read. value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` . For example, for a machine learning model predicting user clicks on a website, an EntityType id could be `user` .

### Request body

The request body contains data with the following structure:

Fields

`entityId` `string`

Required. id for a specific entity. For example, for a machine learning model predicting user clicks on a website, an entity id could be `user_123` .

`featureSelector` ` object ( FeatureSelector  ` )

Required. Selector choosing Features of the target EntityType.

### Response body

If successful, the response body contains an instance of `  ReadFeatureValuesResponse  ` .
