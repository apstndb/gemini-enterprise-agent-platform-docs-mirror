---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles
title: 'REST Resource: projects.locations.ragCorpora.ragFiles'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: RagFile

A RagFile contains user data for chunking, embedding and indexing.

Fields

`name` `string`

Output only. The resource name of the RagFile.

`displayName` `string`

Required. The display name of the RagFile. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

Optional. The description of the RagFile.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this RagFile was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this RagFile was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`fileStatus` ` object ( FileStatus  ` )

Output only. state of the RagFile.

`userMetadata` `string`

Output only. The metadata for metadata search. The userMetadata Needs to be in JSON format.

`rag_file_source` `Union type`

The origin location of the RagFile if it is imported from Google Cloud Storage or Google Drive. `rag_file_source` can be only one of the following:

`gcsSource` ` object ( GcsSource  ` )

Output only. Google Cloud Storage location of the RagFile. It does not support wildcards in the Cloud Storage uri for now.

`googleDriveSource` ` object ( GoogleDriveSource  ` )

Output only. Google Drive location. Supports importing individual files as well as Google Drive folders.

`directUploadSource` ` object ( DirectUploadSource  ` )

Output only. The RagFile is encapsulated and uploaded in the UploadRagFile request.

`slackSource` ` object ( SlackSource  ` )

The RagFile is imported from a Slack channel.

`jiraSource` ` object ( JiraSource  ` )

The RagFile is imported from a Jira query.

`sharePointSources` ` object ( SharePointSources  ` )

The RagFile is imported from a SharePoint source.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;fileStatus&quot;: {object (FileStatus)},&quot;userMetadata&quot;: string,// rag_file_source&quot;gcsSource&quot;: {object (GcsSource)},&quot;googleDriveSource&quot;: {object (GoogleDriveSource)},&quot;directUploadSource&quot;: {object (DirectUploadSource)},&quot;slackSource&quot;: {object (SlackSource)},&quot;jiraSource&quot;: {object (JiraSource)},&quot;sharePointSources&quot;: {object (SharePointSources)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleDriveSource

The Google Drive location for the input content.

Fields

`resourceIds[]` ` object ( ResourceId  ` )

Required. Google Drive resource IDs.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resourceIds&quot;: [{object (ResourceId)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ResourceId

The type and id of the Google Drive resource.

Fields

`resourceType` ` enum ( ResourceType  ` )

Required. The type of the Google Drive resource.

`resourceId` `string`

Required. The id of the Google Drive resource.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resourceType&quot;: enum (ResourceType),&quot;resourceId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ResourceType

The type of the Google Drive resource.

Enums

`RESOURCE_TYPE_UNSPECIFIED`

Unspecified resource type.

`RESOURCE_TYPE_FILE`

File resource type.

`RESOURCE_TYPE_FOLDER`

Folder resource type.

## DirectUploadSource

This type has no fields.

The input content is encapsulated and uploaded in the request.

## SlackSource

The Slack source for the ImportRagFilesRequest.

Fields

`channels[]` ` object ( SlackChannels  ` )

Required. The Slack channels.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;channels&quot;: [{object (SlackChannels)}]}</code></pre></td>
</tr>
</tbody>
</table>

## SlackChannels

SlackChannels contains the Slack channels and corresponding access token.

Fields

`channels[]` ` object ( SlackChannel  ` )

Required. The Slack channel IDs.

`apiKeyConfig` ` object ( ApiKeyConfig  ` )

Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Slack channel access token that has access to the slack channel IDs. See: <https://api.slack.com/tutorials/tracks/getting-a-token> .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;channels&quot;: [{object (SlackChannel)}],&quot;apiKeyConfig&quot;: {object (ApiKeyConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## SlackChannel

SlackChannel contains the Slack channel id and the time range to import.

Fields

`channelId` `string`

Required. The Slack channel id.

`startTime` ` string ( Timestamp  ` format)

Optional. The starting timestamp for messages to import.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Optional. The ending timestamp for messages to import.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
  &quot;channelId&quot;: string,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## JiraSource

The Jira source for the ImportRagFilesRequest.

Fields

`jiraQueries[]` ` object ( JiraQueries  ` )

Required. The Jira queries.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;jiraQueries&quot;: [{object (JiraQueries)}]}</code></pre></td>
</tr>
</tbody>
</table>

## JiraQueries

JiraQueries contains the Jira queries and corresponding authentication.

Fields

`projects[]` `string`

A list of Jira projects to import in their entirety.

`customQueries[]` `string`

A list of custom Jira queries to import. For information about JQL (Jira Query Language), see <https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/>

`email` `string`

Required. The Jira email address.

`serverUri` `string`

Required. The Jira server URI.

`apiKeyConfig` ` object ( ApiKeyConfig  ` )

Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Jira API key. See [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/) .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;projects&quot;: [string],&quot;customQueries&quot;: [string],&quot;email&quot;: string,&quot;serverUri&quot;: string,&quot;apiKeyConfig&quot;: {object (ApiKeyConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## SharePointSources

The SharePointSources to pass to ragFiles.import.

Fields

`sharePointSources[]` ` object ( SharePointSource  ` )

The SharePoint sources.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sharePointSources&quot;: [{object (SharePointSource)}]}</code></pre></td>
</tr>
</tbody>
</table>

## SharePointSource

An individual SharePointSource.

Fields

`clientId` `string`

The Application id for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All.

`clientSecret` ` object ( ApiKeyConfig  ` )

The application secret for the app registered in Azure.

`tenantId` `string`

Unique identifier of the Azure Active Directory Instance.

`sharepointSiteName` `string`

The name of the SharePoint site to download from. This can be the site name or the site id.

`fileId` `string`

Output only. The SharePoint file id. Output only.

`folder_source` `Union type`

The SharePoint folder source. If not provided, uses "root". `folder_source` can be only one of the following:

`sharepointFolderPath` `string`

The path of the SharePoint folder to download from.

`sharepointFolderId` `string`

The id of the SharePoint folder to download from.

`drive_source` `Union type`

The SharePoint drive source. `drive_source` can be only one of the following:

`driveName` `string`

The name of the drive to download from.

`driveId` `string`

The id of the drive to download from.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;clientId&quot;: string,&quot;clientSecret&quot;: {object (ApiKeyConfig)},&quot;tenantId&quot;: string,&quot;sharepointSiteName&quot;: string,&quot;fileId&quot;: string,// folder_source&quot;sharepointFolderPath&quot;: string,&quot;sharepointFolderId&quot;: string// Union type// drive_source&quot;driveName&quot;: string,&quot;driveId&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FileStatus

RagFile status.

Fields

`state` ` enum ( State  ` )

Output only. RagFile state.

`errorStatus` `string`

Output only. Only when the `state` field is ERROR.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;state&quot;: enum (State),&quot;errorStatus&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## State

RagFile state.

Enums

`STATE_UNSPECIFIED`

RagFile state is unspecified.

`ACTIVE`

RagFile resource has been created and indexed successfully.

`ERROR`

RagFile resource is in a problematic state. See `errorMessage` field for details.

## Methods

### `            delete           `

Deletes a RagFile.

### `            get           `

Gets a RagFile.

### `            import           `

Import files from Google Cloud Storage or Google Drive into a RagCorpus.

### `            list           `

Lists RagFiles in a RagCorpus.
