---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/prompt-iteration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/prompt-iteration
title: Prompt iteration strategies
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prompt design often requires a few iterations before you get the desired response consistently. Your prompt design strategy should apply the [Prompt design best practices](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-design-strategies#best-practices) , with incremental refinements. You can iteratively introduce some or all of the best practices when testing for performance that meets your use case needs.

Additionally, the order of the content in the prompt can sometimes affect the response. Try changing the content order and see how the response changes. For example, for multimodal prompts, try adding the files to the prompt before the instructions.

As you receive responses from the model, take note of the aspects that you like and dislike about its responses and modify your prompts to guide the model to responses that best align with your use cases.

## Examples

In this example, let's say you want the model to write ad copy for your product. You could start by defining the following prompt content:

  - **Objective:** Create ad copy
  - **Context:**
      - Categories: scarcity, exclusivity
      - Product description: "Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones & iPads, Windows and Mac laptops, and the Chromebook Pixel."
  - **Constraints:** Each response should be two sentences or less.

Experimenting with how you provide the content to the model can help you to ensure that the model's response best fits your needs. Suppose you give the model the prompt content exactly as written:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>First iteration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Create ad copy.

      Categories: scarcity, exclusivity

      Product description: &quot;Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones &amp; iPads, Windows and Mac laptops, and the Chromebook Pixel.&quot;

      Constraints: Each response should be two sentences or less.
    </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Scarcity

      *  Time is running out to experience the future of entertainment! Get your Chromecast before they&#39;re gone.
      *  Limited quantities available! Don&#39;t miss your chance to own the streaming device everyone&#39;s talking about.

      Exclusivity

      *  Unlock a world of entertainment with Chromecast. Experience the freedom of streaming like never before.
      *  Upgrade your home entertainment with the exclusive Chromecast device. Join the elite group of cord-cutters who stream smarter.
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

Then you can try reformatting the prompt to see how the response changes when the prompt objective, constraints, and some of the context are combined into a single sentence:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Second iteration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Create scarcity and exclusivity-focused ad copy that is less than two sentences.

      Product description: &quot;Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones &amp; iPads, Windows and Mac laptops, and the Chromebook Pixel.&quot;
    </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Options for Scarcity &amp; Exclusivity-Driven Chromecast Ads:

      Option 1 (Scarcity): &quot;Limited quantities available! Get your Chromecast today before they&#39;re gone and unlock a world of on-demand entertainment.&quot;

      Option 2 (Exclusivity): &quot;Experience entertainment like never before. Chromecast: the ultimate upgrade for your TV, available for a limited time.&quot;
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

This time, the model's response contained only one copy option for each category. If you realize that you need at least two options for each category and that you don't want to limit the length of the response, you can modify the constraints and try your prompt again:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Third iteration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Create two ad-copies about scarcity and two ad-copies about exclusivity.

      Product description: &quot;Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones &amp; iPads, Windows and Mac laptops, and the Chromebook Pixel.&quot;
    </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>    Scarcity Ad Copies:
    Ad 1:

    Headline: Don&#39;t miss out! Chromecast is flying off the shelves!

    Body: Experience the magic of Chromecast before it&#39;s too late! Limited quantities are available, so grab yours now and start enjoying your favorite entertainment on the big screen. 

    Ad 2:

    Headline: Last chance! Chromecast is almost sold out.

    Body: Time is running out to get your hands on Chromecast. Upgrade your TV experience today and enjoy seamless streaming from all your devices. Don&#39;t wait, supplies are limited!


    Exclusivity Ad Copies:

    Ad 1:

    Headline: Unlock a world of entertainment with the exclusive Chromecast.

    Body: Join the elite group of Chromecast users and experience the future of television. Enjoy effortless streaming, endless entertainment options, and unparalleled convenience. Chromecast: It&#39;s not just TV, it&#39;s an experience.

    Ad 2:

    Headline: Elevate your home entertainment with the Chromecast advantage.

    Body: Go beyond ordinary TV with Chromecast. Seamlessly stream content from all your devices and enjoy a personalized entertainment experience like no other. Discover the exclusivity of Chromecast today. 
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

In the third iteration, the model's response contained both headline and body fields for the ad copy. For this example, let's say that this response aligns with your ad copy requirements.

Now that you've adjusted the prompt to get a response that aligns with your ad copy requirements, you can update and test the prompt to ensure the model produces similarly formatted responses in the future:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Fourth iteration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Create two ad-copies about scarcity and two ad-copies about exclusivity.

      Include a headline and body for each ad copy.

      Product description: &quot;Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones &amp; iPads, Windows and Mac laptops, and the Chromebook Pixel.&quot;
    </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>    Scarcity Ads:

    Ad 1:

    Headline: Last Chance! Chromecast is Selling Out Fast
    Body: Get the Chromecast experience before it&#39;s gone! Limited quantities remain. Upgrade your TV time today!

    Ad 2:

    Headline: Don&#39;t Miss Out! Chromecast Stock is Running Low
    Body: Time is running out to grab your Chromecast. Enjoy seamless streaming on the big screen. Order now while supplies last!

    Exclusivity Ads:

    Ad 1:

    Headline: Unlock the Ultimate Viewing Experience with Chromecast
    Body: Join the elite group of Chromecast users and enjoy unparalleled streaming convenience. Elevate your entertainment today!

    Ad 2:

    Headline: Experience the Future of Entertainment: Get Your Chromecast
    Body: Be among the first to enjoy the cutting-edge technology of Chromecast. Stream anything, anytime, effortlessly.  Upgrade your home entertainment now!
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

This time, the model's response is very similar to the previous iteration, even with the additional constraints, which means that you successfully iterated upon your prompt.

As demonstrated by the example, prompt iteration is an integral part of the prompt design process that can be used to help you guide the model to produce the best results for your use case.

## What's next

  - Explore more examples of prompts in the [Prompt gallery](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/prompt-gallery) .
  - Learn how to optimize prompts for use with [Google models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models) by using the [Gemini Enterprise Agent Platform prompt optimizer (Preview)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/prompt-optimizer) .
