---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig
title: NotebookSoftwareConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

Fields

`env[]` `object ( EnvVar` )

Optional. Environment variables to be passed to the container. Maximum limit is 100.

`postStartupScriptConfig` ` object ( PostStartupScriptConfig  ` )

Optional. Post startup script config.

`runtime_image` `Union type`

The image to be used by the notebook runtime. Can be one of release name, or custom container image. `runtime_image` can be only one of the following:

`colabImage` ` object ( ColabImage  ` )

Optional. Google-managed NotebookRuntime colab image.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;env&quot;: [{object (EnvVar)}],&quot;postStartupScriptConfig&quot;: {object (PostStartupScriptConfig)},// runtime_image&quot;colabImage&quot;: {object (ColabImage)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ColabImage

Colab image of the runtime.

Fields

`releaseName` `string`

Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release.

`description` `string`

Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11"

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
  &quot;releaseName&quot;: string,
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## PostStartupScriptConfig

Post startup script config.

Fields

`postStartupScript` `string`

Optional. Post startup script to run after runtime is started.

`postStartupScriptUrl` `string`

Optional. Post startup script url to download. Example: `gs://bucket/script.sh`

`postStartupScriptBehavior` ` enum ( PostStartupScriptBehavior  ` )

Optional. Post startup script behavior that defines download and execution behavior.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;postStartupScript&quot;: string,&quot;postStartupScriptUrl&quot;: string,&quot;postStartupScriptBehavior&quot;: enum (PostStartupScriptBehavior)}</code></pre></td>
</tr>
</tbody>
</table>

## PostStartupScriptBehavior

Represents a notebook runtime post startup script behavior.

Enums

`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED`

Unspecified post startup script behavior.

`RUN_ONCE`

Run post startup script after runtime is started.

`RUN_EVERY_START`

Run post startup script after runtime is stopped.

`DOWNLOAD_AND_RUN_EVERY_START`

Download and run post startup script every time runtime is started.
