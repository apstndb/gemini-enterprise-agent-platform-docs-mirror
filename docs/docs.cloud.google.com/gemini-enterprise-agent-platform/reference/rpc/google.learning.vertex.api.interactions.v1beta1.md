---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.learning.vertex.api.interactions.v1beta1
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.learning.vertex.api.interactions.v1beta1
title: Package google.learning.vertex.api.interactions.v1beta1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  InteractionsService  ` (interface)
  - `  VoicesHttpService  ` (interface)
  - `  VoicesService  ` (interface)

## InteractionsService

API that allows users to interact with models and agents.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CancelInteraction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CancelInteraction(              CancelInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             Interaction            </code> )</p>
<p>Cancels an interaction.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CancelInteractionHttp</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CancelInteractionHttp(              CancelInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             HttpBody            </code> )</p>
<p>Cancels an interaction.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateInteraction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateInteraction(              CreateInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             Interaction            </code> )</p>
<p>Creates an interaction.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateInteractionHttp</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateInteractionHttp(              CreateInteractionHttpRequest            </code> ) returns ( <code dir="ltr" translate="no">             HttpBody            </code> )</p>
<p>Generates a set of responses from the model.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateInteractionStream</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateInteractionStream(              CreateInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             InteractionStreamingEvent            </code> )</p>
<p>Creates an interaction and streams the response.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteInteraction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteInteraction(              DeleteInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             DeleteInteractionResponse            </code> )</p>
<p>Deletes an interaction.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetInteraction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetInteraction(              GetInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             Interaction            </code> )</p>
<p>Fully typed proto, unary version of GetInteraction that returns Interaction proto.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetInteractionHttp</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetInteractionHttp(              GetInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             HttpBody            </code> )</p>
<p>Gets an interaction.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetInteractionStream</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetInteractionStream(              GetInteractionRequest            </code> ) returns ( <code dir="ltr" translate="no">             InteractionStreamingEvent            </code> )</p>
<p>Fully typed proto, streaming version of GetInteraction that returns Interaction proto.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListInteractions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListInteractions(              ListInteractionsRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListInteractionsResponse            </code> )</p>
<p>List interactions.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListInteractionsHttp</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListInteractionsHttp(              ListInteractionsRequest            </code> ) returns ( <code dir="ltr" translate="no">             HttpBody            </code> )</p>
<p>List interactions.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## VoicesHttpService

## VoicesService

VoicesService defines typed RPCs for future SDK generation. NOTE: No handlers are currently registered for these RPCs. All traffic is served via VoicesHttpService (the HttpBody-wrapping service). When handlers are added, the scaffolding\_registration\_test in labs/language/genai/Voices/ must be updated to include "VoicesService" in its services argument.
