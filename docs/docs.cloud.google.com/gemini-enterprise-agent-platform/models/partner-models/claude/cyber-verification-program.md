---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program
title: Cyber Verification Program for Claude
description: Enroll in Anthropic's Cyber Verification Program (CVP) on Gemini Enterprise Agent Platform and configure Claude models for defensive cybersecurity tasks.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Anthropic applies real-time cyber safeguards to frontier Claude models to prevent misuse in malicious cyber operations. Anthropic's [Cyber Verification Program](https://support.claude.com/en/articles/14604842-real-time-cyber-safeguards-on-claude-opus-and-sonnet) (CVP) is a trust framework that enables verified organizations to use Claude models for legitimate defensive cybersecurity tasks with default dual-use restrictions lifted.

This document describes how CVP works on Gemini Enterprise Agent Platform, which models are supported, and how to enroll and configure models for your project.

## How cyber safeguards work

Anthropic's real-time evaluation classifiers inspect prompts and completions to protect against cybersecurity-related risks. On Claude Opus 4.7, Claude Opus 4.8, Claude Sonnet 5, and Claude Opus 5, these safeguards categorize activities into two tiers:

- **Prohibited use** : High-risk malicious activities that have little or no legitimate defensive application, such as ransomware development, command-and-control (C2) infrastructure generation, malware authoring, or automated mass data exfiltration. **Prohibited activities are permanently blocked for all users. The Cyber Verification Program never lifts restrictions on prohibited activities.**
- **High-risk dual-use** : Activities that are critical for authorized security operations, but could also be abused by threat actors. Examples include vulnerability discovery, exploitability analysis, proof-of-concept exploit verification, red teaming, and adversary attack path simulation. Dual-use activities are blocked by default, but verified organizations can have these safeguards adjusted through the Cyber Verification Program.

For Claude Opus 5.5, Claude Sonnet 5.5, Claude Mythos 5.1, and new models moving forward, CVP offers three access tiers instead of a single level of access:

- Defense Access
- Red Team Access
- Specialized Access

For more information about these tiers and Anthropic's usage policies, see [Real-time cyber safeguards on Claude](https://support.claude.com/en/articles/14604842-real-time-cyber-safeguards-on-claude-opus-and-sonnet) .

## Supported models

The Cyber Verification Program on Agent Platform supports the following Anthropic models:

- **Claude Opus 4.7 and later, Claude Sonnet 5 and later, Claude Haiku 5.5 and later, and all Claude Mythos models** : Requires enabling both advanced AI features ( `advancedAiEnabled: true` ) and data sharing with Anthropic ( `dataSharingEnabledProvider: ANTHROPIC` ). This includes Claude Opus 4.7, Claude Opus 4.8, and Claude Sonnet 5, which previously required only advanced AI features.
- **Claude Fable models** : CVP doesn't grant reduced blocks on Fable models. Each CVP access tier includes access to Claude Mythos instead.
- **Claude Haiku 4.5, Claude Sonnet 4.5, Claude Sonnet 4.6, Claude Opus 4.5, and Claude Opus 4.6** : Not covered by CVP. The Cyber Verification Program option isn't available for these models.

## Before you begin

Before enrolling in the Cyber Verification Program, ensure that you meet the following prerequisites:

- A Google Cloud project with the Agent Platform API enabled.

- The following Identity and Access Management (IAM) permissions on the project:

  - To accept the Advanced AI Safety Addendum: `aiplatform.consents.update` , which is included in the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) role.
  - To configure publisher model settings: `aiplatform.endpoints.setPublisherModelConfig` , which is included in the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) role.

