---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/lora-qlora
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/lora-qlora
title: LoRA and QLoRA recommendations for LLMs
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page gives you configuration recommendations for tuning large language models (LLM) on Gemini Enterprise Agent Platform by using [Low-Rank Adaptation of Large Language Models (LoRA)](https://arxiv.org/abs/2106.09685) and its more memory-efficient version, [QLoRA](https://arxiv.org/abs/2305.14314) .

## Tuning recommendations

The following table summarizes our recommendations for tuning LLMs by using LoRA or QLoRA:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Specification</th>
<th>Recommended</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPU memory efficiency</td>
<td>QLoRA</td>
<td>QLoRA has about 75% smaller peak GPU memory usage compared to LoRA.</td>
</tr>
<tr class="even">
<td>Speed</td>
<td>LoRA</td>
<td>LoRA is about 66% faster than QLoRA in terms of tuning speed.</td>
</tr>
<tr class="odd">
<td>Cost efficiency</td>
<td>LoRA</td>
<td>While both methods are relatively inexpensive, LoRA is up to 40% less expensive than QLoRA.</td>
</tr>
<tr class="even">
<td>Higher max sequence length</td>
<td>QLoRA</td>
<td>Higher max sequence length increases GPU memory consumption. QLoRA uses less GPU memory so it can support higher max sequence lengths.</td>
</tr>
<tr class="odd">
<td>Accuracy improvement</td>
<td>Same</td>
<td>Both methods offer similar accuracy improvements.</td>
</tr>
<tr class="even">
<td>Higher batch size</td>
<td>QLoRA</td>
<td>QLoRA supports much higher batch sizes. For example, the following are batch size recommendations for tuning openLLaMA-7B on the following GPUs:<br />

<ul>
<li>1 x A100 40G:
<ul>
<li>LoRA: Batch size of 2 is recommended.</li>
<li>QLoRA: Batch size of 24 is recommended.</li>
</ul></li>
<li>1 x L4:
<ul>
<li>LoRA: Batch size of 1 fails with an out of memory error (OOM).</li>
<li>QLoRA: Batch size of 12 is recommended.</li>
</ul></li>
<li>1 x V100:
<ul>
<li>LoRA: Batch size of 1 fails with an out of memory error (OOM).</li>
<li>QLoRA: Batch size of 8 is recommended.</li>
</ul></li>
</ul></td>
</tr>
</tbody>
</table>
