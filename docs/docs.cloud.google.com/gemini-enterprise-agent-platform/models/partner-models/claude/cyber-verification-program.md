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

Anthropic's real-time evaluation classifiers inspect prompts and completions to protect against cybersecurity-related risks. These safeguards categorize activities into two tiers:

  - **Prohibited use** : High-risk malicious activities that have little or no legitimate defensive application, such as ransomware development, command-and-control (C2) infrastructure generation, malware authoring, or automated mass data exfiltration. **Prohibited activities are permanently blocked for all users. The Cyber Verification Program never lifts restrictions on prohibited activities.**
  - **High-risk dual-use** : Activities that are critical for authorized security operations, but could also be abused by threat actors. Examples include vulnerability discovery, exploitability analysis, proof-of-concept exploit verification, red teaming, and adversary attack path simulation. Dual-use activities are blocked by default, but verified organizations can have these safeguards adjusted through the Cyber Verification Program.

For more information about Anthropic's usage policies, see [Real-time cyber safeguards on Claude](https://support.claude.com/en/articles/14604842-real-time-cyber-safeguards-on-claude-opus-and-sonnet) .

## Supported models

The Cyber Verification Program on Agent Platform supports the following Anthropic models:

  - **Claude Opus 4.7, Claude Opus 4.8, and Claude Sonnet 5** : Requires enabling advanced AI features ( `advancedAiEnabled: true` ).
  - **Claude Opus 5** : Requires enabling both advanced AI features ( `advancedAiEnabled: true` ) and data sharing with Anthropic ( `dataSharingEnabledProvider: ANTHROPIC` ).

## Before you begin

