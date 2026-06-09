---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/visualizing-jobs-with-tensorboard
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/visualizing-jobs-with-tensorboard
title: Visualizing jobs with Vertex AI TensorBoard
description: Visualize Managed Training logs in real-time. Configure your workload to stream logs from Cloud Storage to Agent Platform TensorBoard for analysis.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform Managed Training, contact your sales representative for access.

With Managed Training, you can visualize your training logs in near real-time using Vertex AI TensorBoard. Simply configure your workload to save logs to a Cloud Storage bucket, and they will be automatically streamed to the TensorBoard interface for analysis.

### Prerequisites

Before you begin, ensure you have the following:

  - A running Managed Training cluster.
  - A Cloud Storage bucket to store your TensorBoard logs. This bucket must be in the same region as your TensorBoard instance. For setup instructions, see [Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .
  - A Vertex AI TensorBoard instance. For creation instructions, see Create a [Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#create-tensorboard-instance) instance.
  - The correct IAM permissions. To allow Cloud Storage FUSE to read from and write to the storage bucket, the service account used by your cluster's VMs requires the Storage Object User ( `roles/storage.objectUser` ) role.

### Enabling Tensorboard upload

To configure the TensorBoard integration for your job, pass the following arguments using the `--extra` flag in your Slurm job submission:

  - `tensorboard_base_output_dir` : Specifies the Cloud Storage path to upload logs to. For example, `gs://my-bucket/my-logs` .

  - `tensorboard_url` : Specifies the Vertex AI TensorBoard instance, experiment, or run URL. If only an instance is provided, a new experiment and run are created. If omitted, the default TensorBoard instance for the project is used. For example, `projects/123/locations/us-central1/tensorboards/456` .

#### Example

    # Using specific tensorboard instance
    sbatch --extra="tensorboard_base_output_dir=<your-cloud-storage-dir>,tensorboard_url=projects/<project-id>/locations/<location>/tensorboards/<tensorboard-instance-id>" your_script.sbatch

### Writing logs from your training job

Within your training script, access the `AIP_TENSORBOARD_LOG_DIR` environment variable. This variable provides the unique Cloud Storage path where your script should write its TensorBoard logs.

The path follows this structure:

    gs://<your-cloud-storage-path>/<cluster-id>-<cluster-uuid>/tensorboard/job-<job-id>/

The following example shows a complete workflow with two key components: the Slurm submission script that configures the job, and the Python training script that reads the environment variable to write its logs.

Slurm Job Script (simple\_job.sbatch):

    #!/bin/bash
    #SBATCH --job-name=tensorboard-simple-test
    #SBATCH --output=tensorboard-simple-test-%j.out

    # Activate your Python virtual environment if needed
    # source /path/to/your/venv/bin/activate
    python3 simple_logger.py

Python Script (simple\_logger.py):

    import tensorflow as tf
    import os
    
    # Get the log directory from the environment variable
    log_dir = os.environ.get("AIP_TENSORBOARD_LOG_DIR")
    
    print(f"Writing TensorBoard logs to: {log_dir}")
    writer = tf.summary.create_file_writer(log_dir)
    
    with writer.as_default():
        for step in range(10):
            # Simulate some metrics
            loss = 1.0 - (step * 0.1)
            accuracy = 0.6 + (step * 0.04)
    
            # Log the metrics
            tf.summary.scalar('loss', loss, step=step)
            tf.summary.scalar('accuracy', accuracy, step=step)
            writer.flush()
            print(f"Step {step}: loss={loss:.4f}, accuracy={accuracy:.4f}")
    
    writer.close()
    print(f"--- Finished writing metrics to {log_dir} ---")

#### Real-time Log Synchronization

To visualize metrics from a running job, you must periodically close and recreate the summary writer in your training code. This is necessary because `gcsfuse` only syncs log files to Cloud Storage once they are closed. This "flushing" technique ensures that intermediate results are visible in the TensorBoard console before the job completes.

### Viewing Vertex AI TensorBoard

Once your job is submitted, you can monitor its progress by going to the to the [Vertex AI Experiments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-view#console_name) page in the Google Cloud console.

## What's next

Analyze training metrics, visualize model graphs, and profile performance in Vertex AI TensorBoard to debug issues, optimize your model, and prepare the model for integration into a complete MLOps workflow.

  - Deploy your model for inference: Deploy your trained model to a Gemini Enterprise Agent Platform endpoint to serve online inference requests.
      - [Deploy a model to an endpoint](https://docs.cloud.google.com/vertex-ai/docs/general/deployment)
  - Manage your model's lifecycle: Use the Gemini Enterprise Agent Platform Model Registry to version, track, and compare your trained models, which helps maintain model governance and reproducibility.
      - [Introduction to Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction)
  - Set up model monitoring: After deployment, monitor your model for performance drift and data anomalies to help maintain the model's effectiveness in production.
      - [Introduction to Gemini Enterprise Agent Platform Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview)
  - Optimize costs and manage your cluster: Regularly review your cluster utilization and manage its lifecycle (for example, deleting the cluster when not in use) to optimize costs for reserved hardware.
      - [Learn how to manage your training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster)
