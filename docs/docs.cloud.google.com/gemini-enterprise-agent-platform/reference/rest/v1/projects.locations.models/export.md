---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export
title: 'Method: models.export'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.export

Exports a trained, exportable Model to a location specified by the user. A Model is considered to be exportable if it has at least one `  supported export format  ` .

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:export`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported.

### Request body

The request body contains data with the following structure:

Fields

`outputConfig` ` object ( OutputConfig  ` )

Required. The desired output location and configuration.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## OutputConfig

Output configuration for the Model export.

Fields

`exportFormatId` `string`

The id of the format in which the Model must be exported. Each Model lists the `  export formats it supports  ` . If no value is provided here, then the first from the list of the Model's supported formats is used by default.

`artifactDestination` ` object ( GcsDestination  ` )

The Cloud Storage location where the Model artifact is to be written to. Under the directory given as the destination a new one with name " `model-export-<model-display-name>-<timestamp-of-export-call>` ", where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format, will be created. Inside, the Model and any of its supporting files will be written. This field should only be set when the `exportableContent` field of the \[Model.supported\_export\_formats\] object contains `ARTIFACT` .

`imageDestination` ` object ( ContainerRegistryDestination  ` )

The Google Artifact Registry uri where the Model container image will be copied to. This field should only be set when the `exportableContent` field of the \[Model.supported\_export\_formats\] object contains `IMAGE` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;exportFormatId&quot;: string,&quot;artifactDestination&quot;: {object (GcsDestination)},&quot;imageDestination&quot;: {object (ContainerRegistryDestination)}}</code></pre></td>
</tr>
</tbody>
</table>

## ContainerRegistryDestination

The Artifact Registry location for the container image.

Fields

`outputUri` `string`

Required. Artifact Registry URI of a container image. Only Google Artifact Registry are supported now. Accepted forms:

  - Google Artifact Registry path. For example: `gcr.io/projectId/imageName:tag` .

  - Artifact Registry path. For example: `us-central1-docker.pkg.dev/projectId/repoName/imageName:tag` .

If a tag is not specified, "latest" will be used as the default tag.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;outputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
