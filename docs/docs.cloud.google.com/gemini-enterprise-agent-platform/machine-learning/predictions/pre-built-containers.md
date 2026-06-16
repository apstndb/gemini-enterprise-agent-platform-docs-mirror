---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers
title: Prebuilt containers for inference and explanation
description: Learn about using prebuilt containers and explanations for inference.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform provides Docker container images that you run as *prebuilt containers* for serving inferences and [explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/explainable-ai/overview) from trained model artifacts. These containers, which are organized by machine learning (ML) framework and framework version, provide [HTTP inference servers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#server) that you can use to serve inferences with minimal configuration. In many cases, using a prebuilt container is simpler than [creating your own custom container for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) .

This document lists the prebuilt containers for inferences and explanations, and it describes how to use them with model artifacts that you [created using Agent Platform's custom training functionality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) or model artifacts that you created outside of Agent Platform.

## Support policy and schedule

Gemini Enterprise Agent Platform supports each framework version based on a schedule to minimize security vulnerabilities. Review the [Support policy schedule](https://docs.cloud.google.com/vertex-ai/docs/framework-support-policy#support_policy_schedule) to understand the implications of the end-of-support and end-of-availability dates.

## Available container images

Each of the following container images is available in several Artifact Registry repositories, which [store data in various locations](https://docs.cloud.google.com/artifact-registry/docs/repo-locations) . You can use any of the URIs for an image when you perform custom training; each provides the same container image. If you use the Google Cloud console to create a [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource, the Google Cloud console selects the URI that best matches the [location where you are using Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) in order to reduce latency.

> **Note:** Using image names without the `latest` tag isn't supported. You must use an image with the `latest` tag.

### TensorFlow

#### Available TensorFlow container images (Click to expand)

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
<td>2.15</td>
<td>CPU only</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-15:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-15:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-15:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.15</td>
<td>GPU (CUDA 12.x)</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-15:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-15:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-15:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.14</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-14:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-14:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-14:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.14</td>
<td>GPU (CUDA 12.x)</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-14:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-14:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-14:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.13</td>
<td>CPU only</td>
<td>Nov 28, 2024</td>
<td>Nov 28, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.13</td>
<td>GPU (CUDA 12.x)</td>
<td>Nov 28, 2024</td>
<td>Nov 28, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.12</td>
<td>CPU only</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.12</td>
<td>GPU (CUDA 11.x)</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
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
<tr class="odd">
<td>2.7</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.7</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.6</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.6</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.5</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.5</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.4</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.4</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.3</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.3</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.2</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.2</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>2.1</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>2.1</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>1.15</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>1.15</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
</tbody>
</table>

### Optimized TensorFlow runtime

The following container images use the optimized TensorFlow runtime. For more information, see [Use the optimized TensorFlow runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/optimized-tensorflow-runtime) .

#### Available optimized TensorFlow runtime container images (Click to expand)

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

### PyTorch

#### Available PyTorch container images (Click to expand)

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
<td>2.4 (Python 3.9)</td>
<td>CPU only</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-4:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-4:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-4:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.4 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-4:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-4:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-4:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.4 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-4:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-4:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-4:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.3 (Python 3.9)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-3:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-3:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-3:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.3 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-3:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-3:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-3:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.3 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-3:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-3:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-3:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.9)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-2:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-2:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-2:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.2 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-2:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-2:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-2:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-2:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-2:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-2:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.1 (Python 3.9)</td>
<td>CPU only</td>
<td>Dec 01, 2024</td>
<td>Dec 01, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.1 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>Dec 01, 2024</td>
<td>Dec 01, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.1 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>Dec 01, 2024</td>
<td>Dec 01, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>2.0 (Python 3.9)</td>
<td>CPU only</td>
<td>Jul 27, 2024</td>
<td>Jul 27, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>2.0 (Python 3.9)</td>
<td>GPU (CUDA 11.x)</td>
<td>Jul 27, 2024</td>
<td>Jul 27, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>1.13 (Python 3.8)</td>
<td>CPU only</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>1.13 (Python 3.8)</td>
<td>GPU (CUDA 11.x)</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>1.12</td>
<td>CPU only</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>1.12</td>
<td>GPU (CUDA 11.x)</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>1.11</td>
<td>CPU only</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>1.11</td>
<td>GPU (CUDA 11.x)</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td></td>
</tr>
</tbody>
</table>

### scikit-learn

#### Available scikit-learn container images (Click to expand)

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
<td>1.6 (Python 3.10)</td>
<td>CPU only</td>
<td>Oct 14, 2026</td>
<td>Oct 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-6:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-6:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-6:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>1.5 (Python 3.10)</td>
<td>CPU only</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-5:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-5:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-5:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>1.4 (Python 3.10)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-4:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-4:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-4:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>1.3 (Python 3.10)</td>
<td>CPU only</td>
<td>Nov 28, 2024</td>
<td>Nov 28, 2025</td>
<td></td>
</tr>
<tr class="odd">
<td>1.2 (Python 3.10)</td>
<td>CPU only</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>1.0</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>0.24</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>0.23</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>0.22</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>0.20</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
</tbody>
</table>

### XGBoost

#### Available XGBoost container images (Click to expand)

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
<td>2.1 (Python 3.10)</td>
<td>CPU only</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-1:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-1:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-1:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.0 (Python 3.10)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code dir="ltr" translate="no">us-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-0:latest</code></li>
<li><code dir="ltr" translate="no">europe-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-0:latest</code></li>
<li><code dir="ltr" translate="no">asia-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-0:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>1.7 (Python 3.10)</td>
<td>CPU only</td>
<td>June 30, 2024</td>
<td>Dec 30, 2025</td>
<td></td>
</tr>
<tr class="even">
<td>1.6</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>1.5</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>1.4</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>1.3</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>1.2</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>1.1</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="even">
<td>0.90</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
<tr class="odd">
<td>0.82</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td></td>
</tr>
</tbody>
</table>

## Use a prebuilt container

You can specify a prebuilt container for inference when you [create a custom `TrainingPipeline` resource that uploads a `Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#custom-job-model-upload) or when you [import model artifacts as a `Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .

To use one of these prebuilt containers, you must save your model as one or more *model artifacts* that comply with the requirements of the prebuilt container. For more information, see [Export model artifacts for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) .

The following notebooks demonstrate how to use a prebuilt container to serve inferences.

| What do you want to do?                                       | Notebook                                                                                                                                                                                                                                        |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Train and serve a TensorFlow model using a prebuilt container | [Custom training and online inference](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb)                                                               |
| Serve a PyTorch model using a prebuilt container              | [Serving PyTorch image models with prebuilt containers on Agent Platform](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb) |
| Serve a Stable Diffusion model using a prebuilt container     | [Deploy and host a Stable Diffusion model on Agent Platform](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/vertex_endpoints/torchserve/dreambooth_stablediffusion.ipynb)                               |

## Notebooks

> To learn more, run the "Serving PyTorch image models with prebuilt containers on " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fpytorch_image_classification_with_prebuilt_serving_containers.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fpytorch_image_classification_with_prebuilt_serving_containers.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb)

## What's next

  - Learn how to [deploy a model to an endpoint to serve inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .
