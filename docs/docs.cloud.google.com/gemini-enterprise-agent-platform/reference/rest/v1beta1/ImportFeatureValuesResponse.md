---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ImportFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ImportFeatureValuesResponse
title: ImportFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`FeaturestoreService.ImportFeatureValues`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/importFeatureValues#google.cloud.aiplatform.v1beta1.FeaturestoreService.ImportFeatureValues) .

Fields

`importedEntityCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of entities that have been imported by the operation.

`importedFeatureValueCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of feature values that have been imported by the operation.

`invalidRowCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of rows in input source that weren't imported due to either \* Not having any featureValues. \* Having a null entityId. \* Having a null timestamp. \* Not being parsable (applicable for CSV sources).

`timestampOutsideRetentionRowsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number rows that weren't ingested due to having feature timestamps outside the retention boundary.

**JSON representation**

```
{
  "importedEntityCount": string,
  "importedFeatureValueCount": string,
  "invalidRowCount": string,
  "timestampOutsideRetentionRowsCount": string
}
```
