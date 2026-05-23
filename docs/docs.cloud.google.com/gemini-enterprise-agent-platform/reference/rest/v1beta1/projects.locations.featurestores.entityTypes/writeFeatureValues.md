---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/writeFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/writeFeatureValues
title: 'Method: entityTypes.writeFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.writeFeatureValues

Writes feature values of one or more entities of an EntityType.

The feature values are merged into existing entities if any. The feature values to be written must have timestamp within the online storage retention.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{entityType}:writeFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType` `string`

Required. The resource name of the EntityType for the entities being written. value format: `projects/{project}/locations/{location}/featurestores/ {featurestore}/entityTypes/{entityType}` . For example, for a machine learning model predicting user clicks on a website, an EntityType id could be `user` .

### Request body

The request body contains data with the following structure:

Fields

`payloads[]` ` object ( WriteFeatureValuesPayload  ` )

Required. The entities to be written. Up to 100,000 feature values can be written across all `payloads` .

### Response body

If successful, the response body is empty.

## WriteFeatureValuesPayload

Contains feature values to be written for a specific entity.

Fields

`entityId` `string`

Required. The id of the entity.

`featureValues` ` map (key: string, value: object ( FeatureValue  ` ))

Required. feature values to be written, mapping from feature id to value. Up to 100,000 `featureValues` entries may be written across all payloads. The feature generation time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;entityId&quot;: string,&quot;featureValues&quot;: {string: {object (FeatureValue)},...}}</code></pre></td>
</tr>
</tbody>
</table>
