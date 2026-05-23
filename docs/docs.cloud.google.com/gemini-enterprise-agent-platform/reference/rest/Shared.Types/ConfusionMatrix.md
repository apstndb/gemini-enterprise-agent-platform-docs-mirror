---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ConfusionMatrix
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ConfusionMatrix
title: ConfusionMatrix
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`annotationSpecs[]` ` object ( AnnotationSpecRef  ` )

AnnotationSpecs used in the confusion matrix.

For AutoML Text Extraction, a special negative AnnotationSpec with empty `id` and `displayName` of "NULL" will be added as the last element.

`rows[]` ` array ( ListValue  ` format)

rows in the confusion matrix. The number of rows is equal to the size of `annotationSpecs` . `rows[i][j]` is the number of DataItems that have ground truth of the `annotationSpecs[i]` and are predicted as `annotationSpecs[j]` by the Model being evaluated.

For Text Extraction, when `annotationSpecs[i]` is the last element in `annotationSpecs` , i.e. the special negative AnnotationSpec, `rows[i][j]` is the number of predicted entities of `annoatationSpec[j]` that are not labeled as any of the ground truth AnnotationSpec. When annotationSpecs\[j\] is the special negative AnnotationSpec, `rows[i][j]` is the number of entities have ground truth of `annotationSpec[i]` that are not predicted as an entity by the Model. The value of the last cell, i.e. `row[i][j]` where i == j and `annotationSpec[i]` is the special negative AnnotationSpec, is always 0.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;annotationSpecs&quot;: [{object (AnnotationSpecRef)}],&quot;rows&quot;: [array]}</code></pre></td>
</tr>
</tbody>
</table>

## AnnotationSpecRef

Fields

`id` `string`

id of the AnnotationSpec.

`displayName` `string`

Display name of the AnnotationSpec.

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
  &quot;id&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
