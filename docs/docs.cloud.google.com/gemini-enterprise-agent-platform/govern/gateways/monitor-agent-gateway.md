---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway
title: Monitor traffic through Agent Gateway
description: Monitor traffic through Agent Gateway.
data_source: docs.cloud.google.com
---

> **Private Preview — Agent Gateway**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides capabilities to govern and secure AI Agents, so the "Agentic AI Services" Service Specific Terms apply. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> To request access to use Agent Gateway with Agent Runtime, see the [access request page](https://forms.gle/ZLNYKUDW7j2B4a8K7) .

Use this page to learn how to view logs and monitor requests and access control decisions for traffic routed through your Agent Gateway deployment.

## Logging

Agent Gateway logs are generated using the `networkservices.googleapis.com/Gateway` monitored resource.

You can use these logs to monitor access requests to the gateway. This includes the logs created when Agent Gateway is deployed in dry-run mode.

### View logs for a specific gateway

To view the logs for a specific gateway, complete the following steps.

### Console query

1.  In the Google Cloud console, go to the **Logs Explorer** page.

2.  Click the **Show query** toggle.

3.  Paste the following into the query field.
    
        resource.type="networkservices.googleapis.com/Gateway"
        resource.labels.location="REGION"
        resource.labels.gateway_name="AGENT_GATEWAY_NAME"
    
    Replace the following:
    
      - `  REGION  ` : The region of your gateway.
      - `  AGENT_GATEWAY_NAME  ` : The name of your gateway.

4.  Click **Run query** .

### What is logged

Agent Gateway log entries contain information useful for monitoring and debugging traffic to and from your gateway.

Field

Field format

Field type: Required or Optional

Description

**severity**  
**insertID**  
**timestamp**  
**receiveTimestamp**  
**trace**  
**traceSampled**  
**logName**

[LogEntry](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry)

Required

The general fields as described in a log entry.

**httpRequest**

[HttpRequest](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry#HttpRequest)

Required

A common protocol for logging HTTP requests.

**resource**

[MonitoredResource](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/MonitoredResource)

Required

The `MonitoredResource` is the resource type associated with a log entry. The resource type for Agent Gateway is `networkservices.googleapis.com/Gateway` .

**jsonPayload**

object ( [Struct](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf?_ga=#struct) format)

Required

The log entry payload that is expressed as a JSON object. The JSON object contains the following Agent Gateway fields:

`agentGatewayInfo` : Includes information about Agent Gateway requests.

  - `mcpInfo` : Includes information about the MCP method of the request (for example, "tools/list" or "tools/call") and the primary parameter associated with the method, if any. For example, in the case of the "tools/call" method the parameter is the tool name.
  - `agentRegistryResource` : The Agent Registry resource name of the MCP server, agent, or endpoint that was matched to the request.

## Monitoring

Agent Gateway exports some Service Extensions metrics to Cloud Monitoring. If you're delegating authorization to Service Extensions, you can use these metrics to monitor traffic to and from your extension. For details, see [Logging and monitoring for Cloud Load Balancing callouts](https://docs.cloud.google.com/service-extensions/docs/monitor-lb-callouts#monitoring_metrics_for_callouts) .