Before enrolling in the Cyber Verification Program, ensure that you meet the following prerequisites:

  - A Google Cloud project with the Agent Platform API enabled.

  - The following Identity and Access Management (IAM) permissions on the project:
    
      - To accept the Advanced AI Safety Addendum: `aiplatform.consents.update` , which is included in the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) role.
      - To configure publisher model settings: `aiplatform.endpoints.setPublisherModelConfig` , which is included in the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) role.

  - **Data retention understanding** : Enrolling a model in CVP designates that model as "Advanced AI" under Google's [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) . In accordance with Anthropic's safety policies, prompts and responses sent to CVP-enabled models are retained for abuse monitoring for up to 30 days. For more information, see [Advanced AI Safety](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring#advanced_ai_safety) .

  - **Data sharing understanding (Claude Opus 5 only)** : For Claude Opus 5 with CVP, Anthropic requires that data sharing be enabled for abuse monitoring. Enrolling Claude Opus 5 requires both consenting to data retention and configuring data sharing with Anthropic. For more information, see [Log and share requests and responses](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging#enable-data-sharing) .

## How to enroll

Enrolling in the Cyber Verification Program on Agent Platform is a three-step process:

1.  [Accept the Advanced AI Safety Addendum](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#accept-addendum) in the Google Cloud console.
2.  [Complete Anthropic's Cyber Use Case application form](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#complete-use-case-form) .
3.  [Enable advanced AI on each target model and location](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program#enable-advanced-ai) using the `setPublisherModelConfig` API, and if using Claude Opus 5, enable data sharing.

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

1.  Go to the [Anthropic Cyber Use Case form](https://portal.anthropic.com/link?account_source=gcp&program=cvp) .
2.  In the **Surface** section, select **Google Cloud** .
3.  Enter the required information.
4.  Describe your defensive security workflows and use cases (for example, authorized penetration testing, vulnerability research, or security operations).
5.  Submit the form.

### Step 3: Enable advanced AI on the model

After you accept the Advanced AI Safety Addendum and receive approval from Anthropic, configure the required settings on each Claude model you want to use for defensive cybersecurity work. Configuration must be applied per project, location, publisher, and model.

#### For Claude Opus 4.7, Claude Opus 4.8, and Claude Sonnet 5

Call `setPublisherModelConfig` on the `v1beta1` endpoint to enable `advancedAiEnabled` :

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL_ID:setPublisherModelConfig" \
      -d '{
        "publisherModelConfig": {
          "claudeFeatureConfig": {
            "advancedAiEnabled": true
          }
        },
        "updateMask": "claudeFeatureConfig.advancedAiEnabled"
      }'

Replace the following:

  - PROJECT\_ID : Your Google Cloud project ID.
  - MODEL\_ID : The Claude model identifier (for example, `claude-opus-4-8` or `claude-sonnet-5` ).

#### For Claude Opus 5

For Claude Opus 5, Anthropic requires enabling both `advancedAiEnabled` and data sharing with Anthropic ( `dataSharingEnabledProvider` ):

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/claude-opus-5:setPublisherModelConfig" \
      -d '{
        "publisherModelConfig": {
          "claudeFeatureConfig": {
            "advancedAiEnabled": true
          },
          "dataSharingEnabledProvider": "ANTHROPIC"
        },
        "updateMask": "claudeFeatureConfig.advancedAiEnabled,dataSharingEnabledProvider"
      }'

Replace PROJECT\_ID with your Google Cloud project ID.

### Important API considerations

  - **Use `v1beta1`** : The `setPublisherModelConfig` method is supported on the `v1beta1` API surface.
  - **Always include `updateMask`** : The `updateMask` field is essential. If you omit `updateMask` , the call replaces the entire `PublisherModelConfig` object, which inadvertently clears other settings such as `loggingConfig` or `dataSharingEnabledProvider` .
  - **Long-running operation** : This method returns a `google.longrunning.Operation` . Poll the operation until `done: true` is returned.
  - **Configuration scope** : Publisher model configurations are scoped per project, location, publisher, and model. If you use models in multiple regions, configure each endpoint.

### Verify model configuration

To verify that advanced AI is enabled for a specific model, call the `fetchPublisherModelConfig` method:

    curl -X GET \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL_ID:fetchPublisherModelConfig"

If advanced AI is enabled for Claude Opus 4.7, Claude Opus 4.8, and Claude Sonnet 5, the response is as follows:

    {
      "claudeFeatureConfig": {
        "advancedAiEnabled": true
      }
    }

If advanced AI is enabled for Claude Opus 5, the response is as follows:

    {
      "claudeFeatureConfig": {
        "advancedAiEnabled": true
      },
      "dataSharingEnabledProvider": "ANTHROPIC"
    }

## Troubleshooting

This section describes how to resolve common issues that you might encounter when enrolling in or using the Cyber Verification Program.

### Requests are still blocked on cybersecurity tasks

If your prompts continue to trigger safeguard refusals:

1.  **Confirm the activity category** : Verify that the task is a legitimate dual-use task and not a prohibited use case. Prohibited activities (such as ransomware code authoring or malware development) are permanently blocked for all users and cannot be unblocked under CVP.
2.  **Verify Anthropic approval** : Confirm that Anthropic has sent an approval confirmation email for your organization's CVP application.
3.  **Check project alignment** : Ensure that inference requests originate from the same Google Cloud project ID submitted in your Anthropic application and for which the addendum was accepted.
4.  **Confirm model-level configuration** : Call `fetchPublisherModelConfig` on the exact model ID and region you are calling to confirm `advancedAiEnabled: true` is active (and `dataSharingEnabledProvider: ANTHROPIC` for Claude Opus 5). Model configurations are scoped per model, per location, and per project.
5.  **Submit a false-positive appeal** : If you believe a legitimate defensive prompt is being blocked erroneously, submit an appeal using [Anthropic's Cyber Block Report and Appeal form](https://claude.com/form/cyber-block-false-positive-report-cvp-rejection-appeal) .

### Permission denied when accepting the addendum

If you receive a permission error when attempting to accept the addendum in Model Garden, ensure your account has the `aiplatform.consents.update` permission. Contact your project administrator to assign the Agent Platform Administrator role (roles/aiplatform.admin).

### Missing fields in API responses

If calling `fetchPublisherModelConfig` returns an empty object ({}), no custom publisher model settings have been applied to that model. Re-run `setPublisherModelConfig` with the appropriate `updateMask` .

## What's next

  - Read about [Safety classifiers for Claude in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/safety) .
  - Review [Abuse monitoring in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring) .
  - Learn about [Responsible AI practices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai) .
