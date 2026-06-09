---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/machine-types
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/machine-types
title: Specify the machine configuration for a pipeline step
description: Learn how to specify the machine configuration for a pipeline step.
data_source: docs.cloud.google.com
---

Kubeflow pipeline components are factory functions that create pipeline steps. Each component describes the inputs, outputs, and implementation of the component. For example, `train_op` is a component in the following code sample.

For example, a training component could take a CSV file as an input and use it to train a model. By setting the machine type parameters on the pipeline step, you can manage the requirements of each step in your pipeline. If you have two training steps and one step trains on a huge data file and the second step trains on a small data file, you can allocate more memory and CPU to the first task, and fewer resources to the second task.

By default, the component will run on as a Gemini Enterprise Agent Platform [`CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs) using an **e2-standard-4** machine, with 4 core CPUs and 16GB memory. For more information about selecting one of the Google Cloud-specific machine resources listed in [Machine types](https://docs.cloud.google.com/vertex-ai/docs/training/configure-compute#machine-types) , see [Request Google Cloud machine resources with Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/request-gcp-machine-resources) .

The following sample shows you how to set CPU, memory, and GPU configuration settings for a step:

> **Note:** If you want to specify the disk space in the machine configuration, you must [create a custom training job from a component by requesting Google Cloud machine resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/request-gcp-machine-resources#create-customtrainingjob-from-component) instead.

    from kfp import dsl
    
    @dsl.pipeline(name='custom-container-pipeline')
    def pipeline():
      generate = generate_op()
      train = (
        train_op(
          training_data=generate.outputs['training_data'],
          test_data=generate.outputs['test_data'],
          config_file=generate.outputs['config_file'])
        .set_cpu_limit('CPU_LIMIT')
        .set_memory_limit('MEMORY_LIMIT')
        .add_node_selector_constraint(SELECTOR_CONSTRAINT)
        .set_accelerator_type(ACCELERATOR_TYPE)
        .set_accelerator_limit(ACCELERATOR_LIMIT))

Replace the following:

  - CPU\_LIMIT : The maximum CPU limit for this operator. This string value can be a number (integer value for number of CPUs), or a number followed by "m", which means 1/1000. You can specify at most 96 CPUs.

  - MEMORY\_LIMIT : The maximum memory limit for this operator. This string value can be a number, or a number followed by "K" (kilobyte), "M" (megabyte), or "G" (gigabyte). At most 624GB is supported.
    
    > **Note:** Agent Platform Pipelines does not support calling [`set_memory_request`](https://kubeflow-pipelines.readthedocs.io/page/source/dsl.html#kfp.dsl.PipelineTask.set_memory_request) on an operator ; you must use [`set_memory_limit`](https://kubeflow-pipelines.readthedocs.io/page/source/dsl.html#kfp.dsl.PipelineTask.set_memory_request) to request a specific memory amount.

  - SELECTOR\_CONSTRAINT : Each constraint is a key-value pair label. For the container to be eligible to run on a node, the node must have each constraint as a label. For example: `'cloud.google.com/gke-accelerator', 'NVIDIA_TESLA_T4'`
    
    The following constraints are available:
    
      - `NVIDIA_GB200` <sup>+</sup> (includes [GPUDirect-RDMA](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-rdma) )
      - `NVIDIA_B200` <sup>\*</sup> (includes [GPUDirect-RDMA](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-rdma) )
      - `NVIDIA_H100_MEGA_80GB` <sup>\*</sup> (includes [GPUDirect-TCPXO](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-tcpxo) )
      - `NVIDIA_H100_80GB`
      - `NVIDIA_H200_141GB` <sup>\*</sup> (includes [GPUDirect-RDMA](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-rdma) )
      - `NVIDIA_A100_80GB`
      - `NVIDIA_TESLA_A100` (NVIDIA A100 40GB)
      - `NVIDIA_TESLA_P4`
      - `NVIDIA_TESLA_P100`
      - `NVIDIA_TESLA_T4`
      - `NVIDIA_TESLA_V100`
      - `NVIDIA_L4`
      - `NVIDIA_RTX_PRO_6000`
    
    <!-- end list -->
    
      - `TPU_V2`
      - `TPU_V3`

  - ACCELERATOR\_TYPE : The type of accelerator. For more information about the available GPUs and how to configure them, see [GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) . For more information about the available TPU types and how to configure them, see [TPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#tpu) . For more information, see the [`accelerator_type` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.accelerator_type) .

  - ACCELERATOR\_LIMIT : The accelerator (GPU or TPU) limit for the operator. You can specify a positive integer. For more information about the available GPUs and how to configure them, see [GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) . For more information about the available TPUs and how to configure them, see [TPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#tpu) .
    
    > **Note:** Some accelerators are available only in specific locations. For more information, see [Using accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

`CustomJob` supports specific machine types that limit you to a maximum of 96 CPUs and 624GB of memory. Based on the CPU, memory, and accelerator configuration that you specify, Agent Platform Pipelines automatically selects the closest match from the supported machine types.
