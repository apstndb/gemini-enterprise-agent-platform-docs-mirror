---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/best-practices
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/best-practices
title: Best practices for using Semantic governance policies
description: Learn best practices for authorizing tools and authoring effective natural language constraints when using Semantic governance policies.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) and the [Generative AI Service Specific Terms](https://cloud.google.com/terms/service-terms#20) , as well as the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos?e=48754805) .
> 
> When you use this feature with AI Agents, the terms applicable to AI Agents in the Agreement apply.
> 
> Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** Semantic governance policy is a Generative AI Service that uses an LLM to implement natural language policies. LLMs are probabilistic and can make mistakes. Verdicts may not be accurate.

> **Note:** This feature does not support VPC-SC.

Effective governance relies on accurate, clear, and complete descriptions of tools and their parameters. Agentic systems, including agents themselves and governance layers like Semantic governance policies, require more detail than a human would to understand the applicability of available tools.

## Optimize tool descriptions

Use clear descriptions of MCP tools, and clear descriptions of parameters required by those tools.

  - **Insufficient Tool Description:** "Search for items."
  - **Effective Tool Description:** "Search the content catalog by keyword, cast member, genre, or format. Use this when the user wants to see which movies or TV programs are available. Returns top 10 items sorted by relevance."

## Be mindful of limits for descriptions

The Semantic Governance system enforces these length limits for descriptions:

| Description Item | Applies to                                                                           | Length limit    |
| :--------------- | :----------------------------------------------------------------------------------- | :-------------- |
| **Tool**         | The MCP Server, or other tool-exposing entity                                        | 1000 characters |
| **Action**       | An individual tool within the MCP server, or a function call available to your agent | 750 characters  |
| **Parameter**    | A parameter used within a tool or function call                                      | 300 characters  |

If the Semantic Governance runtime receives a description that exceeds any of these limits, it truncates the description to the stated limit, and logs a message.

## When Semantic governance policy intervenes

Semantic governance policy operates specifically as a runtime security check on **proposed tool calls** . It does not intercept, block, or modify standard conversational dialogue between the user and the agent's LLM during brainstorming, planning, or reasoning across multiple turns. The policy engine ( `Conseca` ) intercepts and evaluates requests only at the moment the model proposes invoking a tool to execute an action.

### Scenario 1: Conversational refinement versus tool execution (Denied tool call)

Consider an agent that has an `initiate_marketing_campaign` tool and is governed by the following constraint:

  - **Constraint:** *"Disallow creating or initiating any marketing campaigns without explicit manager approval."*

<!-- end list -->

1.  **Conversational planning:** A user asks the agent, *"Help me design a multi-channel marketing campaign for our new fall product launch."* The LLM converses freely with the user across multiple turns, outlining strategies, drafting email copy, and refining target demographics. The policy engine does **not** block or deny these turns because the model is engaging in conversational reasoning rather than proposing an action.

2.  **Tool invocation:** When the strategy is finalized, the user says, *"Looks great, initiate the marketing campaign now."* The LLM responds by generating a proposed tool call:
    
        initiate_marketing_campaign(campaign_name="Fall Launch", budget=50000)

3.  **Policy intervention and denial:** The Agent Gateway intercepts this proposed tool call and routes it to the policy engine ( `Conseca` ). The policy engine evaluates the action against the constraint, determines that no manager approval exists within the session history, and issues a `DENY` verdict. The tool call is blocked before it executes, and a structured denial rationale is returned to the agent.

### Scenario 2: Compliant tool execution (Allowed tool call)

Consider the same marketing agent after proper supervisory authorization is documented:

1.  **Approval provided:** The user specifies, *"My manager, VP of Corporate Marketing (jordan@example.com), reviewed the brief and approved our $50,000 budget for the Fall Launch campaign. Please initiate it."*

2.  **Tool invocation:** The LLM proposes invoking the action:
    
        initiate_marketing_campaign(campaign_name="Fall Launch", budget=50000, approval="jordan@example.com")

3.  **Policy evaluation and approval:** The policy engine intercepts the tool call, verifies within the conversation turn history that manager approval is documented, and issues an `ALLOW` verdict. The Agent Gateway forwards the call to the underlying tool endpoint, allowing the action to proceed normally.

## Examples of effective constraints

A good constraint removes ambiguity, specifies exact limits (financial, temporal, or geographic), and uses language that matches the tools that the agent is using.

### IT cloud infrastructure (security and cost control)

  - **Scenario:** Testing environments.
  - **Tool:** `provision_cloud_server` (Parameters: `region` , `instance_type` , `duration_hours` ).
  - **Tool Description:** Submits a request to provision a cloud server in a particular region, using a specific instance type, to persist for a given time duration.
  - **Effective Constraint:** *"Allow provisioning of cloud servers only in the 'us-east' or 'eu-west' regions. Deny any requests to provision 'gpu-large' or 'gpu-xlarge' instance types. Limit the duration\_hours parameter to a maximum of 72 hours."*
  - **Why it works:** Uses language that aligns with the tool description, and refers specifically to the parameters accepted by the tool.

### Ecommerce customer service (financial guardrails)

  - **Scenario:** Issuing account credits.
  - **Tool:** `apply_account_credit` (Parameters: `account_id` , `credit_amount` , `reason_category` ).
  - **Effective Constraint:** *"Limit account credits to a maximum of $50 per interaction. Don't apply any credits if the reason\_category is 'shipping\_delay' and the original order date is less than 5 days ago."*
  - **Why it works:** Sets a strict dollar threshold and combines it with a logical condition based on time and category.

## Examples of ineffective constraints

A poor constraint is typically vague, uses subjective language, or fails to map directly to descriptions of tools or tool parameters.

### IT cloud infrastructure (subjective)

  - **Ineffective Constraint:** *"Make sure not to create servers that are too expensive. Keep the duration to a reasonable amount of time."*
  - **Why it fails:** An LLM performs better with hard numbers (for example, "$50 limit") than with abstract concepts like "reasonable" or "expensive."

### Customer service (misaligned terminology)

  - **Ineffective Constraint:** *"Don't give money back to angry shoppers outside of regular business hours."*
  - **Why it fails:** "Give money back" doesn't match tool parameters ( `refund_amount` ). "Angry shoppers" is subjective, and "business hours" is undefined without a timezone.

## Guidance on language

When authoring constraints, follow these guidelines:

  - **Use plain human language:** Use complete sentences in a declarative or imperative sense (for example, *"You mustn't allow..."* or *"Disallow..."* ).
  - **Avoid weak phrasing:** Avoid *"I think it's best if..."* or *"Try to avoid..."* . Phrasing matters for the LLM judge.
  - **Be specific:** Specify constraints with directly stated limits (for example, "$1000", "8 AM to 4 PM EST"). Use wording that aligns with descriptions of tools and parameters.
  - **Avoid contradictions:** Ensure agent-scope and tool-scope constraints don't conflict (for example, different dollar thresholds).

**Test constraints:** You can test your natural language constraints using [dry run mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance#enabling-dry-run-mode) , which evaluates policies without enforcing them.

## What's next

  - Learn about governing skills in [Governing Agent Skills](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/govern-agent-skills) .
  - Learn how to bind policies to gateway egress in [Delegate authorization to Semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#configure-authz-sgp) .
  - Configure policies in [Configure semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance) .
