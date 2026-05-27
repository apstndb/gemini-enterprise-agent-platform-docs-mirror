---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-bulletins
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-bulletins
title: Security bulletins
description: Read the latest security bulletins for Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

The following describes all security bulletins related to Gemini Enterprise Agent Platform.

To get the latest security bulletins delivered to you, do one of the following:

  - Add the URL of this page to your [feed reader](https://wikipedia.org/wiki/Comparison_of_feed_aggregators) .

  - Add the feed URL directly to your feed reader:
    
        https://cloud.google.com/feeds/vertex-ai-security-bulletins.xml

## GCP-2026-012

**Published:** 2026-02-20

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Severity</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>In Google Cloud Gemini Enterprise Agent Platform, a vulnerability involving predictable bucket naming was identified in Vertex AI Experiments from version 1.21.0 up to (but not including) 1.133.0.</p>
<p><strong>What should I do?</strong></p>
<p>No customer action is needed for mitigation.</p>
<p><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-2473">CVE-2026-2473</a> allows an unauthenticated remote attacker to achieve cross-tenant remote code execution, model theft, and poisoning using pre-creating predictably named Cloud Storage buckets (Bucket Squatting). This vulnerability was identified in Vertex AI Experiments version 1.21.0 and is listed under CVE-2026-2473. Mitigations have already been applied to version 1.133.0 and later.</p></td>
<td>High</td>
<td><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-2473">CVE-2026-2473</a></td>
</tr>
</tbody>
</table>

## GCP-2026-011

**Published:** 2026-02-20

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Severity</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A stored Cross-site Scripting (XSS) vulnerability in _genai/_evals_visualization was identified in Google google-cloud-aiplatform (Gemini Enterprise Agent Platform Python SDK Visualization) on Exclusively-Hosted-Service.</p>
<p><strong>What should I do?</strong></p>
<p>Customers will need to update their google-cloud-aiplatform Python SDK to version 1.131.0 (released on 2025-12-16) or later to receive the fix.</p>
<p><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-2472">CVE-2026-2472</a> allows an unauthenticated remote attacker to execute arbitrary JavaScript in a victim's Jupyter or Colab environment using injecting script escape sequences into model evaluation results or dataset JSON data. This vulnerability was identified in Google google-cloud-aiplatform (Gemini Enterprise Agent Platform Python SDK) prior to 1.131.0 and is listed under CVE-2026-2472.</p></td>
<td>High</td>
<td><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-2472">CVE-2026-2472</a></td>
</tr>
</tbody>
</table>

## GCP-2023-036

**Published:** 2023-10-30

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Severity</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.cloud.google.com/deep-learning-vm/docs/images">Deep Learning VM Images</a> is a set of prepackaged virtual machine images with a deep learning framework that are ready to be run out of the box. Recently, an out-of-bounds write vulnerability was discovered in the `ReadHuffmanCodes()` function in the `libwebp` library. This might impact images that use this library.</p>
<p>Google Cloud continuously scans its publicly published images and updates the packages to assure patched distros are included in the latest releases available for customer adoption. Deep Learning VM Images have been updated to ensure that the latest VM images include the patched distros. Customers adopting the latest VM images are not exposed to this vulnerability.</p>
<p><strong>What should I do?</strong></p>
<p>Google Cloud customers using published VM images should ensure that they are adopting the latest images and that their environments are up to date as per the <a href="https://cloud.google.com/architecture/framework/security/shared-responsibility-shared-fate">shared responsibility model</a> .</p>
<p><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-4863">CVE-2023-4863</a> could be exploited by an attacker to execute arbitrary code. This vulnerability was identified in Google Chrome prior to 116.0.5845.187 and in `libwebp` prior to 1.3.2 and is being listed under CVE-2023-4863.</p></td>
<td>High</td>
<td><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-4863">CVE-2023-4863</a></td>
</tr>
</tbody>
</table>

## GCP-2023-029

**Published:** 2023-10-03

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Severity</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TorchServe is used to host PyTorch machine learning models for online prediction. Gemini Enterprise Agent Platform provides prebuilt PyTorch model serving containers which depend on TorchServe. Vulnerabilities were recently discovered in TorchServe which would allow an attacker to take control of a TorchServe deployment if its model management API is exposed. Customers with PyTorch models deployed to Gemini Enterprise Agent Platform online prediction are not affected by these vulnerabilities, since Gemini Enterprise Agent Platform does not expose TorchServe's model management API. Customers using TorchServe outside of Gemini Enterprise Agent Platform should take precautions to ensure their deployments are set up securely.</p>
<p><strong>What should I do?</strong></p>
<p>Gemini Enterprise Agent Platform customers with deployed models using Gemini Enterprise Agent Platform's <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers#pytorch">prebuilt PyTorch serving containers</a> do not need to take any action to address the vulnerabilities, since Gemini Enterprise Agent Platform's deployments do not expose TorchServe's management server to the internet.</p>
<p>Customers who are using the prebuilt PyTorch containers in other contexts, or who are using a custom-built or third-party distribution of TorchServe, should do the following:</p>
<ul>
<li>Ensure that TorchServe's model management API is not exposed to the internet. The model management API can be restricted to local access only by ensuring that the <code dir="ltr" translate="no">           management_address          </code> is bound to <code dir="ltr" translate="no">127.0.0.1</code> .</li>
<li>Use the <code dir="ltr" translate="no">           allowed_urls          </code> setting to ensure that models can be loaded from intended sources only.</li>
<li>Upgrade TorchServe to version 0.8.2, which includes mitigations for this issue, as soon as possible. As a precaution, Gemini Enterprise Agent Platform will release fixed prebuilt containers by 2023-10-13.</li>
</ul>
<p><strong>What vulnerabilities are being addressed?</strong></p>
<p>TorchServe's management API is bound to <code dir="ltr" translate="no">0.0.0.0</code> by default in most TorchServe Docker images, including those released by Gemini Enterprise Agent Platform, making it accessible to external requests. The default IP address for the management API is changed to <code dir="ltr" translate="no">127.0.0.1</code> in TorchServe 0.8.2, mitigating this issue.</p>
<p><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-43654">CVE-2023-43654</a> and <a href="https://github.com/pytorch/serve/security/advisories/GHSA-4mqg-h5jf-j9m7">CVE-2022-1471</a> allow a user with access to the management API to load models from arbitrary sources and remotely execute code. Mitigations for both of these issues are included in TorchServe 0.8.2: the remote code execution path is removed, and a warning is emitted if the default value for <code dir="ltr" translate="no">allowed_urls</code> is used.</p></td>
<td>High</td>
<td><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-43654">CVE-2023-43654</a> , <a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-1471">CVE-2022-1471</a></td>
</tr>
</tbody>
</table>
