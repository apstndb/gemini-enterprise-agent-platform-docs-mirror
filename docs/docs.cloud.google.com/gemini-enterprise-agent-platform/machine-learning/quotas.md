---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas
title: Gemini Enterprise Agent Platform quotas and limits
description: Review quotas and limits that apply to Gemini Enterprise Agent Platform.
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

There are also *limits* on Gemini Enterprise Agent Platform resources. These limits are unrelated to the quota system. Limits can't be changed.

## Rate quotas

The following quotas apply to Gemini Enterprise Agent Platform requests for a given project and supported region. For example, in a single project, you can have up to 30,000 online inference requests per minute in one region and another 30,000 online inference requests per minute in another supported region.

For the quotas of Gemini models, see [Generative AI on Gemini Enterprise Agent Platform quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/quotas) . For information about the quota of OpenMaaS and 3P MaaS models, see [Gemini Enterprise Agent Platform managed models for MaaS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) . For an example of Llama 4 Maverick, see [Llama 4 Maverick 17B-128E](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama4-maverick)

| Request type                                                                                                                         | Requests per minute |
| ------------------------------------------------------------------------------------------------------------------------------------ | ------------------- |
| Resource management (CRUD) requests <sup>1</sup>                                                                                     | 600                 |
| Job or long-running operation (LRO) submission requests <sup>3</sup>                                                                 | 60                  |
| Online inference requests <sup>2</sup>                                                                                               | 30,000              |
| Online inference request throughput                                                                                                  | 1.5 GB              |
| Online explain requests                                                                                                              | 600                 |
| [Vertex AI TensorBoard](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-introduction) Time Series read requests | 60,000              |
| ML Metadata (CRUD) requests                                                                                                          | 12,000              |
| generative AI Caching (CRUD) requests                                                                                                | 200                 |
| Agent Platform Vizier (CRUD) requests                                                                                                | 6,000               |
| Vertex AI Feature Store online serving requests                                                                                      | 300,000             |
| Vertex ML Metadata requests                                                                                                          | 12,000              |
| Number of count tokens or compute tokens requests                                                                                    | 3,000               |

<span class="small"><sup>1</sup> Resource management requests include any request that isn't a job, an LRO, an online inference request, an Agent Platform Vizier request, an ML metadata request, a Vertex AI TensorBoard Timeseries Insights API read request, a Vertex AI Feature Store request, a Vertex AI Feature Store streaming request, or a Vector Search request. Resource management requests can be both global and regional.</span>

<span class="small"><sup>2</sup> This quota applies for public endpoints only.</span> <span class="small"><sup>3</sup> Job or LRO submission requests can be both global and regional.</span>  
  
Jobs or LROs include the following requests:

  - Create or delete a dataset.
  - Import or export data to or from a dataset.
  - Create an endpoint.
  - Create or delete a custom job.
  - Create or delete a data-labeling job.
  - Create or delete a hyper-parameter tuning job.
  - Create or delete a batch-inference job.
  - Create or delete a model.
  - Upload, delete, or export a model.
  - Create or delete a notebook-runtime template.
  - Assign, delete, start, or upgrade a notebook runtime.
  - Create, delete, or update a model monitor.
  - Create or delete a model monitoring job.

## AutoML model quotas

The following quotas apply to each data type and objective for a given project and region. For example, in a particular project and region, you can deploy 10 AutoML image classification models and 10 AutoML image object detection models for a total of 20 deployed models.

### Image

### Classification

| Quota                                        | Value |
| -------------------------------------------- | ----- |
| Concurrent training jobs                     | 5     |
| Concurrent training jobs with explainable AI | 2     |
| Concurrent batch inference jobs              | 5     |
| Concurrent model deployment jobs             | 5     |
| Concurrent model undeployment jobs           | 5     |
| Number of deployed models                    | 10    |

### Object detection

| Quota                           | Value |
| ------------------------------- | ----- |
| Concurrent training jobs        | 5     |
| Concurrent batch inference jobs | 5     |
| Number of deployed models       | 10    |

### Tabular

| Quota                           | Value |
| ------------------------------- | ----- |
| Concurrent training jobs        | 5     |
| Concurrent batch inference jobs | 5     |
| Number of deployed models       | 30    |

## Gemini Enterprise Agent Platform Model Registry

The maximum model size supported by Gemini Enterprise Agent Platform Model Registry is 1 TB.

## AutoML model limits

The following limits apply to each data type for a given project and region. For example, in a particular project and region, you can include a maximum of 1,000,000 images in a batch request input.

### Image

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type of limit</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Image file size</td>
<td>Maximum: 30MB</td>
</tr>
<tr class="even">
<td>Images per dataset</td>
<td>Maximum: 1,000,000</td>
</tr>
<tr class="odd">
<td>Labels per dataset</td>
<td>Minimum: 2<br />
Maximum: 5000</td>
</tr>
<tr class="even">
<td>Images per label</td>
<td>Minimum: 10<br />
Recommended: 1000</td>
</tr>
<tr class="odd">
<td>Batch input CSV file size</td>
<td>Maximum: 100MB</td>
</tr>
<tr class="even">
<td>Number of images in batch input</td>
<td>Maximum: 1,000,000</td>
</tr>
</tbody>
</table>

### Tabular

