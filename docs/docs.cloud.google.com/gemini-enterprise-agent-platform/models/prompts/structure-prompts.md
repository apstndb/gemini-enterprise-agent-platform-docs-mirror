---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/structure-prompts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/structure-prompts
title: Structure prompts
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

How you structure a prompt can affect the model's ability to parse the information in the prompt. It also helps the model correctly interpret how to use the given information. To give structure to a prompt, you can use prefixes or XML tags to delimit different parts or components of a prompt.

## Use prefixes to structure simple prompts

A prefix is a word or phrase followed by a colon to label the information in a prompt. In the following example, "TASK:, "CLASSES:," and "OBJECTS:" are the prefixes.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Prompt:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>TASK:
Classify the OBJECTS.

CLASSES:
- Large
- Small
OBJECTS:
- Rhino
- Mouse
- Snail
- Elephant
  </code></pre>
<strong>Response:</strong>
<pre dir="ltr" data-is-upgraded="" style="white-space: pre-line; border:1px solid Black;" translate="no"><code>- Rhino: Large
- Mouse: Small
- Snail: Small
- Elephant: Large
  </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

## Use XML and other delimiters to structure complex prompts

For complex prompts, use XML and other delimiters to separate components of a prompt. You can use `BEGIN` and `END` or `{}` section delimiters for complex and lengthy prompt components to clearly distinguish them from the actual instructions.

    You are a chatbot agent answering  customer's questions in a chat.
    Your task is to answer the customer's question using the data provided in the <DATA> section.
      - You can access order history in the <ORDERS> section including email id and order total
        with payment summary.
      - Refer to <ORDERLINES> for item level details within each order in <ORDERS>.
    
    Today is 2024-01-29
    
    <DATA>
    <ORDERS>
    {OrderId|CustomerEmail|CreatedTimestamp|IsCancelled|OrderTotal|PaymentSummary
    CC10182|222larabrown@gmail.com|2024-01-19|true|0.0|Not available
    CC10183|baklavainthebalkans@gmail.com|2024-01-19|true|0.0|Not available}
    {...}
    ...
    </ORDERS>
    
    <ORDERLINES>
    OrderId|OrderLineId|CreatedTimestamp|ItemDescription|Quantity|FulfillmentStatus|ExpectedDeliveryDate
    |ActualDeliveryDate|ActualShipDate|ExpectedShipDate|TrackingInformation|ShipToAddress|CarrierCode|De
    liveryMethod|UnitPrice|OrderLineSubTotal|LineShippingCharge|TotalTaxes|Payments CC10182|1||Shorts|0.
    0|unshipped|2024-01-31|2024-02-01|2024-01-30|2024-01-29||||ShipToAddress|115.99|0.0|0.0|0.0|
    ...
    </ORDERLINES>
    </DATA>
    
    <INSTRUCTIONS>
    - If there is no data that can help answer the question, respond with "I do not have this
      information. Please contact customer service".
    - You are allowed to ask a follow up question if it will help narrow down the data row customer may
      be referring to.
    - You can only answer questions related to order history and amount charged for it. Include OrderId
      in the response, when applicable.
    - For everything else, please redirect to the customer service agent. 
    - Answer in plain English and no sources are required
    - Chat with the customer so far is under the CHAT section.
    </INSTRUCTIONS>
    
    QUESTION: How much did I pay for my last order?
    ANSWER:

## What's next

  - Explore more examples of prompts in the [Prompt gallery](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/prompt-gallery) .
