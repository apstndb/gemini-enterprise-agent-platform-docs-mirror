---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelEulaAcceptance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PublisherModelEulaAcceptance
title: PublisherModelEulaAcceptance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for \[ModelGardenService.UpdatePublisherModelEula\]\[\].

Fields

`projectNumber` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The project number requesting access for named model.

`publisherModel` `string`

The publisher model resource name.

`publisherModelEulaAcked` `boolean`

The EULA content acceptance status.

**JSON representation**

```
{
  "projectNumber": string,
  "publisherModel": string,
  "publisherModelEulaAcked": boolean
}
```
