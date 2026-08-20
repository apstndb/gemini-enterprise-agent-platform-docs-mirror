---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/prompting-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/prompting-guide
title: Thinking prompting guide
description: Learn prompting techniques and best practices for Gemini thinking models on Agent Platform, including step-by-step instructions, multishot prompting, system instructions, and debugging.
data_source: docs.cloud.google.com
---

Effective prompting is crucial for maximizing the benefits of the Gemini thinking models. This guide outlines recommended prompting practices for thinking models.

## Start with general instructions

Begin with general instructions that describe the preferred outcome. Start with a low-complexity prompt and observe the model's initial thoughts on how to respond.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Describe the most unusual or striking architectural feature you&#39;ve ever seen in a building or structure.
  </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>&lt;...&gt;
The most unusual architectural feature that has truly stayed with me is the &quot;floating roof&quot; of the
  Heydar Aliyev Center in Baku, Azerbaijan, designed by Zaha Hadid Architects.

Visually, it&#39;s breathtaking. Imagine a vast, undulating landscape of pure white, seemingly draped
over the building. It&#39;s not just a roof in the traditional sense; it&#39;s an extension of the ground,
flowing seamlessly upwards and over the building&#39;s various spaces before curving back down to meet
the earth again. There are no sharp angles, no rigid lines. Instead, everything is fluid, organic,
and continuous. It resembles a giant, pristine white wave frozen in motion, or perhaps a sand dune
sculpted by an unseen wind.
&lt;...&gt;
  </code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

## Provide step-by-step instructions

If the initial attempt does not yield the expected result, refine your prompt by providing more explicit step-by-step instructions to guide Gemini through the problem-solving process for a more focused approach. This lets you steer the model's initial understanding of the task with explicit suggestions and guidance.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Now imagine that architectural feature is not just for looks, but has a specific function or
purpose related to the building&#39;s environment or the people who use it. Explain what that
function could be and how it enhances the building&#39;s overall design and usability.
  </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>&lt;...&gt;
Let&#39;s imagine that the &quot;floating roof&quot; of the Heydar Aliyev Center is not purely aesthetic but
serves a crucial environmental and user-centric function: it&#39;s designed as a sophisticated climate
moderator and natural ventilation system for the Baku environment.

Here&#39;s how this function would work and enhance the building:

Function: Passive Climate Control and Natural Ventilation System

Shading and Solar Heat Mitigation: The undulating curves of the white GFRC roof are strategically
shaped and oriented to provide optimal shading throughout the day, year-round. Baku experiences
intense sun, especially during the summer. The overhanging curves, acting like giant brise-soleils,
would block direct sunlight from hitting the building&#39;s glass facade, significantly reducing solar
heat gain. The varying heights and depths of the curves would create dynamic shade patterns, ensuring
that different parts of the building are shaded at different times of the day, optimizing comfort
and reducing the need for excessive air conditioning. The white color of the GFRC further enhances
this by reflecting a large portion of the solar radiation.
&lt;...&gt;
  </code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

## Multishot prompting with thinking

Multishot prompting in conjunction with thinking can further enhance Gemini's understanding and improve the accuracy of its responses. Provide several examples of input-output pairs, demonstrating the preferred behavior and output format in your prompt.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Example 1:
User: What is the tallest mountain in the world?
Assistant: Mount Everest

Example 2:
User: What is the largest ocean?
Assistant: Pacific Ocean

User: What is the longest river in the world?
Assistant:
  </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Amazon River
  </code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

## Defining output and behavior

When building an application where users will interact directly with the model, you may want to provide guidance for how Gemini's output and responses will sound and be formatted.

### System instructions

System instructions are a set of instructions that the model processes before it processes prompts. They are recalled each time the model is prompted and tell the model how you want it to behave and respond. For example, you can include things like the role or persona, contextual information, and formatting instructions.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>System Instruction: You are a helpful and concise coding tutor. Always provide code examples and explain them briefly.

