---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus
title: Manage your RAG knowledge base (corpus)
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

This page describes how you can manage your corpus for RAG tasks by performing corpus management and file management.

## Corpus management

A corpus, also referred to as an index, is a collection of documents or source of information. The corpus can be queried to retrieve relevant contexts for response generation. When creating a corpus for the first time, the process might take an additional minute.

The following corpus operations are supported:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Operation</th>
<th>Description</th>
<th>Parameters</th>
<th>Examples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Create a RAG corpus.</td>
<td><p>Create a RAG corpus to import or upload documents.</p>
<p>If you're using VPC-SC and it's the first time that you've called <code dir="ltr" translate="no">createRagCorpus</code> and the call returns an error, then just wait a few minutes and retry.</p></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/create">Create parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/create">Create parameters v1</a></p></td>
<td></td>
</tr>
<tr class="even">
<td>Update a RAG corpus.</td>
<td>Update a previously-created RAG corpus to import or upload documents.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/patch">Update parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/patch">Update parameters v1</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td>List a RAG corpus.</td>
<td>List all of the RAG corpora.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/list">List parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/list">List parameters v1</a></p></td>
<td></td>
</tr>
<tr class="even">
<td>Get a RAG corpus.</td>
<td>Get the metadata describing the RAG corpus.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/get">Get parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/get">Get parameters v1</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td>Delete a RAG corpus.</td>
<td>Delete the RAG corpus.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora/delete">Delete parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/delete">Delete parameters v1</a></p></td>
<td></td>
</tr>
</tbody>
</table>

Concurrent operations on corpora aren't supported. For more information, see the [RAG API reference for v1beta1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1) or [RAG API reference for v1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1) .

### File management

The following file operations are supported:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Operation</th>
<th>Description</th>
<th>Parameters</th>
<th>Examples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Upload a RAG file.</td>
<td>Upload a file from local storage with additional information that provides context to the LLM to generate more accurate responses.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/upload">Upload parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/upload">Upload parameters v1</a></p></td>
<td></td>
</tr>
<tr class="even">
<td>Import RAG files.</td>
<td>Import a set of files from some other storage into a storage location.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/import">Import parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/import">Import parameters v1</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td>List RAG files.</td>
<td>List all of the files in the RAG corpus.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/list">List parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/list">List parameters v1</a></p></td>
<td></td>
</tr>
<tr class="even">
<td>Get a RAG file.</td>
<td>Get details about a RAG file for use by the LLM.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/get">Get parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/get">Get parameters v1</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td>Delete a RAG file.</td>
<td>Delete a file from the RAG corpus.</td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/delete">Delete parameters v1beta1</a></p>
<p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/delete">Delete parameters v1</a></p></td>
<td></td>
</tr>
</tbody>
</table>

## What's next

  - [Gemini Enterprise Agent Platform RAG Engine quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/quotas#rag-quotas)

  - To learn more about the Gemini Enterprise Agent Platform RAG Engine, see the following:
    
      - [`RagEngineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig)
    
      - [`RagChunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagChunk)
    
      - [`RagContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagContexts)
    
      - [`RagFileTransformationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig)
    
      - [`RagQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagQuery)
