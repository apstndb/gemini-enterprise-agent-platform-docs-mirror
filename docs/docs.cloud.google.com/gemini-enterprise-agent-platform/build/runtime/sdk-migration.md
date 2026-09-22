---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration
title: Agent Runtime SDK migration guide
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In version 2.0.1 of the Agent Platform SDK, the `agent_engines` module within the SDK was refactored and renamed to `runtimes` under the standalone `agentplatform` package. The page describes the [key changes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration#changes) to the module and how to [migrate your existing code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration#migration) to the new SDK structure. For general information about Agent Runtime, see [Overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime) .

## Key changes

At a high level, service client parameters are initialized on a per-client basis, and the client contains the relevant modules for service interactions. Namely,

    import vertexai
    from vertexai import agent_engines
    vertexai.init(project=GCP_PROJECT, location=GCP_REGION)
    agent_engines.create(...)

is replaced by

    import agentplatform
    # Mandatory for cross-project deployment and for use of the framework-specific templates.
    client = agentplatform.Client(project=GCP_PROJECT, location=GCP_REGION)
    client.runtimes.create(...)

The following namespaces in the SDK are in the deprecation phase. Use the equivalent namespaces from the client-based Agent Platform SDK, which has full feature parity with the deprecated modules and packages.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Legacy namespace</th>
<th>Impacted code</th>
<th>Replacement ( <code dir="ltr" translate="no">agentplatform</code> )</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">vertexai.agent_engines</code></td>
<td>Impacted methods:<br />

<ul>
<li><code dir="ltr" translate="no">vertexai.agent_engines.create</code></li>
<li><code dir="ltr" translate="no">vertexai.agent_engines.get</code></li>
<li><code dir="ltr" translate="no">vertexai.agent_engines.list</code></li>
<li><code dir="ltr" translate="no">vertexai.agent_engines.update</code></li>
<li><code dir="ltr" translate="no">vertexai.agent_engines.delete</code></li>
</ul></td>
<td>Replacement:<br />

<ul>
<li><code dir="ltr" translate="no">client.runtimes.create</code></li>
<li><code dir="ltr" translate="no">client.runtimes.get</code></li>
<li><code dir="ltr" translate="no">client.runtimes.list</code></li>
<li><code dir="ltr" translate="no">client.runtimes.update</code></li>
<li><code dir="ltr" translate="no">client.runtimes.delete</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">client.agent_engines</code></td>
<td>Impacted methods:<br />

<ul>
<li><code dir="ltr" translate="no">client.agent_engines.create_memory</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.delete_memory</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.generate_memories</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.get_memory</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.list_memories</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.retrieve_memories</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.create_session</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.delete_session</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.get_session</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.list_sessions</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.append_session_event</code></li>
<li><code dir="ltr" translate="no">client.agent_engines.list_session_events</code></li>
</ul></td>
<td>Replacement:<br />

<ul>
<li><code dir="ltr" translate="no">client.memory_banks.memories.create</code></li>
<li><code dir="ltr" translate="no">client.memory_banks.memories.delete</code></li>
<li><code dir="ltr" translate="no">client.memory_banks.memories.generate</code></li>
<li><code dir="ltr" translate="no">client.memory_banks.memories.get</code></li>
<li><code dir="ltr" translate="no">client.memory_banks.memories.list</code></li>
<li><code dir="ltr" translate="no">client.memory_banks.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">client.sessions.create</code></li>
<li><code dir="ltr" translate="no">client.sessions.delete</code></li>
<li><code dir="ltr" translate="no">client.sessions.get</code></li>
<li><code dir="ltr" translate="no">client.sessions.list</code></li>
<li><code dir="ltr" translate="no">client.sessions.events.append</code></li>
<li><code dir="ltr" translate="no">client.sessions.events.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Migrate to the client-based design

This section contains code snippets that demonstrate how to migrate your existing Agent Runtime code to the `agentplatform` SDK design. Note: The examples may omit imports, dependencies, and other boilerplate code to improve readability.

### Creating an Agent Runtime instance

### Before

    import vertexai
    from vertexai import agent_engines
    vertexai.init(
      project=PROJECT,
      location=LOCATION,
      staging_bucket=STAGING_BUCKET,
    )
    agent_engines.create(
        local_agent,
        requirements=REQUIREMENTS,
        extra_packages=EXTRA_PACKAGES,
        # ...
    )

### After

    import agentplatform
    client = agentplatform.Client(
      project=PROJECT,
      location=LOCATION,
    )
    client.runtimes.create(
        agent=local_agent,
        config={
            "staging_bucket": STAGING_BUCKET,
            "requirements": REQUIREMENTS,
            "extra_packages": EXTRA_PACKAGES,
            # ...
        },
    )

### Updating an Agent Runtime instance

### Before

    import vertexai
    from vertexai import agent_engines
    vertexai.init(
      project=PROJECT,
      location=LOCATION,
      staging_bucket=STAGING_BUCKET,
    )
    agent_engines.update(
        resource_name,
        agent_engine=local_agent,
        requirements=REQUIREMENTS,
        extra_packages=EXTRA_PACKAGES,
        # ...
    )

### After

    import agentplatform
    client = agentplatform.Client(
      project=PROJECT,
      location=LOCATION,
    )
    client.runtimes.update(
        name=resource_name,
        agent=local_agent,
        config={
            "staging_bucket": STAGING_BUCKET,
            "requirements": REQUIREMENTS,
            "extra_packages": EXTRA_PACKAGES,
            # ...
        },
    )

### Getting an Agent Runtime instance

### Before

    import vertexai
    from vertexai import agent_engines
    vertexai.init(
      project=PROJECT,
      location=LOCATION,
    )
    agent_engine = agent_engines.get(resource_name)

### After

    import agentplatform
    client = agentplatform.Client(
      project=PROJECT,
      location=LOCATION,
    )
    remote_agent = client.runtimes.get(name=resource_name)

### Listing Agent Runtime instances

### Before

    import vertexai
    from vertexai import agent_engines
    vertexai.init(
      project=PROJECT,
      location=LOCATION,
    )
    agent_engine = agent_engines.list()

### After

    import agentplatform
    client = agentplatform.Client(
      project=PROJECT,
      location=LOCATION,
    )
    runtimes = client.runtimes.list()

### Deleting an Agent Runtime instance

### Before

    agent_engine.delete(
        force=True,  # Optional
    )

Alternatively,

    import vertexai
    from vertexai import agent_engines
    vertexai.init(
      project=PROJECT,
      location=LOCATION,
    )
    agent_engine = agent_engines.delete(
        resource_name,  # Required.
        force=True,  # Optional
    )

### After

    remote_agent.delete(
        force=True,     # Optional.
    )

Alternatively,

    import agentplatform
    client = agentplatform.Client(
      project=PROJECT,
      location=LOCATION,
    )
    remote_agent = client.runtimes.delete(
        name=resource_name,  # Required.
        force=True,          # Optional.
    )