| Type of limit                                  | Value                                                       |
| ---------------------------------------------- | ----------------------------------------------------------- |
| Maximum size                                   | 100GB                                                       |
| Number of rows                                 | Between 1,000 and 100,000,000 rows                          |
| Number of columns                              | Between 2 and 1,000 columns                                 |
| Number of concurrently running dataset imports | 5 imports                                                   |
| CSV file size                                  | Maximum: 10GB per file, up to maximum total amount of 100GB |

## Custom-trained model quotas

The following quotas apply to Gemini Enterprise Agent Platform custom-trained models for a given project and region.

> **Note:** The number of CPUs or GPUs are not counted against Compute Engine quotas. They are counted separately and can't be used together.

### Training

| Quota                                | Value |
| ------------------------------------ | ----- |
| Concurrent custom training pipelines | 2,000 |

Number of N1 and E2 CPUs for training, per region

Region

Value

`us-west1`

2,200

`us-west2`

20

`us-west3`

2,200

`us-west4`

20

`us-central1`

2,200

`us-east1`

2,200

`us-east4`

20

`us-east5`

450

`us-south1`

450

`northamerica-northeast1`

2,200

`northamerica-northeast2`

20

`southamerica-east1`

20

`southamerica-west1`

20

`europe-west2`

2,200

`europe-west1`

2,200

`europe-west4`

2,200

`europe-west6`

20

`europe-west3`

2,200

`europe-north1`

20

`europe-central2`

450

`europe-west8`

20

`europe-west9`

450

`europe-southwest1`

20

`asia-south1`

2,200

`asia-south2`

20

`asia-southeast1`

2,200

`asia-southeast2`

2,200

`asia-east2`

2,200

`asia-east1`

2,200

`asia-northeast1`

2,200

`asia-northeast2`

20

`australia-southeast1`

2,200

`australia-southeast2`

20

`asia-northeast3`

2,200

`me-west1`

450

`me-central1`

450

`me-central2`

450

`europe-west12`

450

`africa-south1`

450

Number of N2 CPUs for training, per region

Region

Value

`us-west1`

20

`us-west2`

20

`us-west3`

20

`us-west4`

20

`us-central1`

450

`us-east1`

20

`us-east4`

20

`us-east5`

450

`us-south1`

20

`northamerica-northeast1`

20

`northamerica-northeast2`

20

`southamerica-east1`

20

`southamerica-west1`

20

`europe-west2`

20

`europe-west1`

20

`europe-west4`

450

`europe-west6`

20

`europe-west3`

20

`europe-north1`

20

`europe-central2`

20

`europe-west8`

20

`europe-west9`

450

`europe-southwest1`

20

`asia-south1`

20

`asia-south2`

20

`asia-southeast1`

20

`asia-southeast2`

20

`asia-east2`

20

`asia-east1`

450

`asia-northeast1`

20

`asia-northeast2`

20

`australia-southeast1`

20

`australia-southeast2`

20

`asia-northeast3`

20

`me-west1`

20

`me-central1`

450

`me-central2`

450

`europe-west12`

450

`africa-south1`

450

Number of N4 CPUs for training, per region

Region

Value

`us-west1`

20

`us-west2`

20

`us-west3`

20

`us-west4`

20

`us-central1`

450

`us-east1`

20

`us-east4`

20

`us-east5`

450

`us-south1`

20

`northamerica-northeast1`

20

`northamerica-northeast2`

20

`southamerica-east1`

20

`southamerica-west1`

450

`europe-west2`

20

`europe-west1`

20

`europe-west4`

450

`europe-west6`

20

`europe-west3`

20

`europe-north1`

450

`europe-central2`

20

`europe-west8`

450

`europe-west9`

450

`europe-southwest1`

450

`asia-south1`

20

`asia-south2`

20

`asia-southeast1`

20

`asia-southeast2`

20

`asia-east2`

20

`asia-east1`

450

`asia-northeast1`

20

`asia-northeast2`

180

`australia-southeast1`

20

`australia-southeast2`

450

`asia-northeast3`

20

`me-west1`

20

`me-central1`

450

`me-central2`

450

`europe-west12`

450

`africa-south1`

450

Number of M1 CPUs for training, per region

Region

Value

`us-west1`

0

`us-west2`

0

`us-west3`

0

`us-west4`

0

`us-central1`

0

`us-east1`

0

`us-east4`

0

`us-east5`

0

`us-south1`

0

`northamerica-northeast1`

0

`northamerica-northeast2`

0

`southamerica-east1`

0

`southamerica-west1`

0

`europe-west2`

0

`europe-west1`

0

`europe-west4`

0

`europe-west6`

0

`europe-west3`

0

`europe-north1`

0

`europe-central2`

0

`europe-west8`

0

`europe-west9`

0

`europe-southwest1`

0

`asia-south1`

0

`asia-south2`

0

`asia-southeast1`

0

`asia-southeast2`

0

`asia-east2`

0

`asia-east1`

0

`asia-northeast1`

0

`asia-northeast2`

0

`australia-southeast1`

0

`australia-southeast2`

0

`asia-northeast3`

0

`me-west1`

0

`me-central1`

0

`me-central2`

0

`europe-west12`

0

`africa-south1`

0

Number of C2 CPUs for training, per region

Region

Value

`us-west1`

20

`us-west2`

20

`us-west3`

20

`us-west4`

20

`us-central1`

450

`us-east1`

20

`us-east4`

20

`us-east5`

450

`us-south1`

20

`northamerica-northeast1`

20

`northamerica-northeast2`

20

`southamerica-east1`

20

`southamerica-west1`

20

`europe-west2`

20

`europe-west1`

20

`europe-west4`

450

`europe-west6`

20

