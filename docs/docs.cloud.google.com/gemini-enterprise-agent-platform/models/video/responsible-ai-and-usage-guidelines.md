---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines
title: Responsible AI for Veo on Gemini Enterprise Agent Platform video generation
description: Explains Veo's built-in safety features to block potentially harmful content, Google's content safety filters, and the safety filter codes that you may see when generating Veo videos.
data_source: docs.cloud.google.com
---

Veo on Gemini Enterprise Agent Platform is designed with Google's [AI principles](https://ai.google/responsibility/principles/) in mind. However, it is important for developers to understand how to test and deploy Google's models safely and responsibly. To aid developers, Veo on Gemini Enterprise Agent Platform has built-in safety features to help customers block potentially harmful outputs within their use cases. For more information, see [safety filters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines#safety-filters) .

We encourage customers to use fairness, interpretability, privacy, and security best practices when developing AI applications. For more information, see [The People + AI Guidebook](https://pair.withgoogle.com/guidebook/) .

## Safety filters

Veo on Gemini Enterprise Agent Platform offers several ways to input prompts to generate videos, including text, video, and images. Prompts that are provided to Veo are assessed against a list of safety filters, which include *harmful categories* (for example, `violence` , `sexual` , `derogatory` , and `toxic` ). These safety filters aim to filter out input images and videos that violate the [Google Cloud Platform Acceptable Use Policy](https://cloud.google.com/terms/aup?e=48754805) , [Generative AI Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) , or [Our AI Principles](https://ai.google/responsibility/principles/) .

If the model responds to a request with an error message, such as `The prompt couldn't be submitted` or `it might violate our policies` , then the input is triggering a safety filter. If fewer videos than requested are returned, then some generated output is being blocked for not meeting safety requirements.

## Safety filter code categories

Depending on the safety filters that you configure, your output may contain a safety code similar to: "Veo could not generate videos because the input image violates Agent Platform's usage guidelines. If you think this was an error, send feedback. Support codes: **15236754** "

The code listed in the output corresponds to a specific harmful category.

The following table displays the support code to safety category mappings:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Support code</th>
<th>Safety category</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">58061214</code><br />
<code dir="ltr" translate="no">17301594</code></td>
<td>Child</td>
<td>Rejects requests to generate content depicting children if <code dir="ltr" translate="no">personGeneration</code> isn't set to <code dir="ltr" translate="no">"allow_all"</code> or if the project isn't on the allowlist for this feature.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">29310472</code><br />
<code dir="ltr" translate="no">15236754</code></td>
<td>Celebrity</td>
<td>Rejects requests to generate a photorealistic representation of a prominent person or if the project isn't on the allowlist for this feature.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">64151117</code><br />
<code dir="ltr" translate="no">42237218</code></td>
<td>Video safety violation</td>
<td>General safety violation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">62263041</code></td>
<td>Dangerous content</td>
<td>Potentially dangerous content.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">57734940</code><br />
<code dir="ltr" translate="no">22137204</code></td>
<td>Hate</td>
<td>Hate-related content.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">74803281</code><br />
<code dir="ltr" translate="no">29578790</code><br />
<code dir="ltr" translate="no">42876398</code></td>
<td>Other</td>
<td>Miscellaneous safety issues with the request</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">89371032</code><br />
<code dir="ltr" translate="no">49114662</code><br />
<code dir="ltr" translate="no">63429089</code><br />
<code dir="ltr" translate="no">72817394</code><br />
<code dir="ltr" translate="no">60599140</code><br />
</td>
<td>Prohibited content</td>
<td>Prohibited content related to child safety or other sensitive content.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">35561574</code><br />
<code dir="ltr" translate="no">35561575</code></td>
<td>Third-party content</td>
<td>Guardrails related to third-party content.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">90789179</code><br />
<code dir="ltr" translate="no">43188360</code></td>
<td>Sexual</td>
<td>Sexual or suggestive content.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">78610348</code></td>
<td>Toxic</td>
<td>Toxic content.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">61493863</code><br />
<code dir="ltr" translate="no">56562880</code></td>
<td>Violence</td>
<td>Violent content.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">32635315</code></td>
<td>Vulgar</td>
<td>Vulgar content.</td>
</tr>
</tbody>
</table>

## What's next

  - Learn about [Responsible AI for Large Language Models (LLMs)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai)

  - Learn more about Google's recommendations for [Responsible AI practices](https://ai.google/responsibilities/responsible-ai-practices/?category=general)

  - Read our blog, [A shared agenda for responsible AI progress](https://blog.google/technology/ai/a-shared-agenda-for-responsible-ai-progress/)
