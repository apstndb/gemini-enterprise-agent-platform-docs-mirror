---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `import_rag_files`

Imports files into a RagCorpus from Cloud Storage or Google Drive. This is a long-running operation. Format: 'projects/{project_id}/locations/{region}/ragCorpora/{rag_corpus_id}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `import_rag_files` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "import_rag_files",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `VertexRagDataService.ImportRagFiles` .

### ImportRagFilesRequest

**JSON representation**

```
{
  "parent": string,
  "importRagFilesConfig": {
    object (ImportRagFilesConfig)
  }
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                 |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`               | `string` Required. The name of the RagCorpus resource into which to import files. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`                                                                                                                                                     |
| `importRagFilesConfig` | `object ( `[`ImportRagFilesConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.ImportRagFilesConfig)` )` Required. The config for the RagFiles to be synced and imported into the RagCorpus. `VertexRagDataService.ImportRagFiles` . |

### ImportRagFilesConfig

**JSON representation**

```
{
  "ragFileTransformationConfig": {
    object (RagFileTransformationConfig)
  },
  "ragFileParsingConfig": {
    object (RagFileParsingConfig)
  },
  "maxEmbeddingRequestsPerMin": integer,
  "rebuildAnnIndex": boolean,

  // Union field import_source can be only one of the following:
  "gcsSource": {
    object (GcsSource)
  },
  "googleDriveSource": {
    object (GoogleDriveSource)
  },
  "slackSource": {
    object (SlackSource)
  },
  "jiraSource": {
    object (JiraSource)
  },
  "sharePointSources": {
    object (SharePointSources)
  }
  // End of list of possible types for union field import_source.

  // Union field partial_failure_sink can be only one of the following:
  "partialFailureGcsSink": {
    object (GcsDestination)
  },
  "partialFailureBigquerySink": {
    object (BigQueryDestination)
  }
  // End of list of possible types for union field partial_failure_sink.

  // Union field import_result_sink can be only one of the following:
  "importResultGcsSink": {
    object (GcsDestination)
  },
  "importResultBigquerySink": {
    object (BigQueryDestination)
  }
  // End of list of possible types for union field import_result_sink.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ragFileTransformationConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.RagFileTransformationConfig"><code>RagFileTransformationConfig</code></a><code> )</code></p>
<p>Specifies the transformation config for RagFiles.</p></td>
</tr>
<tr class="even">
<td><code>ragFileParsingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.RagFileParsingConfig"><code>RagFileParsingConfig</code></a><code> )</code></p>
<p>Optional. Specifies the parsing config for RagFiles. RAG will use the default parser if this field is not set.</p></td>
</tr>
<tr class="odd">
<td><code>maxEmbeddingRequestsPerMin</code></td>
<td><p><code>integer</code></p>
<p>Optional. The max number of queries per minute that this job is allowed to make to the embedding model specified on the corpus. This value is specific to this job and not shared across other import jobs. Consult the Quotas page on the project to set an appropriate value here. If unspecified, a default value of 1,000 QPM would be used.</p></td>
</tr>
<tr class="even">
<td><code>rebuildAnnIndex</code></td>
<td><p><code>boolean</code></p>
<p>Rebuilds the ANN index to optimize for recall on the imported data. Only applicable for RagCorpora running on RagManagedDb with <code>retrieval_strategy</code> set to <code>ANN</code> . The rebuild will be performed using the existing ANN config set on the RagCorpus. To change the ANN config, please use the UpdateRagCorpus API.</p>
<p>Default is false, i.e., index is not rebuilt.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>import_source</code> . The source of the import. <code>import_source</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>gcsSource</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.GcsSource"><code>GcsSource</code></a><code> )</code></p>
<p>Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - <code>gs://bucket_name/my_directory/object_name/my_file.txt</code> - <code>gs://bucket_name/my_directory</code></p></td>
</tr>
<tr class="odd">
<td><code>googleDriveSource</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.GoogleDriveSource"><code>GoogleDriveSource</code></a><code> )</code></p>
<p>Google Drive location. Supports importing individual files as well as Google Drive folders.</p></td>
</tr>
<tr class="even">
<td><code>slackSource</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.SlackSource"><code>SlackSource</code></a><code> )</code></p>
<p>Slack channels with their corresponding access tokens.</p></td>
</tr>
<tr class="odd">
<td><code>jiraSource</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.JiraSource"><code>JiraSource</code></a><code> )</code></p>
<p>Jira queries with their corresponding authentication.</p></td>
</tr>
<tr class="even">
<td><code>sharePointSources</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.SharePointSources"><code>SharePointSources</code></a><code> )</code></p>
<p>SharePoint sources.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>partial_failure_sink</code> . Optional. If provided, all partial failures are written to the sink. Deprecated. Prefer to use the <code>import_result_sink</code> . <code>partial_failure_sink</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>partialFailureGcsSink </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.GcsDestination"><code>GcsDestination</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The Cloud Storage path to write partial failures to. Deprecated. Prefer to use <code>import_result_gcs_sink</code> .</p></td>
</tr>
<tr class="odd">
<td><code>partialFailureBigquerySink </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.BigQueryDestination"><code>BigQueryDestination</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The BigQuery destination to write partial failures to. It should be a bigquery table resource name (e.g. "bq://projectId.bqDatasetId.bqTableId"). The dataset must exist. If the table does not exist, it will be created with the expected schema. If the table exists, the schema will be validated and data will be added to this existing table. Deprecated. Prefer to use <code>import_result_bq_sink</code> .</p></td>
</tr>
<tr class="even">
<td>Union field <code>import_result_sink</code> . Optional. If provided, all successfully imported files and all partial failures are written to the sink. <code>import_result_sink</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>importResultGcsSink</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.GcsDestination"><code>GcsDestination</code></a><code> )</code></p>
<p>The Cloud Storage path to write import result to.</p></td>
</tr>
<tr class="even">
<td><code>importResultBigquerySink</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.BigQueryDestination"><code>BigQueryDestination</code></a><code> )</code></p>
<p>The BigQuery destination to write import result to. It should be a bigquery table resource name (e.g. "bq://projectId.bqDatasetId.bqTableId"). The dataset must exist. If the table does not exist, it will be created with the expected schema. If the table exists, the schema will be validated and data will be added to this existing table.</p></td>
</tr>
</tbody>
</table>

### GcsSource

**JSON representation**

```
{
  "uris": [
    string
  ]
}
```

| Fields   |                                                                                                                                                                                         |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uris[]` | `string` Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> . |