`europe-west3`

20

`europe-north1`

20

`europe-central2`

20

`europe-west8`

20

`europe-west9`

450

`europe-southwest1`

20

`asia-south1`

20

`asia-south2`

20

`asia-southeast1`

20

`asia-southeast2`

20

`asia-east2`

20

`asia-east1`

450

`asia-northeast1`

20

`asia-northeast2`

20

`australia-southeast1`

20

`australia-southeast2`

20

`asia-northeast3`

20

`me-west1`

20

`me-central1`

20

`me-central2`

20

`europe-west12`

20

`africa-south1`

20

Number of A2 CPUs for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

Unlimited

`us-east1`

Unlimited

`us-east4`

Unlimited

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Unlimited

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Unlimited

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Unlimited

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent A3 CPUs for training, per region

Region

Value

`us-west1`

Unlimited

`us-west2`

Unlimited

`us-west3`

Unlimited

`us-west4`

Unlimited

`us-central1`

Unlimited

`us-east1`

Unlimited

`us-east4`

Unlimited

`us-east5`

Unlimited

`us-south1`

Unlimited

`northamerica-northeast1`

Unlimited

`northamerica-northeast2`

Unlimited

`southamerica-east1`

Unlimited

`southamerica-west1`

Unlimited

`europe-west2`

Unlimited

`europe-west1`

Unlimited

`europe-west4`

Unlimited

`europe-west6`

Unlimited

`europe-west3`

Unlimited

`europe-north1`

Unlimited

`europe-central2`

Unlimited

`europe-west8`

Unlimited

`europe-west9`

Unlimited

`europe-southwest1`

Unlimited

`asia-south1`

Unlimited

`asia-south2`

Unlimited

`asia-southeast1`

Unlimited

`asia-southeast2`

Unlimited

`asia-east2`

Unlimited

`asia-east1`

Unlimited

`asia-northeast1`

Unlimited

`asia-northeast2`

Unlimited

`australia-southeast1`

Unlimited

`australia-southeast2`

Unlimited

`asia-northeast3`

Unlimited

`me-west1`

Unlimited

`me-central1`

Unlimited

`me-central2`

Unlimited

`europe-west12`

Unlimited

`africa-south1`

Unlimited

Number of concurrent H200 GPUs for training, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

8

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

0

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

8

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of P4 GPUs for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

6

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

6

`us-east1`

Not available

`us-east4`

1

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

6

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

6

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

6

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

6

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of T4 GPUs for training, per region

Region

Value

`us-west1`

2

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

12

`us-east1`

2

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

6

`europe-west1`

Not available

`europe-west4`

2

`europe-west6`

Not available

`europe-west3`

0

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

6

`asia-south2`

Not available

`asia-southeast1`

1

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

6

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

1

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of L4 GPUs for training, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

0

`us-east4`

0

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

0

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

0

`asia-south2`

Not available

`asia-southeast1`

0

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

0

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

0

`europe-west12`

Not available

`africa-south1`

Not available

Number of RTX PRO 6000 GPUs for training, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

0

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

0

`asia-southeast1`

0

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of P100 GPUs for training, per region

Region

Value

`us-west1`

30

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

56

`us-east1`

30

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

30

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

30

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

6

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of V100 GPUs for training, per region

Region

Value

`us-west1`

6

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

6

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

6

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

6

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of A100 GPUs for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

8

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

8

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

8

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent A100 80GB GPUs for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

0

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

0

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

