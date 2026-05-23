---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/few-shot-examples
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/few-shot-examples
title: Include few-shot examples
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

You can include examples in the prompt that show the model what a good response looks like. The model attempts to identify patterns and relationships from the examples and applies them when generating a response. Prompts that contain examples are called *few-shot* prompts, while prompts that provide no examples are called *zero-shot prompts* . Few-shot prompts are often used to regulate the output formatting, phrasing, scoping, or general patterning of model responses. Use specific and varied examples to help the model narrow its focus and generate more accurate results.

Including few-shot examples in your prompts helps make them more reliable and effective. However, you should always accompany few-shot examples with clear instructions. Without clear instructions, models might pick up on unintended patterns or relationships from the examples, which can lead to poor results.

The key points to this strategy are as follows:

  - Including prompt-response examples in the prompt helps the model learn how to respond.
  - Use XML-like markup to markup the examples.
  - Experiment with the number of prompts to include. Depending on the model, too few examples are ineffective at changing model behavior. Too many examples can cause the model to overfit.
  - Use consistent formatting across examples

## Zero-shot versus few-shot prompts

The following zero-shot prompt asks the model to extract the technical specifications from text and output it in JSON format:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>Extract the technical specifications from the text below in JSON format.

Google Pixel 7, 5G network, 8GB RAM, Tensor G2 processor, 128GB of storage, Lemongrass
  </code></pre>
<strong>Response:</strong>
<div class="sourceCode" id="cb2" dir="ltr" data-is-upgraded="" style="border:1px solid Black;" translate="no"><pre class="sourceCode json"><code class="sourceCode json"><span id="cb2-1"><a href="#cb2-1"></a>    <span class="fu">{</span></span>
<span id="cb2-2"><a href="#cb2-2"></a>      <span class="dt">&quot;Network&quot;</span><span class="fu">:</span> <span class="st">&quot;5G&quot;</span><span class="fu">,</span></span>
<span id="cb2-3"><a href="#cb2-3"></a>      <span class="dt">&quot;RAM&quot;</span><span class="fu">:</span> <span class="st">&quot;8GB&quot;</span><span class="fu">,</span></span>
<span id="cb2-4"><a href="#cb2-4"></a>      <span class="dt">&quot;Processor&quot;</span><span class="fu">:</span> <span class="st">&quot;Tensor G2&quot;</span><span class="fu">,</span></span>
<span id="cb2-5"><a href="#cb2-5"></a>      <span class="dt">&quot;Storage&quot;</span><span class="fu">:</span> <span class="st">&quot;128GB&quot;</span><span class="fu">,</span></span>
<span id="cb2-6"><a href="#cb2-6"></a>      <span class="dt">&quot;Color&quot;</span><span class="fu">:</span> <span class="st">&quot;Lemongrass&quot;</span></span>
<span id="cb2-7"><a href="#cb2-7"></a>    <span class="fu">}</span></span>
<span id="cb2-8"><a href="#cb2-8"></a>  </span></code></pre></div>
(gemini-pro)</td>
</tr>
</tbody>
</table>

