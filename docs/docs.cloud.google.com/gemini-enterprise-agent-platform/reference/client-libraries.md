---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/client-libraries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/client-libraries
title: Install the Gemini Enterprise Agent Platform client libraries
description: Install a Gemini Enterprise Agent Platform client library and set up authentication for using the library in a local development environment.
data_source: docs.cloud.google.com
---

Client libraries provide an optimized developer experience for calling the Agent Platform API. The client libraries use each supported language's natural conventions and reduce boilerplate code that you have to write. The following guide explains how to install the libraries and set up authentication for using them in a local development environment.

## Before you begin

1.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

## Client libraries

Agent Platform provides client libraries for the following languages. Select the language that you want to use.

### C\#

Run the following command to add the `Google.Cloud.AIPlatform.V1` package reference to your project file:

    dotnet add package Google.Cloud.AIPlatform.V1

### Try code samples

To view or get individual code samples, go to the [dotnet-aiplatform](https://github.com/GoogleCloudPlatform/dotnet-docs-samples/tree/main/aiplatform/api) GitHub repository.

### Client library documentation

For more information, view the [Agent Platform .NET client library documentation](https://docs.cloud.google.com/dotnet/docs/reference/Google.Cloud.AIPlatform.V1/latest) .

### Java

If you are using Maven, add the following to your dependencies:

    <dependency>
      <groupId>com.google.cloud</groupId>
      <artifactId>google-cloud-aiplatform</artifactId>
      <version>3.35.0</version>
    </dependency>

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

    compile 'com.google.cloud:google-cloud-aiplatform:3.35.0'

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

    libraryDependencies += "com.google.cloud" % "google-cloud-aiplatform" % "3.35.0"

### Try code samples

To view or get individual code samples, go to the [java-aiplatform](https://github.com/GoogleCloudPlatform/java-docs-samples/tree/main/aiplatform/src/main/java/aiplatform) GitHub repository.

### Client library documentation

For more information, view the [Agent Platform client library for Java documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/overview) .

### Node.js

Before installing the library, prepare your environment for [Node.js development](https://docs.cloud.google.com/nodejs/docs/setup) .

Run the following command in your environment to install the client library:

    npm install @google-cloud/aiplatform

### Client library documentation

For more information, view the [Agent Platform client library for Node.js documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

### Python

The Gemini Enterprise Agent Platform Python client library is installed when you install the Vertex AI SDK for Python.

For more information, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/install-sdk) .

### Go

Before installing the library, [prepare your environment for Go development](https://docs.cloud.google.com/go/docs/setup) .

### Review available packages

Review the available Gemini Enterprise Agent Platform API Go packages to determine which package best meets your project's needs:

  - Package [**cloud.google.com/go/vertexai**](https://pkg.go.dev/cloud.google.com/go/vertexai) ( **recommended** )
    
    `vertexai` is a human authored package that provides access to common capabilities and features.
    
    This package is recommended as the starting point for most developers building with the Gemini Enterprise Agent Platform API. To access capabilities and features not yet covered by this package, use the auto-generated `aiplatform` instead.

  - Package [**cloud.google.com/go/aiplatform**](https://pkg.go.dev/cloud.google.com/go/aiplatform)
    
    `aiplatform` is an auto-generated package.
    
    This package is intended for projects that require access to Gemini Enterprise Agent Platform API capabilities and features not yet provided by the human authored `vertexai` package.

### Installation

  - Package [**cloud.google.com/go/vertexai**](https://pkg.go.dev/cloud.google.com/go/vertexai) ( **recommended** )
    
    Run the following command to install this package in your environment:
    
        go get cloud.google.com/go/vertexai

  - Package [**cloud.google.com/go/aiplatform**](https://pkg.go.dev/cloud.google.com/go/aiplatform)
    
    Run the following command to install this package in your environment:
    
        go get cloud.google.com/go/aiplatform

### Samples

  - Package [**cloud.google.com/go/vertexai**](https://pkg.go.dev/cloud.google.com/go/vertexai) ( **recommended** )
    
    Samples for using this package are available, in the `golang-samples` GitHub repository in the top-level `vertexai` directory:
    
    [github.com/GoogleCloudPlatform/golang-samples](https://github.com/GoogleCloudPlatform/golang-samples/) \> [vertexai](https://github.com/GoogleCloudPlatform/golang-samples/tree/main/vertexai)

  - Package [**cloud.google.com/go/aiplatform**](https://pkg.go.dev/cloud.google.com/go/aiplatform)
    
    Samples for using this package are available, in the `golang-samples` GitHub repository in the top-level `aiplatform` directory:
    
    [github.com/GoogleCloudPlatform/golang-samples](https://github.com/GoogleCloudPlatform/golang-samples/) \> [aiplatform](https://github.com/GoogleCloudPlatform/golang-samples/tree/main/aiplatform)

### Client library documentation

For more information about the library, see the Agent Platform client library for Go documentation:

  - Package [**cloud.google.com/go/vertexai**](https://pkg.go.dev/cloud.google.com/go/vertexai) ( **recommended** )
    
      - Gemini Enterprise Agent Platform `cloud.google.com/go/vertexai` [API reference](https://docs.cloud.google.com/go/docs/reference/cloud.google.com/go/vertexai/latest)

  - Package [**cloud.google.com/go/aiplatform**](https://pkg.go.dev/cloud.google.com/go/aiplatform)
    
      - Gemini Enterprise Agent Platform `cloud.google.com/go/aiplatform` v1 [API reference](https://docs.cloud.google.com/go/docs/reference/cloud.google.com/go/aiplatform/latest/apiv1)
      - Gemini Enterprise Agent Platform `cloud.google.com/go/aiplatform` v1beta1 [API reference](https://docs.cloud.google.com/go/docs/reference/cloud.google.com/go/aiplatform/latest/apiv1beta1)
