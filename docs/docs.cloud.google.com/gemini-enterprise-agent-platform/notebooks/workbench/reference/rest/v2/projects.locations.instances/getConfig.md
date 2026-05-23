---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/getConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/getConfig
title: 'Method: projects.locations.instances.getConfig'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Returns various configuration parameters.

### HTTP request

`GET https://notebooks.googleapis.com/v2/{name}/instances:getConfig`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}`

### Request body

The request body must be empty.

### Response body

Response for getting WbI configurations in a location

If successful, the response body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;defaultValues&quot;: {object (DefaultValues)},&quot;supportedValues&quot;: {object (SupportedValues)},&quot;availableImages&quot;: [{object (ImageRelease)}],&quot;disableWorkbenchLegacyCreation&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`defaultValues`

` object ( DefaultValues  ` )

Output only. The default values for configuration.

`supportedValues`

` object ( SupportedValues  ` )

Output only. The supported values for configuration.

`availableImages[]`

` object ( ImageRelease  ` )

Output only. The list of available images to create a WbI.

`disableWorkbenchLegacyCreation`

`boolean`

Output only. Flag to disable the creation of legacy Workbench notebooks (User-managed notebooks and Google-managed notebooks).

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## DefaultValues

DefaultValues represents the default configuration values.

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
  &quot;machineType&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

Output only. The default machine type used by the backend if not provided by the user.

## SupportedValues

SupportedValues represents the values supported by the configuration.

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
  &quot;machineTypes&quot;: [
    string
  ],
  &quot;acceleratorTypes&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineTypes[]`

`string`

Output only. The machine types supported by WbI.

`acceleratorTypes[]`

`string`

Output only. The accelerator types supported by WbI.

## ImageRelease

ConfigImage represents an image release available to create a WbI

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
  &quot;imageName&quot;: string,
  &quot;releaseName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`imageName`

`string`

Output only. The name of the image of the form workbench-instances-vYYYYmmdd- -

`releaseName`

`string`

Output only. The release of the image of the form m123
