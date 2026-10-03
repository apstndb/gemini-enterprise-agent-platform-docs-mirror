---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeleteFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeleteFeatureValuesResponse
title: DeleteFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`FeaturestoreService.DeleteFeatureValues`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/deleteFeatureValues#google.cloud.aiplatform.v1beta1.FeaturestoreService.DeleteFeatureValues) .

Fields

`response` `Union type`

Response based on which delete option is specified in the request The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`selectEntity` `object ( `[`SelectEntity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeleteFeatureValuesResponse#SelectEntity)` )`

Response for request specifying the entities to delete

`selectTimeRangeAndFeature` `object ( `[`SelectTimeRangeAndFeature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeleteFeatureValuesResponse#SelectTimeRangeAndFeature)` )`

Response for request specifying time range and feature

End of mutually exclusive fields.

**JSON representation**

```
{

  // response
  "selectEntity": {
    object (SelectEntity)
  },
  "selectTimeRangeAndFeature": {
    object (SelectTimeRangeAndFeature)
  }
  // Union type
}
```

## SelectEntity

Response message if the request uses the SelectEntity option.

Fields

`offlineStorageDeletedEntityRowCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity id and a timestamp. One entity id can have multiple rows in the offline storage.

`onlineStorageDeletedEntityCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The count of deleted entities in the online storage. Each entity id corresponds to one entity.

**JSON representation**

```
{
  "offlineStorageDeletedEntityRowCount": string,
  "onlineStorageDeletedEntityCount": string
}
```

## SelectTimeRangeAndFeature

Response message if the request uses the SelectTimeRangeAndFeature option.

Fields

`impactedFeatureCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The count of the features or columns impacted. This is the same as the feature count in the request.

`offlineStorageModifiedEntityRowCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The count of modified entity rows in the offline storage. Each row corresponds to the combination of an entity id and a timestamp. One entity id can have multiple rows in the offline storage. Within each row, only the features specified in the request are deleted.

`onlineStorageModifiedEntityCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The count of modified entities in the online storage. Each entity id corresponds to one entity. Within each entity, only the features specified in the request are deleted.

**JSON representation**

```
{
  "impactedFeatureCount": string,
  "offlineStorageModifiedEntityRowCount": string,
  "onlineStorageModifiedEntityCount": string
}
```
