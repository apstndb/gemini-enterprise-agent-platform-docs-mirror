---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-upload-existing-logs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-upload-existing-logs
title: Upload logs to Vertex AI TensorBoard
description: This page shows how to upload existing logs to your Vertex AI TensorBoard instance that were created by training locally, training outside of Gemini Enterprise Agent Platform, created by a colleague, are example logs, or were created using a different Vertex AI TensorBoard instance.
data_source: docs.cloud.google.com
---

You can upload existing logs to your Vertex AI TensorBoard instance that were created by training locally, training outside of Gemini Enterprise Agent Platform, created by a colleague, are example logs, or were created using a different Vertex AI TensorBoard instance. Logs can be shared among multiple Vertex AI TensorBoard instances.

Vertex AI TensorBoard offers Google Cloud CLI and Agent Platform SDK for Python for uploading TensorBoard logs. You can upload logs from any environment that can connect to Google Cloud.

### Agent Platform SDK for Python

### Continuous monitoring

For continuous monitoring call `aiplatform.start_upload_tb_log` at the beginning of the training. The SDK opens a new thread for uploading. This thread monitors for new data in the directory, and uploads it to your Vertex AI TensorBoard experiment. When training completes, call `end_upload_tb_log` to end the uploader thread.

Note that after calling `start_upload_tb_log()` your thread will kept alive even if an exception is thrown. To ensure the thread gets shut down, put any code after `start_upload_tb_log()` and before `end_upload_tb_log()` in a `try` statement, and call `end_upload_tb_log()` in `finally` .

