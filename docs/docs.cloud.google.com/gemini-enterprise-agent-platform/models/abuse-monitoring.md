---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring
title: Abuse monitoring
description: Review how Google monitors potential abuse, enforces Acceptable Use and Prohibited Use policies, and attributes end-user API calls with safety identifiers.
data_source: docs.cloud.google.com
---

Google monitors generative AI traffic on Gemini Enterprise Agent Platform to detect potential violations of the Acceptable Use Policy (AUP) and Prohibited Use Policy. Multi-tenant applications and API resellers can also pass an anonymized `safety_identifier` label so policy feedback targets specific end users rather than an entire project.

## Google models not designated as "Google Frontier Models" or "Advanced AI"

As outlined in Section 4.3 "Generative AI Safety and Abuse" of [Google Cloud Platform Terms of Service](https://cloud.google.com/terms/) , Google uses the following process to detect potential abuse and violations of its [Acceptable Use Policy](https://cloud.google.com/terms/aup) and [Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) as part of providing Generative AI Services to customers.

- **Automated detection** : Google uses automated safety classifiers to detect potential abuse and violations.

- **Prompt logging and human review** : If automated safety classifiers detect suspicious activity that requires further investigation into whether a customer has violated our policies, then Google may log customer prompts solely for the purpose of examining whether a violation of the AUP or Prohibited Use Policy has occurred. This data won't be used to train or fine-tune any AI/ML models. This data is stored securely for up to 90 days in the same region or multi-region selected by the customer for their project and adheres to Google Cloud assurances, such as Data Residency, Access Transparency and VPC Service Controls. Prompt logs for the purposes of abuse monitoring are not encrypted by Customer-managed encryption keys (CMEK).

  - **Action** : Authorized Google employees may assess the flagged prompts and may reach out to the customer for clarification. Failure to address the behavior—or recurring or severe abuse—may result in suspension or termination of the customer's access to Gemini Enterprise Agent Platform or Google Cloud services.

  - **Services in scope** : Google's Generative AI Services.

  - **Customers in scope** : Only customers whose use of Google Cloud is governed by the [Google Cloud Platform Terms of Service](https://cloud.google.com/terms/) . This means that customers with a Google Cloud Master Agreement are exempt from prompt logging for this abuse monitoring by default.

## Google Frontier Models

As outlined in Section 34 of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , "Google Frontier Models," Google uses the following process to detect potential abuse and violations of its agreements, including the [Acceptable Use Policy](https://cloud.google.com/terms/aup) and [Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) , as part of providing Generative AI Services to customers.

- **Prompt and response logging for abuse monitoring** : Google may log customer prompts and responses solely for ensuring safe use of the Google Frontier Models and compliance with customer's Google agreement ("Purpose" set forth in the [Service Specific Terms](https://cloud.google.com/terms/service-terms) ). This includes automated processing to create anonymized shingles and analyze usage patterns solely for the purpose described above. This data won't be used to train or fine-tune any AI/ML models. These logs are stored securely inside the customer's environment for up to 30 days. Prompt logs for the purposes of abuse monitoring are not encrypted by CMEK. Customers are not charged for this logging.

- **ZDR-aligned abuse logging for customers with Cloud Master Agreements** : Section 34 "Google Frontier Models" of [Service Specific Terms](https://cloud.google.com/terms/service-terms) does not give Google the right to conduct human review. Consequently, these logs adhere to ZDR standards for customers with Cloud Master Agreements, as they are stored inside the customer's environment and exempt from human review.

- **Human review of abuse logs for customers covered under Google Cloud online terms** : As outlined in Section 4.3 "Generative AI Safety and Abuse" of [Google Cloud Platform Terms of Service](https://cloud.google.com/terms/) , Google may additionally conduct human review of prompts flagged by our abuse classifiers, solely for the purpose of determining whether a violation of the AUP or Prohibited Use Policy has occurred. This data won't be used to train or fine-tune any AI/ML models. Only customers whose use of Google Cloud is governed by the [Google Cloud Platform Terms of Service](https://cloud.google.com/terms/) are in scope for human review. This means that customers with a Google Cloud Master Agreement are exempt from human review for this abuse monitoring by default.

- **Models in scope** : [Gemini 4 Carbon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon) (Google Frontier Model), [Gemini 4 Carbon for cyber](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon#cyber) (Google Frontier Cyber Model), [Gemini 4 Argon Cyber Permissive](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon#cyber) (Google Frontier Cyber Model)

- **Services in scope** : Google's Generative AI Services.

## Non-Google Advanced AI models

As outlined in the [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) , Google Cloud has implemented a more rigorous abuse monitoring system for models designated as "Advanced AI".

- **Prompt and response logging** : All prompts and responses will be logged and securely stored for up to 30 days for the sole purpose of monitoring for abuse. This data won't be used to train or fine-tune any AI/ML models. This data is stored in the same region or multi-region selected by the customer for their project and adheres to Google Cloud assurances, such as Data Residency, Access Transparency and VPC Service Controls. Prompt and response logs for the purposes of abuse monitoring are not encrypted by CMEK. It may not be possible to opt-out of prompt-response logging when using some Advanced AI features. Please contact your account team for clarification.

- **Automated investigation** : Google and Model Providers deploy automated investigative tools, including safety classifiers, to analyze logged data and detect potential abuse and violations.

- **Action** : Authorized Google employees may assess the flagged prompts and may reach out to the customer for clarification. Failure to address the behavior—or recurring or severe abuse—may result in suspension or termination of the customer's access to Gemini Enterprise Agent Platform or Google Cloud services.

- **Services in scope** : Models and features designated as "Advanced AI", including:

  - Anthropic models:

    - Claude Mythos (all versions)
    - Claude Fable (all versions)
    - Claude Opus \>=4.7 and Sonnet \>=5 when `advanced_ai_enabled` is set to `true` for use within Anthropic's [Cyber Verification Program](https://support.claude.com/en/articles/14604842-real-time-cyber-safeguards-on-claude) (CVP). All other usage of these models is out of scope of the Advanced AI Safety Addendum. To enroll and enable CVP for Claude models, see [Cyber Verification Program for Claude](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/cyber-verification-program) .

  - OpenAI models:

    - GPT Astra (all versions)
    - GPT Sol (all versions)
    - GPT Terra (all versions)
    - GPT Luna (all versions)
    - All other OpenAI models available on the platform are not designated as "Advanced AI" and aren't governed by the Advanced AI Safety Addendum.

- **Customer opt-out** : Some model providers offer Zero Data Retention (ZDR) for specific models, which exempts approved projects from the Advanced AI Safety Addendum, but access is not guaranteed and requires provider approval. Contact your Google Cloud account team for details based on your needs.

### Consent to the Advanced AI Safety Addendum

Consent to the Advanced AI Safety Addendum is required once per project before Advanced AI models can be enabled in that project. Consent is performed in Model Garden through the Google Cloud console before enabling any Advanced AI model.

Consenting users must acknowledge that they are acting on behalf of their organization and possess the requisite authority to bind the customer to the obligations of the addendum. In order to consent, a user must have the `aiplatform.consents.update` permission which is included in the `aiplatform.admin` role.

### Govern the Advanced AI Safety Addendum

To prevent your users from consenting to this addendum admins can:

- Enforce least privileges in [IAM](https://docs.cloud.google.com/iam/docs/roles-overview) for the `aiplatform.consents.update` permission.
- [Disable access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) included in the Advanced AI Safety Addendum scope.

## Partner-specific terms

Use of partner models on Gemini Enterprise Agent Platform is subject to partner-specific terms.

### Anthropic

Use of Anthropic models on Gemini Enterprise Agent Platform is governed by Anthropic's [Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms) or other applicable agreement with Anthropic, with use of Anthropic Advanced AI governed by Section F of Anthropic's [Service Specific Terms](https://www.anthropic.com/legal/service-specific-terms) . The abuse monitoring systems described on this page are used to ensure adherence to these terms.

#### Data retention

For Anthropic Anthropic's Claude Fable 5 on Google Cloud and Mythos 5, prompts and responses are retained for up to 30 days. To use Anthropic's Claude Fable 5 on Google Cloud and Mythos 5, as required by Anthropic, you must enable sharing this data with Anthropic for abuse monitoring.

## Pass an end-user safety identifier in API calls

API resellers, model aggregators, and applications with external users can pass a unique `safety_identifier` key in the request `labels` field. Attaching per-user safety identifiers helps Google attribute policy violations to specific end users and avoid project-wide enforcement actions.

When you pass `safety_identifier` in API requests, follow these requirements:

- **Format and length** : Assign each end user a unique string from 1 to 63 characters containing only lowercase letters, digits, underscores ( `_` ), or hyphens ( `-` ). Values exceeding 63 characters or containing uppercase letters or symbols such as `@` or `.` fail with an HTTP `400 INVALID_ARGUMENT` error. If you hash user IDs with SHA-256, truncate the lowercase hex digest to 63 characters or fewer.
- **Privacy** : Don't include personally identifiable information (PII), such as email addresses or full names, in `safety_identifier` values. Use anonymized usernames or truncated hashes instead.
- **Supported models and endpoints** : Supported on Gemini `generateContent` and `streamGenerateContent` requests ( `global` , multi-region, and regional endpoints) and Veo `predictLongRunning` requests (regional endpoints such as `us-central1` ).
- **Access and billing** : Passing `labels` requires no extra IAM permissions beyond the `aiplatform.endpoints.predict` prediction permission and adds no extra API charges. Keys with more than 1,000 unique values per Cloud Billing account might be omitted from cost reports without affecting abuse attribution. For general label limits, see [Requirements for labels](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls#requirements) .

The following samples pass an end-user `safety_identifier` in the `labels` field:

### REST (Gemini)

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . . For example, `my-genai-project` .
- Replace `user_session_001` in `labels.safety_identifier` with your anonymized end-user identifier (1 to 63 lowercase letters, digits, underscores, or hyphens, with no personally identifiable information).

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.5-flash:generateContent
```

Request JSON body:

```
{
  "contents": [
    {
      "role": "user",
      "parts": [
        {
          "text": "Summarize the key responsibilities of an API gateway."
        }
      ]
    }
  ],
  "labels": {
    "safety_identifier": "user_session_001"
  }
}
```

To send your request, choose one of these options:

#### curl

The following command uses `gcloud auth print-access-token` with user credentials for local testing. In production environments, use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) with an attached service account.

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.5-flash:generateContent"
```

#### PowerShell

The following command uses `gcloud auth print-access-token` with user credentials for local testing. In production environments, use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) with an attached service account.

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.5-flash:generateContent" | Select-Object -Expand Content
```

A successful request returns an HTTP `200 OK` JSON response containing generated `candidates` and `usageMetadata` :

#### Response

```
{
  "candidates": [
    {
      "content": {
        "role": "model",
        "parts": [
          {
            "text": "An API gateway routes client requests, enforces authentication and rate limits, and centralizes observability across backend services."
          }
        ]
      },
      "finishReason": "STOP"
    }
  ],
  "usageMetadata": {
    "promptTokenCount": 10,
    "candidatesTokenCount": 24,
    "totalTokenCount": 34
  }
}
```

### Python (Gemini)

Using the Google Gen AI SDK for Python ( `google-genai >= 1.0.0` ), replace `PROJECT_ID` with your Google Cloud project ID (for example, `my-genai-project` ):

```
from google import genai
from google.genai import types

client = genai.Client(
    vertexai=True,
    project="PROJECT_ID",
    location="global",
)

response = client.models.generate_content(
    model="gemini-3.5-flash",
    contents="Summarize the key responsibilities of an API gateway.",
    config=types.GenerateContentConfig(
        labels={"safety_identifier": "user_session_001"},
    ),
)
print(response.text)
```

### REST (Veo)

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . . For example, `my-genai-project` .
- Replace `user_session_001` in `labels.safety_identifier` with your anonymized end-user identifier (1 to 63 lowercase letters, digits, underscores, or hyphens, with no personally identifiable information).

HTTP method and URL:

```
POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/veo-3.1-generate-001:predictLongRunning
```

Request JSON body:

```
{
  "instances": [
    {
      "prompt": "A slow aerial pan over a coastal lighthouse at sunrise."
    }
  ],
  "parameters": {
    "aspectRatio": "16:9",
    "sampleCount": 1
  },
  "labels": {
    "safety_identifier": "user_session_001"
  }
}
```

To send your request, choose one of these options:

#### curl

The following command uses `gcloud auth print-access-token` with user credentials for local testing. In production environments, use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) with an attached service account.

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/veo-3.1-generate-001:predictLongRunning"
```

#### PowerShell

The following command uses `gcloud auth print-access-token` with user credentials for local testing. In production environments, use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) with an attached service account.

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/veo-3.1-generate-001:predictLongRunning" | Select-Object -Expand Content
```

A successful request returns an HTTP `200 OK` JSON response containing a long-running operation resource `name` :

#### Response

```
{
  "name": "projects/my-genai-project/locations/us-central1/publishers/google/models/veo-3.1-generate-001/operations/7f8e9d0c-1234-5678-9abc-def012345678"
}
```

### Python (Veo)

Using the Google Gen AI SDK for Python ( `google-genai >= 1.69.0` ), replace `PROJECT_ID` with your Google Cloud project ID (for example, `my-genai-project` ):

```
from google import genai
from google.genai import types

client = genai.Client(
    vertexai=True,
    project="PROJECT_ID",
    location="us-central1",
)

operation = client.models.generate_videos(
    model="veo-3.1-generate-001",
    prompt="A slow aerial pan over a coastal lighthouse at sunrise.",
    config=types.GenerateVideosConfig(
        aspect_ratio="16:9",
        labels={"safety_identifier": "user_session_001"},
    ),
)
print(operation.name)
```

## What's next

- Learn about [Responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai) .
- Add [custom metadata labels to API calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls) .
