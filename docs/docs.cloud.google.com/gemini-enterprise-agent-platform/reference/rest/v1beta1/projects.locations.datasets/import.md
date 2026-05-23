---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/import
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/import
title: 'Method: datasets.import'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.import

Imports data into a Dataset.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:import`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Request body

The request body contains data with the following structure:

Fields

`importConfigs[]` ` object ( ImportDataConfig  ` )

Required. The desired input locations. The contents of all input locations will be imported in one batch.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## ImportDataConfig

Describes the location from where we import data into a Dataset, together with the labels that will be applied to the DataItems and the Annotations.

Fields

`dataItemLabels` `map (key: string, value: string)`

Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by `  importSchemaUri  ` , e.g. jsonl file.

`annotationLabels` `map (key: string, value: string)`

Labels that will be applied to newly imported Annotations. If two Annotations are identical, one of them will be deduped. Two Annotations are considered identical if their `  payload  ` , `  payloadSchemaUri  ` and all of their `  labels  ` are the same. These labels will be overridden by Annotation labels specified inside index file referenced by `  importSchemaUri  ` , e.g. jsonl file.

`importSchemaUri` `string`

Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an [OpenAPI 3.0.2 Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) .

`source` `Union type`

The source of the input. `source` can be only one of the following:

`gcsSource` ` object ( GcsSource  ` )

The Google Cloud Storage location for the input content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataItemLabels&quot;: {string: string,...},&quot;annotationLabels&quot;: {string: string,...},&quot;importSchemaUri&quot;: string,// source&quot;gcsSource&quot;: {object (GcsSource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>
