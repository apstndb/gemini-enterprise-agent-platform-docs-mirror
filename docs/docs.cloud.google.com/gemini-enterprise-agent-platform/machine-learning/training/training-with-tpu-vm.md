---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-with-tpu-vm
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-with-tpu-vm
title: Training with TPU accelerators
description: Training with TPU accelerators.
data_source: docs.cloud.google.com
---

Agent Platform supports training with various frameworks and libraries using a TPU VM. When configuring compute resources, you can specify [TPU v2](https://docs.cloud.google.com/tpu/docs/v2) , [TPU v3](https://docs.cloud.google.com/tpu/docs/v3) , or [TPU v5e](https://docs.cloud.google.com/tpu/docs/v5e) VMs. TPU v5e supports JAX 0.4.6+, TensorFlow 2.15+, and PyTorch 2.1+. TPU v6e supports Python 3.10+, JAX 0.4.37+, and PyTorch 2.1+ using PJRT as the default runtime.

For details on configuring TPU VMs for Gemini Enterprise Agent Platform serverless training, see [Configure compute resources for serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#tpu) .

## TensorFlow training

> **Note:** Starting with TPU v6e, TensorFlow is no longer supported.

### Prebuilt container

Use a [prebuilt training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that supports TPUs, and create a [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) .

> **Note:** Prebuilt containers for TPU v5e are not available.

### Custom container

Use a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) in which you have installed versions of the `tensorflow` and `libtpu` specially built for TPU VMs. These libraries are maintained by the Cloud TPU service and are listed in the [Supported TPU configurations](https://docs.cloud.google.com/tpu/docs/supported-tpu-versions#tensorflow) documentation.

> **Note:** Agent Platform supports only TensorFlow 2.11 and newer versions for custom containers and TensorFlow 2.12 and newer versions for prebuilt training containers.

Select the `tensorflow` version of your choice and its corresponding `libtpu` library. Next, install these in your Docker container image when you build the container.

For example, if you want to use TensorFlow 2.15, include the following instructions in your Dockerfile:

``` 
  # Download and install `tensorflow`.
  RUN pip install https://storage.googleapis.com/cloud-tpu-tpuvm-artifacts/tensorflow/tf-2.15.0/tensorflow-2.15.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl

  # Download and install `libtpu`.
  # You must save `libtpu.so` in the '/lib' directory of the container image.
  RUN curl -L https://storage.googleapis.com/cloud-tpu-tpuvm-artifacts/libtpu/1.9.0/libtpu.so -o /lib/libtpu.so

  # TensorFlow training on TPU v5e requires the PJRT runtime. To enable the PJRT
  # runtime, configure the following environment variables in your Dockerfile.
  # For details, see https://cloud.google.com/tpu/docs/runtimes#tf-pjrt-support.
  # ENV NEXT_PLUGGABLE_DEVICE_USE_C_API=true
  # ENV TF_PLUGGABLE_DEVICE_LIBRARY_PATH=/lib/libtpu.so
```

> **Note:** This is not a complete Dockerfile. If you want to use these instructions, add them to a [Dockerfile for a serverless training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container#create_a_dockerfile) . You can also find the corresponding libtpu version for the TensorFlow version from the [Cloud TPU configurations page](https://docs.cloud.google.com/tpu/docs/supported-tpu-configurations#tpu_vm_with_tpu_v4) .

#### TPU Pod

`tensorflow` training on a `TPU Pod` requires additional setup in the training container. Agent Platform maintains a base docker image that handles the initial setup.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Image URIs</th>
<th>Python Version</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp38:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp38:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp38:latest</code></li>
</ul></td>
<td>Python 3.8</td>
</tr>
<tr class="even">
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp310:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp310:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp310:latest</code></li>
</ul></td>
<td>Python 3.10</td>
</tr>
</tbody>
</table>

Here are the steps to build your custom container:

1.  Choose the base image for the Python version of your choice. TPU TensorFlow wheels for TensorFlow 2.12 and lower support Python 3.8. TensorFlow 2.13 and greater support Python 3.10 or greater. For the specific TensorFlow wheels, see [Cloud TPU configurations](https://docs.cloud.google.com/tpu/docs/supported-tpu-configurations#tpu_vm_with_tpu_v4) .
2.  Extend the image with your trainer code and the startup command.

<!-- end list -->

    # Specifies base image and tag
    FROM us-docker.pkg.dev/vertex-ai/training/tf-tpu-pod-base-cp310:latest
    WORKDIR /root
    
    # Download and install `tensorflow`.
    RUN pip install https://storage.googleapis.com/cloud-tpu-tpuvm-artifacts/tensorflow/tf-2.15.0/tensorflow-2.15.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
    
    # Download and install `libtpu`.
    # You must save `libtpu.so` in the '/lib' directory of the container image.
    RUN curl -L https://storage.googleapis.com/cloud-tpu-tpuvm-artifacts/libtpu/1.9.0/libtpu.so -o /lib/libtpu.so
    
    # Copies the trainer code to the docker image.
    COPY your-path-to/model.py /root/model.py
    COPY your-path-to/trainer.py /root/trainer.py
    
    # The base image is setup so that it runs the CMD that you provide.
    # You can provide CMD inside the Dockerfile like as follows.
    # Use CMD, not ENTRYPOINT, to avoid accidentally overriding the pod base image's ENTRYPOINT.
    # Alternatively, you can pass it as an `args` value in ContainerSpec:
    # (https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#containerspec)
    CMD ["python3", "trainer.py"]

> To see an example of how to train a custom TensorFlow model by using TPUs in Pipelines, run the " Pipelines: TPU model train, upload, and deploy using google-cloud-pipeline-components" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_TPU_model_train_upload_deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_TPU_model_train_upload_deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_TPU_model_train_upload_deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_TPU_model_train_upload_deploy.ipynb)

## PyTorch training

You can use prebuilt or custom containers for PyTorch when training with TPUs.

### Prebuilt container

Use a [prebuilt training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that supports TPUs, and create a [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) .

### Custom container

Use a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) in which you have installed the `PyTorch` library.

For example, your Dockerfile might look like the following:

    FROM python:3.10
    
    # v5e, v6e specific requirement - enable PJRT runtime
    ENV PJRT_DEVICE=TPU
    
    # install pytorch and torch_xla
    RUN pip3 install torch~=2.1.0 torchvision torch_xla[tpu]~=2.1.0
     -f https://storage.googleapis.com/libtpu-releases/index.html
    
    # Add your artifacts here
    COPY trainer.py .
    
    # Run the trainer code
    CMD ["python3", "trainer.py"]

#### TPU Pod

The training runs on all hosts of the TPU Pod (see [Run PyTorch code on TPU Pod slices](https://docs.cloud.google.com/tpu/docs/pytorch-pods) ).

Agent Platform waits for a response from all the hosts to decide completion of the job.

## JAX training

To perform JAX training on Agent Platform, you need to provide a container image with your JAX environment.

### Prebuilt container

There are no prebuilt containers for JAX.

### Custom container

Use a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) in which you have installed the `JAX` library.

For example, your Dockerfile might look like the following:

    # Install JAX.
    RUN pip install 'jax[tpu]>=0.4.6' -f https://storage.googleapis.com/jax-releases/libtpu_releases.html
    
    # Add your artifacts here
    COPY trainer.py trainer.py
    
    # Set an entrypoint.
    ENTRYPOINT ["python3", "trainer.py"]

#### TPU Pod

The training runs on all hosts of the TPU Pod (see [Run JAX code on TPU Pod slices](https://docs.cloud.google.com/tpu/docs/jax-pods) ).

Agent Platform watches the first host of the TPU Pod to decide completion of the job. You can use the following code snippet to make sure that all hosts exit at the same time:

    # Your training logic
    ...
    
    if jax.process_count() > 1:
      # Make sure all hosts stay up until the end of main.
      x = jnp.ones([jax.local_device_count()])
      x = jax.device_get(jax.pmap(lambda x: jax.lax.psum(x, 'i'), 'i')(x))
      assert x[0] == jax.device_count()

## Environment variables

The following table details the environment variables that you can use within the container:

| Name            | Value                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------- |
| TPU\_NODE\_NAME | my-first-tpu-node                                                                                  |
| TPU\_CONFIG     | {"project": "tenant-project-xyz", "zone": "us-central1-b", "tpu\_node\_name": "my-first-tpu-node"} |

## Custom Service Account

A custom service account can be used for TPU training. On how to use a custom service account, refer to the [page on how to use a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .

## Private IP (VPC network peering) for training

A private IP can be used for TPU training. Refer to the page on [how to use a private IP for serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip) .

## VPC Service Controls

VPC Service Controls enabled projects can submit TPU training jobs.

## Limitations

The following limitations apply when you train using a TPU VM:

  - [TPUs are only available in certain Agent Platform regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

## TPU types

Refer to [TPU types](https://docs.cloud.google.com/tpu/docs/types-zones) for more information about TPU accelerators such as memory limit.
