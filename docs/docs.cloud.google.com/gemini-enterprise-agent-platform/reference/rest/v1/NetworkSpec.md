---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NetworkSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NetworkSpec
title: NetworkSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Network spec.

Fields

`enableInternetAccess` `boolean`

Whether to enable public internet access. Default false.

`network` `string`

The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)

`subnetwork` `string`

The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}`

**JSON representation**

```
{
  "enableInternetAccess": boolean,
  "network": string,
  "subnetwork": string
}
```
