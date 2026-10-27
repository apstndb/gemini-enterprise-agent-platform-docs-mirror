---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed
title: Use Claude models on Google Cloud (Anthropic managed)
description: Learn how to use Claude models on Google Cloud (Anthropic managed) in {{dynamic_data.site_values.cloud_name}}, compare Anthropic-managed and Google-managed Claude models, and get started with the API.
data_source: docs.cloud.google.com
---

> **Important:** Claude models on Google Cloud (Anthropic managed) allows you to access Claude developer platform on Anthropic-managed infrastructure, with billing and access through Google Cloud. Google Cloud and Anthropic act as separate, independent data processors for their respective parts of the service. The Google Cloud and Google Cloud Marketplace Terms of Service (as applicable) govern Google Cloud's integration layer (IAM authentication, API routing, Cloud Audit Logs, and Google Cloud Marketplace billing). Anthropic's Commercial Terms of Service, Data Processing Addendum, and Usage Policy govern use of the Anthropic-managed Claude API and Console.
>
> Data storage and inference occur on Anthropic-managed infrastructure (which may route outside Google Cloud), and subservices may change without notice. Set the `inference_geo` parameter per request to pin inference to a specific geography. See [Data residency](https://docs.cloud.google.com/gemini-enterprise-agent-platform//resources/data-residency) for details.
>
> Claude models on Google Cloud (Anthropic managed) follows the same data retention policy as Anthropic's 1st party Claude API. Zero Data Retention (ZDR) may be available on request. Contact your Google Cloud or Anthropic account representative to enable it for your account.

**Claude models on Google Cloud (Anthropic managed)** is a service that lets you use Anthropic's Claude developer platform in Google Cloud. Use it to access Anthropic's latest features, including new models and research previews, and the Claude Console.

This page covers the following topics:

- The [key benefits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed#key-benefits) of Claude models on Google Cloud (Anthropic managed)
- A [comparison of Anthropic-managed and Google-managed Claude models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed#compare)
- How to [get started](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed#get-started)
- How to [make API calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed#use-claude-platform)

## Key benefits

Key benefits of using Claude models on Google Cloud (Anthropic managed) include:

- **Access to latest innovation** : Gain immediate access to Anthropic's latest models, features, research previews, and betas as soon as they are released.
- **Google Cloud billing and Identity integration** : Leverage your existing Google Cloud investment. The service integrates with Cloud Billing and Identity and Access Management and draws down on your Google Cloud commitment subject to the [Google Google Cloud Marketplace Commitment Drawdown Policy](https://cloud.google.com/terms/marketplace/commit-policy) .
- **Unified support** : Receive frontline support from Google Cloud Support on Agent Platform-related issues, with specialized backline support provided by Anthropic on the managed service.
- **Anthropic's built-in experience** : Access the Claude Console for managing resources and exploring new features.

## Compare Anthropic-managed and Google-managed Claude models

Claude models on Google Cloud (Anthropic managed) and Claude models (Google managed) on Agent Platform differ in who operates the stack, the API surface, feature availability, and the data processor.

With Claude models on Google Cloud (Anthropic managed) ( `claude.googleapis.com` ), the API and underlying platform are managed by Anthropic on its own systems and are governed by the Anthropic Commercial Terms of Service, including the data processing terms therein, where Anthropic is the data processor.

You should use a Google-managed Claude model if you need any of the following:

- Google-operated inference where Google Cloud is the sole data processor
- Data and inference that stay inside Google Cloud's security boundary (with VPC Service Controls, Customer-managed encryption keys, and regional data residency)
- Coverage under Google Cloud compliance programs (including FedRAMP High, IL4, IL5, SOC, ISO, and HIPAA eligibility)
- Built-in Google Cloud quotas and billing
- Built-in integrations with Google Cloud services such as BigQuery, Model Armor, and Agent Engine.

### Comparison at a glance

The following table outlines the key differences between the Anthropic-managed and Google-managed Claude models:

| Model type             | Anthropic-managed                                                                                                                 | Google-managed                                                 |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Who operates the stack | Anthropic                                                                                                                         | Google                                                         |
| API surface            | `/v1/messages` using `claude.googleapis.com`                                                                                      | Agent Platform prediction endpoints, `/v1/messages`            |
| Feature availability   | Intended to match the first-party Claude API                                                                                      | Per Agent Platform and Model Garden release schedule           |
| Beta features          | Pass through with `anthropic-beta` headers                                                                                        | `anthropic-beta` header support varies by Model Garden release |
| Authentication         | Google Cloud IAM. Application Default Credentials, a service account, or `gcloud auth print-access-token` . No `x-api-key`        | Google Cloud IAM (same credential model)                       |
| Billing                | Google Cloud Marketplace (in CCUs)                                                                                                | Google Cloud (Agent Platform billing)                          |
| Base URL               | `claude.googleapis.com`                                                                                                           | `REGION `` -aiplatform.googleapis.com`                         |
| SDK client             | Platform-specific client class ( `AnthropicGoogleCloud` )                                                                         | Agent Platform client                                          |
| Console                | Google Cloud console for IAM, metrics and monitoring, and Claude Console ( `platform.claude.com` , accessed through Google Cloud) | Google Cloud console (Agent Platform and Model Garden)         |
| Rate limits and quotas | Quota requests can be submitted directly using the console, but rate limits and quotas are managed by Anthropic                   | Managed by Google Cloud (Agent Platform quotas)                |

### Compare supported API features

The following table compares the support level for various API features for both Anthropic-managed and Google-managed Claude models:

| Feature                                            | Description                                                                                                                                                                                   | Anthropic-managed         | Google-managed                       |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|--------------------------------------|
| Thinking (extended, adaptive)                      | Reason through a problem before answering, improving accuracy on complex tasks.                                                                                                               |                           |                                      |
| Prompt caching (automatic and explicit)            | Reuse repeated prompt content instead of reprocessing it, cutting cost and latency. Apply it automatically or choose what gets cached.                                                        |                           |                                      |
| Task budgets (beta)                                | Manage spend on long-running agents, by giving Claude a token allowance for tasks. Claude can better prioritize and wrap up work.                                                             |                           |                                      |
| Tool use (client-defined)                          | Connect to external tools, calling a customer's own functions, APIs, and systems.                                                                                                             |                           |                                      |
| Citations                                          | Return the exact passages that support each claim, to verify answers and surface sources.                                                                                                     |                           |                                      |
| One million context, image/PDF (supported models)  | Handle up to one million tokens per request (enough for entire codebases or hundreds of documents). Reads images and PDFs.                                                                    |                           |                                      |
| Prompt caching (Five minutes, one hour, automatic) | Define how long cached content is kept (5 minutes, 1 hour), to reduce processing time and costs for repetitive tasks.                                                                         |                           |                                      |
| Structured outputs                                 | Guarantee Claude's responses always match specified JSON schemas or custom tool definitions, without retries or parsing errors.                                                               |                           |                                      |
| Batch processing                                   | Submit multiple requests together for asynchronous processing. Useful for large volumes of data, optimizing for cost efficiency, and when immediate responses are not required.               |                           | Using Agent Platform batch inference |
| Service tiers                                      | Offer different tiers of service that allow for balancing availability, performance, and predictable costs, based on the application's needs.                                                 | Priority, Standard, Batch | Provisioned Throughput, Batch        |
| Context editing (beta)                             | Optimize costs, stay within limits, and help agents stay focused and run longer, by clearing specific content from conversation history as it grows.                                          |                           |                                      |
| Anthropic-defined tools                            |                                                                                                                                                                                               |                           |                                      |
| Web Search                                         | Give live web access to search for current information. Responses include citations.                                                                                                          |                           |                                      |
| Web Fetch                                          | Give live web access to pull content from specific web pages and PDFs.                                                                                                                        |                           |                                      |
| Remote MCP (beta)                                  | Connect to external tools and data through remote MCP servers, directly from the API.                                                                                                         |                           |                                      |
| Memory                                             | Save and retrieve information across conversations, so agents build knowledge over time.                                                                                                      |                           |                                      |
| Files API                                          | Upload and manage files once to use with the API, instead of re-sending the same content every time.                                                                                          |                           |                                      |
| Computer Use                                       | Give Claude screenshot, mouse, and keyboard control of a desktop environment for autonomous interaction.                                                                                      |                           |                                      |
| Skills                                             | Reusable resources that give Claude domain-specific expertise: workflows, context, and best practices that turn a general-purpose agent into a specialist.                                    |                           |                                      |
| Code Execution                                     | Allow Claude to write and run code in a sandboxed environment, to analyze data, generate files, and iterate on solutions.                                                                     |                           |                                      |
| Managed Agents (beta)                              | Use a prebuilt, configurable agent harness that runs in managed infrastructure. Best for long-running tasks and asynchronous work.                                                            |                           |                                      |
| Advisor tool (beta)                                | Let a faster, lower-cost executor model (Haiku, Sonnet) consult a higher-intelligence advisor model (Opus) mid-generation for strategic guidance, before the executor model resumes the task. |                           |                                      |

## Get started

> **Note:** To use Claude models on Google Cloud (Anthropic managed), you must have a Claude Platform account.

To get started with Claude models on Google Cloud (Anthropic managed), follow these steps to enable Claude models on Google Cloud (Anthropic managed) for your project:

1.  In the Google Cloud console, go to the **Claude models** page:

2.  In the list of manager options, select **Anthropic managed** .

3.  If you haven't already enabled the Claude API for your project, in the **Enable the Claude API** section, click **Enable API** , and then follow the instructions.

4.  In the **Purchase the product** section, click **Purchase via Marketplace** . You will be redirected to the Marketplace page. You can choose to purchase the product at list price or through negotiated discount or private offer. Once you have successfully purchased the product, click **Manage on Console** to return to the Model Garden page.

5.  In the **Activate Claude Console** section, click **Activate** to provision a new Anthropic organization for your Google Cloud project. Enter a one-time contact email address to receive the setup link, open the link from that inbox, complete the organization details form (organization name, entity type, country, and intended use), and accept Anthropic's Commercial Terms of Service and Usage Policy. Note that this creates a separate Anthropic organization: API keys, workspaces, HIPAA controls, Zero Data Retention (ZDR), and settings from an existing first-party Anthropic organization don't carry over.

## Use Claude models on Google Cloud (Anthropic managed)

After enabling the Claude API and purchasing the product, you can use Claude models on Google Cloud (Anthropic managed) through the Claude Console or using the Claude API.

### Claude Console

To use the Claude Console:

1.  **Grant the `roles/claude.admin` (Claude Platform Admin) role** : To use the Claude Console, you must first [grant the `roles/claude.admin` (Claude Platform Admin) Identity and Access Management (IAM) role for the project](https://docs.cloud.google.com/iam/docs/grant-role-console) .

2.  In the Google Cloud console, go to the **Claude models on Google Cloud (Anthropic managed)** page:

3.  In the **Activate Claude Console** section, click **Open Claude Console** .

### Claude API

You can interact with Claude models on Google Cloud (Anthropic managed) using standard Google Cloud authentication. The API endpoint is `https://claude.googleapis.com/` .

1.  **Grant the `roles/claude.user` (Claude Platform User) role** : To make API calls, you must first [grant the `roles/claude.user` (Claude Platform User) Identity and Access Management (IAM) role for the project](https://docs.cloud.google.com/iam/docs/grant-role-console) .

2.  **Authenticate with Google Cloud** : If you are using a client library or the [Google Cloud CLI](https://docs.cloud.google.com/sdk/gcloud) , authentication is handled automatically. For direct API calls, ensure you have authenticated and can obtain an OAuth 2.0 token. You can get a token using the Google Cloud CLI:

    ```
    gcloud auth print-access-token
    ```

3.  **Call the Messages API** : The API structure mirrors the Anthropic Messages API. You can make requests using Anthropic's Google Cloud client SDKs ( `AnthropicGoogleCloud` ) or directly to workspace-scoped endpoints under `https://claude.googleapis.com/v1/projects/PROJECT_ID/locations/global/workspaces/ANTHROPIC_WORKSPACE_ID/invoke/v1/messages` .

    Here is an example using curl:

    ```
    curl -X POST "https://claude.googleapis.com/v1/projects/${PROJECT_ID}/locations/global/workspaces/${ANTHROPIC_WORKSPACE_ID}/invoke/v1/messages" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -d '{
      "model": "claude-haiku-4-5",
      "max_tokens": 1024,
      "messages": [
        {"role": "user", "content": "Hello, Claude"}
      ]
    }'
    ```

## API reference

For detailed API reference for messages, files, and skills, see the [Anthropic API documentation](https://platform.claude.com/docs/en/api/overview) .

For direct REST calls to workspace-scoped endpoints (such as `/v1/messages` , `/v1/files` , or `/v1/skills` ), use `https://claude.googleapis.com/v1/projects/PROJECT_ID/locations/global/workspaces/ANTHROPIC_WORKSPACE_ID/invoke` as the base URL before the Anthropic API path (for example, `.../invoke/v1/files` ). For organization-level endpoints (such as `/v1/organizations/workspaces` ), use `https://claude.googleapis.com/v1/projects/PROJECT_ID/locations/global/claudeOrganization/invoke` as the base URL.
