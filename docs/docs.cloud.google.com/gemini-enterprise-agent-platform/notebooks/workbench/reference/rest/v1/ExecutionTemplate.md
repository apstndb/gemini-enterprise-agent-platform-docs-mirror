---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate
title: ExecutionTemplate
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The description a notebook execution workload.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;scaleTier&quot;: enum (ScaleTier),&quot;masterType&quot;: string,&quot;acceleratorConfig&quot;: {object (SchedulerAcceleratorConfig)},&quot;labels&quot;: {string: string,...},&quot;inputNotebookFile&quot;: string,&quot;containerImageUri&quot;: string,&quot;outputNotebookFolder&quot;: string,&quot;paramsYamlFile&quot;: string,&quot;parameters&quot;: string,&quot;serviceAccount&quot;: string,&quot;jobType&quot;: enum (JobType),&quot;kernelSpec&quot;: string,&quot;tensorboard&quot;: string,// Union field job_parameters can be only one of the following:&quot;dataprocParameters&quot;: {object (DataprocParameters)},&quot;vertexAiParameters&quot;: {object (VertexAIParameters)}// End of list of possible types for union field job_parameters.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` scaleTier (deprecated)  `

` enum ( ScaleTier  ` )

> This item is deprecated\!

Required. Scale tier of the hardware used for notebook execution. DEPRECATED Will be discontinued. As right now only CUSTOM is supported.

`masterType`

`string`

Specifies the type of virtual machine to use for your training job's master worker. You must specify this field when `scaleTier` is set to `CUSTOM` .

You can use certain Compute Engine machine types directly in this field. The following types are supported:

  - `n1-standard-4`
  - `n1-standard-8`
  - `n1-standard-16`
  - `n1-standard-32`
  - `n1-standard-64`
  - `n1-standard-96`
  - `n1-highmem-2`
  - `n1-highmem-4`
  - `n1-highmem-8`
  - `n1-highmem-16`
  - `n1-highmem-32`
  - `n1-highmem-64`
  - `n1-highmem-96`
  - `n1-highcpu-16`
  - `n1-highcpu-32`
  - `n1-highcpu-64`
  - `n1-highcpu-96`

Alternatively, you can use the following legacy machine types:

  - `standard`
  - `large_model`
  - `complex_model_s`
  - `complex_model_m`
  - `complex_model_l`
  - `standard_gpu`
  - `complex_model_m_gpu`
  - `complex_model_l_gpu`
  - `standard_p100`
  - `complex_model_m_p100`
  - `standard_v100`
  - `large_model_v100`
  - `complex_model_m_v100`
  - `complex_model_l_v100`

Finally, if you want to use a TPU for training, specify `cloud_tpu` in this field. Learn more about the [special configuration options for training with TPU](https://cloud.google.com/ai-platform/training/docs/using-tpus#configuring_a_custom_tpu_machine) .

`acceleratorConfig`

` object ( SchedulerAcceleratorConfig  ` )

Configuration (count and accelerator type) for hardware running notebook execution.

`labels`

`map (key: string, value: string)`

Labels for execution. If execution is scheduled, a field included will be 'nbs-scheduled'. Otherwise, it is an immediate execution, and an included field will be 'nbs-immediate'. Use fields to efficiently index between various types of executions.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`inputNotebookFile`

`string`

Path to the notebook file to execute. Must be in a Google Cloud Storage bucket. Format: `gs://{bucket_name}/{folder}/{notebook_file_name}` Ex: `gs://notebook_user/scheduled_notebooks/sentiment_notebook.ipynb`

`containerImageUri`

`string`

Container Image URI to a DLVM Example: 'gcr.io/deeplearning-platform-release/base-cu100' More examples can be found at: <https://cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container>

`outputNotebookFolder`

`string`

Path to the notebook folder to write to. Must be in a Google Cloud Storage bucket path. Format: `gs://{bucket_name}/{folder}` Ex: `gs://notebook_user/scheduled_notebooks`

`paramsYamlFile`

`string`

Parameters to be overridden in the notebook during execution. Ref <https://papermill.readthedocs.io/en/latest/usage-parameterize.html> on how to specifying parameters in the input notebook and pass them here in an YAML file. Ex: `gs://notebook_user/scheduled_notebooks/sentiment_notebook_params.yaml`

