---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-tpu
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-tpu
title: Deploy a model to Cloud TPU VMs
description: Learn about deploying a model to Cloud TPU VMs.
data_source: docs.cloud.google.com
---

Google Cloud provides access to custom-designed machine learning accelerators called [Tensor Processing Units (TPUs)](https://docs.cloud.google.com/tpu/docs/intro-to-tpu) . TPUs are optimized to accelerate the training and inference of machine learning models, making them ideal for a variety of applications, including natural language processing, computer vision, and speech recognition.

This page describes how to deploy your models to a [single host](https://docs.cloud.google.com/tpu/docs/tpus-in-gke#single-host) Cloud TPU v5e, v6e, or TPU7x for online inference in Gemini Enterprise Agent Platform.

> **Note:** Multi-host deployment is now available in Public preview. For more information, see [Serve Llama 3 open models using multi-host Cloud TPUs on Gemini Enterprise Agent Platform with Saxml](https://docs.cloud.google.com/vertex-ai/docs/predictions/serve-llama3-with-saxml-tpu) .

Only [Cloud TPU version v5e, v6e,](https://docs.cloud.google.com/tpu/docs/tpu-inference) and [TPU7x](https://docs.cloud.google.com/tpu/docs/tpu7x) ( `tpu7x-standard-4t` machine type) are supported. Other Cloud TPU generations are not supported.

To learn which locations Cloud TPU version v5e, v6e, and TPU7x are available in, see [locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#region_considerations) .

## Import your model

For deployment on Cloud TPUs, you must [import your model to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) and configure it to use one of the following containers:

  - [prebuilt optimized TensorFlow runtime container](https://docs.cloud.google.com/vertex-ai/docs/predictions/optimized-tensorflow-runtime) either the `nightly` version, or version `2.15` or later
  - [prebuilt PyTorch TPU container](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#pytorch) version `2.1` or later
  - your own custom container that supports TPUs

### Prebuilt optimized TensorFlow runtime container

To import and run a [TensorFlow `SavedModel`](https://www.tensorflow.org/guide/saved_model) on a Cloud TPU, the model must be TPU-optimized. If your TensorFlow `SavedModel` isn't already TPU optimized, you can optimize your model automatically. To do this, import your model and then Gemini Enterprise Agent Platform optimizes your unoptimized model by using an automatic partitioning algorithm. This optimization doesn't work on all models. If optimization fails, you must manually optimize your model.

The following sample code demonstrates how to use automatic model optimization with automatic partitioning:

``` 
  model = aiplatform.Model.upload(
      display_name='TPU optimized model with automatic partitioning',
      artifact_uri="gs://model-artifact-uri",
      serving_container_image_uri="us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-15:latest",
      serving_container_args=[
      ]
  )
```

<span id="security-best-practice1"></span>

> **Note:** **Security Best Practice** : When you specify an `artifact_uri` that isn't set to a Cloud Storage ( `gs://` ) location, you must set the `staging_bucket` parameter to a Cloud Storage location to help ensure full asset isolation.

For more information on importing models, see [importing models to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .

### Prebuilt PyTorch container

The instructions to import and run a PyTorch model on Cloud TPU are the same as the instructions to import and run a PyTorch model.

For example, [TorchServe for Cloud TPU v5e Inference](https://docs.cloud.google.com/tpu/docs/v5e-inference#torchserve) Then, upload the model artifacts to your Cloud Storage folder and upload your model as shown:

    model = aiplatform.Model.upload(
        display_name='DenseNet TPU model from SDK PyTorch 2.1',
        artifact_uri="gs://model-artifact-uri",
        serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-1:latest",
        serving_container_args=[],
        serving_container_predict_route="/predictions/model",
        serving_container_health_route="/ping",
        serving_container_ports=[8080]
    )

<span id="security-best-practice2"></span>

> **Note:** **Security Best Practice** : When you specify an `artifact_uri` that isn't set to a Cloud Storage ( `gs://` ) location, you must set the `staging_bucket` parameter to a Cloud Storage location to help ensure full asset isolation.

For more information, see [export model artifacts for PyTorch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts#pytorch) and the tutorial notebook for [Serve a PyTorch model using a prebuilt container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb) .

### Custom container

For custom containers, your model does not need to be a TensorFlow model, but it must be TPU optimized. For information on producing a TPU optimized model, see the following guides for common ML frameworks:

  - [TensorFlow](https://www.tensorflow.org/guide/tpu)
  - [PyTorch](https://github.com/pytorch/xla)
  - [JAX/SAX](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/serve-gemma-with-saxml-tpu)

For information on serving models trained with JAX, TensorFlow, or PyTorch on Cloud TPU v5e, see [Cloud TPU v5e Inference](https://docs.cloud.google.com/tpu/docs/v5e-inference#inference-on-lite-pods) .

Make sure your custom container meets the [custom container requirements](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) .

You must [raise the locked memory limit](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/tpus#privileged-mode) so the driver can communicate with the TPU chips over direct memory access (DMA). For example:

### Command line

    ulimit -l 68719476736

### Python

    import resource
    
    resource.setrlimit(
        resource.RLIMIT_MEMLOCK,
        (
            68_719_476_736_000,  # soft limit
            68_719_476_736_000,  # hard limit
        ),
      )

Then, see [Use a custom container for inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) for information on importing a model with a custom container. If you have want to implement pre or post processing logic, consider using [Custom inference routines](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-prediction-routines) .

## Create an endpoint

The instructions for creating an endpoint for Cloud TPUs are the same as the instructions for creating any endpoint.

For example, the following command creates an [`endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) resource:

    endpoint = aiplatform.Endpoint.create(display_name='My endpoint')

The response contains the new endpoint's ID, which you use in subsequent steps.

For more information on creating an endpoint, see [deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#deploy_a_model_to_an_endpoint) .

## Deploy a model

The instructions for deploying a model to Cloud TPUs are the same as the instructions for deploying any model, except you specify one of the following supported Cloud TPU machine types:

| Machine Type        | Number of TPU chips |
| ------------------- | ------------------- |
| `tpu7x-standard-4t` | 4                   |
| `ct6e-standard-1t`  | 1                   |
| `ct6e-standard-4t`  | 4                   |
| `ct6e-standard-8t`  | 8                   |
| `ct5lp-hightpu-1t`  | 1                   |
| `ct5lp-hightpu-4t`  | 4                   |
| `ct5lp-hightpu-8t`  | 8                   |

TPU accelerators are built-in to the machine type. You don't have to specify accelerator type or accelerator count.

For example, the following command deploys a model by calling [`deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) :

    machine_type = 'ct5lp-hightpu-1t'
    
    deployed_model = model.deploy(
        endpoint=endpoint,
        deployed_model_display_name='My deployed model',
        machine_type=machine_type,
        traffic_percentage=100,
        min_replica_count=1
        sync=True,
    )

> **Note:** [Autoscaling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#scaling) for deployments using TPUs is not supported at this time. The system always uses `minReplicaCount` and ignores `maxReplicaCount` for the deployed model.

For more information, see [deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#deploy_a_model_to_an_endpoint) .

## Get online inferences

The instruction for getting online inferences from a Cloud TPU is the same as the instruction for [getting online inferences](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-online-predictions) .

For example, the following command sends an online inference request by calling [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) :

    deployed_model.predict(...)

For custom containers, see the [inference request and response requirements](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#inference) for custom containers.

## Securing capacity

For most regions, the `TPU v5e, v6e, and TPU7x cores per region` [quota for custom model serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#serving) is 0. In some regions, it is limited.

To request a quota increase, see [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase) .

## Pricing

TPU machine types are billed per hour, just like all other machine type in Vertex Prediction. For more information, see [Prediction pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) .

## What's next

  - Learn how to [get an online inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-online-predictions)
