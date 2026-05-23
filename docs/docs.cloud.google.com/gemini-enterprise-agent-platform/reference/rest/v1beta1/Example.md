---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Example
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Example
title: Example
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`displayName` `string`

Optional. The display name for Example.

`exampleId` `string`

Optional. Immutable. Unique identifier of an example. If not specified when upserting new examples, the exampleId will be generated.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Example was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`example_type` `Union type`

The type of the example. Each example type has a defined format `example_type` can be only one of the following:

`storedContentsExample` ` object ( StoredContentsExample  ` )

An example of chat history and its expected outcome to be used with GenerateContent.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;displayName&quot;: string,&quot;exampleId&quot;: string,&quot;createTime&quot;: string,// example_type&quot;storedContentsExample&quot;: {object (StoredContentsExample)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## StoredContentsExample

A ContentsExample to be used with GenerateContent alongside information required for storage and retrieval with Example Store.

Fields

`searchKey` `string`

Optional. (Optional) the search key used for retrieval. If not provided at upload-time, the search key will be generated from `contentsExample.contents` using the method provided by `searchKeyGenerationMethod` . The generated search key will be included in retrieved examples.

`contentsExample` ` object ( ContentsExample  ` )

Required. The example to be used with GenerateContent.

`searchKeyGenerationMethod` ` object ( SearchKeyGenerationMethod  ` )

Optional. The method used to generate the search key from `contentsExample.contents` . This is ignored when uploading an example if `searchKey` is provided.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchKey&quot;: string,&quot;contentsExample&quot;: {object (ContentsExample)},&quot;searchKeyGenerationMethod&quot;: {object (SearchKeyGenerationMethod)}}</code></pre></td>
</tr>
</tbody>
</table>

## ContentsExample

A single example of a conversation with the model.

Fields

`contents[]` ` object ( Content  ` )

Required. The content of the conversation with the model that resulted in the expected output.

`expectedContents[]` ` object ( ExpectedContent  ` )

Required. The expected output for the given `contents` . To represent multi-step reasoning, this is a repeated field that contains the iterative steps of the expected output.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contents&quot;: [{object (Content)}],&quot;expectedContents&quot;: [{object (ExpectedContent)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ExpectedContent

A single step of the expected output.

Fields

`content` ` object ( Content  ` )

Required. A single step's content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: {object (Content)}}</code></pre></td>
</tr>
</tbody>
</table>
