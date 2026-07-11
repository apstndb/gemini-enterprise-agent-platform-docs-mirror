---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/design-multimodal-prompts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/design-multimodal-prompts
title: Design multimodal prompts
description: Learn how to design multimodal prompts that work with the Gemini API.
data_source: docs.cloud.google.com
---

The Gemini API lets you include multimodal inputs like text, images, and video as part of your prompt to Gemini models. This page provides best practices for designing multimodal prompts and how to troubleshoot if your prompts aren't working as expected. For general guidance on prompt design, see [our recommended prompt design strategies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/prompt-design-strategies) , or see the following list of multimodal-specific best practices.

## Prompt design fundamentals

The following sections describe fundamental best practices for designing effective multimodal prompts.

### Use specific instructions

Clear and detailed prompts provide the best results. If you have a specific output in mind, include that requirement in the prompt to increase the likelihood that you get the correct output.

Even when a prompt seems clear to the person who wrote it, the prompt might be underspecified. To customize model behavior, consider how your prompt could be interpreted and ensure that the instructions you give are specific and clear.

If you included the image of this airport board as part of your prompt, asking the model to just "describe this image" could generate a general description. If you need the model to parse the time and city from the image, include that request directly in your prompt.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Model response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/timetable.png" class="fit-picture" alt="An airport timetable board with times and cities." />
<p><em>Describe this image.</em></p></td>
<td><p>The image shows an airport arrivals and departures board.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/timetable.png" class="fit-picture" alt="An airport timetable board with times and cities." />
<p><em>Parse the time and city from the airport board shown in this image into a list.</em></p></td>
<td><ul>
<li>10:50 Moscow</li>
<li>11:05 Edinburgh</li>
<li>11:05 London</li>
<li>11:10 Bucharest</li>
<li>11:30 Kiev</li>
<li>11:35 Dublin</li>
<li>11:45 East Midlands</li>
<li>12:15 Sofia</li>
<li>12:30 London</li>
<li>12:30 Newcastle</li>
<li>12:40 St Petersburg</li>
<li>12:40 London</li>
<li>12:45 Manchester</li>
</ul></td>
</tr>
</tbody>
</table>

-----

### Add examples

The model can accept multiple inputs to use as examples to understand the output you want. Adding these examples can help the model identify the patterns and apply the relationship between the given images and responses to the new example. This is called *"few-shot" learning* .

In the following example, the initial output is a full sentence that also contains the country (Brazil). If the preferred output is only the city, not the country, then adding few-shot examples to your prompt can guide the model to respond in that format.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Prompt</strong></th>
<th><strong>Model response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/redeemer.png" class="fit-picture" alt="The Christ the Redeemer statue in Rio de Janeiro, Brazil." />
<p><em>Determine the city along with the landmark.</em></p></td>
<td><p>The landmark is the Christ the Redeemer statue in Rio de Janeiro, Brazil.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Determine the city along with the landmark.</em></p>
<img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/colosseum.png" class="fit-picture" alt="The Colosseum in Rome, Italy." /></td>
<td><p>city: Rome, landmark: the Colosseum.</p></td>
</tr>
<tr class="even">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/forbidden-city.png" class="fit-picture" alt="The Forbidden City in Beijing, China." /></td>
<td><p>city: Beijing, landmark: Forbidden City</p></td>
</tr>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/redeemer.png" class="fit-picture" alt="The Christ the Redeemer statue in Rio de Janeiro, Brazil." /></td>
<td><p>city: Rio de Janeiro, landmark: Christ the Redeemer statue</p></td>
</tr>
</tbody>
</table>

### Split complex tasks into smaller tasks

For complex tasks like those that require both visual understanding and reasoning, split the task into smaller, more straightforward steps or directly ask the model to think step by step in the prompt.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Model response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/toilet-paper.jpg" class="fit-picture" alt="A picture of three rolls of toilet paper." />
<p><em>When will I run out of toilet paper?</em></p></td>
<td><p>Soon, you only have 3 rolls left.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/toilet-paper.jpg" class="fit-picture" alt="A picture of three rolls of toilet paper." />
<ol>
<li><em>First, count how many toilet paper rolls are in this picture.</em></li>
<li><em>Then, determine how much toilet paper a typical person uses per day.</em></li>
<li><em>Calculate how long these rolls of toilet paper will last.</em></li>
</ol></td>
<td><ol>
<li>There are 3 rolls of toilet paper in this picture.</li>
<li>A typical person uses about 20 sheets of toilet paper per day.</li>
<li>If each roll contains 200 sheets, then each roll will last for about 10 days. Therefore, the 3 rolls will last for about a month.</li>
</ol></td>
</tr>
</tbody>
</table>

