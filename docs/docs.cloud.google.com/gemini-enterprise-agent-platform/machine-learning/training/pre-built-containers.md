---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers
title: Prebuilt containers for serverless training
description: Learn how to use prebuilt containers for serverless training.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform provides Docker container images that you run as *prebuilt containers* for serverless training. These containers, which are organized by machine learning (ML) framework and framework version, include common dependencies that you might want to use in training code. Often, using a prebuilt container is simpler than [creating your own custom container for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

This document lists the prebuilt containers for training, and it describes how to use them with a [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) .

Gemini Enterprise Agent Platform supports each framework version based on a schedule to minimize security vulnerabilities. Review the [Agent Platform framework support policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform//machine-learning/framework-support-policy) to understand the implications of the end-of-support and end-of-availability dates.

## Available container images

Each of the following container images is available in several [Artifact Registry repositories](https://docs.cloud.google.com/artifact-registry/docs/repositories) , which [store data in various locations](https://docs.cloud.google.com/artifact-registry/docs/repo-locations) . You can use any of the URIs for an image when you perform serverless training; each provides the same container image. When using Google Cloud console to perform serverless training, the Google Cloud console selects the URI that best matches the [location where you're using Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) . This reduces latency.

> **Note:** Using image names without the `latest` tag isn't supported. You must use an image with the `latest` tag.

### TensorFlow

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
<td>2.17 (Python 3.10)</td>
<td>CPU only</td>
<td>Jul 11, 2025</td>
<td>Jul 11, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-17.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-17.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-17.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.17.x (latest patch) sympy 1.12 pandas 2.2.3 xgboost 2.1.3 python-json-logger 3.2.1 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.17 (Python 3.10)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jul 11, 2025</td>
<td>Jul 11, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-17.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-17.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-17.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.17.x (latest patch) sympy 1.12 pandas 2.2.3 xgboost 2.1.3 python-json-logger 3.2.1 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.16 (Python 3.10)</td>
<td>CPU only</td>
<td>Jun 28, 2025</td>
<td>Jun 28, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-16.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-16.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-16.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.16.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.16 (Python 3.10)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jun 28, 2025</td>
<td>Jun 28, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-16.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-16.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-16.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.16.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.15 (Python 3.10)</td>
<td>CPU only</td>
<td>Nov 14, 2024</td>
<td>Nov 14, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-15.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-15.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-15.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.15.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.15 (Python 3.10)</td>
<td>GPU (CUDA 12.x)</td>
<td>Nov 14, 2024</td>
<td>Nov 14, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-15.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-15.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-15.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.15.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.15 (Python 3.10)</td>
<td>TPU only</td>
<td>Oct 23, 2024</td>
<td>Oct 23, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-tpu.2-15.cp310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-tpu.2-15.cp310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-tpu.2-15.cp310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.15.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.14 (Python 3.10)</td>
<td>CPU only</td>
<td>Sep 26, 2024</td>
<td>Sep 26, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-14.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-14.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-14.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.14.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.14 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 26, 2024</td>
<td>Sep 26, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-14.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-14.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-14.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.14.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.13 (Python 3.10)</td>
<td>CPU only</td>
<td>Jul 5, 2024</td>
<td>Jul 5, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-13.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-13.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-13.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.13.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.13 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Jul 5, 2024</td>
<td>Jul 5, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-13.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-13.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-13.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.13.x (latest patch) sympy 1.12 xgboost 2.0.3 python-json-logger 2.0.7 WebOb 1.8.7 Paste 3.7.1 webapp2 3.0.0b1 mock 5.1.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.12 (Python 3.10)</td>
<td>CPU only</td>
<td>Jun 30, 2024</td>
<td>Jun 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-12.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-12.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-12.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.12.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.12 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Jun 30, 2024</td>
<td>Jun 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-12.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-12.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-12.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.12.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.12 (Python 3.8)</td>
<td>TPU only</td>
<td>Jun 30, 2024</td>
<td>Jun 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-tpu.2-12:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-tpu.2-12:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-tpu.2-12:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.12.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.11 (Python 3.10)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-11.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-11.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-11.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.11.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.11 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-11.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-11.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-11.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.11.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.11 (Python 3.7)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-11:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-11:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-11:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.11.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.11 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-11:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-11:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-11:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.11.x (latest patch) sympy 1.10.1 xgboost 1.6.2 python-json-logger 2.0.4 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 5.0.0 google-cloud-resource-manager 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.9 (Python 3.10)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-9.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-9.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-9.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.9.x (latest patch) sympy 1.10.1 xgboost 1.6.1 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.5.0 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.9 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-9.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-9.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-9.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.9.x (latest patch) sympy 1.10.1 xgboost 1.6.1 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.5.0 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.9 (Python 3.7)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-9:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-9:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-9:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.9.x (latest patch) sympy 1.10.1 xgboost 1.6.1 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.5.0 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.9 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-9:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-9:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-9:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.9.x (latest patch) sympy 1.10.1 xgboost 1.6.1 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.5.0 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.8 (Python 3.10)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.8.x (latest patch) sympy 1.9 xgboost 1.5.2 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.3.3 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.8 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-8.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-8.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-8.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.8.x (latest patch) sympy 1.9 xgboost 1.5.2 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.3.3 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.8 (Python 3.7)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.8.x (latest patch) sympy 1.9 xgboost 1.5.2 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.3.3 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.8 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-8:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-8:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-8:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.8.x (latest patch) sympy 1.9 xgboost 1.5.2 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.3.3 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.7 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-7:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-7:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-7:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.7.x (latest patch) sympy 1.9 xgboost 1.5.0 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.3.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.7 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-7:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-7:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-7:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.7.x (latest patch) sympy 1.9 xgboost 1.5.0 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.3.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.6 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-6:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.6.x (latest patch) sympy 1.8 xgboost 1.4.2 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.6 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-6:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.6.x (latest patch) sympy 1.8 xgboost 1.4.2 python-json-logger 2.0.2 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 1.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.5 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-5:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-5:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-5:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.5.x (latest patch) sympy 1.8 xgboost 1.4.0 PyYAML 3.13 python-json-logger 2.0.1 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 0.30.3 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.5 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-5:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-5:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-5:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.5.x (latest patch) sympy 1.8 xgboost 1.4.0 PyYAML 3.13 python-json-logger 2.0.1 WebOb 1.8.7 Paste 3.5.0 webapp2 3.0.0b1 mock 4.0.3 google-cloud-resource-manager 0.30.3 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.4 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-4:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.4.x (latest patch) numpy 1.19.4 pandas 1.1.5 scipy 1.5.4 scikit-learn 0.24.0 sympy 1.7.1 statsmodels 0.12.1 xgboost 1.3.1 oauth2client 4.1.3 httplib2 0.15.0 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 3.13 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.0 python-json-logger 2.0.1 wheel 0.36.2 WebOb 1.8.6 Paste 3.5.0 tornado 5.1.1 grpcio 1.32.0 requests 2.25.1 webapp2 3.0.0b1 mock 4.0.3 google-cloud-bigquery 2.6.1 google-cloud-bigtable 1.6.1 google-cloud-datastore 2.1.0 google-cloud-logging 1.15.0 google-cloud-pubsub 2.2.0 google-cloud-resource-manager 0.30.3 google-cloud-storage 1.35.0 joblib 1.0.0 cloudml-hypertune psutil 5.8.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.4 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-4:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.4.x (latest patch) numpy 1.19.4 pandas 1.1.5 scipy 1.5.4 scikit-learn 0.24.0 sympy 1.7.1 statsmodels 0.12.1 xgboost 1.3.1 oauth2client 4.1.3 httplib2 0.15.0 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 3.13 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.0 python-json-logger 2.0.1 wheel 0.36.2 WebOb 1.8.6 Paste 3.5.0 tornado 5.1.1 grpcio 1.32.0 requests 2.25.1 webapp2 3.0.0b1 mock 4.0.3 google-cloud-bigquery 2.6.1 google-cloud-bigtable 1.6.1 google-cloud-datastore 2.1.0 google-cloud-logging 1.15.0 google-cloud-pubsub 2.2.0 google-cloud-resource-manager 0.30.3 google-cloud-storage 1.35.0 joblib 1.0.0 cloudml-hypertune psutil 5.8.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.3 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-3:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-3:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-3:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.3.x (latest patch) numpy 1.18.5 pandas 1.1.3 scipy 1.4.1 scikit-learn 0.23.2 sympy 1.6.2 statsmodels 0.12.0 xgboost 1.2.1 oauth2client 4.1.3 httplib2 0.15.0 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 3.13 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.0 python-json-logger 2.0.1 wheel 0.35.1 WebOb 1.8.6 Paste 3.5.0 tornado 5.1.1 grpcio 1.33.1 requests 2.24.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 2.2.0 google-cloud-bigtable 1.5.1 google-cloud-datastore 1.15.3 google-cloud-logging 1.15.0 google-cloud-pubsub 2.1.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.32.0 joblib 0.17.0 cloudml-hypertune psutil 5.7.2</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.3 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-3:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-3:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-3:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.3.x (latest patch) numpy 1.18.5 pandas 1.1.3 scipy 1.4.1 scikit-learn 0.23.2 sympy 1.6.2 statsmodels 0.12.0 xgboost 1.2.1 oauth2client 4.1.3 httplib2 0.15.0 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 3.13 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.0 python-json-logger 2.0.1 wheel 0.35.1 WebOb 1.8.6 Paste 3.5.0 tornado 5.1.1 grpcio 1.33.1 requests 2.24.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 2.2.0 google-cloud-bigtable 1.5.1 google-cloud-datastore 1.15.3 google-cloud-logging 1.15.0 google-cloud-pubsub 2.1.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.32.0 joblib 0.17.0 cloudml-hypertune psutil 5.7.2</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.2.x (latest patch) numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 0.23.1 sympy 1.6 statsmodels 0.11.1 xgboost 1.1.1 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune psutil 5.7.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.2 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-2:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-2:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-2:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.2.x (latest patch) numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 0.23.1 sympy 1.6 statsmodels 0.11.1 xgboost 1.1.1 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune psutil 5.7.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.1 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-1:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.2-1:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.2-1:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.1.0 numpy 1.18.0 pandas 0.25.3 scipy 1.4.1 scikit-learn 0.22.1 sympy 1.5 statsmodels 0.10.2 xgboost 0.90 oauth2client 4.1.3 httplib2 0.15.0 python-dateutil 2.8.1 six 1.13.0 future 0.18.2 PyYAML 5.2 wrapt 1.11.2 crcmod 1.7 google-api-python-client 1.7.11 python-json-logger 0.1.11 wheel 0.33.6 WebOb 1.8.5 Paste 3.2.3 tornado 5.1.1 grpcio 1.26.0 requests 2.22.0 webapp2 3.0.0b1 mock 3.0.5 google-cloud-bigquery 1.23.1 google-cloud-bigtable 1.2.0 google-cloud-datastore 1.10.0 google-cloud-logging 1.14.0 google-cloud-pubsub 1.1.0 google-cloud-resource-manager 0.30.0 google-cloud-storage 1.23.0 joblib 0.14.1 cloudml-hypertune psutil 5.7.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.1 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.2-1:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.2-1:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.2-1:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 2.1.0 numpy 1.18.0 pandas 0.25.3 scipy 1.4.1 scikit-learn 0.22.1 sympy 1.5 statsmodels 0.10.2 xgboost 0.90 oauth2client 4.1.3 httplib2 0.15.0 python-dateutil 2.8.1 six 1.13.0 future 0.18.2 PyYAML 5.2 wrapt 1.11.2 crcmod 1.7 google-api-python-client 1.7.11 python-json-logger 0.1.11 wheel 0.33.6 WebOb 1.8.5 Paste 3.2.3 tornado 5.1.1 grpcio 1.26.0 requests 2.22.0 webapp2 3.0.0b1 mock 3.0.5 google-cloud-bigquery 1.23.1 google-cloud-bigtable 1.2.0 google-cloud-datastore 1.10.0 google-cloud-logging 1.14.0 google-cloud-pubsub 1.1.0 google-cloud-resource-manager 0.30.0 google-cloud-storage 1.23.0 joblib 0.14.1 cloudml-hypertune psutil 5.7.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.15 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-cpu.1-15:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-cpu.1-15:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-cpu.1-15:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 1.15.0 numpy 1.16.5 pandas 0.24.2 scipy 1.2.2 scikit-learn 0.20.4 sympy 1.4 statsmodels 0.10.1 xgboost 0.82 oauth2client 4.1.3 httplib2 0.12.0 python-dateutil 2.7.5 argparse 1.4.0 six 1.12.0 future 0.17.1 PyYAML 3.13 wrapt 1.11.1 crcmod 1.7 google-api-python-client 1.7.8 python-json-logger 0.1.10 wheel 0.32.3 WebOb 1.8.5 Paste 3.0.6 tornado 5.1.1 grpcio 1.18.0 requests 2.19.0 webapp2 3.0.0b1 mock 2.0.0 google-cloud-bigquery 1.20.0 google-cloud-bigtable 1.0.0 google-cloud-datastore 1.9.0 google-cloud-logging 1.12.1 google-cloud-pubsub 1.0.0 google-cloud-resource-manager 0.29.2 google-cloud-storage 1.19.1 joblib 0.13.0 cloudml-hypertune psutil 5.7.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.15 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/tf-gpu.1-15:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/tf-gpu.1-15:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/tf-gpu.1-15:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>tensorflow 1.15.0 numpy 1.16.5 pandas 0.24.2 scipy 1.2.2 scikit-learn 0.20.4 sympy 1.4 statsmodels 0.10.1 xgboost 0.82 oauth2client 4.1.3 httplib2 0.12.0 python-dateutil 2.7.5 argparse 1.4.0 six 1.12.0 future 0.17.1 PyYAML 3.13 wrapt 1.11.1 crcmod 1.7 google-api-python-client 1.7.8 python-json-logger 0.1.10 wheel 0.32.3 WebOb 1.8.5 Paste 3.0.6 tornado 5.1.1 grpcio 1.18.0 requests 2.19.0 webapp2 3.0.0b1 mock 2.0.0 google-cloud-bigquery 1.20.0 google-cloud-bigtable 1.0.0 google-cloud-datastore 1.9.0 google-cloud-logging 1.12.1 google-cloud-pubsub 1.0.0 google-cloud-resource-manager 0.29.2 google-cloud-storage 1.19.1 joblib 0.13.0 cloudml-hypertune psutil 5.7.0</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### PyTorch

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
<td>2.4 (Python 3.10)</td>
<td>CPU only</td>
<td>Jul 24, 2025</td>
<td>Jul 24, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-4.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-4.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-4.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.4.x (latest patch) pandas 2.2.3 absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 3.2.1 scikit-learn 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.4 (Python 3.10)</td>
<td>GPU only (CUDA 12.x)</td>
<td>Jul 24, 2025</td>
<td>Jul 24, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-4.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-4.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-4.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.4.x (latest patch) pandas 2.2.3 absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 3.2.1 scikit-learn 1.6.1 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.3 (Python 3.10)</td>
<td>CPU only</td>
<td>Apr 24, 2025</td>
<td>Apr 24, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-3.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-3.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-3.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.3.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.3 (Python 3.10)</td>
<td>GPU only (CUDA 12.x)</td>
<td>Apr 24, 2025</td>
<td>Apr 24, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-3.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-3.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-3.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.3.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.10)</td>
<td>CPU only</td>
<td>Jan 30, 2025</td>
<td>Oct 23, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-2.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-2.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-2.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.2.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.2 (Python 3.10)</td>
<td>GPU only (CUDA 12.x)</td>
<td>Jan 30, 2025</td>
<td>Jan 30, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-2.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-2.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-2.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.2.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.10)</td>
<td>TPU only</td>
<td>Nov 6, 2024</td>
<td>Nov 6, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-2.cp310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-2.cp310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-2.cp310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.2.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 tpu-info cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.1 (Python 3.10)</td>
<td>CPU only</td>
<td>Oct 4, 2024</td>
<td>Oct 4, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-1.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-1.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-1.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.1.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.1 (Python 3.10)</td>
<td>GPU only (CUDA 12.x)</td>
<td>Oct 4, 2024</td>
<td>Oct 4, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-1.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-1.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-1.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.1.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.1 (Python 3.8)</td>
<td>TPU only</td>
<td>Oct 23, 2024</td>
<td>Oct 23, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-1.cp310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-1.cp310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-1.cp310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.3.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 tpu-info cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.0 (Python 3.10)</td>
<td>CPU only</td>
<td>Mar 15, 2024</td>
<td>Mar 15, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-0.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-0.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.2-0.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.0.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.0 (Python 3.10)</td>
<td>GPU only (CUDA 11.x)</td>
<td>Mar 15, 2024</td>
<td>Mar 15, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-0.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-0.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.2-0.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.0.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.0 (Python 3.8)</td>
<td>TPU only</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-0:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-0:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-tpu.2-0:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 2.0.x (latest patch) absl-py 2.1.0 cloud-tpu-client 0.10 python-json-logger 2.0.7 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.8 python3-dev python3.7-dev python3-pip python3-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.13 (Python 3.10)</td>
<td>CPU or GPU (CUDA 11.x)</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-13.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-13.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-13.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.13.x (latest patch) absl-py 1.3.0 cloud-tpu-client 0.10 python-json-logger 2.0.4 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.13 (Python 3.7)</td>
<td>CPU or GPU (CUDA 11.x)</td>
<td>Dec 8, 2023</td>
<td>Dec 8, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-13:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-13:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-13:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.13.x (latest patch) absl-py 1.3.0 cloud-tpu-client 0.10 python-json-logger 2.0.4 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.12 (Python 3.10)</td>
<td>CPU or GPU (CUDA 11.x)</td>
<td>May 15, 2024</td>
<td>May 15, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-12.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-12.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-12.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.12.x (latest patch) absl-py 1.3.0 cloud-tpu-client 0.10 python-json-logger 2.0.4 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.12 (Python 3.7)</td>
<td>CPU or GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-12:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-12:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-12:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.12.x (latest patch) absl-py 1.3.0 cloud-tpu-client 0.10 python-json-logger 2.0.4 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.11 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-11:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-11:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-11:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.11.x (latest patch) absl-py 1.0.0 cloud-tpu-client 0.10 python-json-logger 2.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.11 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-11:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-11:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-11:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.11.x (latest patch) absl-py 1.0.0 cloud-tpu-client 0.10 python-json-logger 2.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.10 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-10:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-10:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-10:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.10.x (latest patch) absl-py 1.0.0 cloud-tpu-client 0.10 python-json-logger 2.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.10 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-10:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-10:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-10:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.10.x (latest patch) absl-py 1.0.0 cloud-tpu-client 0.10 python-json-logger 2.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.9 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-9:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-9:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-9:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.9.x (latest patch) absl-py 0.13.0 cloud-tpu-client 0.10 python-json-logger 2.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.9 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-9:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-9:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-9:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PyTorch 1.9.x (latest patch) absl-py 0.13.0 cloud-tpu-client 0.10 python-json-logger 2.0.2 cloudml-hypertune Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.7 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-7:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-7:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-7:latest</code></li>
</ul>
Included dependencies
<a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
<tr class="odd">
<td>1.7 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-7:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-7:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-7:latest</code></li>
</ul>
Included dependencies
<a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
<tr class="even">
<td>1.6 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-xla.1-6:latest</code></li>
</ul>
Included dependencies
<a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
<tr class="odd">
<td>1.6 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-6:latest</code></li>
</ul>
Included dependencies
<a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
<tr class="even">
<td>1.4 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-cpu.1-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-cpu.1-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-cpu.1-4:latest</code></li>
</ul>
Included dependencies
<a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
<tr class="odd">
<td>1.4 (Python 3.7)</td>
<td>GPU (CUDA 11.x)</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/pytorch-gpu.1-4:latest</code></li>
</ul>
Included dependencies
<a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table>

### scikit-learn

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
<td>Jul 11, 2025</td>
<td>Jul 11, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/sklearn-cpu.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/sklearn-cpu.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/sklearn-cpu.1-6:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.26.4 pandas 2.2.3 scipy 1.15.2 scikit-learn 1.6.1 sympy 1.12 xgboost 2.1.3 oauth2client 4.1.3 httplib2 0.22.0 python-dateutil 2.9.0.post0 six 1.17.0 wrapt 1.17.2 google-api-python-client 2.162.0 python-json-logger 3.2.1 wheel 0.45.1 WebOb 1.8.7 Paste 3.7.1 grpcio 1.71.0rc2 requests 2.32.3 webapp2 3.0.0b1 mock 5.1.0 google-cloud-bigquery 3.29.0 google-cloud-datastore 1.15.5 google-cloud-resource-manager 1.6.1 google-cloud-storage 2.19.0 joblib 1.4.2 cloudml-hypertune</td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.6 (Python 3.10)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jul 11, 2025</td>
<td>Jul 11, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/sklearn-gpu.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/sklearn-gpu.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/sklearn-gpu.1-6:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.26.4 pandas 2.2.3 scipy 1.15.2 scikit-learn 1.6.1 sympy 1.12 xgboost 2.1.3 oauth2client 4.1.3 httplib2 0.22.0 python-dateutil 2.9.0.post0 six 1.17.0 wrapt 1.17.2 google-api-python-client 2.162.0 python-json-logger 3.2.1 wheel 0.45.1 WebOb 1.8.7 Paste 3.7.1 grpcio 1.71.0rc2 requests 2.32.3 webapp2 3.0.0b1 mock 5.1.0 google-cloud-bigquery 3.29.0 google-cloud-datastore 1.15.5 google-cloud-resource-manager 1.6.1 google-cloud-storage 2.19.0 joblib 1.4.2 cloudml-hypertune</td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.0 (Python 3.10)</td>
<td>CPU only</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/sklearn-cpu.1-0:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/sklearn-cpu.1-0:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/sklearn-cpu.1-0:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 1.0 sympy 1.6 statsmodels 0.11.1 xgboost 1.6.2 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.10 python3-dev python3.10-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.0 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/sklearn-gpu.1-0:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/sklearn-gpu.1-0:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/sklearn-gpu.1-0:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 1.0 sympy 1.6 statsmodels 0.11.1 xgboost 1.6.2 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.10 python3-dev python3.10-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>0.23 (Python 3.7)</td>
<td>CPU only</td>
<td>Sep 1, 2023</td>
<td>Sep 1, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/scikit-learn-cpu.0-23:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/scikit-learn-cpu.0-23:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/scikit-learn-cpu.0-23:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 0.23.1 sympy 1.6 statsmodels 0.11.1 xgboost 1.1.1 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### XGBoost

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
<td>Jul 11, 2025</td>
<td>Jul 11, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/xgboost-cpu.2-1:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/xgboost-cpu.2-1:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/xgboost-cpu.2-1:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.26.4 pandas 2.2.3 scipy 1.15.2 scikit-learn 1.6.1 sympy 1.12 xgboost 2.1.3 oauth2client 4.1.3 httplib2 0.22.0 python-dateutil 2.9.0.post0 six 1.17.0 wrapt 1.17.2 google-api-python-client 2.162.0 python-json-logger 3.2.1 wheel 0.45.1 WebOb 1.8.7 Paste 3.7.1 grpcio 1.71.0rc2 requests 2.32.3 webapp2 3.0.0b1 mock 5.1.0 google-cloud-bigquery 3.29.0 google-cloud-datastore 1.15.5 google-cloud-resource-manager 1.6.1 google-cloud-storage 2.19.0 joblib 1.4.2 cloudml-hypertune</td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.1 (Python 3.10)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jul 11, 2025</td>
<td>Jul 11, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/xgboost-gpu.2-1:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/xgboost-gpu.2-1:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/xgboost-gpu.2-1:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.26.4 pandas 2.2.3 scipy 1.15.2 scikit-learn 1.6.1 sympy 1.12 xgboost 2.1.3 oauth2client 4.1.3 httplib2 0.22.0 python-dateutil 2.9.0.post0 six 1.17.0 wrapt 1.17.2 google-api-python-client 2.162.0 python-json-logger 3.2.1 wheel 0.45.1 WebOb 1.8.7 Paste 3.7.1 grpcio 1.71.0rc2 requests 2.32.3 webapp2 3.0.0b1 mock 5.1.0 google-cloud-bigquery 3.29.0 google-cloud-datastore 1.15.5 google-cloud-resource-manager 1.6.1 google-cloud-storage 2.19.0 joblib 1.4.2 cloudml-hypertune</td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev gfortran gdb openjdk-8-jdk openjdk-8-jre-headless g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.6 (Python 3.10)</td>
<td>CPU only</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/xgboost-cpu.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/xgboost-cpu.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/xgboost-cpu.1-6:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 0.23.1 sympy 1.6 statsmodels 0.11.1 xgboost 1.6.2 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.10 python3-dev python3.10-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>1.6 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>June 30, 2024</td>
<td>June 30, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/xgboost-gpu.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/xgboost-gpu.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/xgboost-gpu.1-6:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 0.23.1 sympy 1.6 statsmodels 0.11.1 xgboost 1.6.2 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.10 python3-dev python3.10-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>1.1 (Python 3.7)</td>
<td>CPU only</td>
<td>Nov 15, 2023</td>
<td>Nov 15, 2024</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/xgboost-cpu.1-1:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/xgboost-cpu.1-1:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/xgboost-cpu.1-1:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>numpy 1.18.5 pandas 1.0.4 scipy 1.4.1 scikit-learn 0.23.1 sympy 1.6 statsmodels 0.11.1 xgboost 1.1.1 oauth2client 4.1.3 httplib2 0.18.1 python-dateutil 2.8.1 six 1.15.0 future 0.18.2 PyYAML 5.3.1 wrapt 1.12.1 crcmod 1.7 google-api-python-client 1.9.3 python-json-logger 0.1.11 wheel 0.34.2 WebOb 1.8.6 Paste 3.4.1 tornado 5.1.1 grpcio 1.29.0 requests 2.23.0 webapp2 3.0.0b1 mock 4.0.2 google-cloud-bigquery 1.25.0 google-cloud-bigtable 1.2.1 google-cloud-datastore 1.12.0 google-cloud-logging 1.15.0 google-cloud-pubsub 1.6.0 google-cloud-resource-manager 0.30.2 google-cloud-storage 1.29.0 joblib 0.15.1 cloudml-hypertune</td>
<td>curl libcurl3-dev wget zip unzip git vim build-essential ca-certificates pkg-config rsync ca-certificates-java libatlas-base-dev liblapack-dev gfortran libpng-dev libjpeg-dev python3.7 python3-dev python3.7-dev python3-pip python3-setuptools python2.7 python-dev python-setuptools gdb openjdk-8-jdk openjdk-8-jre-headless g++ zlib1g-dev libio-all-perl module-init-tools libsnappy-dev libyaml-0-2 python-opencv</td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### Supported versions of Ray on Vertex AI

[Ray on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray) container images are available. The following versions of prebuilt containers are supported:

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
<th>Ray version</th>
<th>Supported accelerators (and CUDA version, if applicable)</th>
<th>End of patch and support date</th>
<th>End of availability</th>
<th>Supported images</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2.47.1 (Python 3.11)</td>
<td>CPU only</td>
<td>Jul 28, 2026</td>
<td>Jul 28, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-cpu.2-47.py311:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-cpu.2-47.py311:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-cpu.2-47.py311:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.3.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 3.3.0 google-cloud-resource-manager 1.14.2 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.47.1 (Python 3.11)</td>
<td>GPU (CUDA 11.x)</td>
<td>Jul 28, 2026</td>
<td>Jul 28, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-gpu.2-47.py311:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-gpu.2-47.py311:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-gpu.2-47.py311:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.3.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 3.3.0 google-cloud-resource-manager 1.14.2 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.42.0 (Python 3.11)</td>
<td>CPU only</td>
<td>Mar 1, 2026</td>
<td>Mar 1, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-cpu.2-42.py311:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-cpu.2-42.py311:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-cpu.2-42.py311:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.1.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 3.2.1 google-cloud-resource-manager 1.12.4 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.42.0 (Python 3.11)</td>
<td>GPU (CUDA 11.x)</td>
<td>Mar 1, 2026</td>
<td>Mar 1, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-gpu.2-42.py311:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-gpu.2-42.py311:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-gpu.2-42.py311:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.1.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 3.2.1 google-cloud-resource-manager 1.12.4 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.42.0 (Python 3.10)</td>
<td>CPU only</td>
<td>Mar 1, 2026</td>
<td>Mar 1, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-cpu.2-42.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-cpu.2-42.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-cpu.2-42.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.1.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 3.2.1 google-cloud-resource-manager 1.12.4 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.42.0 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>Mar 1, 2026</td>
<td>Mar 1, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-gpu.2-42.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-gpu.2-42.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-gpu.2-42.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.1.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 3.2.1 google-cloud-resource-manager 1.12.4 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.33.0 (Python 3.10)</td>
<td>CPU only</td>
<td>September 16, 2025</td>
<td>September 16, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-cpu.2-33.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-cpu.2-33.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-cpu.2-33.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.1.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 2.0.7 google-cloud-resource-manager 1.12.4 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.33.0 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>September 16, 2025</td>
<td>September 16, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-gpu.2-33.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-gpu.2-33.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-gpu.2-33.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.1.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 2.0.7 google-cloud-resource-manager 1.12.4 setuptools 69.5.1 kubernetes Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>2.9.3 (Python 3.10)</td>
<td>CPU only</td>
<td>May 7, 2025</td>
<td>May 7, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-cpu.2-9.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-cpu.2-9.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-cpu.2-9.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.0.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 2.0.7 google-cloud-resource-manager 1.11.0 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>2.9.3 (Python 3.10)</td>
<td>GPU (CUDA 11.x)</td>
<td>May 7, 2025</td>
<td>May 7, 2026</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/training/ray-gpu.2-9.py310:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/training/ray-gpu.2-9.py310:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/training/ray-gpu.2-9.py310:latest</code></li>
</ul>
Included dependencies
<table>
<thead>
<tr class="header">
<th>PyPI packages</th>
<th>Ubuntu packages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>absl-py 2.0.0 cloud-tpu-client 0.10 cloudml-hypertune python-json-logger 2.0.7 google-cloud-resource-manager 1.11.0 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
<td>ca-certificates-java libatlas-base-dev liblapack-dev g++ libio-all-perl libyaml-0-2 Other <a href="https://docs.cloud.google.com/deep-learning-containers/docs/overview#pre-installed_software">Deep Learning Containers dependencies</a></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

## Train with a prebuilt container

> To see an example of using a prebuilt container for training as part of a more comprehensive workflow, run the "Custom training and online inference" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb)

To use a prebuilt container, read the [guide to configuring container settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) .

If you're using a container image that supports GPUs, make sure to specify the [`machineSpec.acceleratorType` and `machineSpec.acceleratorCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec) fields when you create your `CustomJob` , `HyperparameterTuningJob` , or `TrainingPipeline` resource.

## What's next

- Learn how to [create a Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) to use with a prebuilt container.
