---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs
title: 'REST Resource: projects.locations.notebookExecutionJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NotebookExecutionJob

NotebookExecutionJob represents an instance of a notebook execution.

Fields

`name` `string`

Output only. The resource name of this NotebookExecutionJob. Format: `projects/{projectId}/locations/{location}/notebookExecutionJobs/{job_id}`

`displayName` `string`

The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`executionTimeout` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Max running time of the execution job in seconds (default 86400s / 24 hrs).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`scheduleResourceName` `string`

The Schedule resource name if this job is triggered by one. Format: `projects/{projectId}/locations/{location}/schedules/{scheduleId}`

`jobState` `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/JobState)` )`

Output only. The state of the NotebookExecutionJob.

`status` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookExecutionJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookExecutionJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize NotebookExecutionJobs.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`kernelName` `string`

The name of the kernel to use during notebook execution. If unset, the default kernel is used.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the [`NotebookRuntimeTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates#NotebookRuntimeTemplate) has an encryption spec.

`notebook_source` `Union type`

The input notebook. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`dataformRepositorySource` `object ( `[`DataformRepositorySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs#NotebookExecutionJob.DataformRepositorySource)` )`

The Dataform Repository pointing to a single file notebook repository.

`gcsNotebookSource` `object ( `[`GcsNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs#NotebookExecutionJob.GcsNotebookSource)` )`

The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebookFile.ipynb`

`directNotebookSource` `object ( `[`DirectNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs#NotebookExecutionJob.DirectNotebookSource)` )`

The contents of an input notebook file.

End of mutually exclusive fields.

`environment_spec` `Union type`

The compute config to use for an execution job. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`notebookRuntimeTemplateResourceName` `string`

The NotebookRuntimeTemplate to source compute configuration from.

`customEnvironmentSpec` `object ( `[`CustomEnvironmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs#NotebookExecutionJob.CustomEnvironmentSpec)` )`

The custom compute configuration for an execution job.

End of mutually exclusive fields.

`execution_sink` `Union type`

The location to store the notebook execution result. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsOutputUri` `string`

The Cloud Storage location to upload the result to. Format: `gs://bucket-name`

End of mutually exclusive fields.

`execution_identity` `Union type`

The identity to run the execution as. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`executionUser` `string`

The user email to run the execution as. Only supported by Colab runtimes.

`serviceAccount` `string`

The service account to run the execution as.

End of mutually exclusive fields.

`runtime_environment` `Union type`

Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`workbenchRuntime` `object ( `[`WorkbenchRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs#NotebookExecutionJob.WorkbenchRuntime)` )`

The Workbench runtime configuration to use for the notebook execution.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "executionTimeout": string,
  "scheduleResourceName": string,
  "jobState": enum (JobState),
  "status": {
    object (Status)
  },
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "kernelName": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },

  // notebook_source
  "dataformRepositorySource": {
    object (DataformRepositorySource)
  },
  "gcsNotebookSource": {
    object (GcsNotebookSource)
  },
  "directNotebookSource": {
    object (DirectNotebookSource)
  }
  // Union type

  // environment_spec
  "notebookRuntimeTemplateResourceName": string,
  "customEnvironmentSpec": {
    object (CustomEnvironmentSpec)
  }
  // Union type

  // execution_sink
  "gcsOutputUri": string
  // Union type

  // execution_identity
  "executionUser": string,
  "serviceAccount": string
  // Union type

  // runtime_environment
  "workbenchRuntime": {
    object (WorkbenchRuntime)
  }
  // Union type
}
```

### DataformRepositorySource

The Dataform Repository containing the input notebook.

Fields

`dataformRepositoryResourceName` `string`

The resource name of the Dataform Repository. Format: `projects/{projectId}/locations/{location}/repositories/{repository_id}`

`commitSha` `string`

The commit SHA to read repository with. If unset, the file will be read at HEAD.

**JSON representation**

```
{
  "dataformRepositoryResourceName": string,
  "commitSha": string
}
```

### GcsNotebookSource

The Cloud Storage uri for the input notebook.

Fields

`uri` `string`

The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebookFile.ipynb`

`generation` `string`

The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> .

**JSON representation**

```
{
  "uri": string,
  "generation": string
}
```

### DirectNotebookSource

The content of the input notebook in ipynb format.

Fields

`content` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The base64-encoded contents of the input notebook file.

A base64-encoded string.

**JSON representation**

```
{
  "content": string
}
```

### CustomEnvironmentSpec

Compute configuration to use for an execution job.

Fields

`machineSpec` `object ( ``MachineSpec`` )`

The specification of a single machine for the execution job.

`persistentDiskSpec` `object ( `[`PersistentDiskSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PersistentDiskSpec)` )`

The specification of a persistent disk to attach for the execution job.

`networkSpec` `object ( `[`NetworkSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NetworkSpec)` )`

The network configuration to use for the execution job.

**JSON representation**

```
{
  "machineSpec": {
    object (MachineSpec)
  },
  "persistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  }
}
```

### WorkbenchRuntime

This type has no fields.

Configuration for a Workbench Instances-based environment.

| Methods                                                                                                                                           |                                            |
|---------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs/create) | Creates a NotebookExecutionJob.            |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs/delete) | Deletes a NotebookExecutionJob.            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs/get)       | Gets a NotebookExecutionJob.               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs/list)     | Lists NotebookExecutionJobs in a Location. |
