---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/request-gcp-machine-resources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/request-gcp-machine-resources
title: Learn how to request Google Cloud machine resources in Gemini Enterprise Agent Platform Pipelines
description: Request and allocate specific {{dynamic_data.site_values.cloud_name}} machine resources for your Agent Platform Pipeline components.
data_source: docs.cloud.google.com
---

You can run your Python component on Gemini Enterprise Agent Platform Pipelines by using Google Cloud-specific machine resources offered by Gemini Enterprise Agent Platform custom training.

You can use the [`create_custom_training_job_from_component`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component) method from the [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/gcpc-list) to transform a Python component into a Gemini Enterprise Agent Platform custom training job. [Learn how to create a custom job](https://docs.cloud.google.com/vertex-ai/docs/training/create-custom-job) .

## Create a custom training job from a component using Gemini Enterprise Agent Platform Pipelines

The following sample shows how to use the [`create_custom_training_job_from_component`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component) method to transform a Python component into a custom training job with user-defined Google Cloud machine resources, and then run the compiled pipeline on Gemini Enterprise Agent Platform Pipelines:

    import kfp
    from kfp import dsl
    from google_cloud_pipeline_components.v1.custom_job import create_custom_training_job_from_component
    
    # Create a Python component
    @dsl.component
    def my_python_component():
      import time
      time.sleep(1)
    
    # Convert the above component into a custom training job
    custom_training_job = create_custom_training_job_from_component(
        my_python_component,
        display_name = 'DISPLAY_NAME',
        machine_type = 'MACHINE_TYPE',
        accelerator_type='ACCELERATOR_TYPE',
        accelerator_count='ACCELERATOR_COUNT',
        boot_disk_type: 'BOOT_DISK_TYPE',
        boot_disk_size_gb: 'BOOT_DISK_SIZE',
        network: 'NETWORK',
        reserved_ip_ranges: 'RESERVED_IP_RANGES',
        nfs_mounts: 'NFS_MOUNTS'
        persistent_resource_id: 'PERSISTENT_RESOURCE_ID'
    )
    
    # Define a pipeline that runs the custom training job
    @dsl.pipeline(
      name="resource-spec-request",
      description="A simple pipeline that requests a Google Cloud machine resource",
      pipeline_root='PIPELINE_ROOT',
    )
    def pipeline():
      training_job_task = custom_training_job(
          project='PROJECT_ID',
          location='LOCATION',
      ).set_display_name('training-job-task')

Replace the following:

  - DISPLAY\_NAME : The name of the custom job. If you don't specify the name, the component name is used, by default.

  - MACHINE\_TYPE : The type of the machine for running the custom job—for example, `e2-standard-4` . For more information about machine types, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . If you specified a TPU as the `accelerator_type` , set this to `cloud-tpu` . For more information, see the [`machine_type` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.machine_type) .

  - ACCELERATOR\_TYPE : The type of accelerator attached to the machine. For more information about the available GPUs and how to configure them, see [GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) . For more information about the available TPU types and how to configure them, see [TPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#tpu) . For more information, see the [`accelerator_type` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.accelerator_type) .

  - ACCELERATOR\_COUNT : The number of accelerators attached to the machine running the custom job. If you specify the accelerator type, the accelerator count is set to `1` , by default.

  - BOOT\_DISK\_TYPE : The type of boot disk. For more information, see the [`boot_disk_type` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.boot_disk_type) .

  - BOOT\_DISK\_SIZE : The size of the boot disk in GB. For more information, see the [`boot_disk_size_gb` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.boot_disk_size_gb) .

  - NETWORK : If the custom job is peered to a Compute Engine network that has private services access configured, specify the full name of the network. For more information, see the [`network` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.network) .

  - RESERVED\_IP\_RANGES : A list of names for the reserved IP ranges under the VPC network used to deploy the custom job. For more information, see the [`reserved_ip_ranges` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.reserved_ip_ranges) .

  - NFS\_MOUNTS : A list of NFS mount resources in JSON dict format. For more information, see the [`nfs_mounts` parameter reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component.nfs_mounts) .

  - PERSISTENT\_RESOURCE\_ID (preview): The ID of the persistent resource to run the pipeline. If you specify a persistent resource, the pipeline runs on existing machines associated to the persistent resource, instead of on-demand and short-lived machine resources. Note that the network and CMEK configuration for the pipeline must match the configuration specified for the persistent resource. For more information about persistent resources and how to create them, see [Create a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create#create-persistent-resource-gcloud) .

  - PIPELINE\_ROOT : Specify a Cloud Storage URI that your pipelines service account can access. The artifacts of your pipeline runs are stored within the pipeline root.

  - PROJECT\_ID : The Google Cloud project that this pipeline runs in.

  - LOCATION : The location or region that this pipeline runs in.

## API Reference

For a complete list of arguments supported by the [`create_custom_training_job_from_component`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component) method, see the [Google Cloud Pipeline Components SDK Reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/index.html) .
