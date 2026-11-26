---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/get-started
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/get-started
title: Get started with training clusters
description: Set up a project to use Gemini Enterprise Agent Platform training clusters.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters contact your sales representative for access.

Before you can deploy your first cluster on Gemini Enterprise Agent Platform training clusters, you must configure your Google Cloud project and environment. This guide covers all the necessary prerequisites, which fall into three main categories:

- Project Access: Gaining access to the service, which is by invitation only.

- Resource Configuration: Enabling APIs and setting up the required VPC network and storage services.

- User Permissions: Granting the necessary IAM roles for cluster management and resource access.

Completing these steps prepares your project for a successful deployment.

## Prerequisites

To use training clusters, you must:

1.  **Allowlist your project** by contacting your sales representative for access.
2.  **Obtain capacity** for [GPU clusters](https://docs.cloud.google.com/ai-hypercomputer/docs/process-overview#choose-a-consumption-option-and-obtain-capacity) in supported regions.
3.  **Enable the necessary APIs** , including the Compute Engine, Filestore, Cloud Storage, Managed Lustre (optional), [Hypercomputer Configuration Service](https://docs.cloud.google.com/ai-hypercomputer/docs) , and Agent Platform APIs.
4.  **Configure networking** by ensuring an existing network meets specific conditions (for example, Google Private Access, firewall rules) or by creating a new VPC network and subnetwork.
5.  **Configure storage** by creating a zonal or regional Filestore instance to serve as the `/home` directory and optionally configuring a [Google Cloud managed Lustre instance](https://docs.cloud.google.com/managed-lustre/docs/overview) .
6.  **Grant IAM permissions** to users for cluster management, storage access and SSH access to cluster nodes, as described in the [IAM permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/get-started#iam-permissions) section.

### Supported regions

Accelerator availability varies by region and zone. To check which accelerators are available in each location, see [Using accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

> **Note:** Issuing a request to any regions that aren't on this list causes an API error.

- `us-central1`
- `us-east1`
- `us-east4`
- `us-east5`
- `us-south1`
- `us-west1`
- `us-west4`
- `asia-southeast1`
- `europe-west1`
- `europe-west4`
- `europe-north1`
- `asia-south2`
- `me-central1`

### IAM permissions

1.  Grant the `roles/aiplatform.admin` role to users who will manage your training clusters.

2.  Grant the `roles/aiplatform.viewer` role to users who only need to view clusters and their configurations.

3.  Grant the following IAM roles to the user or service account that manages (creates, deletes, and updates) clusters:

    | Role Name                   | Role ID                                 |
    |-----------------------------|-----------------------------------------|
    | Compute Instance Admin (v1) | `roles/compute.instanceAdmin.v1`        |
    | Logs Writer                 | `roles/logging.logWriter`               |
    | Monitoring Metric Writer    | `roles/monitoring.metricWriter`         |
    | Service Account User        | `roles/iam.serviceAccountUser`          |
    | Service Networking Admin    | `roles/servicenetworking.networksAdmin` |

4.  For SSH access to the Slurm login nodes, grant the following permissions:

    | Permissions                                                                                           | Descriptions                                                                                                         | Purpose                        |
    |-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|--------------------------------|
    | [Compute OS Login](https://docs.cloud.google.com/compute/docs/oslogin/set-up-oslogin#configure_users) | Sign in to a VM as a standard (non-administrator) user. If `sudo` is needed then use Compute OS Admin Login instead. | SSH to the deployed login node |
    | [IAP-secured Tunnel User](https://docs.cloud.google.com/iap/docs/managing-access)                     | Access Tunnel resources which use Identity-Aware Proxy.                                                              | SSH to the deployed login node |

#### Required roles for cluster service accounts

If you leave `runtime_spec.service_account` unset when creating a cluster, Gemini Enterprise Agent Platform training clusters attaches the [Compute Engine default service account](https://docs.cloud.google.com/compute/docs/access/service-accounts#default_service_account) to the cluster nodes. That account might hold project-wide roles such as `roles/editor` , which lets any user or job running on the cluster modify other project resources.

Follow the principle of least privilege by creating and attaching a dedicated [user-managed service account](https://docs.cloud.google.com/iam/docs/service-account-types#user-managed) in the same project as the cluster with only the minimum required roles. If cluster nodes fail to initialize with a custom service account on a previously onboarded project, contact your account team to update your project's service account allowlist. Grant the following IAM roles to the service account attached to your cluster nodes:

| Role Name                | Role ID                         | Purpose                                                                                                                                                                      |
|--------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Logs Writer              | `roles/logging.logWriter`       | Required. Writes cluster and workload logs.                                                                                                                                  |
| Monitoring Metric Writer | `roles/monitoring.metricWriter` | Required. Writes cluster and node metrics.                                                                                                                                   |
| Storage Object User      | `roles/storage.objectUser`      | Optional. Grant on the specific Cloud Storage buckets the cluster uses rather than on the project. Lets nodes read from and write to those buckets using Cloud Storage FUSE. |
| Artifact Registry Reader | `roles/artifactregistry.reader` | Optional. Grant on the specific Artifact Registry repositories the cluster pulls from rather than on the project. Lets nodes pull container images from those repositories.  |

Grant the Service Account User role ( `roles/iam.serviceAccountUser` ) on the cluster's service account to users who create or update clusters, or connect to login nodes.

You can't change `runtime_spec.service_account` after cluster creation. To move an existing cluster off an over-privileged service account, create a new cluster with a dedicated user-managed service account in the same project and delete the existing cluster.

If you can't recreate the cluster, you can reduce the roles granted to its attached service account in place:

1.  Grant the minimum required roles from the preceding table to the cluster's attached service account.
2.  Review [IAM role recommendations](https://docs.cloud.google.com/policy-intelligence/docs/role-recommendations-overview) and audit other workloads in the project that use the same service account to ensure they don't rely on broader permissions.
3.  Revoke overly broad roles such as `roles/editor` from the service account.

> **Caution:** If the existing cluster uses the Compute Engine default service account, other Compute Engine VMs and services in the project might share that service account. Revoking overly broad roles such as `roles/editor` from the default service account affects all workloads using it.

### Enable APIs

1.  Enable the Compute Engine API:

    ```
       gcloud services enable compute.googleapis.com
    ```

2.  Enable the service networking since Filestore must be deployed before creating the cluster.

    ```
       gcloud services enable servicenetworking.googleapis.com
    ```

3.  Enable the Cloud Storage API:

    ```
        gcloud services enable storage.googleapis.com
    ```

4.  Enable the Lustre API (if using Lustre):

    ```
    gcloud services enable lustre.googleapis.com
    ```

5.  Enable the HCS API:

    ```
    gcloud services enable hypercomputecluster.googleapis.com
    ```

6.  Enable the [Gemini Enterprise API](https://console.cloud.google.com/) :

    ```
    gcloud services enable aiplatform.googleapis.com
    ```

7.  Enable the [Cloud Resource Manager API](https://console.cloud.google.com/) :

    ```
    gcloud services enable cloudresourcemanager.googleapis.com
    ```

## What's next

For a detailed guide on creating a training cluster and running your AI/ML workloads, contact your sales representative.
