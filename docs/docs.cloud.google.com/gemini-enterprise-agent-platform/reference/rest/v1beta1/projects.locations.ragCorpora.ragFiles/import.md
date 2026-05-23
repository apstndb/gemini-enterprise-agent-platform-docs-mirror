---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/import
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/import
title: 'Method: ragFiles.import'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragFiles.import

Import files from Google Cloud Storage or Google Drive into a RagCorpus.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /ragFiles:import`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the RagCorpus resource into which to import files. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Request body

The request body contains data with the following structure:

Fields

`importRagFilesConfig` ` object ( ImportRagFilesConfig  ` )

Required. The config for the RagFiles to be synced and imported into the RagCorpus. `  VertexRagDataService.ImportRagFiles  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## ImportRagFilesConfig

Config for importing RagFiles.

Fields

` ragFileChunkingConfig (deprecated)  ` ` object ( RagFileChunkingConfig  ` )

> This item is deprecated\!

Specifies the size and overlap of chunks after importing RagFiles.

`ragFileTransformationConfig` ` object ( RagFileTransformationConfig  ` )

Specifies the transformation config for RagFiles.

`ragFileParsingConfig` ` object ( RagFileParsingConfig  ` )

Optional. Specifies the parsing config for RagFiles. RAG will use the default parser if this field is not set.

` ragFileMetadataConfig (deprecated)  ` ` object ( RagFileMetadataConfig  ` )

> This item is deprecated\!

Specifies the metadata config for RagFiles. Including paths for metadata schema and metadata. Deprecated: Not in use.

`maxEmbeddingRequestsPerMin` `integer`

Optional. The max number of queries per minute that this job is allowed to make to the embedding model specified on the corpus. This value is specific to this job and not shared across other import jobs. Consult the Quotas page on the project to set an appropriate value here. If unspecified, a default value of 1,000 QPM would be used.

`globalMaxEmbeddingRequestsPerMin` `integer`

Optional. The max number of queries per minute that the indexing pipeline job is allowed to make to the embedding model specified in the project. Please follow the quota usage guideline of the embedding model you use to set the value properly.If this value is not specified, maxEmbeddingRequestsPerMin will be used by indexing pipeline job as the global limit.

`rebuildAnnIndex` `boolean`

Rebuilds the ANN index to optimize for recall on the imported data. Only applicable for RagCorpora running on RagManagedDb with `retrieval_strategy` set to `ANN` . The rebuild will be performed using the existing ANN config set on the RagCorpus. To change the ANN config, please use the UpdateRagCorpus API.

Default is false, i.e., index is not rebuilt.

`import_source` `Union type`

The source of the import. `import_source` can be only one of the following:

`gcsSource` ` object ( GcsSource  ` )

Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucketName/my_directory/objectName/my_file.txt` - `gs://bucketName/my_directory`

`googleDriveSource` ` object ( GoogleDriveSource  ` )

Google Drive location. Supports importing individual files as well as Google Drive folders.

`slackSource` ` object ( SlackSource  ` )

Slack channels with their corresponding access tokens.

`jiraSource` ` object ( JiraSource  ` )

Jira queries with their corresponding authentication.

`sharePointSources` ` object ( SharePointSources  ` )

SharePoint sources.

`partial_failure_sink` `Union type`

Optional. If provided, all partial failures are written to the sink. Deprecated. Prefer to use the `import_result_sink` . `partial_failure_sink` can be only one of the following:

` partialFailureGcsSink (deprecated)  ` `object ( GcsDestination` )

> This item is deprecated\!

The Cloud Storage path to write partial failures to. Deprecated. Prefer to use `importResultGcsSink` .

` partialFailureBigquerySink (deprecated)  ` ` object ( BigQueryDestination  ` )

> This item is deprecated\!

The BigQuery destination to write partial failures to. It should be a bigquery table resource name (e.g. "bq://projectId.bqDatasetId.bqTableId"). The dataset must exist. If the table does not exist, it will be created with the expected schema. If the table exists, the schema will be validated and data will be added to this existing table. Deprecated. Prefer to use `import_result_bq_sink` .

`import_result_sink` `Union type`

Optional. If provided, all successfully imported files and all partial failures are written to the sink. `import_result_sink` can be only one of the following:

`importResultGcsSink` `object ( GcsDestination` )

The Cloud Storage path to write import result to.

`importResultBigquerySink` ` object ( BigQueryDestination  ` )

The BigQuery destination to write import result to. It should be a bigquery table resource name (e.g. "bq://projectId.bqDatasetId.bqTableId"). The dataset must exist. If the table does not exist, it will be created with the expected schema. If the table exists, the schema will be validated and data will be added to this existing table.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragFileChunkingConfig&quot;: {object (RagFileChunkingConfig)},&quot;ragFileTransformationConfig&quot;: {object (RagFileTransformationConfig)},&quot;ragFileParsingConfig&quot;: {object (RagFileParsingConfig)},&quot;ragFileMetadataConfig&quot;: {object (RagFileMetadataConfig)},&quot;maxEmbeddingRequestsPerMin&quot;: integer,&quot;globalMaxEmbeddingRequestsPerMin&quot;: integer,&quot;rebuildAnnIndex&quot;: boolean,// import_source&quot;gcsSource&quot;: {object (GcsSource)},&quot;googleDriveSource&quot;: {object (GoogleDriveSource)},&quot;slackSource&quot;: {object (SlackSource)},&quot;jiraSource&quot;: {object (JiraSource)},&quot;sharePointSources&quot;: {object (SharePointSources)}// Union type// partial_failure_sink&quot;partialFailureGcsSink&quot;: {object (GcsDestination)},&quot;partialFailureBigquerySink&quot;: {object (BigQueryDestination)}// Union type// import_result_sink&quot;importResultGcsSink&quot;: {object (GcsDestination)},&quot;importResultBigquerySink&quot;: {object (BigQueryDestination)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>
