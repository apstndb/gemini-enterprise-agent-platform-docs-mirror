---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TensorboardBlob
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TensorboardBlob
title: TensorboardBlob
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

One blob (e.g, image, graph) viewable on a blob metric plot.

Fields

`id` `string`

Output only. A URI safe key uniquely identifying a blob. Can be used to locate the blob stored in the Cloud Storage bucket of the consumer project.

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. The bytes of the blob is not present unless it's returned by the ReadTensorboardBlobData endpoint.

A base64-encoded string.

**JSON representation**

```
{
  "id": string,
  "data": string
}
```
