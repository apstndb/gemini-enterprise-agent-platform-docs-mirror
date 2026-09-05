---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/safety
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/safety
title: Safety (Responsible AI)
description: Learn about the safety tools and practices available in Agent Platform to implement holistic safety for your models.
data_source: docs.cloud.google.com
---

Generative AI models like Gemini require robust safety measures to mitigate risks such as generating harmful content, leaking sensitive information, or being misused. Gemini Enterprise Agent Platform provides a suite of tools and practices to implement holistic safety for your Gemini models.

## Potential safety risks and mitigation strategies

When deploying Gemini models, it's crucial to identify and mitigate various potential risks. A proactive approach to understanding these risks allows for more effective implementation of safety measures. A multi-layered approach to safety is critical, as it can mitigate or prevent:

  - **Content risks:** These can include content that's harmful, profanity and sexualization, and violence and gore.
  - **Brand safety risks:** Generated content may not align with your brand's tone or values, it may endorse competitors or inappropriate products, or generate content that can result in reputational damage.
  - **Alignment risks:** Generated content may be irrelevant or inaccurate.
  - **Security and privacy risks:** Generated content may leak sensitive training data or prompts, or adversarial users may attempt to force the model to override safety protocols or behave in unintended ways.

Our deployed models offer various features to address these potential issues:

  - The default model and non-configurable filters provide a general safety net.
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/safety-system-instructions) provide direct guidance to the model on preferred behavior and topics to avoid.
  - [Content filters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/configure-safety-filters) allow you to set specific thresholds for common harm types.
  - [Gemini as a filter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-for-filtering-and-moderation) offers an advanced, customizable checkpoint for complex or nuanced safety concerns that might be missed by the preceding layers or require more context-aware evaluation.
  - [Sensitive Data Protection](https://docs.cloud.google.com/sensitive-data-protection/docs/sensitive-data-protection-overview#api) specifically addresses the critical risk of sensitive data leakage, in case the model has access to sensitive data. It also enables the ability to create custom block lists.
  - [Model Armor](https://docs.cloud.google.com/model-armor/overview) provides enterprise-grade protection against prompt injection and jailbreaks, content harms, sensitive data exposure, and malware detection.
  - [Content Credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials) add cryptographically signed C2PA metadata to images generated using the Gemini 3 Pro Image model, indicating that they are AI-generated and providing a verifiable history of their origin.

### Available safety tools in Agent Platform for Gemini

Agent Platform offers several tools to manage the safety of your Gemini models. Understanding how each works, their considerations, and ideal use cases will help you build a tailored safety solution.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Approach</th>
<th>How it works</th>
<th>Protection provided</th>
<th>Risks</th>
<th>When to use</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Default settings: Gemini + non-configurable filters</td>
<td>Gemini models are inherently designed with safety and fairness in mind, even when faced with adversarial prompts. Google has invested in comprehensive safety evaluations, including for bias and toxicity. The default settings include an independent protection layer designed to prevent the generation of content related to Child Sexual Abuse Material (CSAM) or Copyrighted Content (Recitation).</td>
<td>Baseline protection against Child sexual abuse material and copyright (Recitation)</td>
<td>Gemini's default safety might not meet your organization's needs. The model can hallucinate or not follow instructions. Motivated attackers may still succeed in jailbreaks and prompt injection</td>
<td>Workflows where no malicious input is expected</td>
</tr>
<tr class="even">
<td>Configurable Filters</td>
<td>Gemini's prebuilt content filters provide additional protection against various categories of harmful content, such as sexual, hate, harassment, or dangerous content. You can configure blocking thresholds for each harm category (e.g., <code dir="ltr" translate="no">BLOCK_LOW_AND_ABOVE</code> , <code dir="ltr" translate="no">BLOCK_MEDIUM_AND_ABOVE</code> , <code dir="ltr" translate="no">BLOCK_ONLY_HIGH</code> ) based on the probability and/or severity of the harmful content. These are an independent layer from the model so are robust against jailbreaks.</td>
<td>Robust against violations for predefined categories, adjustable sensitivity</td>
<td>Lacks fine-grained customization beyond threshold settings for predefined categories. May occasionally block benign content (false positives) or miss some harmful content (false negatives). Only available for response filtering, not prompt filtering.</td>
<td>Provide a base level of safety for user facing applications or agents. If your goal is to ensure content and brand safety, content filters should be paired with system instructions.</td>
</tr>
<tr class="odd">
<td>System Instructions</td>
<td>You can instruct the model on your brand and content safety guidelines through system instructions or preambles. For example, you can tell the model "don't answer questions related to politics" or to adhere to specific brand voice and tone guidelines. System instructions directly guide the model's behavior.</td>
<td>Customizable for content/brand safety, can be highly effective.</td>
<td>The model can hallucinate or not follow instructions. Motivated attackers may still succeed in jailbreaks and prompt injection</td>
<td>Applications or agents requiring adherence to specific brand guidelines or nuanced content policies. If your goal is to ensure content and brand safety, system instructions should be paired with content filters.</td>
</tr>
<tr class="even">
<td>Sensitive Data Protection for custom block lists</td>
<td>The DLP API can inspect text to identify and classify sensitive information based on a wide range of predefined and custom infoType detectors. Once identified, it can apply de-identification techniques such as redaction, masking, or tokenization. The DLP API can also be used to block keywords.
<p><strong>Input protection:</strong> Before sending user prompts or data to Gemini, you can pass the text through the DLP API to redact or mask any sensitive information. This prevents sensitive data from being processed or logged by the model.</p>
<p><strong>Output protection:</strong> If there's a risk that Gemini might inadvertently generate or reveal sensitive information (e.g., if it's summarizing source documents containing PII), the model's output can be scanned by the DLP API before being sent to the user.</p></td>
<td>Robust filtering for profanities or custom words. Robust filtering for sensitive data.</td>
<td>Adds latency. Can lead to over-blocking.</td>
<td>Sensitive Data Protection for agents that have access to sensitive data.</td>
</tr>
<tr class="odd">
<td>Model Armor</td>
<td>Model Armor is a Google Cloud service designed to enhance the security and safety of your AI applications. It works by proactively screening LLM prompts and responses, protecting against various risks and ensuring responsible AI practices. Whether you are deploying AI in Google Cloud or other cloud providers, Model Armor can help you prevent malicious input, verify content safety, protect sensitive data, maintain compliance, and enforce your AI safety and security policies consistently across your AI applications.</td>
<td>Prompt injection and jailbreak filtering, content filters, sensitive data protection, and malware detection and safe browsing.</td>
<td>Cost and latency.</td>
<td>Paid offering for customers with enterprise needs.</td>
</tr>
<tr class="even">
<td>Gemini as a Filter</td>
<td>You can use Gemini to filter prompts and responses for your agent or app. This involves making a second call to a fast and cost-effective Gemini model (such as Gemini Flash or Flash-Lite) to evaluate whether the input from a user or tool, or the output from your primary Gemini model, is safe. The filter model is given instructions to decide if the content is safe or unsafe based on your defined policies including content safety, brand safety, and agent misalignment. This offers robust and highly customizable protection against content safety violations, brand safety issues, model drift, and hallucinations and can analyze text, images, video, and audio for a holistic understanding.</td>
<td>Highly robust and customizable for content/brand safety, drift, hallucination; multimodal understanding.</td>
<td>Additional cost and latency. Chance of extremely rare false negatives.</td>
<td>Provide a custom level of safety for user-facing applications or agents.</td>
</tr>
<tr class="odd">
<td><strong>Combined approach:</strong> configurable filters + system instructions + Sensitive Data Protection + Gemini as a filter</td>
<td>Combines multiple protective layers: input and output data redaction with Sensitive Data Protection, system instructions for brand and topic guidelines, configurable safety filters for predefined harms, and secondary inspection using Gemini as a filter.</td>
<td>Highly robust and customizable for content/brand safety, drift, hallucination; multimodal understanding.</td>
<td>Additional cost and latency.</td>
<td>Provide a robust level of safety for user-facing applications or agents, especially where adversarial and malicious use is expected.</td>
</tr>
<tr class="even">
<td>C2PA Content Credentials</td>
<td>For supported models, Gemini Enterprise Agent Platform automatically adds cryptographically signed Content Credentials to generated images, indicating they are AI-generated and providing a verifiable history of their origin according to the <a href="https://www.c2pa.org/">C2PA</a> standard. For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials</a> .</td>
<td>Transparency about content origin; helps users identify AI-generated images.</td>
<td>Use of non-compliant tools can compromise file authenticity; does not guarantee trustworthiness of media source.</td>
<td>Media generation use cases, where transparency about the origin and history of the file is important for user trust.</td>
</tr>
</tbody>
</table>

### Continuous safety evaluation

Continuous safety evaluation is crucial for AI systems. The AI landscape and misuse methods are constantly evolving, making these evaluations essential.

Regular evaluations provide several key benefits. They help you identify vulnerabilities, assess mitigation effectiveness, adapt to evolving risks, ensure alignment with policies and values, build trust, and maintain compliance.

To achieve these benefits, you can perform various types of evaluations:

  - Development evaluations
  - Assurance evaluations
  - Red teaming
  - External evaluations
  - Benchmark testing

The scope of your evaluation should cover several critical areas:

  - Content safety
  - Brand safety
  - Relevance
  - Bias and fairness
  - Truthfulness
  - Robustness to adversarial attacks

Tools like Agent Platform's [Gen AI evaluation service](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/evaluation-overview) can assist in these efforts. Remember that iterative improvements, based on evaluation findings, are essential for responsible AI development.

## What's next

Overview

### [Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/overview)

Get an overview of how security administrators can define, apply, and manage policies that govern agent interactions.

Guide

### [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls)

Learn about security controls for Google Agent Platform.

Guide

### [Evaluate your agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/evaluate-agents)

Create and deploy a basic agent and use the Gen AI evaluation service to evaluate the agent
