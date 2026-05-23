---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry
title: Skill Registry overview
description: Overview of Skill Registry, a secure, private, and low-latency repository for managing and discovering agent skills.
data_source: docs.cloud.google.com
---

> **Preview:** This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the Service Specific Terms. When you use this feature with AI Agents, the terms applicable to AI Agents in the Agreement apply. Pre-GA features are available "as is" and might have limited support. For more information, see the launch stage descriptions.

Skill Registry serves as a secure, private, and low-latency repository for managing agent skills. Each skill is a self-contained package, including structural instructions, executable code, and documentation, designed to extend an agent's capabilities.

By centralizing these skills, Skill Registry empowers agents to dynamically discover and load the most relevant capabilities based on user intent, thereby optimizing performance and ensuring a secure execution environment.

## Key concepts

Skill Registry introduces two top-level, standard API entities to manage lifecycle and versioning:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Concept</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Skill</strong></td>
<td>A mutable top-level entity containing metadata (such as display name, creation and update timestamps, and labels), the default revision, and the skill's content.<br />
<br />
For examples of the expected skill structure, see the <code dir="ltr" translate="no">SKILL.md</code> files in the <a href="https://github.com/google/skills/tree/main">Google Cloud Skills repository</a> .</td>
</tr>
<tr class="even">
<td><strong>Skill revision</strong></td>
<td>An immutable snapshot of a specific skill version. It includes a name, a description, and an immutable reference to the parent skill resource.</td>
</tr>
</tbody>
</table>

## Skill payload validation

To ensure agents can use valid skill content, the system automatically verifies all skill payloads during creation or updates. These validations are performed asynchronously.

The asynchronous operation fails with a validation error if the system detects any of the following:

  - The file isn't a proper zip file or is missing key information.
  - The zip file is empty.
  - The zip file has more than 10,000 items inside.
  - The file or folder names in the zip contain `..` or start with `/` or `\\` .
  - The zip file contains symbolic links.
  - There are duplicate file or folder names in the zip file.
  - The total size of all files inside the zip is over 500 MB when unzipped.
  - The file is compressed too much, with a compression ratio over 100.
  - The folders inside the zip go more than 8 levels deep.
  - The zip file does not contain a `SKILL.md` file.
  - The `SKILL.md` file has the following issues:
      - The `SKILL.md` file is missing the required YAML front matter or the expected Markdown content.
      - The name field in the YAML front matter is missing, exceeds 64 characters, starts or ends with a hyphen, or contains characters other than lowercase letters, numbers, and hyphens.
      - The description field in the YAML front matter is missing or exceeds 1024 characters.
      - The license field in the YAML front matter exceeds 1024 characters.
      - The instructions in the `SKILL.md` file exceed 500,000 characters.
  - The zipped archive is over 10 MB in size.

## Built-in skills

Skill Registry includes a built-in `gcp-skill-registry` skill. This skill allows agents to interact with Skill Registry to create, search for, and manage available skills, enabling them to register new functionality or discover existing capabilities. Google manages the lifecycle, release, and versioning of this built-in skill, ensuring out-of-the-box functionality.

> **Note:** The system starts the built-in skill ingestion pipeline when you make your first API call to Skill Registry. Because the system provisions this skill during the first call, your first API response doesn't include it; it appears in all subsequent calls.

## What's next

Guide

### [Create and manage skills](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry/create-manage)

Learn how to create, update, search, and delete skills in Skill Registry.
