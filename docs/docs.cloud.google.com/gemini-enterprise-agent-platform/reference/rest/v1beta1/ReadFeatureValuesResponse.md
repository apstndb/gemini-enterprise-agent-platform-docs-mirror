---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse
title: ReadFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`FeaturestoreOnlineServingService.ReadFeatureValues`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/readFeatureValues#google.cloud.aiplatform.v1beta1.FeaturestoreOnlineServingService.ReadFeatureValues) .

Fields

`header` `object ( `[`Header`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#Header)` )`

Response header.

`entityView` `object ( `[`EntityView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#EntityView)` )`

Entity view with feature values. This may be the entity in the Featurestore if values for all Features were requested, or a projection of the entity in the Featurestore if values for only some Features were requested.

**JSON representation**

```
{
  "header": {
    object (Header)
  },
  "entityView": {
    object (EntityView)
  }
}
```

## Header

Response header with metadata for the requested [`ReadFeatureValuesRequest.entity_type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/readFeatureValues#body.PATH_PARAMETERS.entity_type) and Features.

Fields

`entityType` `string`

The resource name of the EntityType from the `ReadFeatureValuesRequest` . value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .

`featureDescriptors[]` `object ( `[`FeatureDescriptor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#FeatureDescriptor)` )`

List of feature metadata corresponding to each piece of [`ReadFeatureValuesResponse.EntityView.data`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#EntityView.FIELDS.data) .

**JSON representation**

```
{
  "entityType": string,
  "featureDescriptors": [
    {
      object (FeatureDescriptor)
    }
  ]
}
```

## FeatureDescriptor

metadata for requested Features.

Fields

`id` `string`

feature id.

**JSON representation**

```
{
  "id": string
}
```

## EntityView

Entity view with feature values.

Fields

`entityId` `string`

id of the requested entity.

`data[]` `object ( `[`Data`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#Data)` )`

Each piece of data holds the k requested values for one requested feature. If no values for the requested feature exist, the corresponding cell will be empty. This has the same size and is in the same order as the features from the header [`ReadFeatureValuesResponse.header`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#FIELDS.header) .

**JSON representation**

```
{
  "entityId": string,
  "data": [
    {
      object (Data)
    }
  ]
}
```

## Data

Container to hold value(s), successive in time, for one feature from the request.

Fields

`data` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`value` `object ( `[`FeatureValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValue)` )`

feature value if a single value is requested.

`values` `object ( `[`FeatureValueList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse#FeatureValueList)` )`

feature values list if values, successive in time, are requested. If the requested number of values is greater than the number of existing feature values, nonexistent values are omitted instead of being returned as empty.

End of mutually exclusive fields.

**JSON representation**

```
{

  // data
  "value": {
    object (FeatureValue)
  },
  "values": {
    object (FeatureValueList)
  }
  // Union type
}
```

## FeatureValueList

Container for list of values.

Fields

`values[]` `object ( `[`FeatureValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValue)` )`

A list of feature values. All of them should be the same data type.

**JSON representation**

```
{
  "values": [
    {
      object (FeatureValue)
    }
  ]
}
```
