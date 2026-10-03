---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ImportFeatureValuesOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ImportFeatureValuesOperationMetadata
title: ImportFeatureValuesOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Details of operations that perform import feature values.

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

Operation metadata for Featurestore import feature values.

`importedEntityCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of entities that have been imported by the operation.

`importedFeatureValueCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of feature values that have been imported by the operation.

`sourceUris[]` `string`

The source URI from where feature values are imported.

`invalidRowCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of rows in input source that weren't imported due to either \* Not having any featureValues. \* Having a null entityId. \* Having a null timestamp. \* Not being parsable (applicable for CSV sources).

`timestampOutsideRetentionRowsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number rows that weren't ingested due to having timestamps outside the retention boundary.

`blockingOperationIds[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

List of ImportFeatureValues operations running under a single EntityType that are blocking this operation.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "importedEntityCount": string,
  "importedFeatureValueCount": string,
  "sourceUris": [
    string
  ],
  "invalidRowCount": string,
  "timestampOutsideRetentionRowsCount": string,
  "blockingOperationIds": [
    string
  ]
}
```
