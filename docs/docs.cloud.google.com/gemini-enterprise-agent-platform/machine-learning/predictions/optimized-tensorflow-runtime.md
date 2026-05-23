---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime
title: Optimized TensorFlow runtime
description: The optimized TensorFlow runtime optimizes models for faster and lower cost inference.
data_source: docs.cloud.google.com
---

> To learn more, run the "Deploy a T5x base model on inferences using the optimized TensorFlow runtime" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/vertex_endpoints/optimized_tensorflow_runtime/t5x_base_optimized_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fvertex_endpoints%2Foptimized_tensorflow_runtime%2Ft5x_base_optimized_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fvertex_endpoints%2Foptimized_tensorflow_runtime%2Ft5x_base_optimized_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/vertex_endpoints/optimized_tensorflow_runtime/t5x_base_optimized_online_prediction.ipynb)

The optimized TensorFlow runtime optimizes models for faster and lower cost inference than open source based [prebuilt TensorFlow Serving containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow "prebuilt TensorFlow Serving containers") . The optimized TensorFlow runtime does this by utilizing Google's proprietary and open source technologies.

The larger a machine learning (ML) model is, the more it can cost to serve it. With the optimized TensorFlow runtime, the cost of serving your ML model and the speed of inference can be lower compared to when you use an open source-based TensorFlow runtime. To take advantage of the optimized TensorFlow runtime when you use Gemini Enterprise Agent Platform, you don't need to modify code. Instead, you choose a serving container image that uses it.

The optimized TensorFlow runtime is backward compatible with [prebuilt TensorFlow Serving containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow "prebuilt TensorFlow Serving containers") . If you're running TensorFlow models with a prebuilt container, you can switch to an optimized TensorFlow runtime container with minimal effort.

While the performance of your model improves when you use the optimized TensorFlow runtime, you should expect the performance impact to vary for different types of models.

## Optimized TensorFlow runtime overview

The optimized TensorFlow runtime uses model optimizations and new proprietary Google technologies to improve the speed and lower the cost of inference compared to open source based [prebuilt TensorFlow Serving containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow "prebuilt TensorFlow Serving containers") .

The optimization occurs when Gemini Enterprise Agent Platform uploads a model, before it runs. After you deploy a model to an endpoint, the optimization log is added to the inference log. You can use these logs to troubleshoot problems that might occur during optimization.

The following topics describe optimization improvements in the optimized TensorFlow runtime.

### Model optimizations

The following three model optimizations are included in the optimized TensorFlow runtime.

#### Model XLA precompilation

