---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/monitor-content-security
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/monitor-content-security
title: Monitor content security
description: Learn how to view content security insights from Model Armor for AI agents governed by your gateways.
data_source: docs.cloud.google.com
---

> **Private Preview — Model Armor insights**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to view content security insights from [Model Armor](https://docs.cloud.google.com/model-armor/overview) for [supported AI agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/monitor-content-security#supported-agents) .

Model Armor screens the requests and responses for security risks, such as indirect prompt injection attacks, sensitive data leakage, and the generation or serving of harmful content. For more information, see [Model Armor](https://docs.cloud.google.com/model-armor/overview) .

## Before you begin

1.  [Configure Model Armor on one or more gateways](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) in your project.
2.  To monitor agents that communicate with a Google Cloud MCP server, [configure Model Armor with MCP servers](https://docs.cloud.google.com/model-armor/model-armor-mcp-google-cloud-integration) .
3.  [Set up tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing) for your agent.

### Required role

To get the permissions that you need to monitor content security violations, ask your administrator to grant you the Monitoring Viewer (\`roles/monitoring.viewer\`) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to monitor content security violations. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to monitor content security violations:

  - \`monitoring.monitoredResourceDescriptors.list\`
  - \`monitoring.metricDescriptors.list\`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Supported agents

The **Security** tab is populated with Model Armor insights for the following agents only:

  - Agents deployed in Agent Runtime and [governed by Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) .
  - Agents deployed in Agent Runtime and [communicating with a Google Cloud MCP server](https://docs.cloud.google.com/model-armor/model-armor-mcp-google-cloud-integration) .

## View the Model Armor insights for an AI agent

To view the content security insights for supported agents, follow these steps:

1.  In the Google Cloud console, go to Agent Registry.
2.  Select your project.
3.  Click the name of the agent.
4.  Click the **Security** tab.

## View the number of flagged or blocked interactions

On the **Security** tab, view the number of interactions, including flagged and blocked interactions. The **Security** tab displays the following metrics:

  - **Total interactions** : The total number of prompts and responses that are analyzed by Model Armor.
  - **Interactions flagged** : The number of interactions that violated a [configured policy in Model Armor templates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) .
  - **Interactions blocked** : The number of interactions blocked if you configured Model Armor in the [`INSPECT_AND_BLOCK`](https://docs.cloud.google.com/model-armor/manage-templates#templates-metadata) mode.

## Monitor content security violations

In the **Violations over time** chart, monitor the number of detected violations over time.

The violations detected are categorized into the following areas:

  - **All detectors** : The total number of violations detected by all detectors, including [prompt injections and jailbreaks](https://docs.cloud.google.com/model-armor/overview#ma-prompt-injection) , [malicious URLs](https://docs.cloud.google.com/model-armor/overview#ma-malicious-url-detection) , responsible AI, and sensitive data.

  - **Responsible AI** : Content violations detected by safety filters, such as harassment and hate speech. For a complete list of responsible AI categories, see [Responsible AI safety filter](https://docs.cloud.google.com/model-armor/overview#ma-responsible-ai-safety-categories) .

  - **Sensitive data** : Content violations involving the presence of [sensitive information types](https://docs.cloud.google.com/sensitive-data-protection/docs/infotypes-reference) or [custom information types](https://docs.cloud.google.com/sensitive-data-protection/docs/creating-custom-infotypes) that you define. For more information, see [Sensitive Data Protection](https://docs.cloud.google.com/model-armor/overview#ma-sensitive-data-prot) .
    
    > **Note:** On the agent-level **Security** tab, counts for sensitive data content violations are included in the total violations count but aren't displayed in a separate category.

For more information about these detectors, see [Model Armor filters](https://docs.cloud.google.com/model-armor/overview#ma-filters) .

## Download violations data to a PNG or CSV file

To download violations data to a PNG or CSV file, follow these steps:

1.  In the **Violations over time** view on the **Security** tab, select the period for which you want to download data.
2.  Click more\_vert **More chart options \> Download** .
3.  Click **Download PNG** or **Download CSV** to download the data in your preferred format.

## What's next

Guide

### [Model Armor audit logging](https://docs.cloud.google.com/model-armor/audit-logging-model-armor)

Learn about audit logging for Model Armor.

Guide

### [Configure logging for Model Armor](https://docs.cloud.google.com/model-armor/configure-logging)

Learn how to configure logging for Model Armor.

Troubleshooting

### [Troubleshoot Model Armor issues](https://docs.cloud.google.com/model-armor/troubleshooting)

Learn how to troubleshoot issues with Model Armor.