### Python

    from typing import Optional
    
    from google.cloud import aiplatform
    
    
    def upload_tensorboard_log_continuously_sample(
        tensorboard_experiment_name: str,
        logdir: str,
        tensorboard_id: str,
        project: str,
        location: str,
        experiment_display_name: Optional[str] = None,
        run_name_prefix: Optional[str] = None,
        description: Optional[str] = None,
    ) -> None:
    
        aiplatform.init(project=project, location=location)
    
        # Continuous monitoring
        aiplatform.start_upload_tb_log(
            tensorboard_id=tensorboard_id,
            tensorboard_experiment_name=tensorboard_experiment_name,
            logdir=logdir,
            experiment_display_name=experiment_display_name,
            run_name_prefix=run_name_prefix,
            description=description,
        )
    
        try:
            print("Insert your code here")
        finally:
            aiplatform.end_upload_tb_log()

  - `tensorboard_experiment_name` : The name of the TensorBoard experiment to upload to.
  - `logdir` : The directory location to check for TensorBoard logs.
  - `tensorboard_id` : The [TensorBoard instance ID](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-setup#tensorboard_id) . If not set, the `tensorboard_id` in `aiplatform.init` is used.
  - `project` : . You can find you Project ID in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : The location where your TensorBoard instance is located.
  - `experiment_display_name` : The display name of the experiment.
  - `run_name_prefix` : If present, all runs created by this invocation will have their name prefixed by this value.
  - `description` : A string description to assign to the experiment.

### One time logging

### Upload TensorBoard logs

Call `aiplatform.upload_tb_log` to perform a one-time upload of TensorBoard logs. This uploads existing data in the logdir and then returns immediately.

### Python

    from typing import Optional
    
    from google.cloud import aiplatform
    
    
    def upload_tensorboard_log_one_time_sample(
        tensorboard_experiment_name: str,
        logdir: str,
        tensorboard_id: str,
        project: str,
        location: str,
        experiment_display_name: Optional[str] = None,
        run_name_prefix: Optional[str] = None,
        description: Optional[str] = None,
        verbosity: Optional[int] = 1,
    ) -> None:
    
        aiplatform.init(project=project, location=location)
    
        # one time upload
        aiplatform.upload_tb_log(
            tensorboard_id=tensorboard_id,
            tensorboard_experiment_name=tensorboard_experiment_name,
            logdir=logdir,
            experiment_display_name=experiment_display_name,
            run_name_prefix=run_name_prefix,
            description=description,
        )

  - `tensorboard_experiment_name` : The name of the TensorBoard experiment.
  - `logdir` : The directory location to check for TensorBoard logs.
  - `tensorboard_id` : The [TensorBoard instance ID](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-setup#tensorboard_id) . If not set, the `tensorboard_id` in `aiplatform.init` is used.
  - `project` : . You can find these Project IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : The location where your TensorBoard instance is located.
  - `experiment_display_name` : The display name of the experiment.
  - `run_name_prefix` : If present, all runs created by this invocation will have their name prefixed by this value.
  - `description` : A string description to assign to the experiment.
  - `verbosity` : Level of statistics verbosity, an integer. Supported values: 0 - No upload statistics are printed. 1 - Print upload statistics while uploading data (default).

### Upload profile logs

Call `aiplatform.upload_tb_log` to upload TensorBoard profile logs to an experiment.

### Python

    from typing import FrozenSet
    
    from google.cloud import aiplatform
    
    
    def upload_tensorboard_profile_logs_to_experiment_sample(
        experiment_name: str,
        logdir: str,
        project: str,
        location: str,
        run_name_prefix: str,
        allowed_plugins: FrozenSet[str] = ["profile"],
    ) -> None:
    
        aiplatform.init(project=project, location=location, experiment=experiment_name)
    
        # one time upload
        aiplatform.upload_tb_log(
            tensorboard_experiment_name=experiment_name,
            logdir=logdir,
            run_name_prefix=run_name_prefix,
            allowed_plugins=allowed_plugins,
        )

  - `experiment_name` : The name of the TensorBoard experiment.
  - `logdir` : The directory location to check for TensorBoard logs.
  - `project` : . You can find these Project IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : The location where your TensorBoard instance is located.
  - `run_name_prefix` : For profile data, this is the run prefix. The directory format within LOG\_DIR should match the following:
      - `/RUN_NAME_PREFIX/plugins/profile/YYYY_MM_DD_HH_SS/`
  - `allowed_plugins` : A list of additional plugins to allow. For uploading profile data, this should include `"profile"`

### CLI

(Optional) Create a dedicated virtual environment to install the Vertex AI TensorBoard uploader Python CLI.

    python3 -m venv PATH/TO/VIRTUAL/ENVIRONMENT
    source PATH/TO/VIRTUAL/ENVIRONMENT/bin/activate

  - `  PATH/TO/VIRTUAL/ENVIRONMENT  ` : your dedicated virtual environment.

Install the Vertex AI TensorBoard package through Agent Platform SDK.

    pip install -U pip
    pip install google-cloud-aiplatform[tensorboard]

Upload TensorBoard logs

1.  Time Series and Blob Data
    
        tb-gcp-uploader--tensorboard_resource_name \
        TENSORBOARD_RESOURCE_NAME \
        --logdir=LOG_DIR \
        --experiment_name=TB_EXPERIMENT_NAME--one_shot=True

2.  Profile Data
    
        tb-gcp-uploader \
        --tensorboard_resource_nameTENSORBOARD_RESOURCE_NAME \
        --logdir=LOG_DIR--experiment_name=TB_EXPERIMENT_NAME \
        --allowed_plugins="profile"--run_name_prefix=RUN_NAME_PREFIX \
        --one_shot=True

<!-- end list -->

  - `  TENSORBOARD_RESOURCE_NAME  ` : The [TensorBoard Resource name](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-setup#tensorboard_resource_name) used to fully identify the Vertex AI TensorBoard instance.
  - `  LOG_DIR  ` : The location of the event logs that resides either in the local file system or Cloud Storage
  - `  TB_EXPERIMENT_NAME  ` : The name of the TensorBoard experiment, for example `test-experiment` .
  - `  RUN_NAME_PREFIX  ` : For profile data, this is the run prefix. The directory format within `  LOG_DIR  ` should match the following:
      - `/RUN_NAME_PREFIX/plugins/profile/YYYY_MM_DD_HH_SS/`

The uploader CLI by default runs indefinitely, monitoring changes in the `LOG_DIR` , and uploads newly added logs. `--one_shot=True` disables the behavior. Run `tb-gcp-uploader --help` for more information.
