---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list
title: 'Method: notebookRuntimes.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookRuntimes.list

Lists NotebookRuntimes in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /notebookRuntimes`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the NotebookRuntimes. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported.

- `notebookRuntime` supports = and !=. `notebookRuntime` represents the NotebookRuntime id, i.e. the last segment of the NotebookRuntime's [`resource name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes#NotebookRuntime.FIELDS.name) .
- `displayName` supports = and != and regex.
- `notebookRuntimeTemplate` supports = and !=. `notebookRuntimeTemplate` represents the NotebookRuntimeTemplate id, i.e. the last segment of the NotebookRuntimeTemplate's [`resource name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimeTemplates#NotebookRuntimeTemplate.FIELDS.name) .
- `healthState` supports = and !=. healthState enum: \[HEALTHY, UNHEALTHY, HEALTH_STATE_UNSPECIFIED\].
- `runtimeState` supports = and !=. runtimeState enum: \[RUNTIME_STATE_UNSPECIFIED, RUNNING, BEING_STARTED, BEING_STOPPED, STOPPED, BEING_UPGRADED, ERROR, INVALID\].
- `runtimeUser` supports = and !=.
- API version is UI only: `uiState` supports = and !=. uiState enum: \[UI_RESOURCE_STATE_UNSPECIFIED, UI_RESOURCE_STATE_BEING_CREATED, UI_RESOURCE_STATE_ACTIVE, UI_RESOURCE_STATE_BEING_DELETED, UI_RESOURCE_STATE_CREATION_FAILED\].
- `notebookRuntimeType` supports = and !=. notebookRuntimeType enum: \[USER_DEFINED, ONE_CLICK\].
- `machineType` supports = and !=.
- `acceleratorType` supports = and !=.

Some examples:

- `notebookRuntime="notebookRuntime123"`
- `displayName="myDisplayName"` and `displayName=~"myDisplayNameRegex"`
- `notebookRuntimeTemplate="notebookRuntimeTemplate321"`
- `healthState=HEALTHY`
- `runtimeState=RUNNING`
- `runtimeUser="test@google.com"`
- `uiState=UI_RESOURCE_STATE_BEING_DELETED`
- `notebookRuntimeType=USER_DEFINED`
- `machineType=e2-standard-4`
- `acceleratorType=NVIDIA_TESLA_T4`

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via [`ListNotebookRuntimesResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list#body.ListNotebookRuntimesResponse.FIELDS.next_page_token) of the previous [`NotebookService.ListNotebookRuntimes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list#google.cloud.aiplatform.v1.NotebookService.ListNotebookRuntimes) call.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Optional. Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

- `displayName`
- `createTime`
- `updateTime`

Example: `displayName, createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for [`NotebookService.ListNotebookRuntimes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list#google.cloud.aiplatform.v1.NotebookService.ListNotebookRuntimes) .

If successful, the response body contains data with the following structure:

Fields

`notebookRuntimes[]` `object ( `[`NotebookRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes#NotebookRuntime)` )`

List of NotebookRuntimes in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to [`ListNotebookRuntimesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "notebookRuntimes": [
    {
      object (NotebookRuntime)
    }
  ],
  "nextPageToken": string
}
```
