---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/streamlit-genai-iap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/streamlit-genai-iap
title: Secure a generative AI app by using IAP
description: Learn how to deploy a generative AI app to Cloud Run and secure it with Identity-Aware Proxy (IAP)
data_source: docs.cloud.google.com
---

This tutorial shows you how to deploy a generative AI app to Cloud Run and secure it with Identity-Aware Proxy (IAP). IAP provides a central authorization layer for HTTPS applications deployed to Cloud Run. You can use IAP to adopt application-level or organization-level access control policies instead of using network-level firewalls.

Note that while it's also possible to use manual or third-party authentication to secure an app deployed to Cloud Run, we recommend using IAP for large volumes or multi-region traffic, to avoid disruptions in the app serving.

In this tutorial, you deploy an app that makes calls to the [Gemini API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/generateContent) . The app is based on the Streamlit framework.

## Prerequisites

This tutorial assumes that you're able to use the following tools and frameworks:

  - **Streamlit** : [Streamlit](https://streamlit.io/) is an open source app framework that lets you create and deploy data applications. It transforms data scripts into web apps by using Python.

  - **Git** : For this tutorial, you use a Git repository to manage the source code of your app. For more information about using Git, see the [Git documentation](https://git-scm.com/doc) .

### Google Cloud services

You must have a basic understanding of the following Google Cloud services:

  - **Generative AI on Gemini Enterprise Agent Platform** : Provides access to Google's LLMs so you can test, tune, and deploy them for use in your applications. [Learn more about Generative AI on Gemini Enterprise Agent Platform.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models)

  - **Cloud Run** : A managed compute platform that lets you deploy and run container images. You create a Cloud Run service to deploy your app. [Learn more about Cloud Run.](https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run)

  - **Cloud Build** : Executes your builds on Google Cloud. For this tutorial, you set up an automatic [Cloud Build trigger](https://docs.cloud.google.com/build/docs/triggers) to build and deploy your app to Cloud Run whenever you push your commits to the Git repository. [Learn more about Cloud Build.](https://docs.cloud.google.com/build/docs/overview)

  - **Cloud Load Balancing** : Helps distribute traffic across multiple instances of your app to achieve scalability. You create an Application Load Balancer to distribute the traffic to the app backend instances hosted on Cloud Run. Cloud Load Balancing is also a prerequisite for IAP. [Learn more about Cloud Load Balancing.](https://docs.cloud.google.com/load-balancing/docs/load-balancing-overview)

  - **Identity-Aware Proxy (IAP)** : You use IAP to create a central authorization layer to secure the app. IAP makes authentication and authorization checks that extend to linked Google Cloud services. IAP also supports and seamlessly integrates with Cloud Load Balancing, making it the most efficient security management option for this tutorial.
    
    To learn more about IAP, see [Identity-Aware Proxy overview](https://docs.cloud.google.com/iap/docs/concepts-overview) .
    
    To understand how IAP works with Cloud Run, see the [Cloud Run section of How IAP Works](https://docs.cloud.google.com/iap/docs/concepts-overview#how_iap_works) .

### Valid domain name

Additionally, you must have a valid domain name for provisioning a certificate, which is required to configure the load balancer.

## Tutorial pages

This tutorial has the following pages:

1.  [Set up your project and source repository.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/setup-environment)

2.  [Create a Cloud Run service.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/create-cloudrun-service)

3.  [Create a load balancer.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/create-loadbalancer)

4.  [Configure Identity-Aware Proxy (IAP).](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/configure-iap)

5.  [Test your IAP-secured app.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/view-app)

6.  [Clean up your project.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/clean-up)

Each page assumes that you've already completed the instructions from the previous pages of the tutorial.
