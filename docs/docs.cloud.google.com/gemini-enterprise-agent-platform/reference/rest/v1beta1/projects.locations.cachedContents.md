---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.cachedContents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.cachedContents
title: 'REST Resource: projects.locations.cachedContents'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: CachedContent

A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

Fields

`name` `string`

Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cachedContent}

`displayName` `string`

Optional. Immutable. The user-generated meaningful display name of the cached content.

`model` `string`

Immutable. The name of the `Model` to use for cached content. Currently, only the published Gemini base models are supported, in form of projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}

`systemInstruction` ` object ( Content  ` )

Optional. Input only. Immutable. Developer set system instruction. Currently, text only

`contents[]` ` object ( Content  ` )

Optional. Input only. Immutable. The content to cache

`tools[]` ` object ( Tool  ` )

Optional. Input only. Immutable. A list of `Tools` the model may use to generate the next response

`toolConfig` ` object ( ToolConfig  ` )

Optional. Input only. Immutable. Tool config. This config is shared for all tools

`createTime` ` string ( Timestamp  ` format)

Output only. Creation time of the cache entry.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. When the cache entry was last updated in UTC time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`usageMetadata` ` object ( UsageMetadata  ` )

Output only. metadata on the usage of the cached content.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Input only. Immutable. Customer-managed encryption key spec for a `CachedContent` . If set, this `CachedContent` and all its sub-resources will be secured by this key.

`expiration` `Union type`

Expiration time of the cached content. `expiration` can be only one of the following:

`expireTime` ` string ( Timestamp  ` format)

timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what was sent on input.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` ` string ( Duration  ` format)

Input only. The TTL for this resource. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;model&quot;: string,&quot;systemInstruction&quot;: {object (Content)},&quot;contents&quot;: [{object (Content)}],&quot;tools&quot;: [{object (Tool)}],&quot;toolConfig&quot;: {object (ToolConfig)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;usageMetadata&quot;: {object (UsageMetadata)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},// expiration&quot;expireTime&quot;: string,&quot;ttl&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## UsageMetadata

metadata on the usage of the cached content.

Fields

`totalTokenCount` `integer`

Total number of tokens that the cached content consumes.

`textCount` `integer`

Number of text characters.

`imageCount` `integer`

Number of images.

`videoDurationSeconds` `integer`

Duration of video in seconds.

`audioDurationSeconds` `integer`

Duration of audio in seconds.

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
  &quot;totalTokenCount&quot;: integer,
  &quot;textCount&quot;: integer,
  &quot;imageCount&quot;: integer,
  &quot;videoDurationSeconds&quot;: integer,
  &quot;audioDurationSeconds&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

### `            delete           `

Deletes cached content

### `            get           `

Gets cached content configurations

### `            list           `

Lists cached contents in a project

### `            patch           `

Updates cached content configurations
