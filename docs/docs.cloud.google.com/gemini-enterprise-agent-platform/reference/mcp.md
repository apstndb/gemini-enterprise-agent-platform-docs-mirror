---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp
title: 'MCP Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Model Context Protocol (MCP) server that provides Agent Platform tools for building, deploying, and scaling both predictive machine learning and generative AI applications on Google Cloud.

A [Model Context Protocol (MCP) server](https://modelcontextprotocol.io/docs/learn/server-concepts) acts as a proxy between an external service that provides context, data, or capabilities to a Large Language Model (LLM) or AI application. MCP servers connect AI applications to external systems such as databases and web services, translating their responses into a format that the AI application can understand.

### Server Setup

You must [enable MCP servers](https://docs.cloud.google.com/mcp/enable-disable-mcp-servers) and [set up authentication](https://docs.cloud.google.com/mcp/authenticate-mcp) before use. For more information about using Google and Google Cloud remote MCP servers, see [Google Cloud MCP servers overview](https://docs.cloud.google.com/mcp/overview) .

### Server Endpoints

An MCP service endpoint is the network address and communication interface (usually a URL) of the MCP server that an AI application (the Host for the MCP client) uses to establish a secure, standardized connection. It is the point of contact for the LLM to request context, call a tool, or access a resource. Google MCP endpoints can be global or regional.

The Agent Platform API MCP server has the following MCP endpoints:

#### Endpoints

  - https://aiplatform.googleapis.com/mcp/generate
  - https://aiplatform.googleapis.com/mcp/predict
  - https://aiplatform.googleapis.com/mcp/notebook
  - https://aiplatform.googleapis.com/mcp/endpoints
  - https://aiplatform.googleapis.com/mcp/models
  - https://aiplatform.googleapis.com/mcp/tuning
  - https://aiplatform.googleapis.com/mcp/evaluation
  - https://aiplatform.googleapis.com/mcp/prompts
  - https://africa-south1-aiplatform.googleapis.com/mcp/generate
  - https://africa-south1-aiplatform.googleapis.com/mcp/predict
  - https://africa-south1-aiplatform.googleapis.com/mcp/notebook
  - https://africa-south1-aiplatform.googleapis.com/mcp/endpoints
  - https://africa-south1-aiplatform.googleapis.com/mcp/models
  - https://africa-south1-aiplatform.googleapis.com/mcp/tuning
  - https://africa-south1-aiplatform.googleapis.com/mcp/evaluation
  - https://africa-south1-aiplatform.googleapis.com/mcp/prompts
  - https://asia-east1-aiplatform.googleapis.com/mcp/generate
  - https://asia-east1-aiplatform.googleapis.com/mcp/predict
  - https://asia-east1-aiplatform.googleapis.com/mcp/notebook
  - https://asia-east1-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-east1-aiplatform.googleapis.com/mcp/models
  - https://asia-east1-aiplatform.googleapis.com/mcp/tuning
  - https://asia-east1-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-east1-aiplatform.googleapis.com/mcp/prompts
  - https://asia-east2-aiplatform.googleapis.com/mcp/generate
  - https://asia-east2-aiplatform.googleapis.com/mcp/predict
  - https://asia-east2-aiplatform.googleapis.com/mcp/notebook
  - https://asia-east2-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-east2-aiplatform.googleapis.com/mcp/models
  - https://asia-east2-aiplatform.googleapis.com/mcp/tuning
  - https://asia-east2-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-east2-aiplatform.googleapis.com/mcp/prompts
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/generate
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/predict
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/notebook
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/models
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/tuning
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-northeast1-aiplatform.googleapis.com/mcp/prompts
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/generate
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/predict
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/notebook
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/models
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/tuning
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-northeast2-aiplatform.googleapis.com/mcp/prompts
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/generate
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/predict
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/notebook
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/models
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/tuning
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-northeast3-aiplatform.googleapis.com/mcp/prompts
  - https://asia-south1-aiplatform.googleapis.com/mcp/generate
  - https://asia-south1-aiplatform.googleapis.com/mcp/predict
  - https://asia-south1-aiplatform.googleapis.com/mcp/notebook
  - https://asia-south1-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-south1-aiplatform.googleapis.com/mcp/models
  - https://asia-south1-aiplatform.googleapis.com/mcp/tuning
  - https://asia-south1-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-south1-aiplatform.googleapis.com/mcp/prompts
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/generate
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/predict
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/notebook
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/models
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/tuning
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-southeast1-aiplatform.googleapis.com/mcp/prompts
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/generate
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/predict
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/notebook
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/endpoints
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/models
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/tuning
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/evaluation
  - https://asia-southeast2-aiplatform.googleapis.com/mcp/prompts
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/generate
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/predict
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/notebook
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/endpoints
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/models
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/tuning
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/evaluation
  - https://australia-southeast1-aiplatform.googleapis.com/mcp/prompts
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/generate
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/predict
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/notebook
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/endpoints
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/models
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/tuning
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/evaluation
  - https://australia-southeast2-aiplatform.googleapis.com/mcp/prompts
  - https://europe-central2-aiplatform.googleapis.com/mcp/generate
  - https://europe-central2-aiplatform.googleapis.com/mcp/predict
  - https://europe-central2-aiplatform.googleapis.com/mcp/notebook
  - https://europe-central2-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-central2-aiplatform.googleapis.com/mcp/models
  - https://europe-central2-aiplatform.googleapis.com/mcp/tuning
  - https://europe-central2-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-central2-aiplatform.googleapis.com/mcp/prompts
  - https://europe-north1-aiplatform.googleapis.com/mcp/generate
  - https://europe-north1-aiplatform.googleapis.com/mcp/predict
  - https://europe-north1-aiplatform.googleapis.com/mcp/notebook
  - https://europe-north1-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-north1-aiplatform.googleapis.com/mcp/models
  - https://europe-north1-aiplatform.googleapis.com/mcp/tuning
  - https://europe-north1-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-north1-aiplatform.googleapis.com/mcp/prompts
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/generate
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/predict
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/notebook
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/models
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/tuning
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-southwest1-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west1-aiplatform.googleapis.com/mcp/generate
  - https://europe-west1-aiplatform.googleapis.com/mcp/predict
  - https://europe-west1-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west1-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west1-aiplatform.googleapis.com/mcp/models
  - https://europe-west1-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west1-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west1-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west2-aiplatform.googleapis.com/mcp/generate
  - https://europe-west2-aiplatform.googleapis.com/mcp/predict
  - https://europe-west2-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west2-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west2-aiplatform.googleapis.com/mcp/models
  - https://europe-west2-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west2-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west2-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west3-aiplatform.googleapis.com/mcp/generate
  - https://europe-west3-aiplatform.googleapis.com/mcp/predict
  - https://europe-west3-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west3-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west3-aiplatform.googleapis.com/mcp/models
  - https://europe-west3-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west3-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west3-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west4-aiplatform.googleapis.com/mcp/generate
  - https://europe-west4-aiplatform.googleapis.com/mcp/predict
  - https://europe-west4-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west4-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west4-aiplatform.googleapis.com/mcp/models
  - https://europe-west4-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west4-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west4-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west6-aiplatform.googleapis.com/mcp/generate
  - https://europe-west6-aiplatform.googleapis.com/mcp/predict
  - https://europe-west6-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west6-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west6-aiplatform.googleapis.com/mcp/models
  - https://europe-west6-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west6-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west6-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west8-aiplatform.googleapis.com/mcp/generate
  - https://europe-west8-aiplatform.googleapis.com/mcp/predict
  - https://europe-west8-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west8-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west8-aiplatform.googleapis.com/mcp/models
  - https://europe-west8-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west8-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west8-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west9-aiplatform.googleapis.com/mcp/generate
  - https://europe-west9-aiplatform.googleapis.com/mcp/predict
  - https://europe-west9-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west9-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west9-aiplatform.googleapis.com/mcp/models
  - https://europe-west9-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west9-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west9-aiplatform.googleapis.com/mcp/prompts
  - https://europe-west12-aiplatform.googleapis.com/mcp/generate
  - https://europe-west12-aiplatform.googleapis.com/mcp/predict
  - https://europe-west12-aiplatform.googleapis.com/mcp/notebook
  - https://europe-west12-aiplatform.googleapis.com/mcp/endpoints
  - https://europe-west12-aiplatform.googleapis.com/mcp/models
  - https://europe-west12-aiplatform.googleapis.com/mcp/tuning
  - https://europe-west12-aiplatform.googleapis.com/mcp/evaluation
  - https://europe-west12-aiplatform.googleapis.com/mcp/prompts
  - https://me-central1-aiplatform.googleapis.com/mcp/generate
  - https://me-central1-aiplatform.googleapis.com/mcp/predict
  - https://me-central1-aiplatform.googleapis.com/mcp/notebook
  - https://me-central1-aiplatform.googleapis.com/mcp/endpoints
  - https://me-central1-aiplatform.googleapis.com/mcp/models
  - https://me-central1-aiplatform.googleapis.com/mcp/tuning
  - https://me-central1-aiplatform.googleapis.com/mcp/evaluation
  - https://me-central1-aiplatform.googleapis.com/mcp/prompts
  - https://me-central2-aiplatform.googleapis.com/mcp/generate
  - https://me-central2-aiplatform.googleapis.com/mcp/predict
  - https://me-central2-aiplatform.googleapis.com/mcp/notebook
  - https://me-central2-aiplatform.googleapis.com/mcp/endpoints
  - https://me-central2-aiplatform.googleapis.com/mcp/models
  - https://me-central2-aiplatform.googleapis.com/mcp/tuning
  - https://me-central2-aiplatform.googleapis.com/mcp/evaluation
  - https://me-central2-aiplatform.googleapis.com/mcp/prompts
  - https://me-west1-aiplatform.googleapis.com/mcp/generate
  - https://me-west1-aiplatform.googleapis.com/mcp/predict
  - https://me-west1-aiplatform.googleapis.com/mcp/notebook
  - https://me-west1-aiplatform.googleapis.com/mcp/endpoints
  - https://me-west1-aiplatform.googleapis.com/mcp/models
  - https://me-west1-aiplatform.googleapis.com/mcp/tuning
  - https://me-west1-aiplatform.googleapis.com/mcp/evaluation
  - https://me-west1-aiplatform.googleapis.com/mcp/prompts
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/generate
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/predict
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/notebook
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/endpoints
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/models
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/tuning
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/evaluation
  - https://northamerica-northeast1-aiplatform.googleapis.com/mcp/prompts
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/generate
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/predict
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/notebook
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/endpoints
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/models
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/tuning
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/evaluation
  - https://northamerica-northeast2-aiplatform.googleapis.com/mcp/prompts
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/generate
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/predict
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/notebook
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/endpoints
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/models
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/tuning
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/evaluation
  - https://southamerica-east1-aiplatform.googleapis.com/mcp/prompts
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/generate
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/predict
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/notebook
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/endpoints
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/models
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/tuning
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/evaluation
  - https://southamerica-west1-aiplatform.googleapis.com/mcp/prompts
  - https://us-central1-aiplatform.googleapis.com/mcp/generate
  - https://us-central1-aiplatform.googleapis.com/mcp/predict
  - https://us-central1-aiplatform.googleapis.com/mcp/notebook
  - https://us-central1-aiplatform.googleapis.com/mcp/endpoints
  - https://us-central1-aiplatform.googleapis.com/mcp/models
  - https://us-central1-aiplatform.googleapis.com/mcp/tuning
  - https://us-central1-aiplatform.googleapis.com/mcp/evaluation
  - https://us-central1-aiplatform.googleapis.com/mcp/prompts
  - https://us-east1-aiplatform.googleapis.com/mcp/generate
  - https://us-east1-aiplatform.googleapis.com/mcp/predict
  - https://us-east1-aiplatform.googleapis.com/mcp/notebook
  - https://us-east1-aiplatform.googleapis.com/mcp/endpoints
  - https://us-east1-aiplatform.googleapis.com/mcp/models
  - https://us-east1-aiplatform.googleapis.com/mcp/tuning
  - https://us-east1-aiplatform.googleapis.com/mcp/evaluation
  - https://us-east1-aiplatform.googleapis.com/mcp/prompts
  - https://us-east4-aiplatform.googleapis.com/mcp/generate
  - https://us-east4-aiplatform.googleapis.com/mcp/predict
  - https://us-east4-aiplatform.googleapis.com/mcp/notebook
  - https://us-east4-aiplatform.googleapis.com/mcp/endpoints
  - https://us-east4-aiplatform.googleapis.com/mcp/models
  - https://us-east4-aiplatform.googleapis.com/mcp/tuning
  - https://us-east4-aiplatform.googleapis.com/mcp/evaluation
  - https://us-east4-aiplatform.googleapis.com/mcp/prompts
  - https://us-east5-aiplatform.googleapis.com/mcp/generate
  - https://us-east5-aiplatform.googleapis.com/mcp/predict
  - https://us-east5-aiplatform.googleapis.com/mcp/notebook
  - https://us-east5-aiplatform.googleapis.com/mcp/endpoints
  - https://us-east5-aiplatform.googleapis.com/mcp/models
  - https://us-east5-aiplatform.googleapis.com/mcp/tuning
  - https://us-east5-aiplatform.googleapis.com/mcp/evaluation
  - https://us-east5-aiplatform.googleapis.com/mcp/prompts
  - https://us-south1-aiplatform.googleapis.com/mcp/generate
  - https://us-south1-aiplatform.googleapis.com/mcp/predict
  - https://us-south1-aiplatform.googleapis.com/mcp/notebook
  - https://us-south1-aiplatform.googleapis.com/mcp/endpoints
  - https://us-south1-aiplatform.googleapis.com/mcp/models
  - https://us-south1-aiplatform.googleapis.com/mcp/tuning
  - https://us-south1-aiplatform.googleapis.com/mcp/evaluation
  - https://us-south1-aiplatform.googleapis.com/mcp/prompts
  - https://us-west1-aiplatform.googleapis.com/mcp/generate
  - https://us-west1-aiplatform.googleapis.com/mcp/predict
  - https://us-west1-aiplatform.googleapis.com/mcp/notebook
  - https://us-west1-aiplatform.googleapis.com/mcp/endpoints
  - https://us-west1-aiplatform.googleapis.com/mcp/models
  - https://us-west1-aiplatform.googleapis.com/mcp/tuning
  - https://us-west1-aiplatform.googleapis.com/mcp/evaluation
  - https://us-west1-aiplatform.googleapis.com/mcp/prompts
  - https://us-west2-aiplatform.googleapis.com/mcp/generate
  - https://us-west2-aiplatform.googleapis.com/mcp/predict
  - https://us-west2-aiplatform.googleapis.com/mcp/notebook
  - https://us-west2-aiplatform.googleapis.com/mcp/endpoints
  - https://us-west2-aiplatform.googleapis.com/mcp/models
  - https://us-west2-aiplatform.googleapis.com/mcp/tuning
  - https://us-west2-aiplatform.googleapis.com/mcp/evaluation
  - https://us-west2-aiplatform.googleapis.com/mcp/prompts
  - https://us-west3-aiplatform.googleapis.com/mcp/generate
  - https://us-west3-aiplatform.googleapis.com/mcp/predict
  - https://us-west3-aiplatform.googleapis.com/mcp/notebook
  - https://us-west3-aiplatform.googleapis.com/mcp/endpoints
  - https://us-west3-aiplatform.googleapis.com/mcp/models
  - https://us-west3-aiplatform.googleapis.com/mcp/tuning
  - https://us-west3-aiplatform.googleapis.com/mcp/evaluation
  - https://us-west3-aiplatform.googleapis.com/mcp/prompts
  - https://us-west4-aiplatform.googleapis.com/mcp/generate
  - https://us-west4-aiplatform.googleapis.com/mcp/predict
  - https://us-west4-aiplatform.googleapis.com/mcp/notebook
  - https://us-west4-aiplatform.googleapis.com/mcp/endpoints
  - https://us-west4-aiplatform.googleapis.com/mcp/models
  - https://us-west4-aiplatform.googleapis.com/mcp/tuning
  - https://us-west4-aiplatform.googleapis.com/mcp/evaluation
  - https://us-west4-aiplatform.googleapis.com/mcp/prompts
  - https://aiplatform.eu.rep.googleapis.com/mcp/generate
  - https://aiplatform.eu.rep.googleapis.com/mcp/predict
  - https://aiplatform.eu.rep.googleapis.com/mcp/notebook
  - https://aiplatform.eu.rep.googleapis.com/mcp/endpoints
  - https://aiplatform.eu.rep.googleapis.com/mcp/models
  - https://aiplatform.eu.rep.googleapis.com/mcp/tuning
  - https://aiplatform.eu.rep.googleapis.com/mcp/evaluation
  - https://aiplatform.eu.rep.googleapis.com/mcp/prompts
  - https://aiplatform.us.rep.googleapis.com/mcp/generate
  - https://aiplatform.us.rep.googleapis.com/mcp/predict
  - https://aiplatform.us.rep.googleapis.com/mcp/notebook
  - https://aiplatform.us.rep.googleapis.com/mcp/endpoints
  - https://aiplatform.us.rep.googleapis.com/mcp/models
  - https://aiplatform.us.rep.googleapis.com/mcp/tuning
  - https://aiplatform.us.rep.googleapis.com/mcp/evaluation
  - https://aiplatform.us.rep.googleapis.com/mcp/prompts

The Agent Platform API MCP server offers the following MCP toolset endpoints:

  - https://aiplatform.googleapis.com/mcp/generate
  - https://aiplatform.googleapis.com/mcp/predict
  - https://aiplatform.googleapis.com/mcp/notebook
  - https://aiplatform.googleapis.com/mcp/endpoints
  - https://aiplatform.googleapis.com/mcp/models
  - https://aiplatform.googleapis.com/mcp/tuning
  - https://aiplatform.googleapis.com/mcp/evaluation
  - https://aiplatform.googleapis.com/mcp/prompts

## MCP Tools

An [MCP tool](https://modelcontextprotocol.io/legacy/concepts/tools) is a function or executable capability that an MCP server exposes to a LLM or AI application to perform an action in the real world. Toolsets are a group of tools that are useful for a specific task. Using toolsets can help your agent perform better because it decreases the number of tools available to your agent.

### Toolsets

The aiplatform.googleapis.com MCP server has the following toolsets:

MCP Toolsets

Endpoint

Description

Tools

/mcp/generate

Generative AI tools

`  `

  - [generate\_content](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content)
  - [count\_tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/count_tokens)
  - [embed\_content](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/embed_content)

/mcp/predict

Prediction tools

`  `

  - [predict](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/predict)
  - [raw\_predict](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/raw_predict)

/mcp/notebook

Colab Enterprise Notebook tools

`  `

  - [colab\_enterprise\_create\_notebook\_runtime\_template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template)
  - [colab\_enterprise\_get\_notebook\_runtime\_template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_get_notebook_runtime_template)
  - [colab\_enterprise\_list\_notebook\_runtime\_templates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_list_notebook_runtime_templates)
  - [colab\_enterprise\_delete\_notebook\_runtime\_template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_delete_notebook_runtime_template)
  - [colab\_enterprise\_update\_notebook\_runtime\_template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_update_notebook_runtime_template)
  - [colab\_enterprise\_create\_notebook\_runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime)
  - [colab\_enterprise\_get\_notebook\_runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_get_notebook_runtime)
  - [colab\_enterprise\_list\_notebook\_runtimes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_list_notebook_runtimes)
  - [colab\_enterprise\_delete\_notebook\_runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_delete_notebook_runtime)
  - [colab\_enterprise\_upgrade\_notebook\_runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_upgrade_notebook_runtime)
  - [colab\_enterprise\_start\_notebook\_runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_start_notebook_runtime)
  - [colab\_enterprise\_stop\_notebook\_runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_stop_notebook_runtime)
  - [notebook\_execution\_create\_job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job)
  - [notebook\_execution\_get\_job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_get_job)
  - [notebook\_execution\_list\_jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_list_jobs)
  - [notebook\_execution\_delete\_job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_delete_job)
  - [create\_notebook\_execution\_schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule)
  - [delete\_notebook\_execution\_schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/delete_notebook_execution_schedule)
  - [get\_notebook\_execution\_schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_notebook_execution_schedule)
  - [list\_notebook\_execution\_schedules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_notebook_execution_schedules)
  - [pause\_notebook\_execution\_schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/pause_notebook_execution_schedule)
  - [resume\_notebook\_execution\_schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/resume_notebook_execution_schedule)
  - [update\_notebook\_execution\_schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_notebook_execution_schedule)
  - [get\_operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_operation)

/mcp/endpoints

Endpoint Management tools

`  `

  - [create\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint)
  - [get\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_endpoint)
  - [list\_endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_endpoints)
  - [update\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_endpoint)
  - [delete\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/delete_endpoint)
  - [get\_operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_operation)

/mcp/models

Model Registry tools

`  `

  - [upload\_model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model)
  - [list\_models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_models)
  - [get\_model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_model)
  - [update\_model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_model)
  - [delete\_model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/delete_model)
  - [create\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint)
  - [get\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_endpoint)
  - [list\_endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_endpoints)
  - [update\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_endpoint)
  - [delete\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/delete_endpoint)
  - [get\_operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_operation)

/mcp/tuning

Model Finetuning tools

`  `

  - [list\_tuning\_jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs)
  - [get\_tuning\_job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_tuning_job)
  - [cancel\_tuning\_job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/cancel_tuning_job)
  - [get\_operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_operation)

/mcp/evaluation

Quality Evaluation tools

`  `

  - [evaluate\_instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances)

/mcp/prompts

Prompt Management tools

`  `

  - [create\_prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_prompt)
  - [get\_prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_prompt)
  - [list\_prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_prompts)
  - [update\_prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_prompt)
  - [delete\_prompt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/delete_prompt)
  - [create\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint)
  - [get\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_endpoint)
  - [list\_endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_endpoints)
  - [update\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_endpoint)
  - [delete\_endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/delete_endpoint)
  - [get\_operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_operation)

### Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `tools/list` method. The following example demonstrates how to use `curl` to list all tools and their specifications currently available within the MCP server.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                      
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
    &quot;method&quot;: &quot;tools/list&quot;,
    &quot;jsonrpc&quot;: &quot;2.0&quot;,
    &quot;id&quot;: 1
}&#39;
                    </code></pre></td>
</tr>
</tbody>
</table>
