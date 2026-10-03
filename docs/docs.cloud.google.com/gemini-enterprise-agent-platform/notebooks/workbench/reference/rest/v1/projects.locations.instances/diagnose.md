---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/diagnose
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/diagnose
title: 'Method: projects.locations.instances.diagnose'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{name}:diagnose`

### Path parameters

| Parameters |                                                                                               |
|------------|-----------------------------------------------------------------------------------------------|
| `name`     | `string` Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}` |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "diagnosticConfig": {
    object (DiagnosticConfig)
  },
  "timeoutMinutes": integer
}
```

| Fields             |                                                                                                                                                                                                                                                                   |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diagnosticConfig` | `object ( `[`DiagnosticConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/diagnose#DiagnosticConfig)` )` Required. Defines flags that are used to run the diagnostic tool |
| `timeoutMinutes`   | `integer` Optional. Maximum amount of time in minutes before the operation times out.                                                                                                                                                                             |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## DiagnosticConfig

Defines flags that are used to run the diagnostic tool

**JSON representation**

```
{
  "gcsBucket": string,
  "relativePath": string,
  "repairFlagEnabled": boolean,
  "packetCaptureFlagEnabled": boolean,
  "copyHomeFilesFlagEnabled": boolean
}
```

| Fields                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gcsBucket`                | `string` Required. User Cloud Storage bucket location (REQUIRED). Must be formatted with path prefix ( `gs://$GCS_BUCKET` ). Permissions: User Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account attached to VM. Google Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account or user credentials attached to VM depending on authentication mode. Cloud Storage bucket Log file will be written to `gs://$GCS_BUCKET/$RELATIVE_PATH/$VM_DATE_$TIME.tar.gz` |
| `relativePath`             | `string` Optional. Defines the relative storage path in the Cloud Storage bucket where the diagnostic logs will be written: Default path will be the root directory of the Cloud Storage bucket ( `gs://$GCS_BUCKET/$DATE_$TIME.tar.gz` ) Example of full path where Log file will be written: `gs://$GCS_BUCKET/$RELATIVE_PATH/`                                                                                                                                                                                                           |
| `repairFlagEnabled`        | `boolean` Optional. Enables flag to repair service for instance                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `packetCaptureFlagEnabled` | `boolean` Optional. Enables flag to capture packets from the instance for 30 seconds                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `copyHomeFilesFlagEnabled` | `boolean` Optional. Enables flag to copy all `/home/jupyter` folder contents                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