Suppose that your use case requires specific formatting, such as using lowercase key names. You can include examples in the prompt that shows the model how to format the JSON. The following few-shot prompt demonstrates an output format where the JSON keys are lowercase:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<div class="sourceCode" id="cb1" dir="ltr" data-is-upgraded="" style="border:1px solid Black;" translate="no"><pre class="sourceCode json"><code class="sourceCode json"><span id="cb1-1"><a href="#cb1-1"></a><span class="er">Extract</span> <span class="er">the</span> <span class="er">technical</span> <span class="er">specifications</span> <span class="er">from</span> <span class="er">the</span> <span class="er">text</span> <span class="er">below</span> <span class="er">in</span> <span class="er">a</span> <span class="er">JSON</span> <span class="er">format.</span></span>
<span id="cb1-2"><a href="#cb1-2"></a></span>
<span id="cb1-3"><a href="#cb1-3"></a><span class="er">&lt;EXAMPLE&gt;</span></span>
<span id="cb1-4"><a href="#cb1-4"></a>  <span class="er">INPUT:</span> <span class="er">Google</span> <span class="er">Nest</span> <span class="er">Wifi,</span> <span class="er">network</span> <span class="er">speed</span> <span class="er">up</span> <span class="er">to</span> <span class="er">1200Mpbs,</span> <span class="er">2.4GHz</span> <span class="er">and</span> <span class="er">5GHz</span> <span class="er">frequencies,</span> <span class="er">WP3</span> <span class="er">protocol</span></span>
<span id="cb1-5"><a href="#cb1-5"></a></span>
<span id="cb1-6"><a href="#cb1-6"></a>  <span class="er">OUTPUT:</span></span>
<span id="cb1-7"><a href="#cb1-7"></a>  <span class="fu">{</span></span>
<span id="cb1-8"><a href="#cb1-8"></a>    <span class="dt">&quot;product&quot;</span><span class="fu">:</span><span class="st">&quot;Google Nest Wifi&quot;</span><span class="fu">,</span></span>
<span id="cb1-9"><a href="#cb1-9"></a>    <span class="dt">&quot;speed&quot;</span><span class="fu">:</span><span class="st">&quot;1200Mpbs&quot;</span><span class="fu">,</span></span>
<span id="cb1-10"><a href="#cb1-10"></a>    <span class="dt">&quot;frequencies&quot;</span><span class="fu">:</span> <span class="ot">[</span><span class="st">&quot;2.4GHz&quot;</span><span class="ot">,</span> <span class="st">&quot;5GHz&quot;</span><span class="ot">]</span><span class="fu">,</span></span>
<span id="cb1-11"><a href="#cb1-11"></a>    <span class="dt">&quot;protocol&quot;</span><span class="fu">:</span><span class="st">&quot;WP3&quot;</span></span>
<span id="cb1-12"><a href="#cb1-12"></a>  <span class="fu">}</span></span>
<span id="cb1-13"><a href="#cb1-13"></a><span class="er">&lt;/EXAMPLE&gt;</span></span>
<span id="cb1-14"><a href="#cb1-14"></a></span>
<span id="cb1-15"><a href="#cb1-15"></a>  <span class="er">Google</span> <span class="er">Pixel</span> <span class="er">7,</span> <span class="er">5G</span> <span class="er">network,</span> <span class="er">8GB</span> <span class="er">RAM,</span> <span class="er">Tensor</span> <span class="er">G2</span> <span class="er">processor,</span> <span class="er">128GB</span> <span class="er">of</span> <span class="er">storage,</span> <span class="er">Lemongrass</span></span>
<span id="cb1-16"><a href="#cb1-16"></a>  </span></code></pre></div>
<strong>Response:</strong>
<div class="sourceCode" id="cb2" dir="ltr" data-is-upgraded="" style="border:1px solid Black;" translate="no"><pre class="sourceCode json"><code class="sourceCode json"><span id="cb2-1"><a href="#cb2-1"></a>    <span class="fu">{</span></span>
<span id="cb2-2"><a href="#cb2-2"></a>      <span class="dt">&quot;product&quot;</span><span class="fu">:</span> <span class="st">&quot;Google Pixel 7&quot;</span><span class="fu">,</span></span>
<span id="cb2-3"><a href="#cb2-3"></a>      <span class="dt">&quot;network&quot;</span><span class="fu">:</span> <span class="st">&quot;5G&quot;</span><span class="fu">,</span></span>
<span id="cb2-4"><a href="#cb2-4"></a>      <span class="dt">&quot;ram&quot;</span><span class="fu">:</span> <span class="st">&quot;8GB&quot;</span><span class="fu">,</span></span>
<span id="cb2-5"><a href="#cb2-5"></a>      <span class="dt">&quot;processor&quot;</span><span class="fu">:</span> <span class="st">&quot;Tensor G2&quot;</span><span class="fu">,</span></span>
<span id="cb2-6"><a href="#cb2-6"></a>      <span class="dt">&quot;storage&quot;</span><span class="fu">:</span> <span class="st">&quot;128GB&quot;</span><span class="fu">,</span></span>
<span id="cb2-7"><a href="#cb2-7"></a>      <span class="dt">&quot;color&quot;</span><span class="fu">:</span> <span class="st">&quot;Lemongrass&quot;</span></span>
<span id="cb2-8"><a href="#cb2-8"></a>    <span class="fu">}</span></span>
<span id="cb2-9"><a href="#cb2-9"></a>  </span></code></pre></div>
(gemini-pro)</td>
</tr>
</tbody>
</table>

Note that the example uses XML-like formatting to separate the components of the prompt. To learn more about how to optimally format few-shot prompts using XML-like formatting, see [Structure prompts](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/structure-prompts) .

## Find the optimal number of examples

You can experiment with the number of examples to provide in the prompt for the most desired results. Models like Gemini can often pick up on patterns using a few examples, though you may need to experiment with what number of examples leads to the desired results. At the same time, if you include too many examples, the model might start to [overfit](https://developers.google.com/machine-learning/glossary#overfitting) the response to the examples.

## What's next

  - Explore more examples of prompts in the [Prompt gallery](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/prompt-gallery) .
