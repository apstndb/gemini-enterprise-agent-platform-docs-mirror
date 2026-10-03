---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FetchFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FetchFeatureValuesResponse
title: FetchFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`FeatureOnlineStoreService.FetchFeatureValues`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/fetchFeatureValues#google.cloud.aiplatform.v1.FeatureOnlineStoreService.FetchFeatureValues)

Fields

`dataKey` `object ( `[`FeatureViewDataKey`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureViewDataKey)` )`

The data key associated with this response. Will only be populated for \[FeatureOnlineStoreService.StreamingFetchFeatureValues\]\[\] RPCs.

`format` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`keyValues` `object ( `[`FeatureNameValuePairList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FetchFeatureValuesResponse#FeatureNameValuePairList)` )`

feature values in keyvalue format.

`protoStruct` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

feature values in proto Struct format.

End of mutually exclusive fields.

**JSON representation**

```
{
  "dataKey": {
    object (FeatureViewDataKey)
  },

  // format
  "keyValues": {
    object (FeatureNameValuePairList)
  },
  "protoStruct": {
    object
  }
  // Union type
}
```

## FeatureNameValuePairList

Response structure in the format of key (feature name) and (feature) value pair.

Fields

`features[]` `object ( `[`FeatureNameValuePair`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FetchFeatureValuesResponse#FeatureNameValuePair)` )`

List of feature names and values.

**JSON representation**

```
{
  "features": [
    {
      object (FeatureNameValuePair)
    }
  ]
}
```

## FeatureNameValuePair

feature name & value pair.

Fields

`name` `string`

feature short name.

`data` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`value` `object ( `[`FeatureValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureValue)` )`

feature value.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,

  // data
  "value": {
    object (FeatureValue)
  }
  // Union type
}
```
