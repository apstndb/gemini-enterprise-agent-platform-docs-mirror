---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles
title: 'REST Resource: projects.locations.servingProfiles'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ServingProfile

Configures the serving behavior for a resource-less GenAI serving.

Fields

`name` `string`

Identifier. The resource name of the ServingProfile.

`displayName` `string`

Required. The display name of the ServingProfile. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

Optional. The description of the ServingProfile.

`scope` ` enum ( ServingProfileScope  ` )

Required. The specific API this ServingProfile applies to.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when the ServingProfile was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when the ServingProfile was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`profile_spec` `Union type`

The profile spec for the ServingProfile. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`cmekConfig` ` object ( CmekConfig  ` )

CMEK configuration for the ServingProfile.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;scope&quot;: enum (ServingProfileScope),&quot;createTime&quot;: string,&quot;updateTime&quot;: string,// profile_spec&quot;cmekConfig&quot;: {object (CmekConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CmekConfig

Configuration for Customer-Managed Encryption Keys (CMEK).

Fields

`encryptionSpec` ` object ( EncryptionSpec  ` )

Required. The customer-managed encryption key spec for the Serving Profile.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;encryptionSpec&quot;: {object (EncryptionSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## ServingProfileScope

The specific API this ServingProfile applies to.

Enums

`SERVING_PROFILE_SCOPE_UNSPECIFIED`

Default value. This value is unused. When users create a ServingProfile, they must choose a scope.

`GEMINI_LIVE`

The scope for Gemini Live.

`INTERACTIONS_API`

The scope for Interactions API.

`RESPONSE_API`

The scope for Response API.

## Methods

### `            create           `

Creates a ServingProfile.

### `            delete           `

Deletes a ServingProfile.

### `            get           `

Gets a ServingProfile.

### `            list           `

Lists ServingProfiles in a Location.

### `            patch           `

Updates a ServingProfile.
