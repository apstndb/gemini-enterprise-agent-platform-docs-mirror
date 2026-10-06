---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/report
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/report
title: 'Method: projects.locations.instances.report'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Allows notebook instances to report their latest instance information to the Notebooks API server. The server will merge the reported information to the instance metadata store. Do not use this method directly.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{name}:report`

### Path parameters

| Parameters |                                                                                               |
|------------|-----------------------------------------------------------------------------------------------|
| `name`     | `string` Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}` |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "vmId": string,
  "metadata": {
    string: string,
    ...
  }
}
```

| Fields     |                                                                                                                                                                                                                                                     |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `vmId`     | `string` Required. The VM hardware token for authenticating the VM. <https://cloud.google.com/compute/docs/instances/verifying-instance-identity>                                                                                                   |
| `metadata` | `map (key: string, value: string)` The metadata reported to Notebooks API. This will be merged to the instance metadata store An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
