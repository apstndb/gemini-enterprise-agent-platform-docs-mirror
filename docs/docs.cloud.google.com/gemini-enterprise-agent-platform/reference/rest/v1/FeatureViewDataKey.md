---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureViewDataKey
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureViewDataKey
title: FeatureViewDataKey
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lookup key for a feature view.

Fields

`key_oneof` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`key` `string`

String key to use for lookup.

`compositeKey` `object ( `[`CompositeKey`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/FeatureViewDataKey#CompositeKey)` )`

The actual Entity id will be composed from this struct. This should match with the way id is defined in the FeatureView spec.

End of mutually exclusive fields.

**JSON representation**

```
{

  // key_oneof
  "key": string,
  "compositeKey": {
    object (CompositeKey)
  }
  // Union type
}
```

## CompositeKey

id that is comprised from several parts (columns).

Fields

`parts[]` `string`

Parts to construct Entity id. Should match with the same id columns as defined in FeatureView in the same order.

**JSON representation**

```
{
  "parts": [
    string
  ]
}
```
