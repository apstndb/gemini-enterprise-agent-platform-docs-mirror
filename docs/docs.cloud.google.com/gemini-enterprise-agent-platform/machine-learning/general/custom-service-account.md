---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account
title: Use a custom service account
description: Learn about how and when to use a custom service account.
data_source: docs.cloud.google.com
---

This guide describes how to configure Gemini Enterprise Agent Platform to use a custom service account in the following scenarios:

  - When you perform [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) , you can configure Agent Platform to use a custom service account in the training container, whether it is a [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) or a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) .

  - When you [deploy a custom-trained `Model` resource to an `Endpoint` resource](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) to serve online predictions, you can configure Agent Platform to use a custom service account in the container that serves predictions, whether it is a [prebuilt container](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) or a [custom container](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) .

  - When you [copy a `Model` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/copy) between projects, you can configure Agent Platform to use a custom service account to access the models in the source project.

## When to use a custom service account

When Agent Platform runs, it generally acts with the permissions of one of several [service accounts](https://docs.cloud.google.com/iam/docs/service-accounts) that Google creates and manages for your Google Cloud project. To grant Agent Platform increased access to other Google Cloud services in certain contexts, you can [add specific roles to Agent Platform's service agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#grant_service_agents_access_to_other_resources) .

However, customizing the permissions of service agents might not provide the fine-grained access control that you want. Some common use cases include:

  - Allowing fewer permissions to Agent Platform jobs and models. The default Agent Platform service agent has access to BigQuery and Cloud Storage.
  - Allowing different jobs access to different resources. You might want to allow many users to launch jobs in a single project, but grant each user's jobs access only to a certain BigQuery table or Cloud Storage bucket.

For example, you might want to individually customize every [custom training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) that you run to have access to different Google Cloud resources outside of your project.

Moreover, customizing the permissions of service agents does not change the permissions available to a container that serves predictions from a custom-trained `Model` .

To customize access each time you perform custom training or to customize the permissions of a custom-trained `Model` 's prediction container, you must use a custom service account.

## Default access

This section describes the default access available to custom training containers and the prediction containers of custom-trained `Model` resources. When you use a custom service account, you override this access for a specific `CustomJob` , `HyperparameterTuningJob` , `TrainingPipeline` , or `DeployedModel` resource.

### Training containers

When you create a `CustomJob` , `HyperparameterTuningJob` , or a custom `TrainingPipeline` , the [training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) runs using your Google Cloud project's Gemini Enterprise Agent Platform Custom Code Service Agent by default.

Learn more about the [Gemini Enterprise Agent Platform Custom Code Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) , including how to give it access to additional Google Cloud resources.

### Prediction containers

When you deploy a custom-trained `Model` to an `Endpoint` , the prediction container runs using a service account managed by Agent Platform. This service account is different from the [Agent Platform service agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) .

The service account that the prediction container uses by default has permission to [read model artifacts](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#artifacts) that Agent Platform makes available at a URI stored in the [`AIP_STORAGE_URI` environment variable](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) . Do not rely on the service account to have any other permissions. You can't customize the permissions of the service account.

## Configure a custom service account

The following sections describe how to set up a custom service account to use with Agent Platform and how to configure a `CustomJob` , `HyperparameterTuningJob` , `TrainingPipeline` , or `DeployedModel` to use the service account. Note that you can't configure a custom service account to pull images from Artifact Registry. Gemini Enterprise Agent Platform uses the default service account to pull images.

### Set up a custom service account

To set up a custom service account, do the following:

1.  [Create a user-managed service account.](https://docs.cloud.google.com/iam/docs/creating-managing-service-accounts#creating) The user-managed service account can be in the same project as your Agent Platform resources or in a different project.

2.  [Grant your new service account IAM roles](https://docs.cloud.google.com/iam/docs/granting-roles-to-service-accounts) that provide access to the Google Cloud services and resources that you want Agent Platform to be able to use during custom training or prediction.

3.  **Optional** : If the user-managed service account is in a different project than your training jobs, you must grant the [Service Account Token Creator role](https://docs.cloud.google.com/iam/docs/service-account-permissions#token-creator-role) (roles/iam.serviceAccountTokenCreator) to the Agent Platform Service Agent of the project where you're using Agent Platform.
    
        gcloud iam service-accounts add-iam-policy-binding \
            --role=roles/iam.serviceAccountTokenCreator \
            --member=serviceAccount:AI_PLATFORM_SERVICE_AGENT \
            CUSTOM_SERVICE_ACCOUNT

4.  **Optional** : If you also plan to use the user-managed service account for predictions, then you must grant the Service Account Admin role ( `roles/iam.serviceAccountAdmin` ) to the Agent Platform Service Agent of the project where you're using Agent Platform:
    
        gcloud iam service-accounts add-iam-policy-binding \
          --role=roles/iam.serviceAccountAdmin \
          --member=serviceAccount:AI_PLATFORM_SERVICE_AGENT \
          CUSTOM_SERVICE_ACCOUNT
    
    Replace the following:
    
      - AI\_PLATFORM\_SERVICE\_AGENT : The email address of your project's Agent Platform Service Agent, which has the following format:
        
        `service- PROJECT_NUMBER @gcp-sa-aiplatform.iam.gserviceaccount.com`
        
        To find the Agent Platform Service Agent, go to the **IAM** page in the Google Cloud console.
    
      - CUSTOM\_SERVICE\_ACCOUNT : The email address of the new user-managed service account that you created in the first step of this section.
    
    > **Note:** This command grants your project's Agent Platform Service Agent the Service Account Admin role *only* for your custom service account resource, not for the whole project. Learn more about [granting permissions at the resource level versus the project level](https://docs.cloud.google.com/iam/docs/overview#resource) .

### Specify a custom service account for Agent Platform resources

The process of configuring Agent Platform to use a specific service account for a resource is called [*attaching* the service account to the resource](https://docs.cloud.google.com/iam/docs/attach-service-accounts#attaching-to-resources) . The following sections describe how to attach the [service account that you created in the previous section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#setup) to several Agent Platform resources.

> **Note:** To attach the service account, you must have the `iam.serviceAccounts.actAs` permission for the service account. If you successfully completed the previous section of this guide, then you likely already have this permission. If you don't have the permission, ask a project administrator to give you access by granting you the [Service Account User role ( `roles/iam.serviceAccountUser` )](https://docs.cloud.google.com/iam/docs/service-account-permissions#user-role) for the custom service account.

#### Attach a service account to a custom training resource

To configure Agent Platform to use your [new service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#setup) during custom training, specify the service account's email address in the `serviceAccount` field of a [`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec) message when you start custom training. Depending on [which type of custom training resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods) you are creating, the placement of this field in your API request differs:

  - **If you are creating a `CustomJob`** , specify the service account's email address in `CustomJob.jobSpec.serviceAccount` .
    
    Learn more about [creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

  - **If you are creating a `HyperparameterTuningJob`** , specify the service account's email address in `HyperparameterTuningJob.trialJobSpec.serviceAccount` .
    
    Learn more about [creating a `HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .

  - **If you are creating a custom `TrainingPipeline` without hyperparameter tuning** , specify the service account's email address in `TrainingPipeline.trainingTaskInputs.serviceAccount` .

  - **If you are creating a custom `TrainingPipeline` with hyperparameter tuning** , specify the service account's email address in `TrainingPipeline.trainingTaskInputs.trialJobSpec.serviceAccount` .

#### Attach a service account to a container that serves online predictions

To configure a custom-trained `Model` 's prediction container to use your [new service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#setup) , specify the service account's email address when you deploy the `Model` to an `Endpoint` :

### Console

Follow [Deploying a model using the Google Cloud console](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-console) . When you specify model settings, select the service account in the **Service account** drop-down list.

### gcloud

Follow [Deploying a model using the Agent Platform API](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) . When you run the `gcloud ai endpoints deploy-model` command, use the `--service-account` flag to specify your service account's email address.

Before using any of the command data below, make the following replacements:

  - ENDPOINT\_ID : The ID for the endpoint.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute)
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.
  - CUSTOM\_SERVICE\_ACCOUNT : The service account's email address. For example: `  SA_NAME @ PROJECT_ID .iam.gserviceaccount.com ` .

Execute the [gcloud ai endpoints deploy-model](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID \
      --region=LOCATION \
      --model=MODEL_ID \
      --display-name=DEPLOYED_MODEL_NAME \
      --machine-type=MACHINE_TYPE \
      --min-replica-count=MIN_REPLICA_COUNT \
      --max-replica-count=MAX_REPLICA_COUNT \
      --traffic-split=0=100 \
      --service-account=CUSTOM_SERVICE_ACCOUNT

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID `
      --region=LOCATION `
      --model=MODEL_ID `
      --display-name=DEPLOYED_MODEL_NAME `
      --machine-type=MACHINE_TYPE `
      --min-replica-count=MIN_REPLICA_COUNT `
      --max-replica-count=MAX_REPLICA_COUNT `
      --traffic-split=0=100 `
      --service-account=CUSTOM_SERVICE_ACCOUNT

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID ^
      --region=LOCATION ^
      --model=MODEL_ID ^
      --display-name=DEPLOYED_MODEL_NAME ^
      --machine-type=MACHINE_TYPE ^
      --min-replica-count=MIN_REPLICA_COUNT ^
      --max-replica-count=MAX_REPLICA_COUNT ^
      --traffic-split=0=100 ^
      --service-account=CUSTOM_SERVICE_ACCOUNT

### API

Follow [Deploying a model using the Agent Platform API](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) . When you send the [`projects.locations.endpoints.deployModel` request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) , set the [`deployedModel.serviceAccount` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.service_account) to the service account's email address.

#### Attach a service account to a CopyModel request

To configure Agent Platform to use your [new service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#setup) when copying a model, specify the service account's email address in the `customServiceAccount` field of the [`CopyModelRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/copy) message. This service account must belong to the destination project where the model is copied to and you need to have the `iam.serviceAccounts.actAs` permission on this service account.

### REST

Follow [Copying a model using the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/copy-model#copy-model-projects) , add the `customServiceAccount` field in the request JSON body.

### API

When you send the [`projects.locations.models.copy` request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/copy) , set the `customServiceAccount` field to the service account's email address.

## Access Google Cloud services in your code

If you configure Agent Platform to use a custom service account by following the instructions in preceding sections, then your training container or your prediction container can access any Google Cloud services and resources that the service account has access to.

To access Google Cloud services, write your [training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) or your [prediction-serving code](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) to use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication#adc) and explicitly specify the project ID or project number of the resource you want to access. Learn more about [writing your code to access other Google Cloud services](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#other-services) .

## Limitations

Custom service accounts in Gemini Enterprise Agent Platform have the following limitations:

  - For batch inference, the Gemini Enterprise Agent Platform service agent will still be used to access BigQuery and Cloud Storage even when a custom service account is configured.
  - There is a maximum of 20 custom service accounts per project per region per service (for example, Vertex AI Inference).

## What's next

  - Learn more about [Access control](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) for Agent Platform.
  - Learn about specific [IAM permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/iam-permissions) and the operations they support.
