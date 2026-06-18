---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts
title: Service accounts for Tabular Workflows
description: Review information about the service accounts used by Tabular Workflows and required roles and permissions.
data_source: docs.cloud.google.com
---

This page explains the service accounts for the following Tabular Workflows:

  - [Tabular Workflow for End-to-End AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#e2e-automl)
  - [Tabular Workflow for Forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#forecasting)
  - [Tabular Workflow for Wide & Deep](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#fte-workflow)
  - [Prophet](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#fte-workflow)
  - [ARIMA+](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#arima)

## Service accounts for Tabular Workflow for End-to-End AutoML

This workflow uses the following service accounts:

| Service account                                                                                                                                                                                                        | Description                                            | Default principal                                                  | Default name                             | Can be overridden |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------ | ---------------------------------------- | ----------------- |
| [Service account for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#e2e-automl-pipelines) | The service account that runs the pipeline             | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [Service account for Dataflow worker](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#e2e-automl-dataflow)                             | The service account that runs the Dataflow workers     | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [AI Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#e2e-automl-aip)                                            | The service account that runs the training containers. | `service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com` | `AI Platform Service Agent`              | No                |

You can change some of the service accounts to an account of your choice. See [Train a model with End-to-End AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/e2e-automl-train) for instructions specific to Google Cloud console or the API.

### Service account for Gemini Enterprise Agent Platform Pipelines

Grant the following roles to the service account for Gemini Enterprise Agent Platform Pipelines in the pipeline project:

| Role                                                                                                                                                             | Permissions                                                                                                                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Gemini Enterprise Agent Platform User](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) | `aiplatform.metadataStores.get` allows the service account to create a pipeline job. `aiplatform.models.upload` allows the service account to upload the model.                                                                                                                          |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)                                                                      | The `storage.objects.get` and `storage.objects.create` permissions of Storage Object Admin allow the service account to access the bucket for the root directory of the pipeline job. The service account needs these permissions even if you are not using a Cloud Storage data source. |
| [Dataflow Developer](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.developer)                                                     | `dataflow.jobs.create` allows the service account to create Dataflow jobs during evaluation.                                                                                                                                                                                             |
| [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser)                                                      | `iam.serviceAccounts.actAs` allows the Agent Platform Pipelines service account to act as the Dataflow worker service account during evaluation.                                                                                                                                         |

### Service account for Dataflow worker

Grant the following roles to the service account for Dataflow worker in the pipeline project:

| Role                                                                                                   | Permissions                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Dataflow Worker](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.worker) | This role allows the service account to access the resources needed to run Dataflow jobs.                                                                                                                                                                                                                                            |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)            | This role allows the service account to access Cloud Storage buckets. The service account needs these permissions even if you are not using a Cloud Storage data source. This role includes all of the permissions granted by the [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role. |

Additionally, grant the following roles to the Dataflow worker service account based on your data source type:

Data source

Role

Where to grant the role

[Standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

Cloud Storage file

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the file belongs to

The following table explains these roles:

| Role                                                                                                   | Permissions                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor) | The `bigquery.jobs.get` and `bigquery.jobs.create` permissions allow the service account to use BigQuery datasets. `bigquery.jobs.create` allows the service account to create temporary BigQuery datasets during statistics and example generation. This role includes all of the permissions granted by the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) role. |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)       | `bigquery.jobs.create` allows the service account to use a BigQuery dataset.                                                                                                                                                                                                                                                                                                                                               |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | This role provides the service account with access to the BigQuery dataset.                                                                                                                                                                                                                                                                                                                                                |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)           | `storage.objects.get` allows the service account to access a Cloud Storage file.                                                                                                                                                                                                                                                                                                                                           |

### AI Platform Service Agent

Ensure that the AI Platform Service Agent in the pipeline project has the following role:

| Role                                                                                                                                                                    | Permissions                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Gemini Enterprise Agent Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) | This role grants permissions for service agents. These permissions include the `storage.object.get` permission and access rights to container images in the Artifact Registry repository. |

If your data source is a BigQuery dataset from another project, grant the following roles to the AI Platform Service Agent in the dataset project:

| Role                                                                                                   | Permissions                                                                                                                  |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | `bigquery.tables.get` allows the service account to get information on the BigQuery dataset before launching a Dataflow job. |

If your data source is a Cloud Storage file from another project, grant the following roles to the AI Platform Service Agent in the file project:

|                                                                                              |                                                                                                                                 |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) | `storage.objects.list` allows the service account to get information on the Cloud Storage file before launching a Dataflow job. |

## Service accounts for Tabular Workflow for Forecasting

This workflow uses the following service accounts:

| Service account                                                                                                                                                                                                         | Description                                            | Default principal                                                  | Default name                             | Can be overridden |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------ | ---------------------------------------- | ----------------- |
| [Service account for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#forecasting-pipelines) | The service account that runs the pipeline             | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [Service account for Dataflow worker](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#forecasting-dataflow)                             | The service account that runs the Dataflow workers     | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [AI Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#forecasting-aip)                                            | The service account that runs the training containers. | `service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com` | `AI Platform Service Agent`              | No                |

You can change some of the service accounts to an account of your choice. To learn more, see [Train a model with Tabular Workflow for Forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting-train) .

### Service account for Gemini Enterprise Agent Platform Pipelines

Grant the following roles to the service account for Gemini Enterprise Agent Platform Pipelines in the pipeline project:

| Role                                                                                                                                                             | Permissions                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Gemini Enterprise Agent Platform User](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) | `aiplatform.metadataStores.get` allows the service account to create a pipeline job. `aiplatform.models.upload` allows the service account to upload the model.                                                                                                                                                                                                                                                    |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)                                                           | `bigquery.tables.create` allows the service account to create temporary tables for Feature Transform Engine prior to launching a Dataflow job. The service account needs this permission even if your data source is not a BigQuery dataset. This role includes all of the permissions granted by the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) role. |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)                                                                 | `bigquery.jobs.create` allows the service account to run BigQuery jobs for Feature Transform Engine prior to launching a Dataflow job. The service account needs this permission even if your data source is not a BigQuery dataset.                                                                                                                                                                               |
| [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser)                                                      | `iam.serviceAccounts.actAs` allows the Agent Platform Pipelines service account to act as the Dataflow worker service account during evaluation.                                                                                                                                                                                                                                                                   |
| [Dataflow Developer](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.developer)                                                     | This role provides access to resources needed to run Dataflow jobs.                                                                                                                                                                                                                                                                                                                                                |

Additionally, grant the following roles to the Gemini Enterprise Agent Platform Pipelines service account based on your data source type:

Data source

Role

Where to grant the role

Cloud Storage file

[Storage Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the file belongs to

[Standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

The following table explains these roles:

|                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | `bigquery.tables.get` provides the service account with access to the dataset. The service account needs this access prior to launching the Dataflow job in the Feature Transform Engine step of the pipeline.                                                                                                                                                                                                                                      |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)           | `storage.objects.get` allows the service account to access the source Cloud Storage file.                                                                                                                                                                                                                                                                                                                                                           |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)            | The `storage.objects.get` and `storage.objects.create` permissions allow the service account to access the bucket for the root directory of the pipeline job. The service account needs these permissions in the pipeline project even if your data source is not a Cloud Storage file. This role includes all of the permissions granted by the [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role. |
| [Storage Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)                   | `storage.buckets.*` permissions allow the service account to validate the Cloud Storage bucket in the Feature Transform Engine step of the pipeline. This role includes all of the permissions granted by the [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role.                                                                                                                                     |

If you perform model evaluation, provide a BigQuery dataset to serve as a destination for the predicted examples. In the project that contains this dataset, grant the following roles to the Gemini Enterprise Agent Platform Pipelines service account:

| Role                                                                                                   | Permissions                                                           |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | This role lets the service account view BigQuery data.                |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)       | `bigquery.jobs.create` lets the service account create BigQuery jobs. |

### Service account for Dataflow worker

Grant the following roles to the service account for Dataflow worker in the pipeline project:

| Role                                                                                                   | Permissions                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)            | This role allows the service account to access Cloud Storage buckets. The service account needs these permissions even if your data source is not a Cloud Storage file.                                       |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)       | `bigquery.jobs.create` allows the service account to perform the Feature Transform Engine step of the pipeline. The service account needs this permission even if your data source is not a BigQuery dataset. |
| [Dataflow Worker](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.worker) | The service account needs all of the permissions granted by this role.                                                                                                                                        |

Additionally, grant the following roles to the Dataflow worker service account based on your data source type:

Data source

Role

Where to grant the role

[Standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

Cloud Storage file

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that runs the pipeline

The following table explains these roles:

| Role                                                                                                   | Permissions                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | `bigquery.tables.get` provides access to the dataset in the Feature Transform Engine step of the pipeline. The service account needs this permission even if your data source is not a BigQuery dataset.                                                                                                       |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor) | This role lets the service account query the table and create temporary tables during the Feature Transform Engine step of the pipeline. This role includes all of the permissions granted by the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) role. |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)           | `storage.objects.get` lets the service account access a Cloud Storage file.                                                                                                                                                                                                                                    |

### AI Platform Service Agent

Ensure that the AI Platform Service Agent in the pipeline project has the following role:

