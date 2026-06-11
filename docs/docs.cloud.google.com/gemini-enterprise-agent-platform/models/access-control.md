---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/access-control
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/access-control
title: Access control
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

To use the generative AI features on Gemini Enterprise Agent Platform, the principals (for example, users, groups, and [service accounts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) ) in your project need to be granted the appropriate IAM role. You can also create custom roles to grant a user-defined set of permissions to a principal. This page shows you the applicable IAM roles to grant and the specific permissions needed for each operation so you can create custom roles.

## Predefined roles

You can grant the users or groups in your project one of the following predefined roles to give them access to the generative AI features on Gemini Enterprise Agent Platform:

  - [Gemini Enterprise Agent Platform Administrator ( `roles/aiplatform.admin` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.admin)
  - [Gemini Enterprise Agent Platform User ( `roles/aiplatform.user` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.user)

To learn more about Gemini Enterprise Agent Platform IAM roles, see [Gemini Enterprise Agent Platform access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .

## Permissions

The following table maps generative AI operations to the permissions required for the operation. If you need fine-grained access control, you can refer to these mappings to create custom roles.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operation</th>
<th>Permissions needed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Make prompt requests</td>
<td><ul>
<li><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Save, view, update, and delete prompts in Vertex AI Studio</td>
<td><ul>
<li><code dir="ltr" translate="no">aiplatform.datasets.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Model tuning</td>
<td><ul>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.*</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.*</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.upload</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">storage.objects.create</code></li>
<li><code dir="ltr" translate="no">storage.objects.update</code></li>
<li><code dir="ltr" translate="no">storage.objects.get</code></li>
<li><code dir="ltr" translate="no">storage.objects.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

To learn more about Gemini Enterprise Agent Platform IAM permissions, see [IAM permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/iam-permissions) .

## What's next

Guide

### [Enable Data Access audit logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/enable-audit-logs)

Enable Data Access audit logs in Agent Platform so that you can monitor usage of your model endpoints.

Guide

### [Control access with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control)

Learn how to use Identity and Access Management (IAM) to manage access to Agent Platform resources.

Overview

### [Introduction to tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3)

Learn how to tune a model by providing a training dataset that contains a set of examples of specific downstream tasks.

Overview

### [Responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai)

Learn about some of the limitations to generative AI and recommended practices for using generative AI.
