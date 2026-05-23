---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/clear-instructions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/clear-instructions
title: Give clear and specific instructions
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Giving the model instructions on what to do is an effective and efficient way to customize model behavior. Be clear, concise, and direct in the instructions, providing the needed context and outlining the desired output. Instructions can be as simple as a list of step-by-step instructions or as complex as mapping out a user's experience and mindset.

## How to write effective instructions

Effective instructions apply the following principles:

  - Tell the model what to do.
  - Be clear and specific.
  - Specify any constraints or formatting requirements for the output.

### Example

For example, suppose you own a cheeseburger restaurant and you want to use a model to help you learn about which menu items are the most popular. You want the model to format transcripts of customer orders in JSON so that you can quickly identify menu items. The following tables demonstrate the different responses the model provides when given generic instructions and specific instructions that follow the instruction principles:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Generic instructions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>  Extract the transcript in JSON.
  Transcript:
  Speaker 1 (Customer): Hi, can I get a cheeseburger and large fries, please?
  Speaker 2 (Restaurant employee): Coming right up! Anything else you&#39;d like to add to your order?
  Speaker 1: Hmmm, maybe a small orange juice. And could I get the fries with ketchup on the side?
  Speaker 2: No problem, one cheeseburger, one large fries with ketchup on the side, and a small
  orange juice. That&#39;ll be $5.87. Drive through to the next window please.
    </code></pre>
<strong>Response:</strong>
<div class="sourceCode" id="cb2" dir="ltr" data-is-upgraded="" style="border:1px solid Black;" translate="no"><pre class="sourceCode json"><code class="sourceCode json"><span id="cb2-1"><a href="#cb2-1"></a>      <span class="fu">{</span></span>
<span id="cb2-2"><a href="#cb2-2"></a>        <span class="dt">&quot;speakers&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-3"><a href="#cb2-3"></a>          <span class="fu">{</span></span>
<span id="cb2-4"><a href="#cb2-4"></a>            <span class="dt">&quot;speaker&quot;</span><span class="fu">:</span> <span class="st">&quot;Customer&quot;</span><span class="fu">,</span></span>
<span id="cb2-5"><a href="#cb2-5"></a>            <span class="dt">&quot;utterances&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-6"><a href="#cb2-6"></a>              <span class="st">&quot;Hi, can I get a cheeseburger and large fries, please?&quot;</span></span>
<span id="cb2-7"><a href="#cb2-7"></a>            <span class="ot">]</span></span>
<span id="cb2-8"><a href="#cb2-8"></a>          <span class="fu">}</span><span class="ot">,</span></span>
<span id="cb2-9"><a href="#cb2-9"></a>          <span class="fu">{</span></span>
<span id="cb2-10"><a href="#cb2-10"></a>            <span class="dt">&quot;speaker&quot;</span><span class="fu">:</span> <span class="st">&quot;Restaurant Employee&quot;</span><span class="fu">,</span></span>
<span id="cb2-11"><a href="#cb2-11"></a>            <span class="dt">&quot;utterances&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-12"><a href="#cb2-12"></a>              <span class="st">&quot;Coming right up! Anything else you&#39;d like to add to your order?&quot;</span></span>
<span id="cb2-13"><a href="#cb2-13"></a>            <span class="ot">]</span></span>
<span id="cb2-14"><a href="#cb2-14"></a>          <span class="fu">}</span><span class="ot">,</span></span>
<span id="cb2-15"><a href="#cb2-15"></a>          <span class="fu">{</span></span>
<span id="cb2-16"><a href="#cb2-16"></a>            <span class="dt">&quot;speaker&quot;</span><span class="fu">:</span> <span class="st">&quot;Customer&quot;</span><span class="fu">,</span></span>
<span id="cb2-17"><a href="#cb2-17"></a>            <span class="dt">&quot;utterances&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-18"><a href="#cb2-18"></a>              <span class="st">&quot;Hmm, maybe a small orange juice. And could I get the fries with ketchup on the</span></span>
<span id="cb2-19"><a href="#cb2-19"></a><span class="st">              side?&quot;</span></span>
<span id="cb2-20"><a href="#cb2-20"></a>            <span class="ot">]</span></span>
<span id="cb2-21"><a href="#cb2-21"></a>          <span class="fu">}</span><span class="ot">,</span></span>
<span id="cb2-22"><a href="#cb2-22"></a>          <span class="fu">{</span></span>
<span id="cb2-23"><a href="#cb2-23"></a>            <span class="dt">&quot;speaker&quot;</span><span class="fu">:</span> <span class="st">&quot;Restaurant Employee&quot;</span><span class="fu">,</span></span>
<span id="cb2-24"><a href="#cb2-24"></a>            <span class="dt">&quot;utterances&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-25"><a href="#cb2-25"></a>              <span class="st">&quot;No problem, one cheeseburger, one large fries with ketchup on the side, and a</span></span>
<span id="cb2-26"><a href="#cb2-26"></a><span class="st">              small orange juice. That&#39;ll be $5.87. Drive through to the next window please.&quot;</span></span>
<span id="cb2-27"><a href="#cb2-27"></a>            <span class="ot">]</span></span>
<span id="cb2-28"><a href="#cb2-28"></a>          <span class="fu">}</span></span>
<span id="cb2-29"><a href="#cb2-29"></a>        <span class="ot">]</span></span>
<span id="cb2-30"><a href="#cb2-30"></a>      <span class="fu">}</span></span>
<span id="cb2-31"><a href="#cb2-31"></a>    </span></code></pre></div>
(gemini-pro)</td>
</tr>
</tbody>
</table>

