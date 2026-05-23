---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/api-errors
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/api-errors
title: API errors
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This guide provides a list of errors that you might encounter from using generative AI components of the Agent Platform API. The errors follow the [error model](https://docs.cloud.google.com/apis/design/errors) of the Google Cloud API, which recommends that we provide guidance on the causes and the solutions specific to the generative AI models.

## API errors

This table provides API error codes and descriptions.

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
<th>HTTP error code</th>
<th>Canonical error code</th>
<th>Cause</th>
<th>Example</th>
<th>Solution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>400</td>
<td><code dir="ltr" translate="no">INVALID_ARGUMENT / FAILED_PRECONDITION</code></td>
<td>Request fails API validation, or you tried to access a model that requires allowlisting or is disallowed by the organization's policy.</td>
<td>Request exceeds the model's input token limit.</td>
<td>Review the model-specific limits. See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models">Google models</a> .</td>
</tr>
<tr class="even">
<td>401</td>
<td><code dir="ltr" translate="no">UNAUTHENTICATED</code></td>
<td>Request isn't authenticated due to a missing, invalid, or expired OAuth token.</td>
<td>Request has invalid authentication credentials.</td>
<td>Verify that the Authorization header contains a valid access token. If you're using the Google Cloud CLI, run <code dir="ltr" translate="no">gcloud auth print-access-token</code> to generate a valid token.</td>
</tr>
<tr class="odd">
<td>403</td>
<td><code dir="ltr" translate="no">PERMISSION_DENIED</code></td>
<td>Client doesn't have sufficient permission to call the API.</td>
<td>Service account doesn't have permission to access the Cloud Storage bucket hosting image or video resources.</td>
<td>1. Verify that all necessary APIs are enabled, and the service account has the right permission to access the selected Agent Platform service. See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/access-control">Access control</a> .<br />
<br />
2. Agent Platform per-product, per-project service account (P4SA) is granted the necessary permission to access resources referenced in the input.</td>
</tr>
<tr class="even">
<td>404</td>
<td><code dir="ltr" translate="no">NOT_FOUND</code></td>
<td>No valid object is found from the designated URL.</td>
<td>Image file not found in the storage URL.</td>
<td>Check and fix the file location.</td>
</tr>
<tr class="odd">
<td>429</td>
<td><code dir="ltr" translate="no">RESOURCE_EXHAUSTED</code></td>
<td>Depending on the error message, the error could be caused by the following:<br />
<br />
1. API quota over the limit.<br />
<br />
2. Server overload due to shared server capacity.<br />
<br />
3. You've reached the daily limit for requests using <code dir="ltr" translate="no">logprobs</code> .</td>
<td>Gemini API exceeds request per minute limit.</td>
<td>1. Check <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Generative AI on Agent Platform quota limits</a> . If needed, apply for a higher quota.<br />
<br />
2. Retry after a few seconds. If the error persists after a prolonged period of time (hours), contact <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/support/getting-support">Agent Platform support</a> .<br />
<br />
3. Consider purchasing <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/error-code-429">Provisioned Throughput</a> .</td>
</tr>
<tr class="even">
<td>499</td>
<td><code dir="ltr" translate="no">CANCELLED</code></td>
<td>Request is cancelled by the client.</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>500</td>
<td><code dir="ltr" translate="no">UNKNOWN / INTERNAL</code></td>
<td>Server error due to overload or dependency failure.</td>
<td>Request is throttled, because the service is temporarily overloaded.</td>
<td>Retry after a few seconds. If the error persists after a prolonged period of time (hours), contact <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/support/getting-support">Agent Platform support</a> .</td>
</tr>
<tr class="even">
<td>503</td>
<td><code dir="ltr" translate="no">UNAVAILABLE</code></td>
<td>Service is temporarily unavailable.</td>
<td>Server isn't responding to the incoming requests.</td>
<td>The unavailable status might be temporary. However, if the error persists, contact <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/support/getting-support">Agent Platform support</a> .</td>
</tr>
<tr class="odd">
<td>504</td>
<td><code dir="ltr" translate="no">DEADLINE_EXCEEDED</code></td>
<td>The request didn't finish within the deadline. If the client sets a deadline shorter than the server's default deadline, it might cause 504 errors.</td>
<td>Client sets a deadline of 10 seconds, which is too short for the requests to finish.</td>
<td>Remove the deadline setting to use the server default, or set a longer deadline.</td>
</tr>
</tbody>
</table>

## Handle errors

Avoid spikes in traffic. Spikes are sudden and significant increases in the number of requests within a very short period of time. Sometimes, spikes in traffic might cause issues for quota enforcement and might increase the chance of server overloading.

Be careful about retrying an event. We recommend retrying no more than two times. The minimum delay is one second with subsequent requests backing up exponentially. For more information, see [Retry strategy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/retry-strategy) .

## What's next

  - Generative AI on Gemini Enterprise Agent Platform has some limitations. To learn more, see [Model limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai#limitations) .
  - Try a quickstart tutorial using [Gemini Enterprise Agent Platform Studio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-studio/quickstart) or the [Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) .
  - Explore pretrained models in [Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .
  - Learn about [quotas and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas) .
  - Learn about [pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
