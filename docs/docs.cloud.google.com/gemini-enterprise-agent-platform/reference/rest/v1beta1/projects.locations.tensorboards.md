---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards
title: 'REST Resource: projects.locations.tensorboards'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Tensorboard

Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

Fields

`name` `string`

Output only. name of the Tensorboard. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

`displayName` `string`

Required. user provided name of this Tensorboard.

`description` `string`

description of this Tensorboard.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a Tensorboard. If set, this Tensorboard and all sub-resources of this Tensorboard will be secured by this key.

`blobStoragePathPrefix` `string`

Output only. Consumer project Cloud Storage path prefix used to store blob data, which can either be a bucket or directory. Does not end with a '/'.

`runCount` `integer`

Output only. The number of Runs stored in this Tensorboard.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Tensorboard was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Tensorboard was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Tensorboards.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`etag` `string`

Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`isDefault` `boolean`

Used to indicate if the TensorBoard instance is the default one. Each project & region can have at most one default TensorBoard instance. Creation of a default TensorBoard instance and updating an existing TensorBoard instance to be default will mark all other TensorBoard instances (if any) as non default.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;blobStoragePathPrefix&quot;: string,&quot;runCount&quot;: integer,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;etag&quot;: string,&quot;isDefault&quot;: boolean,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            batchRead           `

Reads multiple TensorboardTimeSeries' data.

### `            create           `

Creates a Tensorboard.

### `            delete           `

Deletes a Tensorboard.

### `            get           `

Gets a Tensorboard.

### `            list           `

Lists Tensorboards in a Location.

### `            patch           `

Updates a Tensorboard.

### `            readSize           `

Returns the storage size for a given TensorBoard instance.

### `            readUsage           `

Returns a list of monthly active users for a given TensorBoard instance.
