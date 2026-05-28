---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/migrate-google-ai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/migrate-google-ai
title: Migrate from Google AI Studio to Gemini Enterprise Agent Platform
description: Migrate your existing Gemini API in Gemini Enterprise Agent Platform code to Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

As your [Gemini API](https://ai.google.dev/gemini-api/docs) applications mature, you might find that you need a more expansive platform for building and deploying generative AI applications and solutions end-to-end. Gemini Enterprise Agent Platform provides a comprehensive ecosystem of tools to enable developers to harness the power of generative AI, from the initial stages of app development to app deployment, app hosting, and managing complex data at scale.

With Gemini Enterprise Agent Platform, you get access to a suite of Machine Learning Operations (MLOps) tools to streamline usage, deployment, and monitoring of AI models for efficiency and reliability. Additionally, integrations with databases, Development Operations (DevOps) tools, logging, monitoring, and IAM offer a comprehensive approach to managing the entire generative AI lifecycle.

## Differences between using the Gemini API on its own and Gemini Enterprise Agent Platform

The following table summarizes the main differences between the Gemini API and Gemini Enterprise Agent Platform to help you decide which option is right for your use case:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Feature</strong></th>
<th><strong>Gemini API</strong></th>
<th><strong>Gemini Enterprise Agent Platform</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Endpoint names</td>
<td><code dir="ltr" translate="no">generativelanguage.googleapis.com</code></td>
<td><code dir="ltr" translate="no">aiplatform.googleapis.com</code></td>
</tr>
<tr class="even">
<td>Sign up</td>
<td>Google Account</td>
<td>Google Cloud account (with terms agreement and billing)</td>
</tr>
<tr class="odd">
<td>Authentication</td>
<td>API Key or <a href="https://ai.google.dev/gemini-api/docs/oauth">OAuth</a> (if connected to Google Cloud project)</td>
<td>Google Cloud service account</td>
</tr>
<tr class="even">
<td>User interface playground</td>
<td>Google AI Studio</td>
<td>Vertex AI Studio</td>
</tr>
<tr class="odd">
<td>API &amp; SDK</td>
<td>Server and mobile/web client SDKs
<ul>
<li>Server: Python, Node.js, Go, Dart, ABAP</li>
<li>Mobile/Web client (via <a href="https://firebase.google.com/docs/ai-logic">Firebase AI Logic</a> ): Android (Kotlin/Java), Swift, Web, Flutter, and Unity</li>
</ul></td>
<td>Server and mobile/web client SDKs
<ul>
<li>Server: Python, Node.js, Go, Java, ABAP</li>
<li>Mobile/Web client (via <a href="https://firebase.google.com/docs/ai-logic">Firebase AI Logic</a> ): Android (Kotlin/Java), Swift, Web, Flutter, and Unity</li>
</ul></td>
</tr>
<tr class="even">
<td>No-cost usage of API &amp; SDK</td>
<td>Yes, <a href="https://ai.google.dev/gemini-api/docs/billing#is-Gemini-free-in-EEA-UK-CH">where applicable</a></td>
<td>$300 Google Cloud credit for new users</td>
</tr>
<tr class="odd">
<td>Quota (requests per minute)</td>
<td>Varies based on model and pricing plan (see <a href="https://ai.google.dev/pricing">detailed information</a> )</td>
<td>Varies based on model and region (see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">detailed information</a> )</td>
</tr>
<tr class="even">
<td>Commercial terms</td>
<td>Standard Terms of Service. Doesn't count toward Google Cloud commitments. All customers pay the same price.</td>
<td>Enterprise-ready terms for data processing, security, and privacy. Counts toward Google Cloud commitments. Custom contracts and discounts available for large volume workloads (contact sales).</td>
</tr>
<tr class="odd">
<td>Enterprise support and SLA</td>
<td>No enterprise-level support or Service Level Agreements (SLAs).</td>
<td>24/7 enterprise-level support and SLAs for service availability.</td>
</tr>
<tr class="even">
<td>Compliance and governance</td>
<td>No compliance certifications (for example, HIPAA, SOC2). Regulated customers should use Gemini Enterprise Agent Platform instead.</td>
<td>Supports compliance with certifications like HIPAA and SOC2. Provides data residency, customer-managed encryption keys, and Access Transparency.</td>
</tr>
<tr class="odd">
<td>Security</td>
<td>API key authentication.</td>
<td>Authentication using IAM (service accounts, OAuth) for increased security. Enhanced security through Virtual Private Cloud.</td>
</tr>
<tr class="even">
<td>Infrastructure</td>
<td>Global endpoint.</td>
<td>Global endpoint and regional endpoints.</td>
</tr>
<tr class="odd">
<td>Dedicated capacity</td>
<td>No access to dedicated capacity.</td>
<td>Access to Provisioned Throughput for dedicated capacity.</td>
</tr>
<tr class="even">
<td>Model access</td>
<td>Access to Google's models.</td>
<td>Access to a broad selection of Google and third-party models in the Model Garden.</td>
</tr>
<tr class="odd">
<td>Google model improvement</td>
<td><ul>
<li><strong>Free tier</strong> : Your prompts and responses may be used to improve Google products.</li>
<li><strong>Paid tier</strong> : Your prompts, responses, and data are never used to improve Google products.</li>
</ul></td>
<td>Your prompts, responses, and data are never used to improve Google products.</td>
</tr>
<tr class="even">
<td>Advanced features</td>
<td>Standard feature set.</td>
<td>Full support for features like model tuning and a wider variety of embedding models.</td>
</tr>
<tr class="odd">
<td>MLOps</td>
<td>No</td>
<td>Full MLOps on Gemini Enterprise Agent Platform (examples: model evaluation, Model Monitoring, Model Registry)</td>
</tr>
</tbody>
</table>

## Enable APIs

To use Gemini Enterprise Agent Platform, you must enable the Gemini Enterprise Agent Platform API in your Google Cloud project:

Additionally, to build and deploy agents using features like Agent Runtime on Gemini Enterprise Agent Platform or Agent Studio on Gemini Enterprise Agent Platform, you might need to enable the following APIs:

  - [Cloud Storage API](https://console.cloud.google.com/apis/library/storage.googleapis.com)
  - [Cloud Logging API](https://console.cloud.google.com/apis/library/logging.googleapis.com)
  - [Cloud Monitoring API](https://console.cloud.google.com/apis/library/monitoring.googleapis.com)
  - [Cloud Trace API](https://console.cloud.google.com/apis/library/cloudtrace.googleapis.com)
  - [Cloud Resource Manager API](https://console.cloud.google.com/apis/library/cloudresourcemanager.googleapis.com)
  - [Artifact Registry API](https://console.cloud.google.com/apis/library/artifactregistry.googleapis.com)

Other features, such as Agent Gateway or integrations with other Google services like Google Workspace, might require enabling additional APIs. To enable other APIs, visit the [API Library](https://console.cloud.google.com/apis/library) in the Google Cloud console.

## Migration steps

The following sections cover the steps required to migrate your Gemini API code to Gemini Enterprise Agent Platform. These steps assume you have prompt data from Google AI Studio saved in Google Drive.

When migrating to Gemini Enterprise Agent Platform:

  - You can use your existing Google Cloud project (the same one you used to generate your Gemini API key) or you can create a new [Google Cloud project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects) .
  - Supported regions might differ between the Gemini API and Gemini Enterprise Agent Platform. See the list of [supported regions for generative AI on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .
  - Any models you created in Google AI Studio need to be retrained in Gemini Enterprise Agent Platform.

### 1\. Migrate your prompts to Vertex AI Studio

Your Google AI Studio prompt data is saved in a Google Drive folder. This section shows how to migrate your prompts to Vertex AI Studio.

1.  Open [Google Drive](https://drive.google.com) .

2.  Navigate to the **AI\_Studio** folder where the prompts are stored. ![Location of prompts in Google Drive](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/migrate/images/ai-studio-drive.png)

3.  Download your prompts from Google Drive to a local directory.
    
    > **Note:** Prompts downloaded from Google Drive are in the text ( `txt` ) format. Before you upload them to Vertex AI Studio, change the file extensions from `.txt` to `.json` to convert them to JSON files.

4.  Open [Vertex AI Studio](https://console.cloud.google.com/agent-platform/generative) in the Google Cloud console.

5.  In the **Gemini Enterprise Agent Platform** menu, click **Recents \> View all** to open the **Prompt management** menu.

6.  Click download **Import prompt** .

7.  Next to the **Prompt file** field, click **Browse** and select a prompt from your local directory.
    
    To upload prompts in bulk, you must manually combine your prompts into a single JSON file.

8.  Click **Upload** .

### 2\. Upload training data to Vertex AI Studio

To migrate your training data to Gemini Enterprise Agent Platform, you need to upload your data to a Cloud Storage bucket. For more information, see [Introduction to tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models) .

### 3\. Delete unused API Keys

If you no longer need to use your Gemini API key for the Gemini Developer API, then follow security best practices and delete it.

To delete an API key:

1.  Open the [Google Cloud API Credentials](https://console.cloud.google.com/apis/credentials) page.

2.  Find the API key that you want to delete and click the **Actions** icon.

3.  Select **Delete API key** .

4.  In the **Delete credential** modal, select **Delete** .
    
    Deleting an API key takes a few minutes to propagate. After propagation completes, any traffic using the deleted API key is rejected.

> **Important:** If you delete a key that's still used in production and need to recover it, see [`gcloud beta services api-keys undelete`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/services/api-keys/undelete) .

## What's next

  - Try a quickstart tutorial using [Vertex AI Studio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quickstart-sdks/quickstart) or the [Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quickstart-sdks/quickstart-multimodal) .