### GoogleDriveSource

**JSON representation**

```
{
  "resourceIds": [
    {
      object (ResourceId)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                                      |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resourceIds[]` | `object ( `[`ResourceId`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.ResourceId)` )` Required. Google Drive resource IDs. |

### ResourceId

**JSON representation**

```
{
  "resourceType": enum (ResourceType),
  "resourceId": string
}
```

| Fields         |                                                                                                                                                                                                                    |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resourceType` | `enum ( `[`ResourceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.ResourceType)` )` Required. The type of the Google Drive resource. |
| `resourceId`   | `string` Required. The ID of the Google Drive resource.                                                                                                                                                            |

### SlackSource

**JSON representation**

```
{
  "channels": [
    {
      object (SlackChannels)
    }
  ]
}
```

| Fields       |                                                                                                                                                                                                     |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `channels[]` | `object ( `[`SlackChannels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.SlackChannels)` )` Required. The Slack channels. |

### SlackChannels

**JSON representation**

```
{
  "channels": [
    {
      object (SlackChannel)
    }
  ],
  "apiKeyConfig": {
    object (ApiKeyConfig)
  }
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `channels[]`   | `object ( `[`SlackChannel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.SlackChannel)` )` Required. The Slack channel IDs.                                                                                                                                                                                                                                         |
| `apiKeyConfig` | `object ( `[`ApiKeyConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.ApiKeyConfig)` )` Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Slack channel access token that has access to the slack channel IDs. See: <https://api.slack.com/tutorials/tracks/getting-a-token> . |

### SlackChannel

**JSON representation**

```
{
  "channelId": string,
  "startTime": string,
  "endTime": string
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `channelId` | `string` Required. The Slack channel ID.                                                                                                                                                                                                                                                                                                                                                                                       |
| `startTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. The starting timestamp for messages to import. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `endTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. The ending timestamp for messages to import. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .   |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### ApiKeyConfig

**JSON representation**

```
{
  "apiKeySecretVersion": string,
  "apiKeyString": string
}
```

| Fields                |                                                                                                                                                |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `apiKeySecretVersion` | `string` Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version} |
| `apiKeyString`        | `string` The API key string. Either this or `api_key_secret_version` must be set.                                                              |

### JiraSource

**JSON representation**

```
{
  "jiraQueries": [
    {
      object (JiraQueries)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `jiraQueries[]` | `object ( `[`JiraQueries`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.JiraQueries)` )` Required. The Jira queries. |

### JiraQueries

**JSON representation**

```
{
  "projects": [
    string
  ],
  "customQueries": [
    string
  ],
  "email": string,
  "serverUri": string,
  "apiKeyConfig": {
    object (ApiKeyConfig)
  }
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projects[]`      | `string` A list of Jira projects to import in their entirety.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `customQueries[]` | `string` A list of custom Jira queries to import. For information about JQL (Jira Query Language), see <https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/>                                                                                                                                                                                                                                                    |
| `email`           | `string` Required. The Jira email address.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `serverUri`       | `string` Required. The Jira server URI.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `apiKeyConfig`    | `object ( `[`ApiKeyConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.ApiKeyConfig)` )` Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Jira API key. See [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/) . |

### SharePointSources

**JSON representation**

```
{
  "sharePointSources": [
    {
      object (SharePointSource)
    }
  ]
}
```

| Fields                |                                                                                                                                                                                                     |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sharePointSources[]` | `object ( `[`SharePointSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.SharePointSource)` )` The SharePoint sources. |

### SharePointSource

**JSON representation**

```
{
  "clientId": string,
  "clientSecret": {
    object (ApiKeyConfig)
  },
  "tenantId": string,
  "sharepointSiteName": string,
  "fileId": string,

  // Union field folder_source can be only one of the following:
  "sharepointFolderPath": string,
  "sharepointFolderId": string
  // End of list of possible types for union field folder_source.

  // Union field drive_source can be only one of the following:
  "driveName": string,
  "driveId": string
  // End of list of possible types for union field drive_source.
}
```

| Fields                                                                                                                                      |                                                                                                                                                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `clientId`                                                                                                                                  | `string` The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All.              |
| `clientSecret`                                                                                                                              | `object ( `[`ApiKeyConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.ApiKeyConfig)` )` The application secret for the app registered in Azure. |
| `tenantId`                                                                                                                                  | `string` Unique identifier of the Azure Active Directory Instance.                                                                                                                                                           |
| `sharepointSiteName`                                                                                                                        | `string` The name of the SharePoint site to download from. This can be the site name or the site id.                                                                                                                         |
| `fileId`                                                                                                                                    | `string` Output only. The SharePoint file id. Output only.                                                                                                                                                                   |
| Union field `folder_source` . The SharePoint folder source. If not provided, uses "root". `folder_source` can be only one of the following: |                                                                                                                                                                                                                              |
| `sharepointFolderPath`                                                                                                                      | `string` The path of the SharePoint folder to download from.                                                                                                                                                                 |
| `sharepointFolderId`                                                                                                                        | `string` The ID of the SharePoint folder to download from.                                                                                                                                                                   |
| Union field `drive_source` . The SharePoint drive source. `drive_source` can be only one of the following:                                  |                                                                                                                                                                                                                              |
| `driveName`                                                                                                                                 | `string` The name of the drive to download from.                                                                                                                                                                             |
| `driveId`                                                                                                                                   | `string` The ID of the drive to download from.                                                                                                                                                                               |

### GcsDestination

**JSON representation**

```
{
  "outputUriPrefix": string
}
```

| Fields            |                                                                                                                                                                                       |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outputUriPrefix` | `string` Required. Google Cloud Storage URI to output directory. If the uri doesn't end with '/', a '/' will be automatically appended. The directory is created if it doesn't exist. |

### BigQueryDestination

**JSON representation**

```
{
  "outputUri": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>outputUri</code></td>
<td><p><code>string</code></p>
<p>Required. BigQuery URI to a project or table, up to 2000 characters long.</p>
<p>When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist.</p>
<p>Accepted forms:</p>
<ul>
<li>BigQuery path. For example: <code>bq://projectId</code> or <code>bq://projectId.bqDatasetId</code> or <code>bq://projectId.bqDatasetId.bqTableId</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

### RagFileTransformationConfig

**JSON representation**

```
{
  "ragFileChunkingConfig": {
    object (RagFileChunkingConfig)
  }
}
```

| Fields                  |                                                                                                                                                                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ragFileChunkingConfig` | `object ( `[`RagFileChunkingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.RagFileChunkingConfig)` )` Specifies the chunking config for RagFiles. |

### RagFileChunkingConfig

**JSON representation**

```
{

  // Union field chunking_config can be only one of the following:
  "fixedLengthChunking": {
    object (FixedLengthChunking)
  }
  // End of list of possible types for union field chunking_config.
}
```

| Fields                                                                                                                          |                                                                                                                                                                                                                               |
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `chunking_config` . Specifies the chunking config for RagFiles. `chunking_config` can be only one of the following: |                                                                                                                                                                                                                               |
| `fixedLengthChunking`                                                                                                           | `object ( `[`FixedLengthChunking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.FixedLengthChunking)` )` Specifies the fixed length chunking config. |

### FixedLengthChunking

**JSON representation**

```
{
  "chunkSize": integer,
  "chunkOverlap": integer
}
```

| Fields         |                                       |
|----------------|---------------------------------------|
| `chunkSize`    | `integer` The size of the chunks.     |
| `chunkOverlap` | `integer` The overlap between chunks. |

### RagFileParsingConfig

**JSON representation**

```
{

  // Union field parser can be only one of the following:
  "layoutParser": {
    object (LayoutParser)
  },
  "llmParser": {
    object (LlmParser)
  }
  // End of list of possible types for union field parser.
}
```

| Fields                                                                                            |                                                                                                                                                                                                            |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `parser` . The parser to use for RagFiles. `parser` can be only one of the following: |                                                                                                                                                                                                            |
| `layoutParser`                                                                                    | `object ( `[`LayoutParser`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.LayoutParser)` )` The Layout Parser to use for RagFiles. |
| `llmParser`                                                                                       | `object ( `[`LlmParser`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/import_rag_files#Input.Schema.LlmParser)` )` The LLM Parser to use for RagFiles.          |

### LayoutParser

**JSON representation**

```
{
  "processorName": string,
  "maxParsingRequestsPerMin": integer
}
```

| Fields                     |                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `processorName`            | `string` The full resource name of a Document AI processor or processor version. The processor must have type `LAYOUT_PARSER_PROCESSOR` . If specified, the `additional_config.parse_as_scanned_pdf` field must be false. Format: \* `projects/{project_id}/locations/{location}/processors/{processor_id}` \* `projects/{project_id}/locations/{location}/processors/{processor_id}/processorVersions/{processor_version_id}` |
| `maxParsingRequestsPerMin` | `integer` The maximum number of requests the job is allowed to make to the Document AI processor per minute. Consult <https://cloud.google.com/document-ai/quotas> and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM would be used.                                                                                                                             |

### LlmParser

**JSON representation**

```
{
  "modelName": string,
  "maxParsingRequestsPerMin": integer,
  "customParsingPrompt": string
}
```

| Fields                     |                                                                                                                                                                                                                                                                                             |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modelName`                | `string` The name of a LLM model used for parsing. Format: \* `projects/{project_id}/locations/{location}/publishers/{publisher}/models/{model}`                                                                                                                                            |
| `maxParsingRequestsPerMin` | `integer` The maximum number of requests the job is allowed to make to the LLM model per minute. Consult <https://cloud.google.com/vertex-ai/generative-ai/docs/quotas> and your document size to set an appropriate value here. If unspecified, a default value of 5000 QPM would be used. |
| `customParsingPrompt`      | `string` The prompt to use for parsing. If not specified, a default prompt will be used.                                                                                                                                                                                                    |

### ResourceType

The type of the Google Drive resource.

| Enums                       |                            |
|-----------------------------|----------------------------|
| `RESOURCE_TYPE_UNSPECIFIED` | Unspecified resource type. |
| `RESOURCE_TYPE_FILE`        | File resource type.        |
| `RESOURCE_TYPE_FOLDER`      | Folder resource type.      |

## Output Schema

This resource represents a long-running operation that is the result of a network API call.

### Operation

**JSON representation**

```
{
  "name": string,
  "metadata": {
    "@type": string,
    field1: ...,
    ...
  },
  "done": boolean,

  // Union field result can be only one of the following:
  "error": {
    object (Status)
  },
  "response": {
    "@type": string,
    field1: ...,
    ...
  }
  // End of list of possible types for union field result.
}
```

| Fields                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                                                                                                                                                          | `string` The server-assigned name, which is only unique within the same service that originally returns it. If you use the default HTTP mapping, the `name` should be a resource name ending with `operations/{unique_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `metadata`                                                                                                                                                                                                                                                                                                                      | `object` Service-specific metadata associated with the operation. It typically contains progress information and common metadata such as create time. Some services might not provide such metadata. Any method that returns a long-running operation should document the metadata type, if any. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .                                                                                                                                                                                                                     |
| `done`                                                                                                                                                                                                                                                                                                                          | `boolean` If the value is `false` , it means the operation is still in progress. If `true` , the operation is completed, and either `error` or `response` is available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Union field `result` . The operation result, which can be either an `error` or a valid `response` . If `done` == `false` , neither `error` nor `response` is set. If `done` == `true` , exactly one of `error` or `response` can be set. Some services might not provide the result. `result` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `error`                                                                                                                                                                                                                                                                                                                         | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` The error result of the operation in case of failure or cancellation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `response`                                                                                                                                                                                                                                                                                                                      | `object` The normal, successful response of the operation. If the original method returns no data on success, such as `Delete` , the response is `google.protobuf.Empty` . If the original method is standard `Get` / `Create` / `Update` , the response should be the resource. For other methods, the response should have the type `XxxResponse` , where `Xxx` is the original method name. For example, if the original method name is `TakeSnapshot()` , the inferred response type is `TakeSnapshotResponse` . An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
