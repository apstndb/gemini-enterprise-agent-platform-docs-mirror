---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult
title: GoogleMapsResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The result of the Google Maps.

Fields

`places[]` `object ( `[`Places`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult#Places)` )`

The places that were found.

`widgetContextToken` `string`

Resource name of the Google Maps widget context token.

**JSON representation**

```
{
  "places": [
    {
      object (Places)
    }
  ],
  "widgetContextToken": string
}
```

## Places

Fields

`placeId` `string`

The id of the place, in `places/{placeId}` format.

`name` `string`

title of the place.

`url` `string`

URI reference of the place.

`reviewSnippets[]` `object ( `[`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReviewSnippet)` )`

Snippets of reviews that are used to generate answers about the features of a given place in Google Maps.

**JSON representation**

```
{
  "placeId": string,
  "name": string,
  "url": string,
  "reviewSnippets": [
    {
      object (ReviewSnippet)
    }
  ]
}
```