Math problems or other types of word problems can also be broken down into smaller tasks.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Prompt</strong></th>
<th><strong>Response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/math.jpg" class="fit-picture" alt="A picture of mathematical sequence b. b(1) = 15, and b(n) = b(n-1) * (-3)." />
<p>What is the 4th term in the sequence?</p></td>
<td><p>-135</p></td>
</tr>
</tbody>
</table>

The response from the model is incorrect. Try asking the model to parse the problem before answering the prompt.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Prompt</strong></th>
<th><strong>Response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/math.jpg" class="fit-picture" alt="A picture of mathematical sequence b. b(1) = 15, and b(n) = b(n-1) * (-3)." />
<p>Parse the formula in the image first.</p>
<p>Then based on the formula, answer "what's the 4th term in the sequence?".</p></td>
<td><em>Click to expand the result</em> $$b(n) = b(n-1) * (-3)$$ $$b(1) = 15$$
<ol>
<li><p>Substitute n = 4 into the formula:</p>
<p>$$b(4) = b(4-1) * (-3)$$</p>
<p>$$b(4) = b(3) * (-3)$$</p></li>
<li><p>We don't know the value of b(3), so substitute n = 3 into the formula:</p>
<p>$$b(3) = b(3-1) * (-3)$$</p>
<p>$$b(3) = b(2) * (-3)$$</p></li>
<li><p>We don't know the value of b(2), so substitute n = 2 into the formula:</p>
<p>$$b(2) = b(2-1) * (-3)$$</p>
<p>$$b(2) = b(1) * (-3)$$</p></li>
<li><p>We know the value of b(1) is 15, so substitute it into the formula:</p>
<p>$$b(2) = 15 * (-3)$$</p>
<p>$$b(2) = -45$$</p></li>
<li><p>Now that we know the value of b(2), substitute it into the formula for b(3):</p>
<p>$$b(3) = b(2) * (-3)$$</p>
<p>$$b(3) = -45 * (-3)$$</p>
<p>$$b(3) = 135$$</p></li>
<li><p>Now that we know the value of b(3), substitute it into the formula for b(4):</p>
<p>$$b(4) = b(3) * (-3)$$</p>
<p>$$b(4) = 135 * (-3)$$</p>
<p>$$b(4) = -405$$</p></li>
</ol>
<p>Therefore, the 4th term in the sequence is -405.</p></td>
</tr>
</tbody>
</table>

To make the response even more streamlined, you can ask the model to think through the prompt step by step.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/math.jpg" class="fit-picture" alt="A picture of mathematical sequence b. b(1) = 15, and b(n) = b(n-1) * (-3)." />
<p>What is the 4th term in the sequence? Think step by step.</p></td>
<td><p>The first term is 15.</p>
<p>The second term is b(1) * (-3) = 15 * (-3) = -45.</p>
<p>The third term is b(2) * (-3) = -45 * (-3) = 135.</p>
<p>The fourth term is b(3) * (-3) = 135 * (-3) = -405.</p></td>
</tr>
</tbody>
</table>

### Specify the output format

When a certain format is required, you can instruct the model to use that format for its output.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Model response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/excel-example.png" class="fit-picture" alt="A picture of a spreadsheet in Excel." />
<p>Parse the table in this image into Markdown format</p></td>
<td><pre dir="ltr" data-is-upgraded="" translate="no"><code>| Subject   | Status      | Time    | Start date | Due on     |
|-----------|-------------|---------|------------|------------|
| Math      | Done        | 1.5 hrs | 11/29/2023 | 12/1/2023  |
| Geography | Done        | 30 min  | 12/2/2023  | 12/4/2023  |
| Physics   | In progress | 2 hrs   | 12/3/2023  | 12/5/2023  |
| Biology   | Not started | 6 hrs   | 11/2/2016  | 12/6/2023  |
        </code></pre></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Prompt</strong></th>
<th><strong>Model response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/spanish-meal.png" class="fit-picture" alt="A picture of a meal with shrimp, clams, and other ingredients." />
<p>Provide a list of all the following attributes:</p>
<p>ingredients, type of cuisine, vegetarian or not, in JSON format</p></td>
<td><pre dir="ltr" data-is-upgraded="" translate="no"><code>        {
          &quot;ingredients&quot;: [
            &quot;rice&quot;,
            &quot;shrimp&quot;,
            &quot;clams&quot;,
            &quot;mussels&quot;,
            &quot;peas&quot;,
            &quot;tomatoes&quot;,
            &quot;onions&quot;,
            &quot;garlic&quot;,
            &quot;olive oil&quot;,
            &quot;paprika&quot;,
            &quot;salt&quot;,
            &quot;pepper&quot;
          ],
          &quot;type of cuisine&quot;: &quot;Spanish&quot;,
          &quot;vegetarian&quot;: false
        }
        </code></pre></td>
