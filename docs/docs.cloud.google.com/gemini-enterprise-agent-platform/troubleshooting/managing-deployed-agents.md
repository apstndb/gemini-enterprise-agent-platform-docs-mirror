---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/managing-deployed-agents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/managing-deployed-agents
title: Troubleshoot managing deployed agents for Agent Runtime
description: Learn how to resolve common errors when managing deployed agents, such as invalid filters when listing agents.
data_source: docs.cloud.google.com
---

This document describes how to resolve errors that you might encounter when [managing deployed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents) .

## Error when filtering the list of agents

**Issue** :

You receive an error message similar to the following:

    InvalidArgument: 400 Provided filter is not valid.

**Possible cause** :

Your filter isn't formatted properly.

**Recommended solution** :

Update the formatting of your filter so it's formatted correctly. For example, you might be using the following to filter by display name. This filter isn't formatted correctly because it's missing quotation marks:

    from vertexai import agent_engines
    
    agent_engines.list(filter=f'display_name={DISPLAY_NAME}')

In this case, enclose `{DISPLAY_NAME}` in double-quotation marks:

    from vertexai import agent_engines
    
    agent_engines.list(filter=f'display_name="{DISPLAY_NAME}"')
