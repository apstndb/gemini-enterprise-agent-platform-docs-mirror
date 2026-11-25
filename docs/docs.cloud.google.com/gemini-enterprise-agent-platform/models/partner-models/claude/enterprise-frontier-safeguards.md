---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/enterprise-frontier-safeguards
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/enterprise-frontier-safeguards
title: Enterprise Frontier Safeguards for Claude
description: Learn how {{dynamic_data.site_values.cloud_name}} supports Anthropic's Enterprise Frontier Safeguards (EFS) for Claude models, including Legacy ZDR and EFS ZDR with customer-managed storage and encryption.
data_source: docs.cloud.google.com
---

> **Preview — Customer-managed storage and encryption**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** Claude models aren't a Google product, and their availability on Google Cloud is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . EFS eligibility, approval, and program rules are governed by your applicable agreement with Anthropic.

[Enterprise Frontier Safeguards](https://www.anthropic.com/news/enterprise-frontier-safeguards) (EFS), built by Anthropic and tailored in collaboration with Google Cloud, is for eligible enterprises. It combines data privacy and customer infrastructure control with automated misuse detection on frontier Claude models.

Google Cloud supports EFS for Google-managed Claude models in Model Garden, keeping inference and your inputs and outputs within your Google Cloud environment. For Anthropic-managed endpoints, see [Use Claude models on Google Cloud (Anthropic managed)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed) .

This document describes how EFS works, which Claude models are supported, and how to enroll your Google Cloud projects.

## How EFS works on Google-managed Claude models

EFS applies the following controls to enrolled Google Cloud projects:

- **Project-level enrollment.** After your organization is approved, your Google Cloud projects are enrolled in EFS. For enrolled projects, you don't need to accept the [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) or set the `dataSharingEnabledProvider` field for [request-response log sharing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging#share-requests-responses-with-maas-partners) .
- **Zero data retention.** Neither Anthropic nor Google retains your data. With EFS ZDR, you bring your own storage and store your own data. Neither Anthropic nor Google keeps a copy of your inputs and outputs once they're written to your storage. You configure your own access policies and audit logging, and encrypt safety data with your own keys.
- **No operator human review.** Neither Anthropic nor Google personnel access your inputs and outputs. Only automated safety monitoring accesses this data.
- **Your data is never used for training.** Neither Google nor Anthropic trains models or classifiers on your inputs and outputs, whether or not you use EFS. Under EFS, inputs and outputs are used only for automated safety monitoring.
- **Safety Cases.** When automated safety monitoring finds a risk, it creates a Safety Case for you to review. You can read these cases from your Cloud Storage bucket and integrate them with security information and event management (SIEM) systems. Safety Cases don't include inputs and outputs.
- **Storage billing.** You can use Cloud Storage in your Google Cloud project for your storage. Google bills you for that storage as usual, including reads, writes, and key operations, plus any applicable network transfer.

### Safeguard options

Two options are available for enrolled Google Cloud projects: **Legacy Zero data retention (ZDR)** and **EFS ZDR** (Preview). The following table compares how these options handle data retention, encryption, and governance:

| Aspect                          | Legacy ZDR                                                                                                                                                                                                                                                                                                                                                                                        | EFS ZDR (Preview)                                                                                                                                                                                                                                                                                                          |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Input and output retention**  | Neither Google nor Anthropic retains inputs or outputs for abuse monitoring. See [Zero data retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention) .                                                                                                                                                                                            | Neither Anthropic nor Google retains your data. You bring your own storage and store your own data. Inputs and outputs are deleted promptly after they're written to your own storage. You configure your own access policies and audit logging, and encrypt safety data with your own keys.                               |
| **Data storage and encryption** | None.                                                                                                                                                                                                                                                                                                                                                                                             | Inputs and outputs are stored in a bucket in your Google Cloud project and encrypted with customer-managed encryption keys (CMEK) in Cloud Key Management Service (Cloud KMS).                                                                                                                                             |
| **Governance and auditability** | Runs within your Google Cloud project boundary without partner log-sharing egress.                                                                                                                                                                                                                                                                                                                | Runs within your Google Cloud project boundary without partner log-sharing egress. Governed by your Identity and Access Management (IAM) policies and VPC Service Controls perimeters. Operations appear in Cloud Audit Logs when Data Access audit logs are enabled, and you can revoke bucket or key access at any time. |
| **Setup**                       | Currently the default for all EFS-eligible customers.                                                                                                                                                                                                                                                                                                                                             | Configured using the onboarding guide and Terraform module provided by your Google Cloud and Anthropic account teams.                                                                                                                                                                                                      |
| **Availability and duration**   | Available for current Claude models. For Covered Models (such as Claude Fable 5.2) and models accessed through the [Cyber Verification Program (CVP)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program) only, available to eligible customers through June 30, 2027. The date doesn't apply to other current Claude models. | Available in Preview for current Claude Fable and Mythos models as an optional alternative to Legacy ZDR. When Legacy ZDR coverage ends for these models, you will need EFS ZDR to maintain zero data retention.                                                                                                           |

## Supported models

EFS supports the following Claude model families on Google Cloud. EFS-enrolled projects don't require the Advanced AI Safety Addendum or the `dataSharingEnabledProvider` field.

- **Claude Mythos models:** All current versions.
- **Claude Fable models:** All current versions.

Future Claude models might require EFS ZDR rather than Legacy ZDR.

For platform data retention conditions, see [Zero data retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention) .

## Get started

Enrolled projects receive Legacy ZDR by default for current supported Claude models through June 30, 2027. To get started with EFS, complete the following steps:

1.  Contact your Google Cloud account team with the Google Cloud project numbers that call Claude, or submit Anthropic's [Enterprise Frontier Safeguards form](https://claude.com/form/enterprise-frontier-safeguards) . If you apply through Anthropic's form, your Anthropic or Google Cloud account team collects your Google Cloud project numbers after confirming your organization's eligibility.

2.  Optional: To use customer-managed Cloud Storage buckets and Cloud KMS keys instead of Legacy ZDR, request the onboarding guide and Terraform module from your Google Cloud and Anthropic account teams. After Anthropic approves your organization, use the module to create the buckets and access grants. Verify your projects in Anthropic's verification portal, and enable customer-managed storage and keys using Anthropic's API.

3.  After your account team confirms that your project is enrolled, in the Google Cloud console, go to the **Model Garden** page.

4.  Enable the Claude models that you want to use, and then [send online prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude) . You don't need to accept the Advanced AI Safety Addendum or set the `dataSharingEnabledProvider` field.

## Limitations

- **Online prediction only.** EFS controls apply to online prediction methods, such as `rawPredict` and `streamRawPredict` . [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch) aren't supported with EFS controls during Preview.
- **Endpoints and VPC Service Controls.** Customer-managed storage applies only on the endpoints listed in your onboarding guide. If you use VPC Service Controls, the perimeter must allow the EFS service accounts.

## What's next

- [Request predictions with Claude models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude) .
- Learn about the [Cyber Verification Program for Claude](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program) .
- Read about [Abuse monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring) .
- Read about [Zero data retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention) .
- Read about [Safety classifiers for Claude](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/safety) .