User Prompt: Explain what is a closure in Javascript and give an example.
  </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>    function outerFunction(outerVar) {
      function innerFunction(innerVar) {
        console.log(outerVar); // Accessing outerVar from outerFunction&#39;s scope
        console.log(innerVar);
      }
      return innerFunction;
    }

    const closureExample = outerFunction(&#39;I am from outer&#39;);
    closureExample(&#39;I am from inner&#39;);

Explanation:

A closure is created when a function (innerFunction in this example) is defined inside another function
(outerFunction) and the inner function remembers and has access to the variables from the outer
function&#39;s scope, even after the outer function has finished executing.

In the example:

outerFunction is called with &#39;I am from outer&#39; and returns innerFunction.

closureExample now holds a reference to innerFunction.

When closureExample(&#39;I am from inner&#39;) is called, innerFunction executes.

Even though outerFunction has already finished, innerFunction can still access and use outerVar
(which is &#39;I am from outer&#39;) because of the closure.

In essence, the innerFunction &quot;closes over&quot; the variables of its outer function&#39;s scope, creating
a closure.
  </code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

### Verification and reflection

Include specific verification steps in either the system instructions or your prompts directly. For example, ask Gemini to verify its sources, review its reasoning, identify potential errors, and check its final answer.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>    Verify the following statement and provide your sources: The capital of Brazil is Rio de Janeiro.
  </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>The statement &quot;The capital of Brazil is Rio de Janeiro&quot; is incorrect.

The current capital of Brazil is Brasília.

Rio de Janeiro was the capital of Brazil for a significant period, from 1763 to 1960. However, the
capital was moved to Brasília in 1960 as part of a plan to develop the country&#39;s interior and create
a more centrally located capital.

Verification and Sources:

You can easily verify this information from numerous reliable sources:

Encyclopedias:

Britannica: Searching for &quot;Brazil&quot; on Britannica will clearly state Brasília as the capital.

https://www.britannica.com/place/Brazil (Look for the &quot;Capital&quot; information in the introductory summary or &quot;Geography&quot; section)

Wikipedia: The Wikipedia article for &quot;Brazil&quot; also states Brasília as the capital.

https://en.wikipedia.org/wiki/Brazil (Look in the infobox or introductory section)

Government and Official Sources:

CIA World Factbook: This is a highly reliable source for country information. Searching for &quot;Brazil&quot;
will list Brasília as the capital.

https://www.cia.gov/the-world-factbook/countries/brazil/ (Look under &quot;Government&quot; &gt; &quot;Capital&quot;)

Official Website of the Brazilian Government (if accessible and in English): While navigating official
government websites can sometimes be complex, they would definitively list Brasília as the capital.

Geographic Resources:

National Geographic: Their website and publications will confirm Brasília as the capital of Brazil.

Atlases and Geography Textbooks: Any modern atlas or geography textbook will list Brasília as the capital.

Why the confusion?

The confusion might arise because:

Rio de Janeiro is a very famous Brazilian city: It&#39;s a major tourist destination, known for its
beaches, Carnival, and iconic landmarks like Christ the Redeemer. Its past status as capital adds
to its historical significance and public recognition.

Historical context: Rio de Janeiro was the capital for a long time. People who learned about Brazil
in the past might remember it as the capital.

In conclusion, the statement is false. The capital of Brazil is Brasília, not Rio de Janeiro. Rio
de Janeiro was the former capital but is no longer the current capital.

You can confidently use the sources listed above to verify this information.
  </code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

## Debugging and steering

Agent Studio provides developers access to the model's thoughts in the UI. This is helpful as a developer reviewing your prompt when debugging:

### Analyze the thought process

Carefully review Gemini's thought process to identify any areas where it may have gone astray. This analysis can provide valuable clues for refining your prompts and getting your expected response consistently in your application.

*Example Scenario: If Gemini's thought process shows it misunderstood a step in a complex instruction, you can refine the prompt to clarify that specific step.*

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Step 1: Summarize the following article about quantum physics.
Step 2: Translate the summary into Spanish.
Step 3: Extract the key entities from the Spanish summary.

Article: ... [Article Text] ...</code></pre>
<strong>Gemini's Thought Process Analysis (Example):</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>The user wants me to process an article about Google&#39;s new quantum chip called Willow in three steps:
Step 1: Summarize the article.
Step 2: Translate the summary into Spanish.
Step 3: Extract the key entities from the Spanish summary.

Let&#39;s break down each step.

Step 1: Summarize the article.
I need to read the article and identify the main points. The article is about Google&#39;s new quantum
chip, Willow, and its achievements. The key achievements are:

Exponential error reduction as qubits scale up.

Outperforming supercomputers in a benchmark computation (RCS).

Willow is a step towards commercially relevant quantum computing.

It&#39;s the first system below threshold for quantum error correction.

It achieved a benchmark computation in under 5 minutes that would take a supercomputer 10 septillion years.

It was fabricated in a new facility.

It has state-of-the-art performance and high quality qubits.

Google is looking towards real-world applications with Willow.

Quantum computing will benefit AI.

I will synthesize these points into a concise summary.

Step 2: Translate the summary into Spanish.
Once I have the summary in English, I will translate it into Spanish. I need to ensure the translation
is accurate and natural-sounding in Spanish.

Step 3: Extract the key entities from the Spanish summary.
After translating the summary, I will identify and extract the key entities. Key entities are typically
nouns or noun phrases that represent important objects, concepts, or actors. In this context, they
will likely include:

Names of chips (Willow, Sycamore)

Companies/Organizations (Google Quantum AI, Google Research)

Technologies (quantum chip, quantum computer, qubits, quantum error correction, superconducting
quantum system, classical computers, supercomputers, AI)

Benchmarks (random circuit sampling, RCS)

People (Julian Kelly, Peter Shor, David Deutsch, Sergio Boixo, Hartmut Neven, John Preskill)

Concepts (exponential error reduction, below threshold, beyond breakeven, state-of-the-art performance,
commercially relevant applications, quantum mechanics, multiverse, T1 times, system benchmarks,
algorithmic benchmarks)

I will need to carefully review the Spanish summary to identify these entities and list them out.</code></pre></td>
</tr>
</tbody>
</table>

### Provide corrective feedback

If you observe errors or inconsistencies in Gemini's reasoning, provide corrective feedback in your prompt and the system instructions to anticipate where the model's response may deviate from your intended outcome.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>You are an expert in botany. When asked to identify a plant, focus on leaf shape, flower structure, and stem characteristics.

Identify this plant based on these characteristics: ... [Plant Characteristics Description] ...

Previous incorrect response focused on habitat only. Please disregard habitat and focus on morphology.</code></pre>
<strong>Refined Prompt (if needed based on thought process):</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Previous incorrect response focused on habitat only. Please disregard habitat and focus on morphology.</code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Tabebuia vellosoi</code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

## Making the best of long outputs and long-form thinking

Thinking generates "thoughts" as part of the Token Output that showcases Gemini's detailed reasoning. To make the most of these outputs:

### Review the reasoning

Pay close attention to Gemini's reasoning process (available in the Agent Studio UI), how it broke down the task and the choices it made for your output. This can help you understand how it arrived at its conclusion.

### Provide guidance in reasoning

If you want your output to be particularly lengthy, you may want to provide more guidance in your prompt to constrain the amount of thinking needed to accomplish the task presented in the prompt. This lets you reserve more of the token output for your response.

*Example: For a detailed report, you might specify sections and subsections in your prompt to guide Gemini's thinking and structure the output efficiently.*

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>Generate a detailed report on the impact of climate change on coastal ecosystems.

Report Structure:

Introduction

Rising Sea Levels
2.1. Impact on Mangroves
2.2. Impact on Coral Reefs

Ocean Acidification
3.1. Impact on Shellfish
3.2. Impact on Plankton

Extreme Weather Events
4.1. Increased Storm Intensity
4.2. Coastal Erosion

Conclusion

Provide detailed analysis within each section.</code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line;" translate="no"><code>&lt;...&gt;
Climate Change Impact on Coastal Ecosystems: A Detailed Report

1.  Introduction

Coastal ecosystems, the dynamic interface between land and sea, are among the most productive and
biodiverse environments on Earth. They provide crucial ecosystem services, including coastal protection,
fisheries, carbon sequestration, and support for a vast array of species. However, these vital
ecosystems are increasingly threatened by the multifaceted impacts of climate change. Driven by
anthropogenic greenhouse gas emissions, climate change is manifesting in several interconnected ways
that are profoundly altering the physical and chemical conditions of coastal environments. This report
will delve into the key impacts of climate change on coastal ecosystems, focusing on rising sea levels,
ocean acidification, and extreme weather events, and their specific consequences for critical habitats
like mangroves and coral reefs, and key organisms like shellfish and plankton. Understanding these
impacts is crucial for developing effective conservation and management strategies to mitigate the
damage and enhance the resilience of these invaluable ecosystems.

2.  Rising Sea Levels

Rising sea levels are a direct and significant consequence of global warming, driven by thermal
expansion of seawater and the melting of land ice (glaciers and ice sheets). This phenomenon poses a
direct threat to low-lying coastal ecosystems by inundating habitats, altering salinity regimes, and
increasing erosion rates. The rate of sea level rise is accelerating, and projections for the 21st
century indicate a continued upward trend, with potentially devastating consequences for coastal
environments.

2.1. Impact on Mangroves

Mangrove forests are unique coastal ecosystems found in tropical and subtropical intertidal zones.
They provide numerous benefits, including coastal protection against storms, nursery grounds for
fish and invertebrates, and significant carbon sequestration...
&lt;...&gt;</code></pre>
(gemini-2.5-pro-exp-03-25)</td>
</tr>
</tbody>
</table>

## What's next

Overview

### [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)

Learn about Gemini thinking capabilities, supported models, and how to configure thinking levels.

Guide

### [Thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/thought-signatures)

Learn how to preserve the Gemini reasoning state during multi-turn and multi-step conversations using thought signatures.

Guide

### [Prompt design strategies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/prompt-design-strategies)

Explore general prompt design strategies for Gemini models.
