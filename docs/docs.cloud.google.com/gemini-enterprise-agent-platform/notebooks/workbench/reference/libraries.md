---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/libraries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/libraries
title: Agent Platform Workbench client libraries
description: Start writing code for Agent Platform Workbench in C++, C#, Go, Java, Node.js, PHP, Python, Ruby.
data_source: docs.cloud.google.com
---

This page shows how to get started with the Cloud Client Libraries for the Notebooks API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](https://docs.cloud.google.com/apis/docs/client-libraries-explained) .

<span id="installing_the_client_library"></span>

## Install the client library

### C++

See the [GitHub `README`](https://github.com/googleapis/google-cloud-cpp/blob/main/README.md) for details about this client library's requirements and to install dependencies.

### C\#

    Install-Package Google.Cloud.Notebooks.V1 -Pre

For more information, see [Setting Up a C\# Development Environment](https://docs.cloud.google.com/dotnet/docs/setup) .

### Go

    go get cloud.google.com/go/notebooks

For more information, see [Setting Up a Go Development Environment](https://docs.cloud.google.com/go/docs/setup) .

### Java

If you are using [Maven](https://maven.apache.org/) , add the following to your `pom.xml` file. For more information about BOMs, see [The Google Cloud Platform Libraries BOM](https://cloud.google.com/java/docs/bom) .

    <dependencyManagement>
      <dependencies>
        <dependency>
          <groupId>com.google.cloud</groupId>
          <artifactId>libraries-bom</artifactId>
          <version>26.83.0</version>
          <type>pom</type>
          <scope>import</scope>
        </dependency>
      </dependencies>
    </dependencyManagement>
    
    <dependencies>
      <dependency>
        <groupId>com.google.cloud</groupId>
        <artifactId>google-cloud-notebooks</artifactId>
      </dependency>
    </dependencies>

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

    implementation 'com.google.cloud:google-cloud-notebooks:1.90.0'

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

    libraryDependencies += "com.google.cloud" % "google-cloud-notebooks" % "1.90.0"

For more information, see [Setting Up a Java Development Environment](https://docs.cloud.google.com/java/docs/setup) .

### Node.js

    npm install @google-cloud/notebooks

For more information, see [Setting Up a Node.js Development Environment](https://docs.cloud.google.com/nodejs/docs/setup) .

### PHP

    composer require google/cloud

For more information, see [Using PHP on Google Cloud](https://docs.cloud.google.com/php/docs) .

### Python

**Mac/Linux**

    pip install virtualenv
    virtualenv ENVIRONMENT_NAME
    source ENVIRONMENT_NAME/bin/activate
    ENVIRONMENT_NAME/bin/pip install google-cloud-notebooks

**Windows**

    pip install --upgrade google-cloud-notebooks
    pip install virtualenv
    virtualenv ENVIRONMENT_NAME
    ENVIRONMENT_NAME\Scripts\activate
    ENVIRONMENT_NAME\Scripts\pip.exe install google-cloud-notebooks

For more information, see [Setting Up a Python Development Environment](https://docs.cloud.google.com/python/docs/setup) .

### Ruby

    gem install google-cloud-notebooks

For more information, see [Setting Up a Ruby Development Environment](https://docs.cloud.google.com/ruby/docs/setup) .

<span id="setting_up_authentication"></span>

## Set up authentication

To authenticate calls to Google Cloud APIs, client libraries support [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) ; the libraries look for credentials in a set of defined locations and use those credentials to authenticate requests to the API. With ADC, you can make credentials available to your application in a variety of environments, such as local development or production, without needing to modify your application code.

For production environments, the way you set up ADC depends on the service and context. For more information, see [Set up Application Default Credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc) .

For a local development environment, you can set up ADC with the credentials that are associated with your Google Account:

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI. After installation, [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the Google Cloud CLI by running the following command:
    
        gcloud init
    
    If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

2.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .
    
    A sign-in screen appears. After you sign in, your credentials are stored in the [local credential file used by ADC](https://docs.cloud.google.com/docs/authentication/application-default-credentials#personal) .

<span id="using_the_client_library"></span>

## Use the client library

The following examples show how to use the client library in some of the available languages.

### C++

    // Copyright 2022 Google LLC
    //
    // Licensed under the Apache License, Version 2.0 (the "License");
    // you may not use this file except in compliance with the License.
    // You may obtain a copy of the License at
    //
    // https://www.apache.org/licenses/LICENSE-2.0
    //
    // Unless required by applicable law or agreed to in writing, software
    // distributed under the License is distributed on an "AS IS" BASIS,
    // WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    // See the License for the specific language governing permissions and
    // limitations under the License.
    
    //! [all]
    #include "google/cloud/notebooks/v2/notebook_client.h"
    #include "google/cloud/location.h"
    #include <iostream>
    
    int main(int argc, char* argv[]) try {
      if (argc != 3) {
        std::cerr << "Usage: " << argv[0] << " project-id location-id\n";
        return 1;
      }
    
      auto const location = google::cloud::Location(argv[1], argv[2]);
    
      namespace notebooks = ::google::cloud::notebooks_v2;
      auto client = notebooks::NotebookServiceClient(
          notebooks::MakeNotebookServiceConnection());
    
      for (auto i : client.ListInstances(location.FullName())) {
        if (!i) throw std::move(i).status();
        std::cout << i->DebugString() << "\n";
      }
    
      return 0;
    } catch (google::cloud::Status const& status) {
      std::cerr << "google::cloud::Status thrown: " << status << "\n";
      return 1;
    }
    //! [all]

### Node.js

    // Copyright 2026 Google LLC
    //
    // Licensed under the Apache License, Version 2.0 (the "License");
    // you may not use this file except in compliance with the License.
    // You may obtain a copy of the License at
    //
    //      http://www.apache.org/licenses/LICENSE-2.0
    //
    // Unless required by applicable law or agreed to in writing, software
    // distributed under the License is distributed on an "AS IS" BASIS,
    // WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    // See the License for the specific language governing permissions and
    // limitations under the License.
    
    'use strict';
    
    async function main(projectId, location) {
      /**
       * TODO(developer): Uncomment these variables before running the sample.
       */
      // const projectId = 'my-project';
      // const location = 'global';
    
      // Imports the Google Cloud Some API library
      const {NotebookServiceClient} = require('@google-cloud/notebooks');
      const client = new NotebookServiceClient();
      async function listInstances() {
        const [instances] = await client.listInstances({
          parent: `projects/${projectId}/locations/${location}`,
        });
        for (const instance of instances) {
          console.info(`instance: ${instance.name}`);
        }
      }
      listInstances();
    }
    
    main(...process.argv.slice(2));
    process.on('unhandledRejection', err => {
      console.error(err.message);
      process.exitCode = 1;
    });

<span id="additional_resources"></span>

## Additional resources

### C++

The following list contains links to more resources related to the client library for C++:

  - [API reference](https://docs.cloud.google.com/cpp/docs/reference/notebooks/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-cpp/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D%5Bc%2B%2B%5D)
  - [Source code](https://github.com/googleapis/google-cloud-cpp)

### C\#

The following list contains links to more resources related to the client library for C\#:

  - [API reference](https://docs.cloud.google.com/dotnet/docs/reference/Google.Cloud.Notebooks.V1/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-dotnet/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bc%23%5D)
  - [Source code](https://github.com/googleapis/google-cloud-dotnet)

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://pkg.go.dev/cloud.google.com/go/notebooks)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](https://docs.cloud.google.com/java/docs/reference/google-cloud-notebooks/latest/overview)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-java/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/google-cloud-java)

### Node.js

The following list contains links to more resources related to the client library for Node.js:

  - [API reference](https://docs.cloud.google.com/nodejs/docs/reference/notebooks/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-node/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bnode.js%5D)
  - [Source code](https://github.com/googleapis/google-cloud-node)

### PHP

The following list contains links to more resources related to the client library for PHP:

  - [API reference](https://docs.cloud.google.com/php/docs/reference/cloud-notebooks/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bphp%5D)
  - [Source code](https://github.com/googleapis/google-cloud-php)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](https://docs.cloud.google.com/python/docs/reference/notebooks/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-python/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/google-cloud-python)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

  - [API reference](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-notebooks/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
  - [`  ` on Stack Overflow](https://stackoverflow.com/search?q=%5B%5D+%5Bruby%5D)
  - [Source code](https://github.com/googleapis/google-cloud-ruby)