For more information, see [View and manage quotas](https://docs.cloud.google.com/docs/quotas/view-manage#managing_your_quota_console) .

Number of concurrent H100 GPUs for training, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

0

`us-east5`

0

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

0

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

0

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent B200 GPUs for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

0

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

0

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

0

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent GB200 GPUs for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent H100 Mega GPUs for training, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

0

`us-central1`

0

`us-east1`

Not available

`us-east4`

0

`us-east5`

0

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

0

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

0

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

0

`asia-northeast2`

Not available

`australia-southeast1`

0

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

For more information, see [View and manage quotas](https://docs.cloud.google.com/docs/quotas/view-manage#managing_your_quota_console) .

Number of TPU V2 cores for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

0

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of TPU V2 pod cores for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

Not available

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of TPU V3 cores for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

0

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of TPU V3 pod cores for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

Not available

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of TPU7x chips for training, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

HDD usage (GB) during training, per region

Region

Value

`us-west1`

180,000

`us-west2`

3,600

`us-west3`

180,000

`us-west4`

3,600

`us-central1`

180,000

`us-east1`

180,000

`us-east4`

3,600

`us-east5`

3,600

`us-south1`

180,000

`northamerica-northeast1`

180,000

`northamerica-northeast2`

3,600

`southamerica-east1`

3,600

`southamerica-west1`

3,600

`europe-west2`

180,000

`europe-west1`

180,000

`europe-west4`

180,000

`europe-west6`

3,600

`europe-west3`

180,000

`europe-north1`

3,600

`europe-central2`

180,000

`europe-west8`

3,600

`europe-west9`

180,000

`europe-southwest1`

3,600

`asia-south1`

180,000

`asia-south2`

3,600

`asia-southeast1`

180,000

`asia-southeast2`

180,000

`asia-east2`

180,000

`asia-east1`

180,000

`asia-northeast1`

180,000

`asia-northeast2`

3,600

`australia-southeast1`

180,000

`australia-southeast2`

3,600

`asia-northeast3`

180,000

`me-west1`

180,000

`me-central1`

3,600

`me-central2`

3,600

`europe-west12`

3,600

`africa-south1`

3,600

SSD usage (GB) during training, per region

Region

Value

`us-west1`

75,000

`us-west2`

450

`us-west3`

75,000

`us-west4`

450

`us-central1`

75,000

`us-east1`

75,000

`us-east4`

450

`us-east5`

450

`us-south1`

75,000

`northamerica-northeast1`

75,000

`northamerica-northeast2`

450

`southamerica-east1`

450

`southamerica-west1`

450

`europe-west2`

75,000

`europe-west1`

75,000

`europe-west4`

75,000

`europe-west6`

450

`europe-west3`

75,000

`europe-north1`

450

`europe-central2`

75,000

`europe-west8`

450

`europe-west9`

75,000

`europe-southwest1`

450

`asia-south1`

75,000

`asia-south2`

450

`asia-southeast1`

75,000

`asia-southeast2`

75,000

`asia-east2`

75,000

`asia-east1`

75,000

`asia-northeast1`

75,000

`asia-northeast2`

450

`australia-southeast1`

75,000

`australia-southeast2`

450

`asia-northeast3`

75,000

`me-west1`

75,000

`me-central1`

450

`me-central2`

450

`europe-west12`

450

`africa-south1`

450

Hyperdisk Balanced usage (GB) during training, per region

Region

Value

`us-west1`

75,000

`us-west2`

450

`us-west3`

450

`us-west4`

450

`us-central1`

75,000

`us-east1`

450

`us-east4`

75,000

`us-east5`

450

`us-south1`

75,000

`northamerica-northeast1`

450

`northamerica-northeast2`

450

`southamerica-east1`

450

`southamerica-west1`

450

`europe-west2`

450

`europe-west1`

75,000

`europe-west4`

75,000

`europe-west6`

450

`europe-west3`

450

`europe-north1`

450

`europe-central2`

450

`europe-west8`

450

`europe-west9`

450

`europe-southwest1`

450

`asia-south1`

75,000

`asia-south2`

450

`asia-southeast1`

450

`asia-southeast2`

450

`asia-east2`

450

`asia-east1`

450

`asia-northeast1`

450

`asia-northeast2`

450

`australia-southeast1`

450

`australia-southeast2`

450

`asia-northeast3`

450

`me-west1`

450

`me-central1`

450

`me-central2`

450

`europe-west12`

450

`africa-south1`

450

### Serving

| Quota                                    | Value |
| ---------------------------------------- | ----- |
| Number of deployed custom model replicas | 100   |

Number of CPUs for serving, per region

Region

Value

`us-west1`

2,200

`us-west2`

2,200

`us-west3`

2,200

`us-west4`

16

`us-central1`

2,200

`us-east1`

2,200

`us-east4`

2,200

`us-east5`

16

`us-south1`

450

`northamerica-northeast1`

2,200

`northamerica-northeast2`

450

`southamerica-east1`

2,200

`southamerica-west1`

450

`europe-west2`

2,200

`europe-west1`

2,200

`europe-west4`

2,200

`europe-west6`

2,200

`europe-west3`

2,200

`europe-north1`

16

`europe-central2`

450

`europe-west8`

16

`europe-west9`

16

`europe-southwest1`

16

`asia-south1`

2,200

`asia-south2`

16

`asia-southeast1`

2,200

`asia-southeast2`

2,200

`asia-east2`

2,200

`asia-east1`

2,200

`asia-northeast1`

2,200

`asia-northeast2`

16

`australia-southeast1`

2,200

`australia-southeast2`

16

`asia-northeast3`

2,200

`me-west1`

450

`me-central1`

16

`me-central2`

16

`europe-west12`

16

`africa-south1`

16

Number of concurrent H200 GPUs for serving, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

0

`us-east5`

Not available

`us-south1`

8

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

0

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

8

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of P100 GPUs for serving, per region

Region

Value

`us-west1`

30

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

56

`us-east1`

30

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

30

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

30

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of P4 GPUs for serving, per region

Region

Value

`us-west1`

Not available

`us-west2`

6

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

6

`us-east1`

Not available

`us-east4`

6

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

6

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

6

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

6

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

6

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of T4 GPUs for serving, per region

Region

Value

`us-west1`

12

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

12

`us-east1`

12

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

12

`europe-west1`

Not available

`europe-west4`

12

`europe-west6`

Not available

`europe-west3`

0

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

6

`asia-south2`

Not available

`asia-southeast1`

6

`asia-southeast2`

Not available

`asia-east2`

12

`asia-east1`

6

`asia-northeast1`

6

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

6

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of L4 GPUs for serving, per region

Region

Value

`us-west1`

28

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

28

`us-east1`

28

`us-east4`

28

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

28

`europe-west1`

28

`europe-west4`

28

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

28

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

28

`asia-northeast1`

28

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of V100 GPUs for serving, per region

Region

Value

`us-west1`

6

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

6

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

6

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of A100 GPUs for serving, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

14

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

14

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

14

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

14

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

14

`me-west1`

1

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of A100 80GB GPUs for serving, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

1

`us-east1`

Not available

`us-east4`

1

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

1

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

1

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent B200 GPUs for serving, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of concurrent GB200 GPUs for serving, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

0

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

Not available

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of H100 GPUs for serving, per region

Region

Value

`us-west1`

8

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

16

`us-east1`

Not available

`us-east4`

0

`us-east5`

16

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

16

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

16

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of H100 Mega GPUs for serving, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

0

`us-central1`

0

`us-east1`

Not available

`us-east4`

0

`us-east5`

0

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

0

`europe-west4`

0

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

0

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

0

`asia-northeast2`

Not available

`australia-southeast1`

0

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of RTX Pro 6000 GPUs for serving, per region

Region

Value

`us-west1`

0

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

8

`us-east1`

8

`us-east4`

0

`us-east5`

Not available

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

0

`europe-west4`

8

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

0

`asia-southeast1`

0

`asia-southeast2`

8

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of v5e TPU Chips for serving, per region

Region

Value

`us-west1`

4

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

0

`us-central1`

32

`us-east1`

Not available

`us-east4`

Not available

`us-east5`

Not available

`us-south1`

32

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

32

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

32

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

Not available

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

Number of v6e TPU Chips for serving, per region

Region

Value

`us-west1`

Not available

`us-west2`

Not available

`us-west3`

Not available

`us-west4`

Not available

`us-central1`

Not available

`us-east1`

0

`us-east4`

Not available

`us-east5`

0

`us-south1`

Not available

`northamerica-northeast1`

Not available

`northamerica-northeast2`

Not available

`southamerica-east1`

Not available

`southamerica-west1`

Not available

`europe-west2`

Not available

`europe-west1`

Not available

`europe-west4`

8

`europe-west6`

Not available

`europe-west3`

Not available

`europe-north1`

Not available

`europe-central2`

Not available

`europe-west8`

Not available

`europe-west9`

Not available

`europe-southwest1`

Not available

`asia-south1`

Not available

`asia-south2`

Not available

`asia-southeast1`

Not available

`asia-southeast2`

Not available

`asia-east2`

Not available

`asia-east1`

Not available

`asia-northeast1`

0

`asia-northeast2`

Not available

`australia-southeast1`

Not available

`australia-southeast2`

Not available

`asia-northeast3`

Not available

`me-west1`

Not available

`me-central1`

Not available

`me-central2`

Not available

`europe-west12`

Not available

`africa-south1`

Not available

## Custom-trained model limits

The following limits apply to Gemini Enterprise Agent Platform custom-trained models for a given project and region.

### Serving

| Limit                            | Value  |
| -------------------------------- | ------ |
| Number of replicas per project   | 200    |
| Number of containers per cluster | 25,000 |

## Vertex AI Feature Store

This section lists the quotas and limits for the following:

  - [Vertex AI Feature Store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#feature_store)

  - [Vertex AI Feature Store (Legacy)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#featurestore_legacy)

### Vertex AI Feature Store

The following quotas apply to a given project and region. For example, in a single project, you can have 200 online serving nodes in `us-central1` and another 50 nodes in `us-east4` .

| Quota                                                                                                     | Value     |
| --------------------------------------------------------------------------------------------------------- | --------- |
| Online serving requests per minute                                                                        | 300,000   |
| Maximum number of `FeatureOnlineStore` instances                                                          | 10        |
| Maximum number of search requests per minute                                                              | 6,000,000 |
| Maximum number of online serving nodes across all Optimized `FeatureOnlineStore` instances in the project | 80        |
| Maximum number of `FeatureView` instances across all `FeatureOnlineStore` instances                       | 30        |

Vertex AI Feature Store also has the following limits. You can't request an increase to any of the limits in the following table:

| Limit                                                                                                                                                   | Value           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| Maximum number of `FeatureGroup` resources in a project and location                                                                                    | 250             |
| Maximum number of `Feature` resources within a `FeatureGroup`                                                                                           | 10,000          |
| Maximum size of feature data per entity                                                                                                                 | 5 MB            |
| Number of entity IDs per online serving request ( `FetchFeatureValues` )                                                                                | 1               |
| Maximum length of an entity ID                                                                                                                          | 4076 characters |
| Storage limit for an Optimized online serving ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ) node | 200 GB          |

### Vertex AI Feature Store (Legacy)

The following quotas apply to a given project and region. For example, in a single project, you can have 75 concurrent batch jobs in `us-central1` and another 75 jobs in `europe-west4` .

| Quota                                                                          | Value   |
| ------------------------------------------------------------------------------ | ------- |
| Online serving requests per minute                                             | 300,000 |
| Streaming ingestion requests per minute                                        | 60,000  |
| Streaming ingestion write throughput per minute                                | 1.2 GB  |
| Feature creation requests per minute                                           | 100     |
| Online serving nodes across all featurestores                                  | 30      |
| Concurrent batch jobs (ingestion, serving, and delete feature values combined) | 75      |
| Concurrent requests to delete feature values                                   | 1       |
| Entity types across all featurestores                                          | 75      |

Vertex AI Feature Store (Legacy) also has the following limits. You can't request an increase to any of the limits in the following table:

| Limit                                                                                                    | Value                         |
| -------------------------------------------------------------------------------------------------------- | ----------------------------- |
| Storage limit for an online serving node                                                                 | 5 TB                          |
| Total data in the offline store                                                                          | Unlimited                     |
| Features per entity type                                                                                 | 5,000                         |
| Number of create, update, and delete featurestore requests per day per project per region                | 500                           |
| For streaming ingestion, the size per request                                                            | 1 MB                          |
| For streaming read, the number of entities that can be included per request                              | 100                           |
| For batch import, the number of files that can be included per request                                   | 5,000 for Avro or 500 for CSV |
| For batch serving and exports, the number of features you can request                                    | 5,000                         |
| For batch ingestion and streaming ingestion, the oldest timestamp for which feature data can be ingested | 4,000 days from current date  |

The data retention limit in Vertex AI Feature Store (Legacy) has the following default value, which you can override:

| Data retention defaults                                                                             | Default value                    |
| --------------------------------------------------------------------------------------------------- | -------------------------------- |
| Data retention in offline store (oldest feature value timestamp after which the values are deleted) | 4,000 days from the current date |
| Data retention in online store (oldest feature value timestamp after which the values are deleted)  | 4,000 days from the current date |

You can override the data retention limit in the following ways:

  - To override the data retention limit for the online store, set the `online_storage_ttl_days` parameter while creating or updating a featurestore.

  - To override the data retention limit for the offline store, set the `offline_storage_ttl_days` parameter while creating or updating an entity type.

> **Note:** Vertex AI Feature Store (Legacy) uses column-partitioned tables from BigQuery. Your project can make up to 30,000 partition modifications per day for a column-partitioned table in BigQuery. If you exceed this limit, Gemini Enterprise Agent Platform returns an error. For more information about this error, see [Number of partition modifications for column-partitioned tables quota errors](https://docs.cloud.google.com/bigquery/docs/troubleshoot-quotas#ts-number-column-partition-quota) .  
> [Learn more about limits for BigQuery partitioned tables.](https://docs.cloud.google.com/bigquery/quotas#partitioned_tables)

## Vector Search

The following quotas apply to Vector Search for a given project in each region.

| Quota                                         | Value   |
| --------------------------------------------- | ------- |
| Concurrent index creation operations          | 5       |
| Concurrent index update operations            | 5       |
| Number of deployed index nodes                | 50      |
| Number of deployed index N2D nodes            | 5       |
| Number of Index                               | 100     |
| Streaming Update requests per minute          | 6,000   |
| Streaming Update throughput(in KB) per minute | 120,000 |

## Vertex ML Metadata

The following limits apply to Vertex ML Metadata for a given project in each region.

| Limit                                                           | Value         |
| --------------------------------------------------------------- | ------------- |
| Maximum serialized size of the metadata field within a resource | 204,800 bytes |
| Maximum serialized size of metadata schemas                     | 204,800 bytes |

## Gemini Enterprise Agent Platform Pipelines

The following quotas and limits apply to Gemini Enterprise Agent Platform Pipelines for a given project in each region.

| Quota                                            | Value |
| ------------------------------------------------ | ----- |
| Running pipeline tasks in parallel <sup>\*</sup> | 600   |
| Concurrent pipeline runs <sup>\*</sup>           | 300   |

<sup>\*</sup> Pipeline run and task requests beyond this limit are queued until resources are available.

Agent Platform Pipelines have the following limits. Note that, unlike quotas, you can't request an increase to a limit.

| Limit                                                                                     | Value         |
| ----------------------------------------------------------------------------------------- | ------------- |
| Number of pipeline tasks per job                                                          | 10,000        |
| Input and output artifacts per pipeline task                                              | 100           |
| Input and output artifacts per pipeline job                                               | 10,000        |
| Maximum size of JSON payload containing output parameters and artifacts per pipeline task | 131,072 bytes |
| Maximum running time for a pipeline task <sup>\*\*</sup>                                  | 7 days        |

<sup>\*</sup> Pipeline tasks running beyond this limit are cancelled.

## Colab Enterprise quotas and limits

Colab Enterprise quotas and limits are listed separately. See [Colab Enterprise quotas and limits](https://docs.cloud.google.com/colab/docs/quotas) .

## Quota increases

If you want to increase any of your quotas for Gemini Enterprise Agent Platform, you can use the Google Cloud console to request a quota increase.

> **Note:** refer to [Available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#available-regions) and [Region considerations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#region_considerations) and only apply for quota increase in the supported locations.

For more information about submitting a quota increase request, see the following sections of [View and manage quotas](https://docs.cloud.google.com/docs/quotas/view-manage) :

  - [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase)

## Quotas by region and model

### View and edit the quotas in the Google Cloud console

> **Caution:** Before you begin, make sure that you have [enabled the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment) for your project. If the API isn't enabled, the Agent Platform quotas won't display.

To view and edit the quotas in the Google Cloud console, do the following:

1.  Go to the **Quotas and System Limits** page.
2.  To adjust the quota, copy and paste the property `aiplatform.googleapis.com/generate_content_requests_per_minute_per_project_per_base_model` in the **Filter** . Press **Enter** .
3.  Click the three dots at the end of the row, and select **Edit quota** .
4.  Enter a new quota value in the pane, and click **Submit request** .

### View the requests per minute (RPM) quotas by region and by model

By default, Gemini models 2.0 and later use [Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo) .

The following table lists the requests per minute for each model. Quotas are the same for all regions unless otherwise specified.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Base model</th>
<th>Requests per minute</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>base_model : gemini-2.0-flash-001</td>
<td>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a> .</td>
</tr>
<tr class="even">
<td>base_model : gemini-2.0-flash-lite-001</td>
<td>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a> .</td>
</tr>
<tr class="odd">
<td>base_model : imagegeneration</td>
<td>100</td>
</tr>
<tr class="even">
<td>base_model : imagetext</td>
<td>500</td>
</tr>
<tr class="odd">
<td>base_model : multimodalembedding</td>
<td>120</td>
</tr>
<tr class="even">
<td>base_model : textembedding-gecko</td>
<td>1500</td>
</tr>
<tr class="odd">
<td>base_model : gemini-embedding</td>
<td>100000</td>
</tr>
<tr class="even">
<td>base_model : videotext</td>
<td>Iowa (us-central1): 120<br />
All other regions: Not available</td>
</tr>
</tbody>
</table>

### Increase the quotas

If you want to increase any of your quotas for Agent Platform, you can use the Google Cloud console to request a quota increase.

## RAG Engine quotas

> **Preview**
> 
> Some of the RAG features are Preview offerings, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as-is" and may have limited support, and changes to Pre-GA products and features may not be compatible with other Pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) . By using the Gemini API on Gemini Enterprise Agent Platform, you agree to the Generative AI Preview [terms and conditions](https://cloud.google.com/trustedtester/aitos) (Preview Terms).

For each service to perform retrieval-augmented generation (RAG) using RAG Engine, the following quotas apply, with the quota measured as requests per minute (RPM).

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Service</th>
<th style="text-align: right;">Quota</th>
<th>Metric</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>RAG Engine data management APIs</td>
<td style="text-align: right;">60 RPM</td>
<td><code dir="ltr" translate="no">VertexRagDataService requests per minute per region</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">RetrievalContexts</code> API</td>
<td style="text-align: right;">600 RPM</td>
<td><code dir="ltr" translate="no">VertexRagService retrieve requests per minute per region</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">base_model: textembedding-gecko</code></td>
<td style="text-align: right;">1,500 RPM</td>
<td><code dir="ltr" translate="no">Online prediction requests per base model per minute per region per base_model</code><br />
<br />
An additional filter for you to specify is <code dir="ltr" translate="no">base_model: textembedding-gecko</code><br />
</td>
</tr>
</tbody>
</table>

The following limits apply:

| Service                                              |  Limit | Metric                                                   |
| ---------------------------------------------------- | -----: | -------------------------------------------------------- |
| Concurrent `ImportRagFiles` requests                 |  3 RPM | `VertexRagService concurrent import requests per region` |
| Maximum number of files per `ImportRagFiles` request | 10,000 | `VertexRagService import rag files requests per region`  |

For more rate limits and quotas, see [Generative AI on Gemini Enterprise Agent Platform rate limits](https://docs.cloud.google.com/vertex-ai/docs/quotas) .

| Service                     |  Quota | Metric                                                            |
| --------------------------- | -----: | ----------------------------------------------------------------- |
| `AsyncRetrieveContexts` API | 60 RPM | `VertexRagService async retrieval requests per minute per region` |
| `AskContexts` API           | 60 RPM | `VertexRagService ask contexts requests per minute per region`    |

## Batch requests

The quotas and limits for batch inference jobs are the same across all regions.  

### Concurrent batch inference job limits for Gemini models

There are no predefined quota limits on batch inference for Gemini models. Instead, the batch service provides access to a large, shared pool of resources, dynamically allocated based on the model's real-time availability and demand across all customers for that model. When more customers are active and saturated the model's capacity, your batch requests might be queued for capacity.  

### Concurrent batch inference job quotas non-Gemini models

The following table lists the quotas for the number of concurrent batch inference jobs, which don't apply to Gemini models:

| **Quota**                                                                        | **Value** |
| -------------------------------------------------------------------------------- | --------- |
| `aiplatform.googleapis.com/textembedding_gecko_concurrent_batch_prediction_jobs` | 4         |

If the number of tasks submitted exceeds the allocated quota, the tasks are placed in a queue and processed when the quota capacity becomes available.

## Custom-trained model quotas

The following quotas apply to Generative AI on Gemini Enterprise Agent Platform tuned models for a given project and region:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Quota</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Restricted image training TPU V3 pod cores per region<br />
* <em>supported Region - europe-west4</em></td>
<td>64</td>
</tr>
<tr class="even">
<td>Restricted image training Nvidia A100 80GB GPUs per region<br />
* <em>supported Region - us-central1</em><br />
* <em>supported Region - us-east4</em></td>
<td><br />
8<br />
2</td>
</tr>
</tbody>
</table>

<span class="small">\* Tuning scenarios have accelerator reservations in specific regions. Quotas for tuning are supported and must be requested in specific regions.</span>

## Embedding limits

Requests for `gemini-embedding-001` are subject to regional quotas, while requests for `gemini-embedding-2` are subject to global quotas.

| Base model                      | Quota      | Metric                                                                                  |
| ------------------------------- | ---------- | --------------------------------------------------------------------------------------- |
| base\_model: gemini-embedding   | 5,000,000  | `aiplatform.googleapis.com/embed_content_input_tokens_per_minute_per_base_model`        |
| base\_model: gemini-embedding-2 | 10,000,000 | `aiplatform.googleapis.com/global_embed_content_input_tokens_per_minute_per_base_model` |
| base\_model: gemini-embedding-2 | 40,000     | `aiplatform.googleapis.com/global_embed_content_requests_per_minute_per_base_model`     |

Requests for `gemini-embedding-001` using the `predict` API are also subject to the following quotas:

| Base model                    | Quota   | Metric                                                                |
| ----------------------------- | ------- | --------------------------------------------------------------------- |
| base\_model: gemini-embedding | 100,000 | `aiplatform.googleapis.com/online_prediction_requests_per_base_model` |
| base\_model: N/A              | 30,000  | `aiplatform.googleapis.com/online_prediction_requests`                |

## Gen AI evaluation service service quotas

The Gen AI evaluation service uses Gemini 2.5 Flash as a default judge model for model-based metrics. A single evaluation request for a model-based metric might result in multiple underlying requests to the Gen AI evaluation service. Each model's consumption is calculated at the organization level, which means that any requests directed to judge model for model inference and model-based evaluation contribute to the model's consumption. Quotas for the Gen AI evaluation service and the underlying judge model are shown in the following table:

| **Request quota**                             | **Default quota**                                                                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Gen AI evaluation service requests per minute | 1,000 requests per project per region                                                                                           |
| Gemini throughput                             | Depends on model and [consumption option](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo) |
| Concurrent evaluation runs                    | 20 concurrent evaluation runs per project per region                                                                            |

If you receive an error related to quotas while using the Gen AI evaluation service, you might need to file a quota increase request. See [View and manage quotas](https://docs.cloud.google.com/docs/quotas/view-manage) for more information.

| **Limit**                                 | **Value**  |
| ----------------------------------------- | ---------- |
| Gen AI evaluation service request timeout | 60 seconds |

When you use the Gen AI evaluation service for the first time in a new project, you might experience an initial setup delay up to two minutes. If your first request fails, wait a few minutes and then retry. Subsequent evaluation requests typically complete within 60 seconds.

The maximum input and output tokens for model-based metrics depend on the model used as the judge model. See [Google models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models) for a list of models.

## Pipeline evaluation quotas

If you receive an error related to quotas while using the [evaluation pipelines service](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/side-by-side-eval) , you might need to file a quota increase request. See [View and manage quotas](https://docs.cloud.google.com/docs/quotas/view-manage) for more information. The evaluation pipelines service uses Gemini Enterprise Agent Platform Pipelines to run `PipelineJobs` . See [relevant quotas for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#vertex-pipelines) . The following are general quota recommendations:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Service</strong></th>
<th><strong>Quota</strong></th>
<th><strong>Recommendation</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Agent Platform API</td>
<td>Concurrent LLM batch prediction jobs per region</td>
<td>Pointwise: 1 * num_concurrent_pipelines<br />
<br />
Pairwise: 2 * num_concurrent_pipelines</td>
</tr>
<tr class="even">
<td>Agent Platform API</td>
<td>Evaluation requests per minute per region</td>
<td>1000 * num_concurrent_pipelines</td>
</tr>
</tbody>
</table>

Additionally, the relevant quota for model-based metrics depends on which judge model you use:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Tasks</strong></th>
<th><strong>Quota</strong></th>
<th><strong>Base model</strong></th>
<th><strong>Recommendation</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">summarization</code><br />
<code dir="ltr" translate="no">question_answering</code></td>
<td>Online prediction requests per base model per minute per region per base_model</td>
<td><code dir="ltr" translate="no">text-bison</code></td>
<td>60 * num_concurrent_pipelines</td>
</tr>
</tbody>
</table>

## Gemini Enterprise Agent Platform Agent Engine quotas

The following quotas apply to [Vertex AI Agent Engine](https://docs.cloud.google.com/vertex-ai/docs/agent-engine/overview) for a given project in each region:

| Description                                                                          | Quota | Metric                                                                         |
| ------------------------------------------------------------------------------------ | ----- | ------------------------------------------------------------------------------ |
| Create, delete, or update Vertex AI Agent Engine resources per minute                | 10    | `aiplatform.googleapis.com/reasoning_engine_service_write_requests`            |
| Create, delete, or update Vertex AI Agent Engine sessions per minute                 | 100   | `aiplatform.googleapis.com/session_write_requests`                             |
| Get, list, or retrieve Vertex AI Agent Engine sessions per minute                    | 10000 | `aiplatform.googleapis.com/session_read_requests`                              |
| `Query` or `StreamQuery` Vertex AI Agent Engine per minute                           | 90    | `aiplatform.googleapis.com/reasoning_engine_service_query_requests`            |
| Append event to Vertex AI Agent Engine sessions per minute                           | 300   | `aiplatform.googleapis.com/session_event_append_requests`                      |
| Maximum number of Vertex AI Agent Engine resources                                   | 100   | `aiplatform.googleapis.com/reasoning_engine_service_entities`                  |
| Create, delete, or update Vertex AI Agent Engine memory resources per minute         | 100   | `aiplatform.googleapis.com/memory_bank_write_requests`                         |
| Get, list, or retrieve from Vertex AI Agent Engine Memory Bank per minute            | 300   | `aiplatform.googleapis.com/memory_bank_read_requests`                          |
| Sandbox environment (Code Execution) execute requests per minute                     | 1000  | `aiplatform.googleapis.com/sandbox_environment_execute_requests`               |
| Sandbox environment (Code Execution) entities per region                             | 1000  | `aiplatform.googleapis.com/sandbox_environment_entities`                       |
| Sandbox environment (Code Execution) write requests per minute                       | 500   | `aiplatform.googleapis.com/sandbox_environment_write_requests`                 |
| A2A Agent post requests like `sendMessage` and `cancelTask` per minute               | 60    | `aiplatform.googleapis.com/a2a_agent_post_requests`                            |
| A2A Agent get requests like `getTask` and `getCard` per minute                       | 600   | `aiplatform.googleapis.com/a2a_agent_get_requests`                             |
| Concurrent live bidirectional connections using the `BidiStreamQuery` API per minute | 10    | `aiplatform.googleapis.com/reasoning_engine_service_concurrent_query_requests` |

## Troubleshoot error code 429

To troubleshoot the 429 error, see [Error code 429](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/error-code-429) .

## What's next

  - Learn more about [Agent Platform quotas and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/quotas) .
