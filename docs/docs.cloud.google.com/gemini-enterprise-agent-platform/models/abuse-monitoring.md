---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring
title: Abuse monitoring
description: Learn how Google detects potential abuse and violations of its Acceptable Use Policy and Prohibited Use Policy for Generative AI Services.
data_source: docs.cloud.google.com
---

As outlined in Section 4.3 "Generative AI Safety and Abuse" of [Google Cloud Platform Terms of Service](https://cloud.google.com/terms/) , Google uses the following process to detect potential abuse and violations of its [Acceptable Use Policy](https://cloud.google.com/terms/aup) and [Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) as part of providing Generative AI Services to customers.

  - **Automated detection** : Google uses automated safety classifiers to detect potential abuse and violations. For technical details on how safety classifiers work, see [Configure safety filters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/configure-safety-filters) .

  - **Prompt logging** : If automated safety classifiers detect suspicious activity that requires further investigation into whether a customer has violated our policies, then Google may log customer prompts solely for the purpose of examining whether a violation of the AUP or Prohibited Use Policy has occurred. This data won't be used to train or fine-tune any AI/ML models. This data is stored securely for up to 90 days in the same region or multi-region selected by the customer for their project and adheres to Google Cloud assurances, such as Data Residency, Access Transparency and VPC Service Controls. Prompt logs for the purposes of abuse monitoring are not encrypted by Customer-managed encryption keys (CMEK). Customers also have the option to request an opt-out from abuse logging (see below).

  - **Action** : Authorized Google employees may assess the flagged prompts and may reach out to the customer for clarification. Failure to address the behavior—or recurring or severe abuse—may result in suspension or termination of the customer's access to Gemini Enterprise Agent Platform or Google Cloud services.

  - **Services in scope** : Google's Generative AI Services.

  - **Customers in scope** : Only customers whose use of Google Cloud is governed by the [Google Cloud Platform Terms of Service](https://cloud.google.com/terms/) . This means that customers with a Google Cloud Master Agreement are exempt from prompt logging for this abuse monitoring by default.

  - **Customer opt-out** : Customers may request for an exception by filling out this [form](https://forms.gle/mtjKKas8a82grYN6A) . If approved, Google won't store any prompts associated with the approved Google Cloud account.

## Advanced AI safety

As outlined in the [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) , Google Cloud has implemented a more rigorous abuse monitoring system for models designated as "Advanced AI".

  - **Prompt and response logging** : All prompts and responses will be logged and securely stored for up to 60 days for the sole purpose of monitoring for abuse. This data won't be used to train or fine-tune any AI/ML models. This data is stored in the same region or multi-region selected by the customer for their project and adheres to Google Cloud assurances, such as Data Residency, Access Transparency and VPC Service Controls. Prompt and response logs for the purposes of abuse monitoring are not encrypted by Customer-managed encryption keys (CMEK). It may not be possible to opt-out of prompt-response logging when using some Advanced AI features. Please contact your account team for clarification.

  - **Automated investigation** : Google deploys automated investigative tools, including safety classifiers, to analyze logged data and detect potential abuse and violations.

  - **Action** : Authorized Google employees may assess the flagged prompts and may reach out to the customer for clarification. Failure to address the behavior—or recurring or severe abuse—may result in suspension or termination of the customer's access to Gemini Enterprise Agent Platform or Google Cloud services.

  - **Services in scope** : Models and features designated as "Advanced AI", including:
    
      - Claude Mythos (all versions)
      - Claude Opus \>=4.7 when used for high risk dual use or prohibited use cases covered under Anthropic's [Cyber Verification Program](https://support.claude.com/en/articles/14604842-real-time-cyber-safeguards-on-claude)

## Partner-specific terms

### Anthropic

Use of Anthropic models on Gemini Enterprise Agent Platform are further beholden to Anthropic's acceptable use policy and commercial use policy documented on anthropic.com. The abuse monitoring systems described above are used to ensure adherence to these terms.

## What's next

  - Learn about [Responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai) .