</tr>
</tbody>
</table>

## Troubleshoot a multimodal prompt

Troubleshooting a prompt can involve improving the language of your prompt, directing the focus of your prompt, or tuning parameters. These different approaches can lead to improved results, especially after determining the root cause of the issue.

### Focus on the relevant part of an image

To improve the response, point out which parts of the image are most relevant to the prompt.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Model response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/diapers.png" class="fit-picture" alt="A picture of the side of a box of diapers; the number 198 is written on the box." />
<p>How many days will these diapers last a baby?</p></td>
<td><p>The diapers will last for 198 days before they run out.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/diapers.png" class="fit-picture" alt="A picture of the side of a box of diapers; the number 198 is written on the box." />
<p>How long will these diapers last before I run out?</p>
<p>Use the weight shown on the box to determine the child's age, and use the total number of diapers in the box.</p>
<p>Divide the total number by how many diapers the child goes through per day.</p></td>
<td><p>The box contains 198 diapers. The box states the diapers are for a child weighing 22-37 lbs.</p>
<p>The average child in this weight range is likely between 1 and 2 years old.</p>
<p>A 2-year-old typically goes through 6 diapers per day, therefore, the diapers will last around 33 days (198/6).</p></td>
</tr>
</tbody>
</table>

### Tailor the model's response to input

Ask the model to describe the images before performing the task in the prompt.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Model response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/packing.jpg" class="fit-picture" alt="A picture of a person packing a suitcase." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/mall.jpg" class="fit-picture" alt="A picture of an empty hallway in a shopping mall." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/toilet-paper.jpg" class="fit-picture" alt="A picture of three rolls of toilet paper." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/ocean.jpg" class="fit-picture" alt="A picture of dark clouds breaking over the sea." />
<p>What is in common between these images?</p></td>
<td><p>All four images are examples of landscape photography.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/packing.jpg" class="fit-picture" alt="A picture of a person packing a suitcase." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/mall.jpg" class="fit-picture" alt="A picture of an empty hallway in a shopping mall." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/toilet-paper.jpg" class="fit-picture" alt="A picture of three rolls of toilet paper." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/ocean.jpg" class="fit-picture" alt="A picture of dark clouds breaking over the sea." />
<p>First, describe what's in each image in detail. What's in common between these images?</p></td>
<td><p>The first image shows a person packing a suitcase. The second image shows an empty hallway in a shopping mall. The third image shows a roll of toilet paper. The fourth image shows a dark and stormy sea.</p>
<p>The commonality between these images is that they are all examples of liminal spaces. Liminal spaces are places or situations that are in between two other places or situations. They are often characterized by a sense of uncertainty or ambiguity.</p>
<p>The first image shows the person in between being at home and being on a trip. The second image shows the hallway in between two stores. The third image is of toilet paper, which can represent a bathroom. A bathroom is a transitional space between private and public realms. It's a place where we prepare ourselves to enter or leave the outside world.</p>
<p>The fourth image shows the sea in between being calm and being stormy.</p>
<p>Liminal spaces can be both exciting and unsettling. They can be a place of new beginning or a place of endings. They can be a place of reflection or a place of action.</p></td>
</tr>
</tbody>
</table>

You can explicitly ask the model to refer to what's in the image.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/packing.jpg" class="fit-picture" alt="A picture of a person packing a suitcase." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/mall.jpg" class="fit-picture" alt="A picture of an empty hallway in a shopping mall." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/toilet-paper.jpg" class="fit-picture" alt="A picture of three rolls of toilet paper." /> <img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/ocean.jpg" class="fit-picture" alt="A picture of dark clouds breaking over the sea." />
<p>What is in common between these images? Refer to what's in the images in your response.</p></td>
<td><p>All of the images are related to travel. The first image shows a person packing a suitcase, the second image shows an empty hallway in a shopping mall, the third image shows a stack of toilet paper, and the fourth image shows a dark and stormy sea.</p>
<p>These images are all related to travel because they are all things that people need or use when they travel. The first image shows a person packing a suitcase, which is something that people do when they are going on a trip. The second image shows an empty hallway in a shopping mall, which is a place where people often go to buy things for their trips. The third image shows a stack of toilet paper, which is something that people often use when they are traveling. The fourth image shows a dark and stormy sea, which is something that people often encounter when they are traveling.</p></td>
</tr>
</tbody>
</table>