When a TensorFlow model runs, all operations run individually. There is a small amount of overhead with running individual operations. The optimized TensorFlow runtime can remove some of this overhead by leveraging [XLA](https://www.tensorflow.org/xla) to precompile all or a portion of the TensorFlow graph into larger kernels.

Model XLA precompilation is optional and disabled by default. To learn how to enable model XLA precompilation during a deployment, see [Enable model XLA precompilation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime#enable-xla-precompilation) .

#### Model compression optimizations

The optimized TensorFlow runtime can run some models faster with a small impact on model precision enabling model compression optimization. When model compression optimization is enabled, the optimized TensorFlow runtime utilizes techniques such as quantization and weight pruning to run models faster.

The model compression optimization feature is disabled by default. To learn how to enable model compression optimization during a deployment, see [Enable model compression optimization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime#enable-compression-optimization) .

#### Improved tabular model performance on GPUs

TensorFlow tabular models are usually served on CPUs because they can't utilize accelerators effectively. The optimized TensorFlow runtime addresses this by running computationally expensive parts of the model on GPUs. The rest of the model runs on CPUs by minimizing communication between the host and accelerator. Running the expensive parts of the model on GPUs and the rest on CPUs makes serving tabular models faster and cost less.

The optimized TensorFlow runtime optimizes serving the following tabular model types.

  - [Tabular Keras models](https://www.tensorflow.org/guide/keras/serialization_and_saving)
  - [Tabular estimator models and wide-n-deep models (deprecated)](https://www.tensorflow.org/tutorials/estimator/premade)

#### Automatic model optimization for Cloud TPU

The prebuilt optimized TensorFlow runtime containers that support Cloud TPUs can automatically partition and optimize your models to be run on TPUs. For more information, see [Deploy to Cloud TPU](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-tpu#prebuilt-tf) .

### Use of the TensorFlow runtime (TFRT)

The Optimized TensorFlow runtime can use the [TensorFlow runtime (TFRT)](https://github.com/tensorflow/runtime) . The TFRT efficiently uses multithreaded host CPUs, supports asynchronous programming models, and is optimized for low-level efficiency.

The TFRT CPU is enabled in all optimized TensorFlow runtime runtime CPU container images except version 2.8. To disable the TFRT CPU, set the `use_tfrt` flag to `false` .

The TFRT GPU is available on nightly optimized TensorFlow runtime GPU container images and stable optimized TensorFlow runtime GPU container images versions 2.13 and later. To enable the TFRT GPU, set the `use_tfrt` and `allow_precompilation` flags to `true` . TFRT on a GPU container image minimizes data transfer overhead between the host CPU and the GPU. After you enable TFRT, it works together with XLA compilation. Because XLA precompilation is enabled, you might experience some side effects such as increased latency on the first request. For more information, see [Enable model XLA precompilation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime#enable-xla-precompilation) .

### Use of the Google runtime

Because the optimized TensorFlow runtime is built using Google's internal stack, it can take advantage of running on Google's proprietary runtime environment.

## Optimized TensorFlow runtime container images

Gemini Enterprise Agent Platform provides two types of optimized TensorFlow runtime container images: stable and nightly.

### Stable container images

Stable optimized TensorFlow runtime containers are bound to a specific TensorFlow version, just like the open source based [prebuilt TensorFlow Serving containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow "prebuilt TensorFlow Serving containers") . Optimized TensorFlow runtime containers bound to a specific version are maintained for the same duration as the open source build that is bound to the same version. The optimized TensorFlow runtime builds have the same properties as open source TensorFlow builds, except with faster inference.

Builds are backward compatible. This means you should be able to run models trained on older TensorFlow versions using a more recent container. Recent containers should perform better than older ones. In rare exceptions, a model trained on an older TensorFlow version might not work with a more recent container.

### Nightly containers images

Nightly optimized TensorFlow runtime builds include the most recent improvements and optimizations, but might not be as reliable as stable builds. They are primarily used for experimental purposes. Nightly build names include the label `nightly` . Unlike the stable container images, nightly containers are not covered by the [Gemini Enterprise Agent Platform Service Level Agreement (SLA)](https://cloud.google.com/vertex-ai/sla) .

### Available container images

The following nightly and stable optimized TensorFlow runtime Docker container images are available.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>ML framework version</th>
<th>Supported accelerators (and CUDA version, if applicable)</th>
<th>End of patch and support date</th>
<th>End of availability</th>
<th>Supported images</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>nightly</td>
<td>CPU only</td>
<td>Not applicable</td>
<td>Not applicable</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>nightly</td>
<td>GPU (CUDA 12.x)</td>
<td>Not applicable</td>
<td>Not applicable</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.nightly:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.nightly:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.nightly:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>nightly</td>
<td>Cloud TPU</td>
<td>Not applicable</td>
<td>Not applicable</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.nightly:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.nightly:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.nightly:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.17</td>
<td>CPU only</td>
<td>Jul 11, 2024</td>
<td>Jul 11, 2025</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-17:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-17:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-17:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.17</td>
<td>GPU (CUDA 12.x)</td>
<td>Jul 11, 2024</td>
<td>Jul 11, 2025</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.2-17:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.2-17:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.2-17:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.17</td>
<td>Cloud TPU</td>
<td>Jul 11, 2024</td>
<td>Jul 11, 2025</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-17:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-17:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-17:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.16</td>
<td>CPU only</td>
<td>Apr 26, 2024</td>
<td>Apr 26, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.16</td>
<td>GPU (CUDA 12.x)</td>
<td>Apr 26, 2024</td>
<td>Apr 26, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.16</td>
<td>Cloud TPU</td>
<td>Apr 26, 2024</td>
<td>Apr 26, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.15</td>
<td>CPU only</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.15</td>
<td>GPU (CUDA 12.x)</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.15</td>
<td>Cloud TPU</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.14</td>
<td>CPU only</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.14</td>
<td>GPU (CUDA 12.x)</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.13</td>
<td>CPU only</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.13</td>
<td>GPU (CUDA 11.x)</td>
<td>Aug 15, 2024</td>
<td>Aug 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.12</td>
<td>CPU only</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.12</td>
<td>GPU (CUDA 11.x)</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.11</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.11</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.10</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.10</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.9</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.9</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.8</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.8</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
</tbody>
</table>

## Use the optimized TensorFlow runtime with a private endpoint

Using private endpoints to serve online inferences with Gemini Enterprise Agent Platform provides a low-latency, secure connection to the Gemini Enterprise Agent Platform online inference service that is faster than using public endpoints. The optimized TensorFlow runtime likely serves latency sensitive models, so you might consider using it with private endpoints. For more information, see [Use private endpoints for online inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/using-private-endpoints) .

## Deploy a model using the optimized TensorFlow runtime

The process to deploy a model for inference using the optimized TensorFlow runtime is almost the same as the process to deploy models using open source based [prebuilt TensorFlow Serving containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow "prebuilt TensorFlow Serving containers") . The only differences are that you specify a container image that uses the optimized TensorFlow runtime when you create your model and you can enable the optimization flags described earlier in this document. For example, if you deployed your model with the `us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-8:latest` container, you can serve the same model with the optimized TensorFlow runtime by using the using `us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-8:latest` container.

The following code sample shows you how to create a model with the `us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest` optimized TensorFlow runtime container. To deploy this model, you use the same process that you use to deploy a model with other [prebuilt TensorFlow Serving containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow "prebuilt TensorFlow Serving containers") .

For more information about the `ModelServiceClient` used in this sample, see [Class ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceClient) . For more information about how to deploy models using Gemini Enterprise Agent Platform, see [Deploy a model using the Agent Platform API](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) . For more information about the `allow_precompilation` and `allow_compression` settings, see [Model optimizations](https://docs.cloud.google.com/vertex-ai/docs/predictions/optimized-tensorflow-runtime#model_optimizations) described earlier in this document.

``` 
    from google.cloud.aiplatform import gapic as aip
    PROJECT_ID = PROJECT_ID
    REGION = LOCATION
    API_ENDPOINT = f"{REGION}-aiplatform.googleapis.com"
    PARENT = f"projects/{PROJECT_ID}/locations/{REGION}"

    client_options = {"api_endpoint": API_ENDPOINT}
    model_service_client = aip.ModelServiceClient(client_options=client_options)
    tf_opt_model_dict = {
        "display_name": "DISPLAY_NAME",
        "metadata_schema_uri": "",
        "artifact_uri": "MODEL_URI",
        "container_spec": {
            "image_uri": "us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest",
            "args": [
                # The optimized TensorFlow runtime includes the following
                # options that can be set here.
                # "--allow_precompilation=true" - enable XLA precompilation
                # "--allow_compression=true" - enable
                #    model compression optimization
            ],
        },
    }
    tf_opt_model = model_service_client.upload_model(
        parent=PARENT,
        model=tf_opt_model_dict).result(timeout=180).model
```

### Model optimization flags

When you deploy a model using the optimized TensorFlow runtime, you can enable two features that might further optimize serving TensorFlow models.

1.  [Model XLA precompilation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime#enable-xla-precompilation)
2.  [Optimization that affects model compression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime#enable-compression-optimization)

You can enable model XLA precompilation and model compression optimization at the same time. The following sections describe how to enable these options using flags during deployment.

#### Enable model XLA precompilation

To configure the optimized TensorFlow runtime to precompile models, set the `allow_precompilation` flag to `true` . Model XLA precompilation works for different kinds of models, and in most cases improves performance. XLA precompilation works best for requests with large batch sizes.

Model XLA precompilation happens when the first request with the new batch size arrives. To ensure that the runtime is initialized before the first request, you can include a warmup requests file. For more information, see [SavedModel warmup](https://www.tensorflow.org/tfx/serving/saved_model_warmup) in the TensorFlow documentation.

XLA precompilation takes between several seconds and several minutes to complete, depending on the model complexity. If you use model XLA precompilation, you should consider the following.

  - If you use a warmup file, try to include requests with batch sizes that represent the batch sizes you expect your model to receive. Providing a large number of requests in your warmup file slows down the startup of your model server.

  - If you expect your model to receive requests with different batch sizes, you might want to enable server-side batching with a set of fixed values for `allow_batch_sizes` . For more information about how to enable server-side
    
    batching, see [Enable server-side request batching for TensorFlow](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts#enable_server-side_request_batching_for_tensorflow) in the TensorFlow documentation.

  - Because XLA precompilation adds memory overhead, some large models might fail with an *out of memory* error on the GPU.

It's recommended that you test XLA precompilation on your model before enabling this feature in production.

#### Enable model compression optimization

To configure optimized TensorFlow runtime to use model compression optimization, set its `allow_compression` flag to `true` . Test how enabling this flag affects the precision of your model, and then determine if you want to enable it in production.

#### Disable optimizations

To configure optimized TensorFlow runtime to run models without optimization, set its `disable_optimizer` flag to `true` .

## Optimized TensorFlow runtime limits

The optimized TensorFlow runtime has the following limitations:

  - The optimized TensorFlow runtime is not compatible with older NVIDIA GPUs such as Tesla P4 and Tesla P100.
  - The optimized TensorFlow runtime supports only [*sampled Shapley*](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview#sampled-shapley) explainability at this time.

## Pricing

Deploying models using the optimized TensorFlow runtime doesn't incur additional charges. The cost is the same as other inference deployments where you're charged based on the number of VMs and accelerators that are used. For more information, see [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .
