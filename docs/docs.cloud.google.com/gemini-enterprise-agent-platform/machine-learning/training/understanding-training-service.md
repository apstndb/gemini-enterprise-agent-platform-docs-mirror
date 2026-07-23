---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/understanding-training-service
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/understanding-training-service
title: Understand the Gemini Enterprise Agent Platform serverless training service
description: Learn about the state of a training cluster through the lifecycle of a training job, and how Gemini Enterprise Agent Platform handles training errors.
data_source: docs.cloud.google.com
---

This page explains the state of a training cluster through the lifecycle of a training job, and how Agent Platform handles training errors. You can use this information to adapt your training code accordingly.

## Lifecycle of a training job

This section explains how Agent Platform handles worker VMs through the lifecycle of a training job.

### Queue a new job

When you create a `CustomJob` or `HyperparameterTuningJob` , the job might remain in the [`JOB_STATE_QUEUED` state](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState) for some time before Agent Platform runs it. This period is usually brief, but if your Google Cloud project does not have sufficient remaining [custom training quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#training) for your job, then Agent Platform keeps the job queued until you have sufficient quotas.

### Start workers in parallel

When a training job starts, Agent Platform schedules as many workers as possible in a short amount of time. As a result, workers may start up in parallel instead of sequentially. In order to reduce startup latency, Agent Platform starts running your code on each worker as soon as it becomes available. When all the workers are available, Agent Platform sets the job state to `JOB_STATE_RUNNING` .

In most cases, your machine learning framework automatically handles the workers starting in parallel. If you're using a distribution strategy in your training code, you may need to adjust it manually to handle workers starting in parallel. Learn more about distribution strategies in [TensorFlow](https://www.tensorflow.org/guide/distributed_training) and in [PyTorch](https://pytorch.org/tutorials/intermediate/dist_tuto.html) .

### Restart workers during the training job

During a training job, Agent Platform can restart your workers from any worker pool with the same hostname. This can occur for the following reasons:

  - *VM maintenance* : When the VM running a worker is subjected to VM maintenance, Agent Platform restarts the worker on another VM. Learn more about [live migration](https://docs.cloud.google.com/compute/docs/instances/live-migration) for VM maintenance.

  - *Non-zero exits* : If any worker exits with a non-zero exit code, Agent Platform restarts that worker immediately in the same VM.
    
      - If a worker fails due to [a common error](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/understanding-training-service#common-errors) , it is treated as a *permanent error* , and Agent Platform shuts down the entire job. If any containers restart before Agent Platform shuts down the entire job, these containers may produce logs in Cloud Logging.
      - If a worker fails due to a *non-permanent error* (any error not listed in the [common errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/understanding-training-service#common-errors) ), Agent Platform allows the restarted worker to continue running, with up to five restarts per worker. After five restarts, if a worker fails again, Agent Platform retries the entire job up to three times before failing the entire job.

To handle worker restarts in your training code, save checkpoints regularly during training so that you can restore from checkpoints when a worker restarts. If you expect training to take more than four hours, we recommend that you save a checkpoint at least once every four hours. Learn how to use training checkpoints in [TensorFlow](https://www.tensorflow.org/guide/checkpoint) and in [PyTorch](https://pytorch.org/tutorials/recipes/recipes/saving_and_loading_a_general_checkpoint.html) .

### Successfully completing a job

A training job completes successfully when its primary replica exits with exit code 0. At that point, Agent Platform shuts down all the other running workers.

## How Agent Platform handles training job errors

This section explains how Agent Platform handles common training job errors and internal errors.

About one minute after a job ends, Agent Platform sets the error code on the training job object, based on the exit code.

### Handle common errors

Agent Platform shuts down all workers if it encounters any of the following issues:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Error Type</strong></td>
<td><strong>Error Message/Log</strong></td>
<td><strong>Note</strong></td>
</tr>
<tr class="even">
<td>User code exception</td>
<td>The replica REPLICA_NAME exited with a non-zero status of EXIT_CODE . Termination reason: REASON .</td>
<td>If the job encountered exit codes that could be transient, Agent Platform tries to restart the job up to three times. The potentially transient error codes that prompt Agent Platform to retry the job include the following:
<ul>
<li><code dir="ltr" translate="no">SIGABRT</code>
<ul>
<li><code dir="ltr" translate="no">ExitCode 6</code></li>
<li><code dir="ltr" translate="no">ExitCode 134</code> (custom containers)</li>
</ul></li>
<li><code dir="ltr" translate="no">SIGSEGV</code>
<ul>
<li><code dir="ltr" translate="no">ExitCode 11</code></li>
<li><code dir="ltr" translate="no">ExitCode 139</code> (custom containers)</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Out-of-memory</td>
<td>The replica REPLICA_NAME ran out of memory and exited with a non-zero status of EXIT_CODE .</td>
<td>GKE reserves memory on Agent Platform nodes. On the smallest machine types (such as <code dir="ltr" translate="no">n1-standard-4</code> ), Agent Platform system agents can take up to 40% of total memory. For larger VMs, the overhead is relatively small. Compare <a href="https://docs.cloud.google.com/kubernetes-engine/docs/concepts/cluster-architecture#memory_cpu">allocatable memory for <code dir="ltr" translate="no">n1-standard</code> machine types</a> .</td>
</tr>
<tr class="even">
<td>Insufficient capacity in your region (Compute Engine stockout)</td>
<td>Resources are insufficient in region: REGION_NAME . Try a different region or use a different accelerator.</td>
<td>A <em>stockout</em> happens when Compute Engine is at capacity for your selected CPU or GPU in your region. It is unrelated to your project quota. When this happens, Agent Platform attempts to restart the job up to three times.<br />
<br />
For jobs running on A2 and A3 VMs, Dynamic Workload Scheduler lets you schedule jobs that run when the requested GPU resources become available, rather than failing with a stockout error. For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/schedule-jobs-dws">Schedule training jobs based on resource availability</a> .</td>
</tr>
</tbody>
</table>

### Handle internal errors

If Agent Platform has an internal error, it attempts to restart a job twice (three attempts in total). If the restart attempts also fail, Agent Platform returns an internal error with the message: `Internal error occurred for the current attempt` .
