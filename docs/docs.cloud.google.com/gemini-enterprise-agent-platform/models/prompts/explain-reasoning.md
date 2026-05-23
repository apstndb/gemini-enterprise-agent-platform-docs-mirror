---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/explain-reasoning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/explain-reasoning
title: Instruct the model to explain its reasoning
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

When you tell the model to explain its reasoning, the model responds with the steps that it employs to solve the problem. Going through this process can sometimes improve accuracy and nuance, especially for challenging queries.

The reasoning steps are included as part of the response. To parse out the reasoning steps from the answer that you're looking for, you can specify an output format by using XML or other separators.

## Examples

For example, suppose you're writing a cooking blog and you want the model to tell you how readers might interpret different parts of the blog. If you don't instruct the model to explain its reasoning, the response from the model might not be as useful as you'd like:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>No reasoning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>    What is the most likely interpretation of this sentence?
    
    The sentence: &quot;The chef seasoned the chicken and put it in the oven because it looked pale.&quot;
    </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>    The chef seasoned the chicken and put it in the oven because it lacked color and needed cooking.
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

While you learned about how the model predicts readers might interpret the sentence, it might be useful for you to understand more about the specific predictions that the model made to produce the response. As demonstrated in the following example, the quality of the response might also improve:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Explain reasoning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>    What is the most likely interpretation of this sentence? Explain your reasoning
    
    The sentence: &quot;The chef seasoned the chicken and put it in the oven because it looked pale.&quot;
    </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>      Interpreting &quot;The chef seasoned the chicken and put it in the oven because it looked pale.&quot;

      The most likely interpretation is that the chef seasoned the chicken to add flavor and color, then put it in the oven to cook it.

      Here&#39;s the reasoning:

      - Seasoning is typically used to enhance the flavor of food. Chefs often use spices, herbs, and other ingredients to make their dishes more appealing.
      - &quot;Pale&quot; suggests the chicken lacked visual appeal before being seasoned. This could imply it was unseasoned or simply lacking color from spices.
      - Putting the chicken in the oven is a common cooking method. The sentence implies the chef&#39;s intention is to cook the chicken, not just season it.

      Therefore, the chef&#39;s actions are likely aimed at both improving the taste and appearance of the chicken through seasoning and then cooking it in the oven.
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

Another technique you can use to improve the model's response is to instruct the model to think step-by-step and explain it's reasoning. This requires the model to break down the input into steps and provide the reasoning its using to solve the problem:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Think step-by-step</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>    What is the most likely interpretation of this sentence? Think step by step and print out
    the thinking process.

    Please output in JSON format with final answer in &#39;answer&#39;, and thinking steps in &#39;think&#39; fields.
    
    The sentence: &quot;The chef seasoned the chicken and put it in the oven because it looked pale.&quot;
    </code></pre>
<strong>Response:</strong>
<div class="sourceCode" id="cb2" dir="ltr" data-is-upgraded="" style="border:1px solid Black;" translate="no"><pre class="sourceCode json"><code class="sourceCode json"><span id="cb2-1"><a href="#cb2-1"></a>    <span class="fu">{</span></span>
<span id="cb2-2"><a href="#cb2-2"></a>      <span class="dt">&quot;answer&quot;</span><span class="fu">:</span> <span class="st">&quot;The chef seasoned the chicken to enhance its flavor and put it in the oven to cook it because it appeared to be undercooked.&quot;</span><span class="fu">,</span></span>
<span id="cb2-3"><a href="#cb2-3"></a>      <span class="dt">&quot;think&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-4"><a href="#cb2-4"></a>        <span class="fu">{</span></span>
<span id="cb2-5"><a href="#cb2-5"></a>          <span class="dt">&quot;step&quot;</span><span class="fu">:</span> <span class="dv">1</span><span class="fu">,</span></span>
<span id="cb2-6"><a href="#cb2-6"></a>          <span class="dt">&quot;thought&quot;</span><span class="fu">:</span> <span class="st">&quot;The chef seasoned the chicken. This suggests that the chef is preparing the chicken for cooking.&quot;</span></span>
<span id="cb2-7"><a href="#cb2-7"></a>        <span class="fu">}</span><span class="ot">,</span></span>
<span id="cb2-8"><a href="#cb2-8"></a>        <span class="fu">{</span></span>
<span id="cb2-9"><a href="#cb2-9"></a>          <span class="dt">&quot;step&quot;</span><span class="fu">:</span> <span class="dv">2</span><span class="fu">,</span></span>
<span id="cb2-10"><a href="#cb2-10"></a>          <span class="dt">&quot;thought&quot;</span><span class="fu">:</span> <span class="st">&quot;The chef put the chicken in the oven. This indicates that the chef is cooking the chicken.&quot;</span></span>
<span id="cb2-11"><a href="#cb2-11"></a>        <span class="fu">}</span><span class="ot">,</span></span>
<span id="cb2-12"><a href="#cb2-12"></a>        <span class="fu">{</span></span>
<span id="cb2-13"><a href="#cb2-13"></a>          <span class="dt">&quot;step&quot;</span><span class="fu">:</span> <span class="dv">3</span><span class="fu">,</span></span>
<span id="cb2-14"><a href="#cb2-14"></a>          <span class="dt">&quot;thought&quot;</span><span class="fu">:</span> <span class="st">&quot;The sentence states that the chicken looked pale. Pale chicken is often undercooked.&quot;</span></span>
<span id="cb2-15"><a href="#cb2-15"></a>        <span class="fu">}</span><span class="ot">,</span></span>
<span id="cb2-16"><a href="#cb2-16"></a>        <span class="fu">{</span></span>
<span id="cb2-17"><a href="#cb2-17"></a>          <span class="dt">&quot;step&quot;</span><span class="fu">:</span> <span class="dv">4</span><span class="fu">,</span></span>
<span id="cb2-18"><a href="#cb2-18"></a>          <span class="dt">&quot;thought&quot;</span><span class="fu">:</span> <span class="st">&quot;Combining these observations, it is most likely that the chef seasoned the chicken to enhance its flavor and put it in the oven to cook it because it appeared to be undercooked.&quot;</span></span>
<span id="cb2-19"><a href="#cb2-19"></a>        <span class="fu">}</span></span>
<span id="cb2-20"><a href="#cb2-20"></a>      <span class="ot">]</span></span>
<span id="cb2-21"><a href="#cb2-21"></a>    <span class="fu">}</span></span>
<span id="cb2-22"><a href="#cb2-22"></a>    </span></code></pre></div>
(gemini-pro)</td>
</tr>
</tbody>
</table>

By prompting the model to print out its thinking process, the model generated a more thorough response and you learned more about how it generated that response.

## What's next

  - Explore more examples of prompts in the [Prompt gallery](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/prompt-gallery) .
