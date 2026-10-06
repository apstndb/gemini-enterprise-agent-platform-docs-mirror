---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate
title: ExecutionTemplate
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The description a notebook execution workload.

**JSON representation**

```
{
  "scaleTier": enum (ScaleTier),
  "masterType": string,
  "acceleratorConfig": {
    object (SchedulerAcceleratorConfig)
  },
  "labels": {
    string: string,
    ...
  },
  "inputNotebookFile": string,
  "containerImageUri": string,
  "outputNotebookFolder": string,
  "paramsYamlFile": string,
  "parameters": string,
  "serviceAccount": string,
  "jobType": enum (JobType),
  "kernelSpec": string,
  "tensorboard": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "dataprocParameters": {
    object (DataprocParameters)
  },
  "vertexAiParameters": {
    object (VertexAIParameters)
  }
  // End of mutually exclusive fields.
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
<td><code>scaleTier </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate#ScaleTier"><code>ScaleTier</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Required. Scale tier of the hardware used for notebook execution. DEPRECATED Will be discontinued. As right now only CUSTOM is supported.</p></td>
</tr>
<tr class="even">
<td><code>masterType</code></td>
<td><p><code>string</code></p>
<p>Specifies the type of virtual machine to use for your training job's master worker. You must specify this field when <code>scaleTier</code> is set to <code>CUSTOM</code> .</p>
<p>You can use certain Compute Engine machine types directly in this field. The following types are supported:</p>
<ul>
<li><code>n1-standard-4</code></li>
<li><code>n1-standard-8</code></li>
<li><code>n1-standard-16</code></li>
<li><code>n1-standard-32</code></li>
<li><code>n1-standard-64</code></li>
<li><code>n1-standard-96</code></li>
<li><code>n1-highmem-2</code></li>
<li><code>n1-highmem-4</code></li>
<li><code>n1-highmem-8</code></li>
<li><code>n1-highmem-16</code></li>
<li><code>n1-highmem-32</code></li>
<li><code>n1-highmem-64</code></li>
<li><code>n1-highmem-96</code></li>
<li><code>n1-highcpu-16</code></li>
<li><code>n1-highcpu-32</code></li>
<li><code>n1-highcpu-64</code></li>
<li><code>n1-highcpu-96</code></li>
</ul>
<p>Alternatively, you can use the following legacy machine types:</p>
<ul>
<li><code>standard</code></li>
<li><code>large_model</code></li>
<li><code>complex_model_s</code></li>
<li><code>complex_model_m</code></li>
<li><code>complex_model_l</code></li>
<li><code>standard_gpu</code></li>
<li><code>complex_model_m_gpu</code></li>
<li><code>complex_model_l_gpu</code></li>
<li><code>standard_p100</code></li>
<li><code>complex_model_m_p100</code></li>
<li><code>standard_v100</code></li>
<li><code>large_model_v100</code></li>
<li><code>complex_model_m_v100</code></li>
<li><code>complex_model_l_v100</code></li>
</ul>
<p>Finally, if you want to use a TPU for training, specify <code>cloud_tpu</code> in this field. Learn more about the <a href="https://cloud.google.com/ai-platform/training/docs/using-tpus#configuring_a_custom_tpu_machine">special configuration options for training with TPU</a> .</p></td>
</tr>
<tr class="odd">
<td><code>acceleratorConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate#SchedulerAcceleratorConfig"><code>SchedulerAcceleratorConfig</code></a><code> )</code></p>
<p>Configuration (count and accelerator type) for hardware running notebook execution.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Labels for execution. If execution is scheduled, a field included will be 'nbs-scheduled'. Otherwise, it is an immediate execution, and an included field will be 'nbs-immediate'. Use fields to efficiently index between various types of executions.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>inputNotebookFile</code></td>
<td><p><code>string</code></p>
<p>Path to the notebook file to execute. Must be in a Google Cloud Storage bucket. Format: <code>gs://{bucket_name}/{folder}/{notebook_file_name}</code> Ex: <code>gs://notebook_user/scheduled_notebooks/sentiment_notebook.ipynb</code></p></td>
</tr>
<tr class="even">
<td><code>containerImageUri</code></td>
<td><p><code>string</code></p>
<p>Container Image URI to a DLVM Example: 'gcr.io/deeplearning-platform-release/base-cu100' More examples can be found at: <a href="https://cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container">https://cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container</a></p></td>
</tr>
<tr class="odd">
<td><code>outputNotebookFolder</code></td>
<td><p><code>string</code></p>
<p>Path to the notebook folder to write to. Must be in a Google Cloud Storage bucket path. Format: <code>gs://{bucket_name}/{folder}</code> Ex: <code>gs://notebook_user/scheduled_notebooks</code></p></td>
</tr>
<tr class="even">
<td><code>paramsYamlFile</code></td>
<td><p><code>string</code></p>
<p>Parameters to be overridden in the notebook during execution. Ref <a href="https://papermill.readthedocs.io/en/latest/usage-parameterize.html">https://papermill.readthedocs.io/en/latest/usage-parameterize.html</a> on how to specifying parameters in the input notebook and pass them here in an YAML file. Ex: <code>gs://notebook_user/scheduled_notebooks/sentiment_notebook_params.yaml</code></p></td>
</tr>
<tr class="odd">
<td><code>parameters</code></td>
<td><p><code>string</code></p>
<p>Parameters used within the 'inputNotebookFile' notebook.</p></td>
</tr>
<tr class="even">
<td><code>serviceAccount</code></td>
<td><p><code>string</code></p>
<p>The email address of a service account to use when running the execution. You must have the <code>iam.serviceAccounts.actAs</code> permission for the specified service account.</p></td>
</tr>
<tr class="odd">
<td><code>jobType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate#JobType"><code>JobType</code></a><code> )</code></p>
<p>The type of Job to be used on this execution.</p></td>
</tr>
<tr class="even">
<td><code>kernelSpec</code></td>
<td><p><code>string</code></p>
<p>Name of the kernel spec to use. This must be specified if the kernel spec name on the execution target does not match the name in the input notebook file.</p></td>
</tr>
<tr class="odd">
<td><code>tensorboard</code></td>
<td><p><code>string</code></p>
<p>The name of a Vertex AI [Tensorboard] resource to which this execution will upload Tensorboard logs. Format: <code>projects/{project}/locations/{location}/tensorboards/{tensorboard}</code></p></td>
</tr>
<tr class="even">
<td>Parameters for an execution type. NOTE: There are currently no extra parameters for VertexAI jobs. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>dataprocParameters</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate#DataprocParameters"><code>DataprocParameters</code></a><code> )</code></p>
<p>Parameters used in Dataproc JobType executions.</p></td>
</tr>
<tr class="even">
<td><code>vertexAiParameters</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate#VertexAIParameters"><code>VertexAIParameters</code></a><code> )</code></p>
<p>Parameters used in Vertex AI JobType executions.</p></td>
</tr>
<tr class="odd">
<td>End of mutually exclusive fields.</td>
<td></td>
</tr>
</tbody>
</table>

## ScaleTier

Required. Specifies the machine types, the number of replicas for workers and parameter servers.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>SCALE_TIER_UNSPECIFIED</code></td>
<td>Unspecified Scale Tier.</td>
</tr>
<tr class="even">
<td><code>BASIC</code></td>
<td>A single worker instance. This tier is suitable for learning how to use Cloud ML, and for experimenting with new models using small datasets.</td>
</tr>
<tr class="odd">
<td><code>STANDARD_1</code></td>
<td>Many workers and a few parameter servers.</td>
</tr>
<tr class="even">
<td><code>PREMIUM_1</code></td>
<td>A large number of workers with many parameter servers.</td>
</tr>
<tr class="odd">
<td><code>BASIC_GPU</code></td>
<td>A single worker instance with a K80 GPU.</td>
</tr>
<tr class="even">
<td><code>BASIC_TPU</code></td>
<td>A single worker instance with a Cloud TPU.</td>
</tr>
<tr class="odd">
<td><code>CUSTOM</code></td>
<td><p>The CUSTOM tier is not a set tier, but rather enables you to use your own cluster specification. When you use this tier, set values to configure your processing cluster according to these guidelines:</p>
<ul>
<li>You <em>must</em> set <code>ExecutionTemplate.masterType</code> to specify the type of machine to use for your master node. This is the only required setting.</li>
</ul></td>
</tr>
</tbody>
</table>

## SchedulerAcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `coreCount` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus) to find a valid combination. TPUs are not supported.

**JSON representation**

```
{
  "type": enum (SchedulerAcceleratorType),
  "coreCount": string
}
```

| Fields      |                                                                                                                                                                                                                      |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | `enum ( `[`SchedulerAcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate#SchedulerAcceleratorType)` )` Type of this accelerator. |
| `coreCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Count of cores of this accelerator.                                                                                           |

## SchedulerAcceleratorType

Hardware accelerator types for AI Platform Training jobs.

| Enums                                    |                                                  |
|------------------------------------------|--------------------------------------------------|
| `SCHEDULER_ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type. Default to no GPU. |
| `NVIDIA_TESLA_K80`                       | Nvidia Tesla K80 GPU.                            |
| `NVIDIA_TESLA_P100`                      | Nvidia Tesla P100 GPU.                           |
| `NVIDIA_TESLA_V100`                      | Nvidia Tesla V100 GPU.                           |
| `NVIDIA_TESLA_P4`                        | Nvidia Tesla P4 GPU.                             |
| `NVIDIA_TESLA_T4`                        | Nvidia Tesla T4 GPU.                             |
| `NVIDIA_TESLA_A100`                      | Nvidia Tesla A100 GPU.                           |
| `TPU_V2`                                 | TPU v2.                                          |
| `TPU_V3`                                 | TPU v3.                                          |

## JobType

The backend used for this execution.

| Enums                  |                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_TYPE_UNSPECIFIED` | No type specified.                                                                                                                  |
| `VERTEX_AI`            | Custom Job in `aiplatform.googleapis.com` . Default value for an execution.                                                         |
| `DATAPROC`             | Run execution on a cluster with Dataproc as a job. <https://cloud.google.com/dataproc/docs/reference/rest/v1/projects.regions.jobs> |

## DataprocParameters

Parameters used in Dataproc JobType executions.

**JSON representation**

```
{
  "cluster": string
}
```

| Fields    |                                                                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| `cluster` | `string` URI for cluster used to run Dataproc execution. Format: `projects/{PROJECT_ID}/regions/{REGION}/clusters/{CLUSTER_NAME}` |

## VertexAIParameters

Parameters used in Vertex AI JobType executions.

**JSON representation**

```
{
  "network": string,
  "env": {
    string: string,
    ...
  }
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `network` | `string` The full name of the Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Job should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is a network name. Private services access must already be configured for the network. If left unspecified, the job is not peered with any network. |
| `env`     | `map (key: string, value: string)` Environment variables. At most 100 environment variables can be specified and unique. Example: `GCP_BUCKET=gs://my-bucket/samples/` An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                        |
