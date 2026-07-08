---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek
title: Customer-managed encryption keys (CMEK)
description: Use customer-managed encryption keys (CMEK) for Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

By default, Gemini Enterprise Agent Platform encrypts customer content at rest. Agent Platform handles encryption for you without any additional actions on your part. This option is called *Google default encryption* .

If you want to control your encryption keys, then you can use customer-managed encryption keys (CMEKs) in [Cloud KMS](https://docs.cloud.google.com/kms/docs) with CMEK-integrated services including Agent Platform. Using Cloud KMS keys gives you control over their protection level, location, rotation schedule, usage and access permissions, and cryptographic boundaries. Using Cloud KMS also lets you [track key usage](https://docs.cloud.google.com/kms/docs/view-key-usage) , view audit logs, and control key lifecycles. Instead of Google owning and managing the symmetric [key encryption keys (KEKs)](https://docs.cloud.google.com/kms/docs/envelope-encryption#key_encryption_keys) that protect your data, you control and manage these keys in Cloud KMS.

After you set up your resources with CMEKs, the experience of accessing your Agent Platform resources is similar to using Google default encryption. For more information about your encryption options, see [Customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/kms/docs/cmek) .

This guide describes some benefits of using CMEK for Gemini Enterprise Agent Platform resources and walks through how to configure a training job to use CMEK.

For more information about how to use CMEK for Colab Enterprise, see the [Colab Enterprise CMEK page](https://docs.cloud.google.com/colab/docs/cmek) . For more information about how to use CMEK for Gemini Enterprise Agent Platform Workbench instances, see the [Agent Platform Workbench instances CMEK page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek) .

## CMEK for Gemini Enterprise Agent Platform resources

The following sections describe basic information about CMEK for Gemini Enterprise Agent Platform resources that you must understand before configuring CMEK for your jobs.

### Benefits of CMEK

In general, CMEK is most useful if you need full control over the keys used to encrypt your data. With CMEK, you can manage your keys within Cloud KMS. For example, you can rotate or disable a key or you can set up a rotation schedule using the Cloud KMS API. For more information about CMEK in general, including when and why to enable it, see the [Cloud KMS documentation](https://docs.cloud.google.com/kms/docs/cmek) .

When you run an [AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#automl) or [custom](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) **training** job, your code runs on one or more virtual machine (VM) instances managed by Gemini Enterprise Agent Platform. When you enable CMEK for Gemini Enterprise Agent Platform resources, the key that you designate, rather than a key managed by Google, is used to encrypt data on the boot disks of these VMs. The CMEK key encrypts the following kinds of data:

  - The copy of your code on the VMs.
  - Any data that gets loaded by your code.
  - Any temporary data that gets saved to the local disk by your code.
  - Automl-trained models.
  - Media files (data) uploaded into media datasets.

In general, the CMEK key does *not* encrypt metadata associated with your operation, like the job's name and region, or a dataset's display name. Metadata associated with operations is always encrypted using Google's default encryption mechanism.

For **datasets** , when a user imports data into dataset, the data items and annotations are CMEK-encrypted. The dataset display name is not CMEK-encrypted.

For **models** , the models stored in the storage system (for example, disk) are CMEK-encrypted. All the model evaluation results are CMEK-encrypted.

For **endpoints** , all model files used for the model deployment under the endpoint are CMEK-encrypted. This does not include any in-memory data.

For **batch prediction** , any temporary files (such as model files, logs, VM disks) used to execute the batch prediction job are CMEK-encrypted. Batch prediction results are stored in the user provided destination. Consequently, Agent Platform respects the default value of the destination's encryption config. Otherwise, results will also be encrypted with CMEK.

For **data labeling** , any input files (image, text, tabular), temporary discussion (for example, questions, feedback) and output (labeling result) are CMEK-encrypted. The annotation spec display names are not CMEK-encrypted.

For **agents** , CMEK encrypts all source files used for agent development. Additionally, container images and deployed instances for the agent are also CMEK-encrypted.

### External keys

You can use [Cloud External Key Manager (Cloud EKM)](https://docs.cloud.google.com/kms/docs/ekm) to create external keys, that you manage, to encrypt data within Google Cloud.

When you use a Cloud EKM key, Google has no control over the availability of your externally-managed key. If you request access to a resource encrypted with an externally-managed key, and the key is unavailable, then Gemini Enterprise Agent Platform will reject the request. There can be a delay of up to 10 minutes before you can access the resource once the key becomes available.

For more considerations when using external keys, see [Cloud External Key Manager](https://docs.cloud.google.com/kms/docs/ekm#considerations) .

### Use CMEK with other Google Cloud products

Configuring CMEK for Gemini Enterprise Agent Platform resources does *not* automatically configure CMEK for other Google Cloud products that you use together with Gemini Enterprise Agent Platform. To use CMEK to encrypt data in other Google Cloud products, additional configuration is required. For example:

  - **Cloud Storage** : When you perform custom training, Agent Platform usually loads your data from Cloud Storage. When you [use a Python training application and a prebuilt container for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) , Gemini Enterprise Agent Platform also loads your code from a Cloud Storage bucket. In addition, some training jobs export trained model artifacts (for example, a TensorFlow SaveModel directory) to a Cloud Storage bucket as part of their output.
    
    To ensure that your data in Cloud Storage is encrypted with CMEK, read the [Cloud Storage guide to using customer-managed encryption keys](https://docs.cloud.google.com/storage/docs/encryption/using-customer-managed-keys) . You can set your encryption key as the default key for the Cloud Storage bucket(s) that you use with Gemini Enterprise Agent Platform, or you can use it to encrypt specific objects.
    
    [Learn more about how Cloud Storage uses CMEK.](https://docs.cloud.google.com/storage/docs/encryption/customer-managed-keys)

  - **Artifact Registry** : When you [use a custom container for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) , you can configure Agent Platform to load your container image from Artifact Registry.
    
    To ensure that your container image is encrypted with CMEK, read the [Artifact Registry guide to CMEK](https://docs.cloud.google.com/artifact-registry/docs/cmek) .

  - **Cloud Logging** : When you run a training job, Gemini Enterprise Agent Platform training saves logs to [Logging](https://docs.cloud.google.com/logging/docs) . To encrypt these logs by using CMEK, see [Configure CMEK for Cloud Logging](https://docs.cloud.google.com/logging/docs/routing/managed-encryption) .

### Current CMEK-supported resources

The current Gemini Enterprise Agent Platform resources covered by CMEK are as follows. CMEK support for Preview features is in Preview status as well.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Resource</th>
<th>Material encrypted</th>
<th>Documentation links</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets">Dataset</a></td>
<td><ul>
<li>All user imported data (for example, text content) for <code dir="ltr" translate="no">DataItems</code> and <code dir="ltr" translate="no">Annotations</code> .</li>
<li>User created content such as <code dir="ltr" translate="no">AnnotationSpecs</code> , <code dir="ltr" translate="no">ColumnSpecs</code> .</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/create-dataset">Create a dataset for training classification and regression models</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/create-dataset">Create a dataset for training forecast models</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models">Model</a></td>
<td><ul>
<li>Uploaded model files.</li>
<li>Evaluation results of the trained model.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model">Train a classification or regression model</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model">Train a forecast model</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console">Train an AutoML Edge model using the Google Cloud console</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api">Train an AutoML Edge model using the Agent Platform API</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline">Creating training pipelines</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model">Importing models to Agent Platform</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints">Endpoint</a></td>
<td><ul>
<li>All model files used for the model deployment under the endpoint. This does <em>not</em> include any in-memory data, but the model will be auto-undeployed if the key is disabled.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console">Deploying a model using the Google Cloud console</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api">Deploying a model using the Agent Platform API</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs">CustomJob</a></td>
<td><ul>
<li>The copy of your code on the VMs used to run the operation.</li>
<li>Any data that gets loaded by your code.</li>
<li>Any temporary data that gets saved to the local disk by your code.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job">Creating custom training jobs</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline">Creating training pipelines</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs">HyperparameterTuningJob</a></td>
<td><ul>
<li>The copy of your code on the VMs used to run the operation.</li>
<li>Any data that gets loaded by your code.</li>
<li>Any temporary data that gets saved to the local disk by your code.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning">Using hyperparameter tuning</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines">TrainingPipeline</a></td>
<td><ul>
<li>The copy of your code on the VMs used to run the operation.</li>
<li>Any data that gets loaded by your code.</li>
<li>Any temporary data that gets saved to the local disk by your code.</li>
<li>AutoML-trained models.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model">Train a classification or regression model</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model">Train a forecast model</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console">Train an AutoML Edge model using the Google Cloud console</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api">Train an AutoML Edge model using the Agent Platform API</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline">Creating training pipelines</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs">BatchPredictionJob</a> (excludes AutoML image batchPrediction)</td>
<td><ul>
<li>Any temporary files (for example, model files, logs, VM disks) used in the job to proceed the batch prediction job.</li>
<li>If the written results of the BatchPrediction are stored in the user provided destination, it will respect the encryption config of its default value. Otherwise, it will also be encrypted with CMEK.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions">Get batch predictions and explanations for a classification or regression model</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/get-predictions">Get predictions for a forecast model</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs">ModelDeploymentMonitoringJob</a></td>
<td><ul>
<li>Any temporary files (for example, training dataset files, logs, VM disks) used in the job to process the model deployment monitoring job.</li>
<li>Any data used for detection monitoring anomalies.</li>
<li>If the key is disabled, the model deployment monitoring job will be paused.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Setting up model monitoring</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs">PipelineJob</a></td>
<td><ul>
<li>The pipeline job and all of its sub-resources.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline">Running a pipeline</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores">MetadataStore</a></td>
<td><ul>
<li>All content in the metadata store.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/configure">Configuring your project's metadata store</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards">TensorBoard</a></td>
<td><ul>
<li>All data from the uploaded TensorBoard logs including scalars, histograms, graph defs, images, and text.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Using Vertex AI TensorBoard</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores">Featurestore</a></td>
<td><ul>
<li>The featurestore and all content in the featurestore.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/managing-featurestores">Managing featurestores</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes">Index</a></td>
<td><ul>
<li>All data files used for Vector Search indexes stored in Cloud Storage, Pub/Sub, and internal storage. Index and IndexEndpoint must be created with the same key.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/create-manage-index">Manage indexes</a></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes">IndexEndpoint</a></td>
<td><ul>
<li>All data files used for Vector Search indexes stored in Cloud Storage, Pub/Sub, and internal storage. Index and IndexEndpoint must be created with the same key.</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/deploy-index-public">Deploy and manage public endpoints</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/deploy-index-vpc">Deploy and manage index endpoints in a VPC network</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect">Vector Search Private Service Connect</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes">Colab Enterprise runtime</a></td>
<td><ul>
<li>The boot disk and data disks of the runtime's VM</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/colab/docs/cmek">Use customer-managed encryption keys (CMEK) in Colab Enterprise</a></li>
</ul></td>
</tr>
<tr class="even">
<td>Colab Enterprise notebook</td>
<td><ul>
<li>The notebook file and its comments</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/colab/docs/cmek">Use customer-managed encryption keys (CMEK) in Colab Enterprise</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines">Agent Runtime</a></td>
<td><ul>
<li>The copy of your agent source files, including code, scripts, and any dependency files</li>
<li>The container images built from your agent source files</li>
<li>The running instances deployed from your agent container images</li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview">Agent Runtime overview</a></li>
</ul></td>
</tr>
</tbody>
</table>

### CMEK support for Generative AI tuning pipelines

CMEK support is provided in the tuning pipeline of the following models:

  - `BERT`
  - `T5`
  - `image-generation (GPU)`

### Limitations

CMEK support isn't provided in the following:

  - AutoML image model batch prediction ( `BatchPredictionJob` )
  - TPU tuning
  - Agent Platform Memory Bank or Agent Platform Sessions configured to use the global endpoint. Cloud KMS requires encryption keys to reside within a fixed geographic data residency boundary. Because the global region lacks a physical geographic boundary, it is barred from encrypting localized regional or multi-regional resources.

## Configure CMEK for your resources

The following sections describe how to create a key ring and key in Cloud Key Management Service, grant Agent Platform encrypter and decrypter permissions for your key, and create resources that use CMEK.

### Before you begin

This guide assumes that you use two separate Google Cloud projects to configure CMEK for Agent Platform data:

  - A project for managing your encryption key (referred to as the "Cloud KMS project").
  - A project for accessing Agent Platform data or output in Cloud Storage, and interacting with any other Google Cloud products that you need for your use case (referred to as the "AI Platform project").

This recommended setup supports a [*separation of duties*](https://docs.cloud.google.com/kms/docs/separation-of-duties) .

Alternatively, you can use a single Google Cloud project for the whole guide. To do so, use the same project for all of the following tasks that refer to the Cloud KMS project and the tasks that refer to the AI Platform project.

#### Set up the Cloud KMS project

#### Set up the AI Platform project

#### Set up the Google Cloud CLI

The gcloud CLI is required for some steps in this guide and optional for others.

[Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI. After installation, [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the Google Cloud CLI by running the following command:

    gcloud init

If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

> **Note:** You can run the gcloud CLI in the Google Cloud console without installing the Google Cloud CLI. To run the gcloud CLI in the Google Cloud console, [use Cloud Shell](https://console.cloud.google.com/?cloudshell=true) .

### Create a key ring and key

Follow the [Cloud KMS guide to creating symmetric keys](https://docs.cloud.google.com/kms/docs/creating-keys) to create a key ring and a key. When you create your key ring, specify [a region that supports Agent Platform operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) as [the key ring's location](https://docs.cloud.google.com/kms/docs/locations) . Agent Platform training only supports CMEK when your resource and key use the same region. You must not specify a dual-regional, multi-regional, or global location for your key ring.

Make sure to create your key ring and key in your Cloud KMS project.

### Grant Agent Platform permissions

To use CMEK for your resources, you must grant Agent Platform permission to encrypt and decrypt data using your key. Agent Platform uses a [Google-managed service agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) to run operations using your resources. This service account is identified by an email address with the following format:

    service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com

To find the appropriate service account for your AI Platform project, go to the **IAM** page in the Google Cloud console and find the member that matches this email address format, with the [project number](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy#projects) for your AI Platform project replacing the AI\_PLATFORM\_PROJECT\_NUMBER variable. The service account also has the name `Agent Platform Service Agent` .

Make note of the email address for this service account, and use it in the following steps to grant it permission to encrypt and decrypt data using your key. You can grant permission by using the Google Cloud console or by using the Google Cloud CLI:

### Google Cloud console

1.  In the Google Cloud console, **Click Security** and select **Key Management** . This will take you to **Cryptographic Keys** page and select your Cloud KMS project.

2.  Click on the name of the key ring that you created in [a preceding section of this guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#creating-key-ring-and-key) to go to the **Key ring details** page.

3.  Select the checkbox for the key that you created in [a preceding section of this guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#creating-key-ring-and-key) . If an info panel labeled with the name of your key is not already open, click **Show info panel** .

4.  In the info panel, click **person\_add Add member** to open the **Add members to " KEY\_NAME "** dialog. In this dialog, do the following:
    
    1.  In the **New members** box, enter the service account email address that you made a note of in the preceding section: `service- AI_PLATFORM_PROJECT_NUMBER @gcp-sa-aiplatform.iam.gserviceaccount.com`
    
    2.  In the **Select a role** drop-down list, click **Cloud KMS** and then select the **Cloud KMS CryptoKey Encrypter/Decrypter** role.
    
    3.  Click **Save** .

### gcloud

Run the following command:

    gcloud kms keys add-iam-policy-binding KEY_NAME \
      --keyring=KEY_RING_NAME \
      --location=REGION \
      --project=KMS_PROJECT_ID \
      --member=serviceAccount:service-AI_PLATFORM_PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com \
      --role=roles/cloudkms.cryptoKeyEncrypterDecrypter

In this command, replace the following placeholders:

  - KEY\_NAME : The name of the key that you created in [a preceding section of this guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#creating-key-ring-and-key) .
  - KEY\_RING\_NAME : The key ring that you created in [a preceding section of this guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#creating-key-ring-and-key) .
  - REGION : The region where you created your key ring.
  - KMS\_PROJECT\_ID : The ID of your Cloud KMS project.
  - AI\_PLATFORM\_PROJECT\_NUMBER : The project number of your AI Platform project, which you noted in the preceding section as part of a service account email address.

### Create resources with the KMS key

When you create a new [CMEK-supported resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#resource-list) you can specify your key as one of the create parameters.

### Console

When you create a new [CMEK-supported resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#resource-list) in the [Agent Platform section of the Google Cloud console](https://console.cloud.google.com/agent-platform/) , you can select your key in the general or advanced option section:

![Select encryption key for resource section](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/general/images/select-encryption-key.png)

### REST & CMD Line

When you create a [supported resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#resource-list) , add an [`encryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec) object to your request and set the `encryptionSpec.kmsKeyName` field to point to your key resource.

For example, when [creating a `dataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/overview) resource you would specify your key in the request body:

``` 
 {
   "displayName": DATASET_NAME,
   "metadataSchemaUri": METADATA_URI,
   "encryptionSpec": {
     "kmsKeyName": "projects/PROJECT_ID/locations/LOCATION_ID/keyRings/KEY_RING_NAME/cryptoKeys/KEY_NAME"
   }
 }
```

### Java

When you create a supported resource, set the `EncryptionSpec` to point to your key resource. See the [Agent Platform client library for Java](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/overview) documentation for more information.

### Node.js

When you create a supported resource, set the `encryptionSpec` parameter to point to your key resource. See the [Agent Platform client library for Node.js](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) documentation for more information.

### Python

When you create a supported resource, set the `encryption_spec` parameter to point to your key resource. See the [Python Client for Cloud AI Platform](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) documentation for more information.

## What's next

  - Learn more about [CMEK on Google Cloud](https://docs.cloud.google.com/kms/docs/cmek) .
  - Learn [how to use CMEK with other Google Cloud products](https://docs.cloud.google.com/kms/docs/use-keys-google-cloud) .