- **Data retention understanding** : Enrolling a model in CVP designates that model as "Advanced AI" under Google's [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) . In accordance with Anthropic's safety policies, prompts and responses sent to CVP-enabled models are retained for abuse monitoring for up to 30 days. For more information, see [Advanced AI Safety](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring#advanced_ai_safety) .

- **Data sharing understanding** : Anthropic requires that data sharing be enabled for abuse monitoring on all models enrolled in CVP. Enrolling a model requires both consenting to data retention and configuring data sharing with Anthropic. For more information, see [Log and share requests and responses](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging#enable-data-sharing) .

## How to enroll

Enrolling in the Cyber Verification Program on Agent Platform is a three-step process:

1.  [Accept the Advanced AI Safety Addendum](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#accept-addendum) in the Google Cloud console.
2.  [Complete Anthropic's Cyber Use Case application form](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#complete-use-case-form) .
3.  [Enable advanced AI and data sharing with Anthropic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#enable-advanced-ai) on each target model and location in the Google Cloud console or by using the `setPublisherModelConfig` API.

### Step 1: Accept the Advanced AI Safety Addendum

An authorized administrator must accept the Advanced AI Safety Addendum once per Google Cloud project.

To accept the addendum, do the following:

1.  In the Google Cloud console, go to **Model Garden** .

2.  Select an eligible Claude model. See [Supported models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#supported-models) .

3.  On the model details page, find the **Cyber Verification Program (Optional)** card.

4.  Click **Steps to enroll** to expand the enrollment checklist.

5.  In **Step 1: Accept the Advanced AI Safety Addendum** , review the addendum, and then select the confirmation checkbox acknowledging that you are authorized to bind your organization to the addendum.

6.  Click **Accept** .

> **Note:** Acceptance must be performed through Model Garden in the Google Cloud console. No API method is available for this step.

### Step 2: Complete Anthropic's Cyber Use Case form

An authorized representative of your security team must submit an application directly to Anthropic:

1.  Sign in to Anthropic's [Verification Portal](https://portal.anthropic.com/link?account_source=gcp&program=cvp) .
2.  Open **Linked accounts** , select **Link account** , and then choose **Google Cloud** .
3.  Enter your project ID (not the project number).
4.  Run the `gcloud` command shown, select **I've granted access** , and then select **Verify** .
5.  Open **Programs** , choose **Cyber Verification Program** , and then select **Apply** .
6.  Describe your defensive security workflows and use cases (for example, authorized penetration testing, vulnerability research, or security operations).
7.  Submit the form.
8.  After Anthropic approves your application, return to the Verification Portal and open the **Cyber Verification Program** page.
9.  Under **Access on linked accounts** , turn on your approved access level for the project.

### Step 3: Enable advanced AI and data sharing on the model

After you accept the Advanced AI Safety Addendum and receive approval from Anthropic, configure the required settings on each Claude model you want to use for defensive cybersecurity work. Configuration must be applied per project, location, publisher, and model.

#### Use the Google Cloud console

1.  In the Google Cloud console, go to **Model Garden** , and then select the Claude model.
2.  Select **Cyber Verification Program** .
3.  Under **Enable advanced AI mode** , turn on **Enable advanced AI capabilities** .
4.  Under **Turn on Human Review** , turn on **Share request-response log with partner?** , enter `Anthropic` to confirm, and then click **Enable** .
5.  Click **Complete CVP setup** .
6.  Repeat these steps for each model that you want to use with CVP.

If the model's page doesn't show the **Cyber Verification Program** option, or if you prefer the API, use the API call in the next section. For Claude Mythos models, these settings are already in place as a condition of using the model.

#### Use the API

Call `setPublisherModelConfig` on the `v1beta1` endpoint to enable both `advancedAiEnabled` and data sharing with Anthropic ( `dataSharingEnabledProvider` ):

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL_ID:setPublisherModelConfig" \
  -d '{
    "publisherModelConfig": {
      "claudeFeatureConfig": {
        "advancedAiEnabled": true
      },
      "dataSharingEnabledProvider": "ANTHROPIC"
    },
    "updateMask": "claudeFeatureConfig.advancedAiEnabled,dataSharingEnabledProvider"
  }'
```

Replace the following:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` MODEL_ID ` : The Claude model identifier (for example, `claude-opus-5-5` or `claude-sonnet-5` ).

### Important API considerations

- **Use `v1beta1`** : The `setPublisherModelConfig` method is supported on the `v1beta1` API surface.
- **Always include `updateMask`** : The `updateMask` field is essential. If you omit `updateMask` , the call replaces the entire `PublisherModelConfig` object, which inadvertently clears other settings such as `loggingConfig` or `dataSharingEnabledProvider` .
- **Long-running operation** : This method returns a `google.longrunning.Operation` . Poll the operation until `done: true` is returned.
- **Configuration scope** : Publisher model configurations are scoped per project, location, publisher, and model. If you use models in multiple regions, configure each endpoint. The examples on this page configure the global endpoint. For another location, change both the hostname and the `locations/` segment of the URL. For a multi-region endpoint ( `us` or `eu` ), use `aiplatform. `` LOCATION `` .rep.googleapis.com` . For a regional endpoint (for example, `us-east5` ), use `LOCATION `` -aiplatform.googleapis.com` .

### Verify model configuration

To verify that both settings are enabled for a specific model, call the `fetchPublisherModelConfig` method:

```
curl -X GET \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL_ID:fetchPublisherModelConfig"
```

If both settings are enabled, the response is as follows:

```
{
  "claudeFeatureConfig": {
    "advancedAiEnabled": true
  },
  "dataSharingEnabledProvider": "ANTHROPIC"
}
```

## Troubleshooting

This section describes how to resolve common issues that you might encounter when enrolling in or using the Cyber Verification Program.

### Requests are still blocked on cybersecurity tasks

If advanced AI or data sharing isn't enabled for the project, model, and location that you call, requests still succeed, but Anthropic's default cyber safeguards apply.

If your prompts continue to trigger safeguard refusals:

1.  **Confirm the activity category** : Verify that the task is a legitimate dual-use task and not a prohibited use case. Prohibited activities (such as ransomware code authoring or malware development) are permanently blocked for all users and cannot be unblocked under CVP.
2.  **Verify Anthropic approval** : Confirm that Anthropic has sent an approval confirmation email for your organization's CVP application, and that your approved access level is turned on for the project under **Access on linked accounts** in the Verification Portal.
3.  **Check project alignment** : Ensure that inference requests originate from the same Google Cloud project ID submitted in your Anthropic application and for which the addendum was accepted.
4.  **Confirm model-level configuration** : Call `fetchPublisherModelConfig` on the exact model ID and region you are calling to confirm `advancedAiEnabled: true` and `dataSharingEnabledProvider: ANTHROPIC` are both set. Model configurations are scoped per model, per location, and per project.
5.  **Submit a false-positive appeal** : If you believe a legitimate defensive prompt is being blocked erroneously, submit an appeal using [Anthropic's Cyber Block Report and Appeal form](https://claude.com/form/cyber-block-false-positive-report-cvp-rejection-appeal) .

### Permission denied when accepting the addendum

If you receive a permission error when attempting to accept the addendum in Model Garden, ensure your account has the `aiplatform.consents.update` permission. Contact your project administrator to assign the Agent Platform Administrator role ( `roles/aiplatform.admin` ).

### Missing fields in API responses

If calling `fetchPublisherModelConfig` returns an empty object ( `{}` ), no custom publisher model settings have been applied to that model. Re-run `setPublisherModelConfig` with the appropriate `updateMask` .

## What's next

- Read about [Safety classifiers for Claude in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/safety) .
- Review [Abuse monitoring in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring) .
- Learn about [Responsible AI practices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai) .