In the example, generic instructions lead to a response with more JSON fields than what you need to identify the menu items customers are ordering. Improve the instructions by making more specific output constraints, as demonstrated in the following table:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Specific instructions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>  Extract the items from this transcript in JSON and separate drinks from food.
  Transcript:
  Speaker 1 (Customer): Hi, can I get a cheeseburger and large fries, please?
  Speaker 2 (Restaurant employee): Coming right up! Anything else you&#39;d like to add to your order?
  Speaker 1: Hmmm, maybe a small orange juice. And could I get the fries with ketchup on the side?
  Speaker 2: No problem, one cheeseburger, one large fries with ketchup on the side, and a small
  orange juice. That&#39;ll be $5.87. Drive through to the next window please.
    </code></pre>
<strong>Response:</strong>
<div class="sourceCode" id="cb2" dir="ltr" data-is-upgraded="" style="border:1px solid Black;" translate="no"><pre class="sourceCode json"><code class="sourceCode json"><span id="cb2-1"><a href="#cb2-1"></a>      <span class="fu">{</span></span>
<span id="cb2-2"><a href="#cb2-2"></a>        <span class="dt">&quot;drinks&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-3"><a href="#cb2-3"></a>          <span class="st">&quot;orange juice&quot;</span></span>
<span id="cb2-4"><a href="#cb2-4"></a>        <span class="ot">]</span><span class="fu">,</span></span>
<span id="cb2-5"><a href="#cb2-5"></a>        <span class="dt">&quot;food&quot;</span><span class="fu">:</span> <span class="ot">[</span></span>
<span id="cb2-6"><a href="#cb2-6"></a>          <span class="st">&quot;cheeseburger&quot;</span><span class="ot">,</span></span>
<span id="cb2-7"><a href="#cb2-7"></a>          <span class="st">&quot;large fries&quot;</span></span>
<span id="cb2-8"><a href="#cb2-8"></a>        <span class="ot">]</span></span>
<span id="cb2-9"><a href="#cb2-9"></a>      <span class="fu">}</span></span>
<span id="cb2-10"><a href="#cb2-10"></a>    </span></code></pre></div>
(gemini-pro)</td>
</tr>
</tbody>
</table>

By applying the instruction principles, this example went from a response that contained too much data to one that contained exactly the data required for this use case. Instructions that use the instruction princples can help you guide the model to deliver the most helpful response for your use case.

## What's next

  - Explore more examples of prompts in the [Prompt gallery](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/prompt-gallery) .
