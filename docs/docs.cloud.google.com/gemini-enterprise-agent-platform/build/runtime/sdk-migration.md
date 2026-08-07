---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration
title: Agent Runtime SDK migration guide
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In version v1.112.0 of the Vertex AI SDK, the `agent_engines` module within the Vertex AI SDK for Python was refactored to a [client-based design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime#migration) . The page describes the [key changes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration#changes) to the module and how to [migrate your existing code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/sdk-migration#migration) to the client based design. For general information about Agent Runtime, see [Overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime) .

## Key changes

At a high level, service client parameters are initialized on a per-client basis, and the client contains the relevant modules for service interactions. Namely,

    import vertexai
    from vertexai import agent_engines
    vertexai.init(project=GCP_PROJECT, location=GCP_REGION)
    agent_engines.create(...)

is replaced by

    import vertexai
    # Mandatory for cross-project deployment and for use of the framework-specific templates.
    vertexai.init(project=GCP_PROJECT, location=GCP_REGION)
    client = vertexai.Client(project=GCP_PROJECT, location=GCP_REGION)
    client.agent_engines.create(...)

The following namespaces for Agent Runtime in the Vertex AI SDK are in the deprecation phase. Use the equivalent namespaces from the client-based Vertex AI SDK, which has full feature parity with the deprecated modules and packages.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Vertex AI SDK namespace</th>
<th>Impacted code</th>
<th>Client-based Vertex AI SDK replacement</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">vertexai.agent_engines</code></td>
<td>Impacted methods:<br />

<ul>
<li><code dir="ltr" translate="no">vertexai.agent_engines.create</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">vertexai.agent_engines.get</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">vertexai.agent_engines.list</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">vertexai.agent_engines.update</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">vertexai.agent_engines.delete</code></li>
</ul></td>
<td>Replacement:<br />

<ul>
<li><code dir="ltr" translate="no">client.agent_engines.create</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.get</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.list</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.update</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.delete</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">client.agent_engines</code></td>
<td>Impacted methods:<br />

<ul>
<li><code dir="ltr" translate="no">client.agent_engines.create_memory</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.delete_memory</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.generate_memories</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.get_memory</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.list_memories</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.retrieve_memories</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.create_session</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.delete_session</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.get_session</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.list_sessions</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.append_session_event</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.list_session_events</code></li>
</ul></td>
<td>Replacement:<br />

<ul>
<li><code dir="ltr" translate="no">client.agent_engines.memories.create</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.memories.delete</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.memories.generate</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.memories.get</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.memories.list</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.memories.retrieve</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.sessions.create</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.sessions.delete</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.sessions.get</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.sessions.list</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.sessions.events.append</code></li>
</ul>
<ul>
<li><code dir="ltr" translate="no">client.agent_engines.sessions.events.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Migrate to the client-based design

This section contains code snippets that demonstrate how to migrate your existing Agent Runtime code to the client-based design. Note: The examples may omit imports, dependencies, and other boilerplate code to improve readability.

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

    import vertexai
    client = vertexai.Client(
      project=PROJECT,
      location=LOCATION,
    )
    client.agent_engines.create(
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

    import vertexai
    client = vertexai.Client(
      project=PROJECT,
      location=LOCATION,
    )
    client.agent_engines.update(
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

    import vertexai
    client = vertexai.Client(
      project=PROJECT,
      location=LOCATION,
    )
    agent_engine = client.agent_engines.get(name=resource_name)

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

    import vertexai
    client = vertexai.Client(
      project=PROJECT,
      location=LOCATION,
    )
    agent_engine = client.agent_engines.list()

### Deleting an Agent Runtime instance

### Before

    agent_engine.delete(
        force=True,  # Optional
    )

Alternatively, `py import vertexai from vertexai import agent_engines vertexai.init( project=PROJECT, location=LOCATION, ) agent_engine = agent_engines.delete( resource_name, # Required. force=True, # Optional )`

### After

    agent_engine.delete(
        force=True,     # Optional.
    )

Alternatively, `py import vertexai client = vertexai.Client( project=PROJECT, location=LOCATION, ) agent_engine = client.agent_engines.delete( name=resource_name, # Required. force=True, # Optional. )`
