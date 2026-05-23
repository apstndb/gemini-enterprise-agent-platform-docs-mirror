---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-retries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-retries
title: Configure retries for a pipeline task
description: Learn how to configure retry policies in Gemini Enterprise Agent Platform Pipelines to handle pipeline task failures in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

You can specify whether a pipeline task must be rerun if it fails, by configuring the retries for that task. You can set the number of attempts to rerun the task on failure and the delay between subsequent retries.

Use the following code sample to configure the failure policy of a pipeline task named `train_op` by using the [`set_retry`](https://kubeflow-pipelines.readthedocs.io/page/source/dsl.html#kfp.dsl.PipelineTask.set_retry) method in the Kubeflow Pipelines SDK:

    from kfp import dsl
    
    @dsl.pipeline(name='custom-container-pipeline')
    def pipeline():
      generate = generate_op()
      train = (
        train_op(
          training_data=generate.outputs['training_data'],
          test_data=generate.outputs['test_data'],
          config_file=generate.outputs['config_file'])
        .set_retry(
          num_retries=NUMBER_OF_RETRIES,
          backoff_duration='BACKOFF_DURATION',
          backoff_factor=BACKOFF_FACTOR,
          backoff_maxk_duration='BACKOFF_MAX_DURATION'
        )

Replace the following:

  - NUMBER\_OF\_RETRIES : The number of times to retry the task upon failure.

  - BACKOFF\_DURATION : Optional. The duration of time wait after the task fails before retrying. If you don't set this parameter, the duration is set to `0s` , by default.

  - BACKOFF\_FACTOR : Optional. The factor by which the backoff duration is multiplied for each subsequent retry. If you don't set this parameter, the backoff factor is set to `2.0` , by default.

  - BACKOFF\_MAX\_DURATION : Optional. The maximum backoff duration between subsequent retries. If you don't set this parameter, the maximum duration is set to `3600s` , by default.

> **Caution:** You can't pass output parameters from other pipeline tasks or pipeline input parameters as parameter values for the set\_retry method. These values must be available when you compile the pipeline.
