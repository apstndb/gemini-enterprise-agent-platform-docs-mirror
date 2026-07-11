---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries
title: Google Gen AI libraries
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page provides information on downloading and installing the latest libraries for the Gemini API. If you're new to the Gemini API, get started with the [API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/quickstart) .

## Important note about google-genai libraries

We've recently launched a new set of libraries that provide a more consistent and streamlined experience for accessing Google's generative AI models across different Google services.

Gemini Enterprise Agent Platform libraries are only supported on Gemini Enterprise Agent Platform.

## Key library updates

<table>
<thead>
<tr class="header">
<th>Language</th>
<th>Gemini Enterprise Agent Platform library</th>
<th>New library (Recommended)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://ai.google.dev/gemini-api/docs/libraries#python"><strong>Python</strong></a></td>
<td><a href="https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform"><code dir="ltr" translate="no">google-cloud-aiplatform</code></a><br />
GenerativeModel Module Deprecated in May 2026</td>
<td><a href="https://github.com/googleapis/python-genai"><code dir="ltr" translate="no">google-genai</code></a></td>
</tr>
<tr class="even">
<td><a href="https://ai.google.dev/gemini-api/docs/libraries#go"><strong>Go</strong></a></td>
<td><a href="https://pkg.go.dev/cloud.google.com/go/vertexai"><code dir="ltr" translate="no">cloud.google.com/vertexai</code></a><br />
Deprecated in May 2026</td>
<td><a href="http://google.golang.org/genai"><code dir="ltr" translate="no">google.golang.org/genai</code></a></td>
</tr>
<tr class="odd">
<td><a href="https://ai.google.dev/gemini-api/docs/libraries#javascript"><strong>JavaScript and TypeScript</strong></a></td>
<td><a href="https://www.npmjs.com/package/@google-cloud/vertexai"><code dir="ltr" translate="no">@google-cloud/vertexai</code></a><br />
Deprecated in May 2026</td>
<td><a href="https://www.npmjs.com/package/@google/genai"><code dir="ltr" translate="no">@google/genai</code></a><br />
Available in <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries#install-javascript">Preview</a></td>
</tr>
<tr class="even">
<td><a href="https://ai.google.dev/gemini-api/docs/libraries#java"><strong>Java</strong></a></td>
<td><a href="https://mvnrepository.com/artifact/com.google.cloud/google-cloud-vertexai"><code dir="ltr" translate="no">google-cloud-vertexai</code></a><br />
Deprecated in May 2026</td>
<td><a href="https://github.com/googleapis/java-genai"><code dir="ltr" translate="no">java-genai</code></a><br />
Available in <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries#install-java">Preview</a></td>
</tr>
<tr class="odd">
<td><a href="https://ai.google.dev/gemini-api/docs/libraries#csharp"><strong>.NET</strong></a></td>
<td><a href="https://www.nuget.org/packages/Google.Cloud.AIPlatform.V1"><code dir="ltr" translate="no">Google.Cloud.AIPlatform.V1</code></a><br />
Deprecated in May 2026</td>
<td><a href="https://github.com/googleapis/dotnet-genai"><code dir="ltr" translate="no">Google.GenAI</code></a><br />
Available in <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries#install-dotnet">Preview</a></td>
</tr>
</tbody>
</table>

Users are encouraged to start with the new library and migrate from previous libraries.

## Install a library

The following examples can help you get started in various programming languages.

Python Go JavaScript/TypeScript Java .NET

Install our [Python library](https://pypi.org/project/google-genai) by running:

``` 
    pip install google-genai
  
```

Install our [Go library](https://pkg.go.dev/google.golang.org/genai) by running:

``` 
    go get google.golang.org/genai
  
```

Install our [JavaScript/TypeScript library](https://www.npmjs.com/package/@google/genai) by running:

``` 
    npm install @google/genai
  
```

The [new JavaScript and TypeScript library](https://ai.google.dev/gemini-api/docs/libraries) is available in [*preview*](https://cloud.google.com/products#product-launch-stages) , which means it may not be feature complete and that we may need to introduce breaking changes.

However, we recommend that you start using the [new SDK](https://www.npmjs.com/package/@google/genai) instead of the previous, deprecated version as long as you're comfortable with these caveats.

Install our [Java library](https://github.com/googleapis/java-genai) by adding the dependencies in Maven:

``` 
<dependencies>
  <dependency>
    <groupId>com.google.genai</groupId>
    <artifactId>google-genai</artifactId>
    <version>0.8.0</version>
  </dependency>
</dependencies>
  
```

The new Java library is available in [*preview*](https://cloud.google.com/products#product-launch-stages) , which means it may not be feature complete and that we may need to introduce breaking changes.

However, we recommend that you start using the [new SDK](https://github.com/googleapis/java-genai) instead of the previous, deprecated version as long as you're comfortable with these caveats.

Install our [.NET library](https://www.nuget.org/packages/Google.GenAI) by running:

``` 
    dotnet add package Google.GenAI
  
```

The new .NET library is available in [*preview*](https://cloud.google.com/products#product-launch-stages) , which means it may not be feature complete and that we may need to introduce breaking changes.

However, we recommend that you start using the [new SDK](https://github.com/googleapis/dotnet-genai) instead of the previous, deprecated version as long as you're comfortable with these caveats.
