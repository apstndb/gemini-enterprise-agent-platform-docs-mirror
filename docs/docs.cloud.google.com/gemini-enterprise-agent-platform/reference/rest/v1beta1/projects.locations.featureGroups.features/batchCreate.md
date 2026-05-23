---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/batchCreate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/batchCreate
title: 'Method: features.batchCreate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.features.batchCreate

Creates a batch of Features in a given FeatureGroup.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /features:batchCreate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

### Request body

The request body contains data with the following structure:

Fields

`requests[]` ` object ( CreateFeatureRequest  ` )

Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each child request message can be omitted. If `parent` is set in a child request, then the value must match the `parent` value in this request message.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## CreateFeatureRequest

Request message for `  FeaturestoreService.CreateFeature  ` . Request message for `  FeatureRegistryService.CreateFeature  ` .

Fields

`parent` `string`

Required. The resource name of the EntityType or FeatureGroup to create a feature. Format for entityType as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` Format for featureGroup as parent: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

`feature` ` object ( Feature  ` )

Required. The feature to create.

`featureId` `string`

Required. The id to use for the feature, which will become the final component of the feature's resource name.

This value may be up to 128 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.

The value must be unique within an EntityType/FeatureGroup.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;feature&quot;: {object (Feature)},&quot;featureId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
