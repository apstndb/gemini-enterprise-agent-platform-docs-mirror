---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-controls
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-controls
title: Security controls for machine learning services
description: Learn about security controls for Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform implements Google Cloud security controls to help secure your models and training data. Some security controls aren't supported by Generative AI features in Gemini Enterprise Agent Platform. The following table lists the security controls available for Gemini Enterprise Agent Platform machine learning features.

|                                  | [Data residency (at-rest) <sup>1</sup>](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/security-controls#drz1) | [Customer-managed encryption key (CMEK)](https://docs.cloud.google.com/kms/docs/cmek) | [VPC Service Controls (VPC-SC)](https://docs.cloud.google.com/vpc-service-controls/docs/overview) | [Access Transparency (AXT)](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview) |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| Gemini Enterprise Agent Platform | ✔                                                                                                                                               | ✔                                                                                     | ✔                                                                                                 | ✔                                                                                                              |
| RAG Engine                       |                                                                                                                                                 |                                                                                       | ✔                                                                                                 |                                                                                                                |
| Vector Search                    | ✔                                                                                                                                               |                                                                                       | ✔                                                                                                 |                                                                                                                |

<sup>1</sup> Vertex AI Feature Store and Vertex Data Labeling don't meet data-at-rest commitments.

Learn more about Data residency by expanding [General Service Terms](https://cloud.google.com/terms/service-terms#panel0-1) and reading **1. Data Location** .

## Learn more

- Learn more about [Generative AI security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) .
