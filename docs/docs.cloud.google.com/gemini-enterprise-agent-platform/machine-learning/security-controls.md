---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-controls
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-controls
title: Security controls for machine learning services
description: Learn about security controls for Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform implements Google Cloud security controls to help secure your models and training data. Some security controls aren't supported by Generative AI features in Gemini Enterprise Agent Platform. The following table lists the security controls available for Gemini Enterprise Agent Platform machine learning features.

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
<th></th>
<th style="text-align: center;"><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-controls#drz1">Data residency (at-rest) <sup>1</sup></a></th>
<th style="text-align: center;"><a href="https://docs.cloud.google.com/kms/docs/cmek">Customer-managed encryption key (CMEK)</a></th>
<th style="text-align: center;"><a href="https://docs.cloud.google.com/vpc-service-controls/docs/overview">VPC Service Controls<br />
(VPC-SC)</a></th>
<th style="text-align: center;"><a href="https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview">Access Transparency (AXT)</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Gemini Enterprise Agent Platform</td>
<td style="text-align: center;">✔</td>
<td style="text-align: center;">✔</td>
<td style="text-align: center;">✔</td>
<td style="text-align: center;">✔</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform RAG Engine</td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;">✔</td>
<td style="text-align: center;"></td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Vector Search 2</td>
<td style="text-align: center;">✔</td>
<td style="text-align: center;"></td>
<td style="text-align: center;">✔</td>
<td style="text-align: center;"></td>
</tr>
</tbody>
</table>

<sup>1</sup> Vertex AI Feature Store and Vertex Data Labeling don't meet data-at-rest commitments.

<span id="drz1">Learn more about Data residency by expanding</span> [General Service Terms](https://cloud.google.com/terms/service-terms#panel0-1) and reading **1. Data Location** .

## Learn more

  - Learn more about [Generative AI security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) .
