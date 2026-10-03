---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutomaticResources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutomaticResources
title: AutomaticResources
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration. Each Model supporting these resources documents its specific guidelines.

Fields

`minReplicaCount` `integer`

Immutable. The minimum number of replicas that will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas up to [`maxReplicaCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutomaticResources#FIELDS.max_replica_count) , and as traffic decreases, some of these extra replicas may be freed. If the requested value is too large, the deployment will error.

`maxReplicaCount` `integer`

Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, a no upper bound for scaling under heavy traffic will be assume, though Agent Platform may be unable to scale beyond certain replica number.

**JSON representation**

```
{
  "minReplicaCount": integer,
  "maxReplicaCount": integer
}
```