| Role                                                                                                                                                                    | Permissions                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Gemini Enterprise Agent Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) | This role grants permissions for service agents. These permissions include the `storage.object.get` permission and access rights to container images in the Artifact Registry repository. |

If you perform model evaluation, provide a BigQuery dataset to serve as a destination for the predicted examples. In the project that contains this dataset, grant the following roles to the Gemini Enterprise Agent Platform Pipelines service account:

| Role                                                                                                   | Permissions                                                           |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor) | This role lets the service account edit BigQuery data.                |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)       | `bigquery.jobs.create` lets the service account create BigQuery jobs. |

## Service accounts for Tabular Workflow for Wide & Deep, and Prophet

These workflows use the following service accounts:

| Service account                                                                                                                                                                                                          | Description                                            | Default principal                                                  | Default name                             | Can be overridden |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------ | ---------------------------------------- | ----------------- |
| [Service account for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#fte-workflow-pipelines) | The service account that runs the pipeline             | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [Service account for Dataflow worker](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#fte-workflow-dataflow)                             | The service account that runs the Dataflow workers     | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [AI Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#fte-workflow-aip)                                            | The service account that runs the training containers. | `service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com` | `AI Platform Service Agent`              | No                |

You can change some of the service accounts to an account of your choice. For For Tabular Workflow for Wide & Deep instructions, see [Train a model with Wide & Deep](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/wide-and-deep-train) . For Prophet instructions, see [Forecasting with Prophet](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-prophet) .

### Service account for Gemini Enterprise Agent Platform Pipelines

Grant the following roles to the service account for Gemini Enterprise Agent Platform Pipelines in the pipeline project:

| Role                                                                                                                                                             | Permissions                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Gemini Enterprise Agent Platform User](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) | `aiplatform.metadataStores.get` allows the service account to create a pipeline job. `aiplatform.models.upload` allows the service account to upload the model.                                                                                                                                                                                                                                                    |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)                                                           | `bigquery.tables.create` allows the service account to create temporary tables for Feature Transform Engine prior to launching a Dataflow job. The service account needs this permission even if your data source is not a BigQuery dataset. This role includes all of the permissions granted by the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) role. |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)                                                                 | `bigquery.jobs.create` allows the service account to run BigQuery jobs for Feature Transform Engine prior to launching a Dataflow job. The service account needs this permission even if your data source is not a BigQuery dataset.                                                                                                                                                                               |
| [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser)                                                      | `iam.serviceAccounts.actAs` allows the Agent Platform Pipelines service account to act as the Dataflow worker service account during evaluation.                                                                                                                                                                                                                                                                   |
| [Dataflow Developer](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.developer)                                                     | This role provides access to resources needed to run Dataflow jobs.                                                                                                                                                                                                                                                                                                                                                |

Additionally, grant the following roles to the Gemini Enterprise Agent Platform Pipelines service account based on your data source type:

Data source

Role

Where to grant the role

Cloud Storage file

[Storage Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the file belongs to

[Standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

The following table explains these roles:

|                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | `bigquery.tables.get` provides the service account with access to the dataset. The service account needs this access prior to launching the Dataflow job in the Feature Transform Engine step of the pipeline.                                                                                                                                                                                                                                      |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)           | `storage.objects.get` allows the service account to access the source Cloud Storage file.                                                                                                                                                                                                                                                                                                                                                           |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)            | The `storage.objects.get` and `storage.objects.create` permissions allow the service account to access the bucket for the root directory of the pipeline job. The service account needs these permissions in the pipeline project even if your data source is not a Cloud Storage file. This role includes all of the permissions granted by the [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role. |
| [Storage Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)                   | `storage.buckets.*` permissions allow the service account to validate the Cloud Storage bucket in the Feature Transform Engine step of the pipeline. This role includes all of the permissions granted by the [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role.                                                                                                                                     |

### Service account for Dataflow worker

Grant the following roles to the service account for Dataflow worker in the pipeline project:

| Role                                                                                                   | Permissions                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)            | This role allows the service account to access Cloud Storage buckets. The service account needs these permissions even if your data source is not a Cloud Storage file.                                       |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)       | `bigquery.jobs.create` allows the service account to perform the Feature Transform Engine step of the pipeline. The service account needs this permission even if your data source is not a BigQuery dataset. |
| [Dataflow Worker](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.worker) | The service account needs all of the permissions granted by this role.                                                                                                                                        |

Additionally, grant the following roles to the Dataflow worker service account based on your data source type:

Data source

Role

Where to grant the role

[Standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

Cloud Storage file

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that runs the pipeline

The following table explains these roles:

| Role                                                                                                   | Permissions                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | `bigquery.tables.get` provides access to the dataset in the Feature Transform Engine step of the pipeline. The service account needs this permission even if your data source is not a BigQuery dataset.                                                                                                       |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor) | This role lets the service account query the table and create temporary tables during the Feature Transform Engine step of the pipeline. This role includes all of the permissions granted by the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) role. |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)           | `storage.objects.get` lets the service account access a Cloud Storage file.                                                                                                                                                                                                                                    |

### AI Platform Service Agent

Ensure that the AI Platform Service Agent in the pipeline project has the following role:

| Role                                                                                                                                                                    | Permissions                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Gemini Enterprise Agent Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) | This role grants permissions for service agents. These permissions include the `storage.object.get` permission and access rights to container images in the Artifact Registry repository. |

## Service accounts for ARIMA+

This workflow uses the following service accounts:

| Service account                                                                                                                                                                                                   | Description                                            | Default principal                                                  | Default name                             | Can be overridden |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------ | ---------------------------------------- | ----------------- |
| [Service account for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#arima-pipelines) | The service account that runs the pipeline             | `PROJECT_NUMBER-compute@developer.gserviceaccount.com`             | `Compute Engine default service account` | Yes               |
| [AI Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#arima-aip)                                            | The service account that runs the training containers. | `service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com` | `AI Platform Service Agent`              | No                |

You can change the Gemini Enterprise Agent Platform Pipelines service account to an account of your choice. See [Forecasting with ARIMA+](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-arima/overview) for more information.

### Service account for Gemini Enterprise Agent Platform Pipelines

Grant the following roles to the service account for Gemini Enterprise Agent Platform Pipelines in the pipeline project:

| Role                                                                                                                                                             | Permissions                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Gemini Enterprise Agent Platform User](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) | `aiplatform.metadataStores.get` allows the service account to create a pipeline job. `aiplatform.models.upload` allows the service account to upload the model.                                                                                                                                                                                                                                                    |
| [BigQuery Data Editor](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataEditor)                                                           | `bigquery.tables.create` allows the service account to create temporary tables for Feature Transform Engine prior to launching a Dataflow job. The service account needs this permission even if your data source is not a BigQuery dataset. This role includes all of the permissions granted by the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) role. |
| [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)                                                                 | `bigquery.jobs.create` allows the service account to run BigQuery jobs for Feature Transform Engine prior to launching a Dataflow job. The service account needs this permission even if your data source is not a BigQuery dataset.                                                                                                                                                                               |
| [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser)                                                      | `iam.serviceAccounts.actAs` allows the Agent Platform Pipelines service account to act as the Dataflow worker service account during evaluation.                                                                                                                                                                                                                                                                   |
| [Dataflow Developer](https://docs.cloud.google.com/dataflow/docs/concepts/access-control#dataflow.developer)                                                     | This role provides access to resources needed to run Dataflow jobs.                                                                                                                                                                                                                                                                                                                                                |

Additionally, grant the following roles to the Gemini Enterprise Agent Platform Pipelines service account based on your data source type:

Data source

Role

Where to grant the role

Cloud Storage file

[Storage Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the file belongs to

[Standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [standard BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard_tables)

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the table belongs to

[BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

[BigQuery view](https://docs.cloud.google.com/bigquery/docs/tables-intro#views) of a [BigQuery external table](https://docs.cloud.google.com/bigquery/docs/tables-intro#external_tables) that has a source Cloud Storage file

[Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that runs the pipeline

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the view belongs to

[BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer)

Project that the external table belongs to

[Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)

Project that the source file belongs to

The following table explains these roles:

|                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) | `bigquery.tables.get` provides the service account with access to the dataset. The service account needs this access prior to launching the Dataflow job in the Feature Transform Engine step of the pipeline.                                                                                                                                                                                                                                      |
| [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)           | `storage.objects.get` allows the service account to access the source Cloud Storage file.                                                                                                                                                                                                                                                                                                                                                           |
| [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)            | The `storage.objects.get` and `storage.objects.create` permissions allow the service account to access the bucket for the root directory of the pipeline job. The service account needs these permissions in the pipeline project even if your data source is not a Cloud Storage file. This role includes all of the permissions granted by the [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role. |
| [Storage Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles)                   | `storage.buckets.*` permissions allow the service account to validate the Cloud Storage bucket in the Feature Transform Engine step of the pipeline. This role includes all of the permissions granted by the [Storage Object Admin](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) role.                                                                                                                                     |

### AI Platform Service Agent

Ensure that the AI Platform Service Agent in the pipeline project has the following role:

| Role                                                                                                                                                                    | Permissions                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Gemini Enterprise Agent Platform Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) | This role grants permissions for service agents. These permissions include the `storage.object.get` permission and access rights to container images in the Artifact Registry repository. |