The same tips work for creative output. Explicitly ask the model to include aspects from the image; this can improve the output.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Model response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/rabbit.jpg" class="fit-picture" alt="A picture of a brown rabbit." />
<p>Can you write me a poem about this image?</p></td>
<td><pre dir="ltr" data-is-upgraded="" translate="no"><code>Little bunny, so soft and brown,
        Hopping through the field, up and down.
        Your ears so long, your tail so small,
        You&#39;re the cutest creature of them all.</code></pre>
<pre dir="ltr" data-is-upgraded="" translate="no"><code>You nibble on the grass, so green and sweet,
        And hop away when you see me.
        But I&#39;ll always be your friend,
        Little bunny, until the very end.</code></pre></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Updated prompt</strong></th>
<th><strong>Improved response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/rabbit.jpg" class="fit-picture" alt="A picture of a brown rabbit." />
<p>Can you write me a descriptive and dramatic poem about this image and include the location?</p></td>
<td><pre dir="ltr" data-is-upgraded="" translate="no"><code>Little bunny on the green,
        Ears so long, so keen.
        What do you see out there,
        In the distance, where you stare?</code></pre>
<pre dir="ltr" data-is-upgraded="" translate="no"><code>Is it the ocean blue,
        Sparkling in the sun&#39;s hue?
        Or the waves that crash and roar,
        A rhythm that you adore?</code></pre>
<pre dir="ltr" data-is-upgraded="" translate="no"><code>Little bunny, tell me true,
        What captures your attention so?
        Is it the salty breeze,
        Or the seagulls&#39; cries that please?</code></pre>
<pre dir="ltr" data-is-upgraded="" translate="no"><code>Perhaps it&#39;s the vastness of it all,
        A world so big and small.
        A place where dreams can roam,
        And adventures can be sown.</code></pre>
<pre dir="ltr" data-is-upgraded="" translate="no"><code>Little bunny, I wonder what you dream,
        As you sit on the grass, so serene.
        Do you yearn to explore the deep,
        Or stay on land, where you can leap?</code></pre>
<pre dir="ltr" data-is-upgraded="" translate="no"><code>Whatever it may be, little bunny,
        Keep that spark of wonder burning brightly.
        For in your dreams and aspirations,
        Lies a world waiting for your creation.</code></pre></td>
</tr>
</tbody>
</table>

### Determine how the prompt failed

A prompt can fail because the model did not understand the image at all, or because it did not perform the correct reasoning steps afterward. To disambiguate between those reasons, ask the model to describe what's in the image.

In this example, if the model responds with a snack that seems surprising when paired with tea (like popcorn), first determine whether the model recognized that the image contains tea.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Prompt for troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/tea-set.png" class="fit-picture" alt="A picture of a tea set." />
<p>What's a snack I can make in 1 minute that would go well with this?</p></td>
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/tea-set.png" class="fit-picture" alt="A picture of a tea set." />
<p>Describe what's in this image.</p></td>
</tr>
</tbody>
</table>

Asking the model to explain its reasoning can help narrow down which part of the reasoning broke down, if any.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompt</th>
<th>Prompt for troubleshooting</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/tea-set.png" class="fit-picture" alt="A picture of a tea set." />
<p>What's a snack I can make in 1 minute that would go well with this?</p></td>
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/images/tea-set.png" class="fit-picture" alt="A picture of a tea set." />
<p>What's a snack I can make in 1 minute that would go well with this? Please explain why.</p></td>
</tr>
</tbody>
</table>

### Tune the sampling parameters

In each request, you send not only the multimodal prompt but a set of sampling parameters to the model. The model can generate different results for different parameter values. Experiment with the different parameters to get the best values for the task. The most commonly adjusted parameters are the following:

  - [Temperature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/design-multimodal-prompts#temperature)
  - [top-P](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/design-multimodal-prompts#top-p)

#### Temperature

Temperature is used for sampling during response generation, which occurs when top-P and top-K are applied. Temperature controls the degree of randomness in token selection. Lower temperatures are good for prompts that require a more deterministic and less open-ended or creative response, while higher temperatures can lead to more diverse or creative results. A temperature of 0 is deterministic, meaning that the highest probability response is most likely to be selected.

For most use cases, start with a temperature of 0.4. If you need more creative results, increase the temperature. If you observe clear hallucinations, reduce the temperature.

#### Top-P

Top-P changes how the model selects tokens for output. Tokens are selected from the most to least probable until the sum of their probabilities equals the top-P value. For example, if tokens A, B, and C have a probability of 0.6, 0.3, 0.1 and the top-P value is 0.9, then the model will select either A or B as the next token by using temperature and excludes C as a candidate.

Specify a lower value for less random responses and a higher value for more random responses. The default value of top-P is 1.0.

## What's next

  - Try a quickstart tutorial using the [Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) .
  - To get started using the Gemini API, see the [Gemini API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) .
