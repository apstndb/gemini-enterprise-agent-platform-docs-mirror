---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks
title: Supported frameworks
description: Lists the supported frameworks for Agent Platform services.
data_source: docs.cloud.google.com
---

This page lists the supported frameworks and their constituent packages for the following services:

- [Prebuilt containers for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#custom_training)

- [Prebuilt containers for predictions and explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#predictions)

- [Prebuilt containers for Ray on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#ray)

- [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#pipelines)

For an in-depth explanation of the framework support policy, see [Agent Platform framework support policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/framework-support-policy) .

## Supported frameworks for custom training

Gemini Enterprise Agent Platform uses container images to configure cloud resources to service your training requests. The following versions are supported for [custom training prebuilt containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) :

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

## Supported frameworks for predictions and explanations

Gemini Enterprise Agent Platform uses container images to configure cloud resources to service your prediction requests. The following versions are supported for [prebuilt containers for predictions and explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers) :

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
<li><code>us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-15:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-15:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-15:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.15</td>
<td>GPU (CUDA 12.x)</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-15:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-15:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-15:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.14</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-14:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-14:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-14:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.14</td>
<td>GPU (CUDA 12.x)</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-14:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-14:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/tf2-gpu.2-14:latest</code></li>
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
<li><code>us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.nightly:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>nightly</td>
<td>GPU (CUDA 12.x)</td>
<td>Not applicable</td>
<td>Not applicable</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.nightly:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.nightly:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.nightly:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>nightly</td>
<td>Cloud TPU</td>
<td>Not applicable</td>
<td>Not applicable</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.nightly:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.nightly:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.nightly:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.17</td>
<td>CPU only</td>
<td>Jul 11, 2024</td>
<td>Jul 11, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-17:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-17:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-cpu.2-17:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.17</td>
<td>GPU (CUDA 12.x)</td>
<td>Jul 11, 2024</td>
<td>Jul 11, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.2-17:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.2-17:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-gpu.2-17:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.17</td>
<td>Cloud TPU</td>
<td>Jul 11, 2024</td>
<td>Jul 11, 2025</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-17:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-17:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai-restricted/prediction/tf_opt-tpu.2-17:latest</code></li>
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
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-4:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.4 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-4:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.4 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-4:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.3 (Python 3.9)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-3:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-3:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-3:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.3 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-3:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-3:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-3:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.3 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-3:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-3:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-3:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.9)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-2:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-2:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-cpu.2-2:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.2 (Python 3.9)</td>
<td>GPU (CUDA 12.x)</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-2:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-2:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-gpu.2-2:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>2.2 (Python 3.9)</td>
<td>Cloud TPU</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-2:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-2:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/pytorch-tpu.2-2:latest</code></li>
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
<li><code>us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-6:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-6:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-6:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>1.5 (Python 3.10)</td>
<td>CPU only</td>
<td>July 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-5:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-5:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-5:latest</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>1.4 (Python 3.10)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-4:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-4:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-4:latest</code></li>
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
<li><code>us-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-1:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-1:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-1:latest</code></li>
</ul></td>
</tr>
<tr class="even">
<td>2.0 (Python 3.10)</td>
<td>CPU only</td>
<td>Jan 14, 2026</td>
<td>Jan 14, 2027</td>
<td><ul>
<li><code>us-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-0:latest</code></li>
<li><code>europe-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-0:latest</code></li>
<li><code>asia-docker.pkg.dev/vertex-ai/prediction/xgboost-cpu.2-0:latest</code></li>
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

## Supported versions of Ray on Gemini Enterprise Agent Platform

[Ray on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray) container images are available. The following versions of prebuilt containers are supported:

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

## Supported frameworks for pipelines

[Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline#version-pipeline) supports the following ML framework SDK versions:

- [Kubeflow Pipelines (KFP) SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#supported-kfp-sdk)

- [TensorFlow Extended (TFX) SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#supported-tfx-sdk)

- [Google Cloud Pipeline Components (GCPC)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#gcpc_framework)

Since these frameworks are periodically updated to patch bugs and vulnerabilities, it's recommended that you always use the latest patch version and stay within the end of support date. Customer support is not provided if a version is beyond the end of support date. For more information, see [Gemini Enterprise Agent Platform framework support policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/framework-support-policy) .

In general, follow these guidelines while using pipeline templates:

- Stay up-to-date with the latest patch version of the ML framework.

- Upgrade new and existing pipeline templates to the latest minor version of the ML framework at least once every 12 months.

- When a new major version of an ML framework is made available, migrate new and existing pipeline templates to the new major version within 24 months.

### Kubeflow Pipelines SDK

KFP is the most commonly used framework for authoring and orchestrating pipelines in Agent Platform Pipelines. Agent Platform Pipelines can execute pipeline definitions compiled using KFP into the [`pipeline_spec`](https://github.com/kubeflow/pipelines/blob/master/api/v2alpha1/pipeline_spec.proto) Intermediate Representation (IR YAML format) v2.0 or later.

Agent Platform Pipelines supports the following versions of the KFP SDK:

| Framework                                                                                | Release date | End of support date |
|------------------------------------------------------------------------------------------|--------------|---------------------|
| [KFP SDK 2](https://github.com/kubeflow/pipelines/blob/master/sdk/RELEASE.md)            | Jun 20, 2023 | Not applicable      |
| [KFP SDK 1.8](https://github.com/kubeflow/pipelines/blob/sdk/release-1.8/sdk/RELEASE.md) | Sep 3, 2021  | Dec 20, 2024        |

The latest version of the KFP SDK will drop support for [end-of-life](https://devguide.python.org/versions/) Python versions on the day they are declared end-of-life. The only exception to this is Python 3.7, for which support will be dropped on April 23, 2024.

### TensorFlow Extended (TFX) SDK

TensorFlow releases a new minor version of the TensorFlow Extended (TFX) SDK about every quarter. You can still run pipelines compiled from earlier versions of the SDK, but only the latest minor version of the SDK receives patches. Therefore, we recommend you keep up-to-date with the latest minor version.

| Framework                                                                              | Release date      | End of support date |
|----------------------------------------------------------------------------------------|-------------------|---------------------|
| [TensorFlow Extended SDK 1.15](https://github.com/tensorflow/tfx/releases/tag/v1.15.0) | April 29, 2024    | April 29, 2025      |
| [TensorFlow Extended SDK 1.14](https://github.com/tensorflow/tfx/releases/tag/v1.14.0) | September 6, 2023 | September 6, 2024   |
| [TensorFlow Extended SDK 1.13](https://github.com/tensorflow/tfx/releases/tag/v1.13.0) | May 3, 2023       | May 3, 2024         |
| [TensorFlow Extended SDK 1.12](https://github.com/tensorflow/tfx/releases/tag/v1.12.0) | Dec 19, 2022      | Dec 19, 2023        |
| [TensorFlow Extended SDK 1.11](https://github.com/tensorflow/tfx/releases/tag/v1.11.0) | Nov 23, 2022      | Nov 23, 2023        |
| [TensorFlow Extended SDK 1.10](https://github.com/tensorflow/tfx/releases/tag/v1.10.0) | Oct 4, 2022       | Oct 4, 2023         |
| [TensorFlow Extended SDK 1.9](https://github.com/tensorflow/tfx/releases/tag/v1.9.0)   | Jul 15, 2022      | Jul 15, 2023        |
| [TensorFlow Extended SDK 1.8](https://github.com/tensorflow/tfx/releases/tag/v1.8.0)   | May 25, 2022      | May 25, 2023        |

### Google Cloud Pipeline Components

Agent Platform Pipelines publishes and regularly patches the following Python packages and container images to assist in [KFP definitions](https://www.kubeflow.org/docs/components/pipelines/v2/introduction/#what-is-a-pipeline) :

| Framework                                                                                                                  | Release date | End of patch and support date | End of availability date | Supported images                                             |
|----------------------------------------------------------------------------------------------------------------------------|--------------|-------------------------------|--------------------------|--------------------------------------------------------------|
| [Google Cloud Pipeline Components 2](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/RELEASE.md) | Jun 20, 2023 | Not applicable                | Not applicable           | `gcr.io/ml-pipeline/google-cloud-pipeline-components:latest` |
| [Google Cloud Pipeline Components 1](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/RELEASE.md) | Feb 25, 2022 | Dec 20, 2024                  | Jun 20, 2025             | `gcr.io/ml-pipeline/google-cloud-pipeline-components:1.0.*`  |

The latest version of the Google Cloud Pipeline Components SDK will drop support for [end-of-life](https://devguide.python.org/versions/) Python versions on the day they are declared end-of-life. The only exception to this is Python 3.7, for which support will be dropped on April 23, 2024.

## What's next

- [Learn more about the Gemini Enterprise Agent Platform shared responsibility](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/shared-responsibility) .
