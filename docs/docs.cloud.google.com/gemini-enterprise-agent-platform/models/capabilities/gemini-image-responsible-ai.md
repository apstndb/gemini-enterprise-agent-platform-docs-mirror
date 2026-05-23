---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-responsible-ai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-responsible-ai
title: Gemini image generation and responsible AI
description: Learn about responsible AI when using Gemini to generate images.
data_source: docs.cloud.google.com
---

To ensure a safe and responsible experience, Agent Platform's image generation capabilities are equipped with a multi-layered safety approach. This is designed to prevent the creation of inappropriate content, including sexually explicit, dangerous, violent, hateful, or toxic material.

All users must adhere to the Generative AI Prohibited Use Policy. This policy strictly forbids the generation of content that:

  - Relates to child sexual abuse or exploitation.
  - Facilitates violent extremism or terrorism.
  - Facilitates non-consensual intimate imagery.
  - Facilitates self-harm.
  - Is sexually explicit.
  - Constitutes hate speech.
  - Promotes harassment or bullying.

When provided with an unsafe prompt, the model might refuse to generate an image, or the prompt or generated response might be blocked by our safety filters.

  - Model refusal: If a prompt is potentially unsafe, the model might refuse to process the request. If this happens, the model usually gives a text response saying it can't generate unsafe images. The `FinishReason` is `STOP` .
  - Safety filter blocking:
      - If the prompt is identified as potentially harmful by a safety filter, the API returns `BlockedReason` in `PromptFeedback` .
      - If the response is identified as potentially harmful by a safety filter, the API response includes a `FinishReason` of `IMAGE_SAFETY` , `IMAGE_PROHIBITED_CONTENT` , or similar.

### Safety filter code categories

Depending on the safety filters you configure, your output may contain a safety reason code similar to the following:

``` 
    {
      "raiFilteredReason": "ERROR_MESSAGE. Support codes: 56562880"
    }
```

The listed code corresponds to a specific harmful category. The code-to-category mappings are as follows:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Error code</th>
<th>Safety category</th>
<th>Description</th>
<th>Content filtered: prompt input or image output</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>58061214<br />
17301594</td>
<td>Child</td>
<td>Detects child content that isn't allowed due to the API request settings or allowlisting.</td>
<td>input (prompt): 58061214<br />
output (image): 17301594</td>
</tr>
<tr class="even">
<td>29310472<br />
15236754</td>
<td>Celebrity</td>
<td>Detects a photorealistic representation of a celebrity in the request.</td>
<td>input (prompt): 29310472<br />
output (image): 15236754</td>
</tr>
<tr class="odd">
<td>62263041</td>
<td>Dangerous content</td>
<td>Detects content that's potentially dangerous in nature.</td>
<td>input (prompt)</td>
</tr>
<tr class="even">
<td>57734940<br />
22137204</td>
<td>Hate</td>
<td>Detects hate-related topics or content.</td>
<td>input (prompt): 57734940<br />
output (image): 22137204</td>
</tr>
<tr class="odd">
<td>74803281<br />
29578790<br />
42876398</td>
<td>Other</td>
<td>Detects other miscellaneous safety issues with the request.</td>
<td>input (prompt): 42876398<br />
output (image): 29578790, 74803281</td>
</tr>
<tr class="even">
<td>39322892</td>
<td>People/Face</td>
<td>Detects a person or face when it isn't allowed due to the request safety settings.</td>
<td>output (image)</td>
</tr>
<tr class="odd">
<td>92201652</td>
<td>Personal information</td>
<td>Detects Personally Identifiable Information (PII) in the text, such as credit card numbers, home addresses, or other similar information.</td>
<td>input (prompt)</td>
</tr>
<tr class="even">
<td>89371032<br />
49114662<br />
72817394</td>
<td>Prohibited content</td>
<td>Detects a request for prohibited content.</td>
<td>input (prompt): 89371032<br />
output (image): 49114662, 72817394</td>
</tr>
<tr class="odd">
<td>90789179<br />
63429089<br />
43188360</td>
<td>Sexual</td>
<td>Detects content that's sexual in nature.</td>
<td>input (prompt): 90789179<br />
output (image): 63429089, 43188360</td>
</tr>
<tr class="even">
<td>78610348</td>
<td>Toxic</td>
<td>Detects toxic topics or content in the text.</td>
<td>input (prompt)</td>
</tr>
<tr class="odd">
<td>61493863<br />
56562880</td>
<td>Violence</td>
<td>Detects violence-related content from the image or text.</td>
<td>input (prompt): 61493863<br />
output (image): 56562880</td>
</tr>
<tr class="even">
<td>32635315</td>
<td>Vulgar</td>
<td>Detects vulgar topics or content from the text.</td>
<td>input (prompt)</td>
</tr>
<tr class="odd">
<td>64151117</td>
<td>Celebrity or child</td>
<td>Detects photorealistic representation of a celebrity or child that violates Google's safety policies.</td>
<td>input (prompt)<br />
output (image)</td>
</tr>
</tbody>
</table>

## What's next?

See the following links for more information about Gemini image generation:

  - [Generate images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation)

  - [Edit images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images)

  - [Gemini image generation limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-limitations)

  - [Gemini image generation best practices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-best-practices)
