---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-gateway-regulatory-compliance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-gateway-regulatory-compliance
title: Regulatory support in Agent Gateway
description: This document describes the features and APIs in Agent Gateway that help you align Agent Gateway with your regulatory requirements. This document assumes that you're using [Assured Workloads](/assured-workloads/docs/overview).
data_source: docs.cloud.google.com
---

This document describes the features, configurations and APIs in Agent Gateway that align with the controls for supported control packages. This document assumes that you're using [Assured Workloads](https://docs.cloud.google.com/assured-workloads/docs/overview) .

Show All Data Boundary for ITAR

## Data Boundary for ITAR

### Supported services

The following table lists the Agent Gateway APIs and versions that meet the requirements of Data Boundary for ITAR.

| Service                        | Version | Status    |
|--------------------------------|---------|-----------|
| networkservices.googleapis.com | v1      | SUPPORTED |

### Compliance supported regions

Agent Gateway is available for Data Boundary for ITAR in the following Google Cloud regions:

- us-central1
- us-central2
- us-east1
- us-east4
- us-east5
- us-south1
- us-west1
- us-west2
- us-west3
- us-west4

### Fields not intended for Sensitive data

The following table provides an illustrative list of field categories and specific fields that aren't suitable for sensitive information. To maintain compliance, avoid placing protected data in these fields. For a complete list, contact your Google Cloud representative.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="header">
<th>Category</th>
<th>Fields</th>
</tr>

<tr class="odd">
<td>Filtering and pagination</td>
<td><ul>
<li><code>filter</code></li>
<li><code>pageToken</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Gateway network configuration</td>
<td><ul>
<li><code>agentGateway.agentConnectivityTemplate</code></li>
<li><code>agentGateway.networkConfig.dnsPeeringConfig.domains</code></li>
<li><code>agentGateway.networkConfig.dnsPeeringConfig.targetNetwork</code></li>
<li><code>agentGateway.networkConfig.dnsPeeringConfig.targetProject</code></li>
<li><code>agentGateway.networkConfig.egress.networkAttachment</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Gateway proxy and registry references</td>
<td><ul>
<li><code>agentGateway.registries</code></li>
<li><code>agentGateway.selfManaged.resourceUri</code></li>
<li><code>agentGateway.selfManaged.resourceUris</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Resource descriptions and metadata</td>
<td><ul>
<li><code>agentConnectivityTemplate.description</code></li>
<li><code>agentConnectivityTemplate.etag</code></li>
<li><code>agentGateway.description</code></li>
<li><code>agentGateway.etag</code></li>
<li><code>etag</code></li>
<li><code>updateMask.paths</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Resource identification</td>
<td><ul>
<li><code>agentConnectivityTemplate.name</code></li>
<li><code>agentConnectivityTemplateId</code></li>
<li><code>agentGateway.name</code></li>
<li><code>agentGatewayId</code></li>
<li><code>name</code></li>
<li><code>parent</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Resource labels</td>
<td><ul>
<li><code>agentConnectivityTemplate.labels.key</code></li>
<li><code>agentConnectivityTemplate.labels.value</code></li>
<li><code>agentGateway.labels.key</code></li>
<li><code>agentGateway.labels.value</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>Template network configuration</td>
<td><ul>
<li><code>agentConnectivityTemplate.egressNetworkConfig.dnsPeeringConfig.domain</code></li>
<li><code>agentConnectivityTemplate.egressNetworkConfig.dnsPeeringConfig.domains</code></li>
<li><code>agentConnectivityTemplate.egressNetworkConfig.dnsPeeringConfig.targetNetwork</code></li>
<li><code>agentConnectivityTemplate.egressNetworkConfig.networkAttachment</code></li>
<li><code>agentConnectivityTemplate.egressNetworkConfig.tlsConfig.trustConfig</code></li>
<li><code>agentConnectivityTemplate.egressNetworkConfig.trustConfig</code></li>
</ul></td>
</tr>
</tbody>
</table>

  

## What's next

- Learn more about [compliance in Google Cloud](https://cloud.google.com/compliance) .
