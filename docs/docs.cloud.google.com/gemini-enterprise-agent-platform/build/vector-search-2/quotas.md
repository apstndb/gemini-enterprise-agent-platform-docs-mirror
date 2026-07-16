---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/quotas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/quotas
title: Agent Retrieval quotas
description: Learn about using quotas in Agent Retrieval (formerly Vector Search 2.0).
data_source: docs.cloud.google.com
---

Google Cloud uses quotas to help ensure fairness and reduce spikes in resource use and availability. A quota restricts how much of a Google Cloud resource your Google Cloud project can use. Quotas apply to a range of resource types, including hardware, software, and network components. For example, quotas can restrict the number of API calls to a service, the number of load balancers used concurrently by your project, or the number of projects that you can create. Quotas protect the community of Google Cloud users by preventing the overloading of services. Quotas also help you to manage your own Google Cloud resources.

The Cloud Quotas system does the following:

  - Monitors your consumption of Google Cloud products and services
  - Restricts your consumption of those resources
  - Provides a way to [request changes to the quota value](https://docs.cloud.google.com/docs/quotas/help/request_increase) and [automate quota adjustments](https://docs.cloud.google.com/docs/quotas/quota-adjuster)

In most cases, when you attempt to consume more of a resource than its quota allows, the system blocks access to the resource, and the task that you're trying to perform fails.

Quotas generally apply at the Google Cloud project level. Your use of a resource in one project doesn't affect your available quota in another project. Within a Google Cloud project, quotas are shared across all applications and IP addresses.

For more information, see the [Cloud Quotas overview](https://docs.cloud.google.com/docs/quotas/overview) .

In Agent Retrieval (formerly Vector Search 2.0), quotas are enforced to protect the service, ensure fair sharing of capacity between projects, and give you more predictable performance and cost. Quotas are tracked independently by region. For example, usage in `us-central` doesn't affect your quota in `europe-west4` .

## Metrics

All metric names are prefixed with `vectorsearch.googleapis.com/` .

## Rate quotas (requests/min and bytes/min)

For data rate quotas, quotas are evaluated *per minute* and apply *per project* and *per region* (or *multi-region* ), and optionally *per Collection* .

Each accepted API call increments the counter by **one request** (or N bytes for byte quotas). Counters are **per calendar minute** and use a sliding-window evaluation (there is no hard reset at : `00` ).

You can run at the limit continuously without seeing a "refill" effect.

When a counter exceeds its limit, additional requests return `RESOURCE_EXHAUSTED` (HTTP 429) with `reason="RATE_LIMIT_EXCEEDED"` and the exact metric name in the `quota_metric` field.

### Control-plane rate quotas

The following quotas apply to resource lifecycle, and read and list operations on Collections and indexes for a given project and region.

**Scope** : per project, per region

**Unit** : `1/min`

**Limits** : requests per minute.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric</th>
<th>Counts</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">collection_management_requests</code></td>
<td><code dir="ltr" translate="no">collections.create</code><br />
<code dir="ltr" translate="no">collections.update</code><br />
<code dir="ltr" translate="no">collections.delete</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">collection_read_requests</code></td>
<td><code dir="ltr" translate="no">collections.get</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">collection_list_requests</code></td>
<td><code dir="ltr" translate="no">collections.list</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">index_management_requests</code></td>
<td><code dir="ltr" translate="no">indexes.create</code><br />
<code dir="ltr" translate="no">indexes.update</code><br />
<code dir="ltr" translate="no">indexes.delete</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">index_read_requests</code></td>
<td><code dir="ltr" translate="no">indexes.get</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">index_list_requests</code></td>
<td><code dir="ltr" translate="no">indexes.list</code></td>
</tr>
</tbody>
</table>

### Long-running operation (LRO) requests

The following quotas apply to long running read, list, cancel, and delete operations for a given project and region.

**Scope** : per project, per region

**Unit** : `1/min`

**Limits** : requests per minute.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric</th>
<th>Counts</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">lro_requests</code></td>
<td><code dir="ltr" translate="no">operations.get</code><br />
<code dir="ltr" translate="no">operations.list</code><br />
<code dir="ltr" translate="no">operations.cancel</code><br />
<code dir="ltr" translate="no">operations.delete</code></td>
</tr>
</tbody>
</table>

### Data-plane rate quotas

The following quotas apply to Data Objects, query, and search traffic for a given project, region, and collection.

**Note** : Search requests quotas ( `search_requests` ) are consumed for text search and semantic search.

**Scope** : per project, per region, per Collection

**Unit** : `1/min`

**Limits** : requests per minute, per Collection

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric</th>
<th>Counts</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">data_object_writes</code></td>
<td><code dir="ltr" translate="no">dataObjects.create</code><br />
<code dir="ltr" translate="no">dataObjects.update</code><br />
<code dir="ltr" translate="no">dataObjects.delete</code> \<br />
Each Data Object included in<br />
<code dir="ltr" translate="no">batchCreate</code><br />
<code dir="ltr" translate="no">batchUpdate</code><br />
<code dir="ltr" translate="no">batchDelete</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">data_object_reads</code></td>
<td><code dir="ltr" translate="no">dataObjects.get</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">query_requests</code></td>
<td><code dir="ltr" translate="no">dataObjects.query</code> (metadata-only filter queries)</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">search_requests</code></td>
<td><code dir="ltr" translate="no">dataObjects.search</code> when running a dense or sparse ANN.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">knn_search_requests</code></td>
<td><code dir="ltr" translate="no">dataObjects.search</code> when running an exhaustive KNN search.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">batch_search_requests</code></td>
<td><code dir="ltr" translate="no">dataObjects.batchSearch</code> (one request regardless of sub-searches)</td>
</tr>
</tbody>
</table>

### Data-plane throughput quotas

The following quotas apply to bytes written per minute for a given project, region, and Collection.

**Scope** : per project, per region, per Collection

**Unit** : `1/min`

**Limits** : requests per minute, per Collection

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Metric</th>
<th>Counts</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">data_object_write_bytes</code></td>
<td>The sum of serialized data and vector bytes written by all<br />
<code dir="ltr" translate="no">create</code> , <code dir="ltr" translate="no">update</code> , <code dir="ltr" translate="no">delete</code> , <code dir="ltr" translate="no">batchCreate</code> , <code dir="ltr" translate="no">batchUpdate</code> , and<br />
<code dir="ltr" translate="no">batchDelete</code> calls for Collections, Data Objects, and indexes.</td>
</tr>
</tbody>
</table>

### Batch operations

  - `batchCreate, batchUpdate, batchDelete dataObjects` : each individual Data Object in the request counts as **one write** against `data_object_writes` and contributes its serialized size in bytes to `data_object_write_bytes` .

  - `batchSearch dataObjects` : counts as **one request** against `batch_search_requests` regardless of how many sub-searches are bundled. Batch search causes the subsearches quota to also be counted.

## Allocation quotas (current count)

Allocation quotas are a *current count* .

Counters are a live count of resources or in-flight operations owned by the project.

The count increases on resource creation or operation start and decreases on deletion or operation completion.

When the limit is reached, the next create call returns `RESOURCE_EXHAUSTED` . Delete an existing resource or wait for an LRO to finish to free quota.

### Control-plane allocation quotas

The following quotas apply to the number of resources or in-flight operations a project may hold for a given project and region, including the following:

  - Collections
  - Indexes
  - Concurrent create, import, and export operations on Collections, Data Objects, and indexes

**Scope** : per project, per region

**Unit** : `1`

**Limits** : absolute counts (precise quotas)

| Metric                             | Counts                                                                       |
| ---------------------------------- | ---------------------------------------------------------------------------- |
| `collections`                      | The number of Collections that exist in the project/region.                  |
| `indexes`                          | The number of indexes (summed across all Collections) in the project/region. |
| `concurrent_index_operations`      | The in-flight index LROs (Create/Update/Delete).                             |
| `concurrent_collection_operations` | The in-flight Collection LROs (Create/Update/Delete).                        |
| `concurrent_data_object_imports`   | The in-flight `dataObjects.import` LROs.                                     |
| `concurrent_data_object_exports`   | The in-flight `dataObjects.export` LROs.                                     |

## Auto-embedding

Auto-embedding uses the Gemini API in Vertex AI ( `aiplatform.googleapis.com` ). Each API request counts against `search_requests` or `data_object_writes` *and* the embedding call counts against prediction quotas. Ensure both APIs have headroom.

## Usage Examples

The following sections describe how different usage scenarios impact quotas.

### Sustained write workload

You are ingesting documents (data plus a 768-dim dense vector, about 4 KB) into a single Collection in `us-central1` . Two quotas apply simultaneously:

    data_object_writes        (requests per minute, per collection)
    data_object_write_bytes   (bytes per minute, per collection)

You are limited by **whichever ceiling you hit first** . With small objects, the request-rate quota usually binds. With large objects, the bytes quota binds.

Check both metrics in the Google Cloud console to know which one is closest to its limit.

### Search-heavy workload

A serving workload sending ANN queries to a single Collection consumes `search_requests` . If your peak queries per second (QPS) approaches your per Collection limit, either request an increase or distribute traffic across multiple Collections in the same region.

### Many small Collections

If you plan to create more Collections than your project's `collections` limit allows, request an increase **before** you start creating. Otherwise, the create call that exceeds the limit will fail with `RESOURCE_EXHAUSTED` .

### Batch search

A `batchSearch` containing 10 sub-searches consumes exactly **one** `batch_search_requests` , but each sub-search still counts against its respective per-sub-search metric only at the level of the outer batch. Plan batch fan-out accordingly.

## Viewing quotas

To view your quotas:

1.  Open the [IAM & Admin \> Quotas page](https://console.cloud.google.com/iam-admin/quotas) in the Google Cloud console.
2.  Filter for the `Vector Search API` service.
3.  Use the **Dimensions (e.g. location)** column to filter by region and by Collection for data-plane quotas.

The current effective limit for every metric is shown in the Google Cloud console Quotas page next to the metric name, filtered by region and, for data-plane quotas, Collection.

## Set quota alerts

We recommend setting an alert at **80% utilisation** for the quotas your workload depends on. For more information, go to [Set up quota alerts](https://cloud.google.com/docs/quotas/set-up-quota-alerts) and [Use quota metrics in alerting policies](https://cloud.google.com/monitoring/alerts/using-quota-metrics) .

## Failures

A request that is rejected because it exceeded a quota does **not** count against the quota itself.

Requests that fail for other reasons ( `INVALID_ARGUMENT, NOT_FOUND` , and so on) **do** count against the rate quota because the service still has to evaluate them.

**`vector_schema` validation failures are counted** . They are rejected at the API layer after the rate-quota check is made.

## Exceeding quotas

When a request is throttled, the API returns:

    gRPC:   RESOURCE_EXHAUSTED (8)
    HTTP:   429 Too Many Requests

The error message includes the exact metric that was exceeded.

For example:

    Quota exceeded for quota metric 'vectorsearch.googleapis.com/search_requests'
    and limit 'SearchRequestsPerMinutePerProjectPerRegionPerCollection' of service
    'vectorsearch.googleapis.com' for consumer 'project_number:123456789012'.

When this occurs, you may [request a quota increase](https://docs.cloud.google.com/docs/quotas/view-manage#requesting_higher_quota) .

## Recommended client behavior

Clients should:

  - **Retry with exponential backoff and jitter** for transient rate-limit errors. Start at about 1 second and back off up to about 32 seconds.
  - **Not retry** errors caused by allocation quotas (for example, `"too many collections"` ). Delete a resource or [request an increase instead](https://docs.cloud.google.com/docs/quotas/view-manage#requesting_higher_quota) .
  - **Spread writes** across Collections or regions if a single Collection hot-spots its `data_object_writes` or `data_object_write_bytes` quotas.
  - **Pre-warm** . If you know a launch will exceed your current limits, request an increase at least a few business days in advance.

### Quota increase request (QIR)

To request a quota increase:

1.  Open the [IAM & Admin \> Quotas page](https://console.cloud.google.com/iam-admin/quotas) in the Google Cloud console.
2.  Select the row(s) you want to increase.
3.  Click **Edit Quotas** , enter the new value and a brief business justification, and submit. Include:
      - The **metric name** (for example, `vectorsearch.googleapis.com/search_requests` ).
      - The **region** and (for data-plane) **Collection ID** .
      - Your **target throughput** and a short description of the workload (steady versus spiky, expected peak QPS, expected dataset size, and so on).

The request is routed to the Agent Retrieval team for review. Most increases up to 2x the default are approved automatically. Larger increases may require additional review.

## See Also

  - [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections)
  - [Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects)
  - [Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes)
  - [Cloud Quotas documentation](https://cloud.google.com/docs/quotas)
  - [Set up quota alerts and monitoring](https://cloud.google.com/docs/quotas/set-up-quota-alerts)
  - [Chart and monitor quota metrics](https://cloud.google.com/monitoring/alerts/using-quota-metrics)