`parameters`

`string`

Parameters used within the 'inputNotebookFile' notebook.

`serviceAccount`

`string`

The email address of a service account to use when running the execution. You must have the `iam.serviceAccounts.actAs` permission for the specified service account.

`jobType`

` enum ( JobType  ` )

The type of Job to be used on this execution.

`kernelSpec`

`string`

Name of the kernel spec to use. This must be specified if the kernel spec name on the execution target does not match the name in the input notebook file.

`tensorboard`

`string`

The name of a Agent Platform \[Tensorboard\] resource to which this execution will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

Union field `job_parameters` . Parameters for an execution type. NOTE: There are currently no extra parameters for VertexAI jobs. `job_parameters` can be only one of the following:

`dataprocParameters`

` object ( DataprocParameters  ` )

Parameters used in Dataproc JobType executions.

`vertexAiParameters`

` object ( VertexAIParameters  ` )

Parameters used in Agent Platform JobType executions.

## ScaleTier

Required. Specifies the machine types, the number of replicas for workers and parameter servers.

Enums

`SCALE_TIER_UNSPECIFIED`

Unspecified Scale Tier.

`BASIC`

A single worker instance. This tier is suitable for learning how to use Cloud ML, and for experimenting with new models using small datasets.

`STANDARD_1`

Many workers and a few parameter servers.

`PREMIUM_1`

A large number of workers with many parameter servers.

`BASIC_GPU`

A single worker instance with a K80 GPU.

`BASIC_TPU`

A single worker instance with a Cloud TPU.

`CUSTOM`

The CUSTOM tier is not a set tier, but rather enables you to use your own cluster specification. When you use this tier, set values to configure your processing cluster according to these guidelines:

  - You *must* set `ExecutionTemplate.masterType` to specify the type of machine to use for your master node. This is the only required setting.

## SchedulerAcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `coreCount` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus) to find a valid combination. TPUs are not supported.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (SchedulerAcceleratorType),&quot;coreCount&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

` enum ( SchedulerAcceleratorType  ` )

Type of this accelerator.

`coreCount`

`string ( int64 format)`

Count of cores of this accelerator.

## SchedulerAcceleratorType

Hardware accelerator types for AI Platform Training jobs.

Enums

`SCHEDULER_ACCELERATOR_TYPE_UNSPECIFIED`

Unspecified accelerator type. Default to no GPU.

`NVIDIA_TESLA_K80`

Nvidia Tesla K80 GPU.

`NVIDIA_TESLA_P100`

Nvidia Tesla P100 GPU.

`NVIDIA_TESLA_V100`

Nvidia Tesla V100 GPU.

`NVIDIA_TESLA_P4`

Nvidia Tesla P4 GPU.

`NVIDIA_TESLA_T4`

Nvidia Tesla T4 GPU.

`NVIDIA_TESLA_A100`

Nvidia Tesla A100 GPU.

`TPU_V2`

TPU v2.

`TPU_V3`

TPU v3.

## JobType

The backend used for this execution.

Enums

`JOB_TYPE_UNSPECIFIED`

No type specified.

`VERTEX_AI`

Custom Job in `aiplatform.googleapis.com` . Default value for an execution.

`DATAPROC`

Run execution on a cluster with Dataproc as a job. <https://cloud.google.com/dataproc/docs/reference/rest/v1/projects.regions.jobs>

## DataprocParameters

Parameters used in Dataproc JobType executions.

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
  &quot;cluster&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`cluster`

`string`

URI for cluster used to run Dataproc execution. Format: `projects/{PROJECT_ID}/regions/{REGION}/clusters/{CLUSTER_NAME}`

## VertexAIParameters

Parameters used in Agent Platform JobType executions.

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
  &quot;network&quot;: string,
  &quot;env&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`network`

`string`

The full name of the Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Job should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is a network name.

Private services access must already be configured for the network. If left unspecified, the job is not peered with any network.

`env`

`map (key: string, value: string)`

Environment variables. At most 100 environment variables can be specified and unique. Example: `GCP_BUCKET=gs://my-bucket/samples/`

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .
