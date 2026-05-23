---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek
title: Customer-managed encryption keys
description: Use customer-managed encryption keys (CMEK) with Agent Platform Workbench instances
data_source: docs.cloud.google.com
---

# Customer-managed encryption keys (CMEK)

By default, Gemini Enterprise Agent Platform Workbench encrypts customer content at rest. Agent Platform Workbench handles encryption for you without any additional actions on your part. This option is called *Google default encryption* .

If you want to control your encryption keys, then you can use customer-managed encryption keys (CMEKs) in [Cloud KMS](https://docs.cloud.google.com/kms/docs) with CMEK-integrated services including Agent Platform Workbench. Using Cloud KMS keys gives you control over their protection level, location, rotation schedule, usage and access permissions, and cryptographic boundaries. Using Cloud KMS also lets you [track key usage](https://docs.cloud.google.com/kms/docs/view-key-usage) , view audit logs, and control key lifecycles. Instead of Google owning and managing the symmetric [key encryption keys (KEKs)](https://docs.cloud.google.com/kms/docs/envelope-encryption#key_encryption_keys) that protect your data, you control and manage these keys in Cloud KMS.

After you set up your resources with CMEKs, the experience of accessing your Agent Platform Workbench resources is similar to using Google default encryption. For more information about your encryption options, see [Customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/kms/docs/cmek) .

This page describes some specific benefits and limitations of using CMEK with Gemini Enterprise Agent Platform Workbench and shows how to configure a new Agent Platform Workbench instance to use CMEK.

For more information about how to use CMEK for Gemini Enterprise Agent Platform, see the [Agent Platform CMEK page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/general/cmek) .

## Benefits of CMEK

In general, CMEK is most useful if you need full control over the keys used to encrypt your data. With CMEK, you can manage your keys within Cloud Key Management Service. For example, you can rotate or disable a key or you can set up a rotation schedule by using the Cloud KMS API.

When you run a Agent Platform Workbench instance, your instance runs on a virtual machine (VM) managed by Gemini Enterprise Agent Platform Workbench. When you enable CMEK for a Agent Platform Workbench instance, Agent Platform Workbench uses the key that you designate, rather than a key managed by Google, to encrypt data on the boot disks of the VM.

The CMEK key *doesn't* encrypt metadata, like the instance's name and region, associated with your Agent Platform Workbench instance. Metadata associated with Agent Platform Workbench instances is always encrypted using Google's default encryption mechanism.

## Limitations of CMEK

To decrease latency and to prevent cases where resources depend on services that are spread across multiple failure domains, Google recommends that you protect regional Agent Platform Workbench instances with keys in the same location.

  - You can encrypt regional Agent Platform Workbench instances by using keys in the same location or in the global location. For example, you can encrypt data in a disk in zone `us-west1-a` by using a key in `us-west1` or `global` .
  - You can encrypt global instances by using keys in any location.
  - <span id="other-products"></span> Configuring CMEK for Agent Platform Workbench *doesn't* automatically configure CMEK for other Google Cloud products that you use. To use CMEK to encrypt data in other Google Cloud products, you must complete additional configuration.

## Configure CMEK for your Agent Platform Workbench instance

The following sections describe how to create a key ring and key in Cloud Key Management Service, grant the service account encrypter and decrypter permissions for your key, and create a Agent Platform Workbench instance that uses CMEK.

### Before you begin

We recommend using a setup that supports a [*separation of duties*](https://docs.cloud.google.com/kms/docs/separation-of-duties) . To configure CMEK for Agent Platform Workbench, you can use two separate Google Cloud projects:

  - A Cloud KMS project: a project for managing your encryption key
  - A Agent Platform Workbench project: a project for accessing Agent Platform Workbench instances and interacting with any other Google Cloud products that you need for your use case

Alternatively, you can use a single Google Cloud project. To do so, use the same project for all of the following tasks.

#### Set up the Cloud KMS project

#### Set up the Agent Platform Workbench project

#### Set up the Google Cloud CLI

The gcloud CLI is required for some steps on this page and optional for others.

[Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI. After installation, [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the Google Cloud CLI by running the following command:

    gcloud init

If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

> **Note:** You can run the gcloud CLI in the Google Cloud console without installing the Google Cloud CLI. To run the gcloud CLI in the Google Cloud console, [use Cloud Shell](https://console.cloud.google.com/?cloudshell=true) .

### Create a key ring and key

When you create a key ring and key, keep the following requirements in mind:

  - When you choose your key ring's location, use either `global` or the location where your Agent Platform Workbench instance will be.

  - Make sure to create your key ring and key in your Cloud KMS project.

To create a key ring and a key, see [Create symmetric encryption keys](https://docs.cloud.google.com/kms/docs/creating-keys) .

### Grant Agent Platform Workbench permissions

To use CMEK for your Agent Platform Workbench instance, you must grant your Agent Platform Workbench instance permission to encrypt and decrypt data using your key. You grant this permission to your project's [service agent](https://docs.cloud.google.com/iam/docs/service-agents) and the Compute Engine service account.

To find the specific accounts for your Agent Platform Workbench project, use the Google Cloud console.

1.  In the Google Cloud console, go to the **IAM** page

2.  Select **Include Google-provided role grants** .

3.  Find the members that match the following email address formats. Make note of the email addresses, and use them in the following steps.
    
      - Your project's service agent's email address looks like the following:
        
            service-NOTEBOOKS_PROJECT_NUMBER@gcp-sa-notebooks.iam.gserviceaccount.com
    
      - The Compute Engine service account's email address looks like the following:
        
            service-NOTEBOOKS_PROJECT_NUMBER@compute-system.iam.gserviceaccount.com
    
    Replace `  NOTEBOOKS_PROJECT_NUMBER  ` with the [project number](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy#projects) for your Agent Platform Workbench project.
    
    To grant these accounts permission to encrypt and decrypt data using your key, you can use the Google Cloud console or the gcloud CLI.
    
    ### Console
    
    1.  In the Google Cloud console, go to the **Key management** page.
    
    2.  Select your Cloud KMS project.
    
    3.  Click the name of the key ring that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key) . The **Key ring details** page opens.
    
    4.  Select the checkbox for the key that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key) . If an info panel labeled with the name of your key isn't already open, click **Show info panel** .
    
    5.  In the info panel, click person\_add **Add member** . The **Add members to " KEY\_NAME "** dialog opens. In this dialog, do the following:
        
        1.  In the **New members** field, enter your project's service agent's email address:
            
                service-NOTEBOOKS_PROJECT_NUMBER@gcp-sa-notebooks.iam.gserviceaccount.com
        
        2.  In the **Select a role** list, click **Cloud KMS** and then select the **Cloud KMS CryptoKey Encrypter/Decrypter** role.
        
        3.  Click **Save** .
    
    6.  Repeat these steps for the Compute Engine service agent:
        
            service-NOTEBOOKS_PROJECT_NUMBER@compute-system.iam.gserviceaccount.com
    
    ### gcloud
    
    1.  To grant your project's service agent permission to encrypt and decrypt data using your key, run the following command:
        
            gcloud kms keys add-iam-policy-binding KEY_NAME \
              --keyring=KEY_RING_NAME \
              --location=REGION \
              --project=KMS_PROJECT_ID \
              --member=serviceAccount:service-NOTEBOOKS_PROJECT_NUMBER@gcp-sa-notebooks.iam.gserviceaccount.com \
              --role=roles/cloudkms.cryptoKeyEncrypterDecrypter
        
        Replace the following:
        
          - `  KEY_NAME  ` : the name of the key that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key)
          - `  KEY_RING_NAME  ` : the key ring that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key)
          - `  REGION  ` : the region where you created your key ring
          - `  KMS_PROJECT_ID  ` : the ID of your Cloud KMS project
          - `  NOTEBOOKS_PROJECT_NUMBER  ` : the project number of your Agent Platform Workbench project, which you noted in the preceding section as part of a service account email address.
    
    2.  To grant the Compute Engine service account permission to encrypt and decrypt data using your key, run the following command:
        
            gcloud kms keys add-iam-policy-binding KEY_NAME \
              --keyring=KEY_RING_NAME \
              --location=REGION \
              --project=KMS_PROJECT_ID \
              --member=serviceAccount:service-NOTEBOOKS_PROJECT_NUMBER@compute-system.iam.gserviceaccount.com \
              --role=roles/cloudkms.cryptoKeyEncrypterDecrypter

### Create a Agent Platform Workbench instance with CMEK

After you have granted your Agent Platform Workbench instance permission to encrypt and decrypt data using your key, you can create a Agent Platform Workbench instance that encrypts data using this key.

The following example shows how to encrypt and decrypt data using your key by using the Google Cloud console.

To create a Agent Platform Workbench instance with a customer-managed encryption key, you can use the Google Cloud console or the gcloud CLI:

### Console

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Details** section, provide the following information for your new instance:
    
      - **Name** : a name for your new instance
      - **Region** : the region that your key and key ring are in
      - **Zone** : a zone within the region that you selected

5.  In the **Disks** section, in **Encryption** , select **Customer-managed encryption key (CMEK)** .

6.  Click **Select a customer-managed key** .
    
      - If the customer-managed key that you want to use is in the list, select it.
    
      - If the customer-managed key that you want to use isn't in the list, enter the resource ID for your customer-managed key. The resource ID for your customer-managed key looks like the following:
        
            projects/NOTEBOOKS_PROJECT_NUMBER/locations/REGION/keyRings/KEY_RING_NAME/cryptoKeys/KEY_NAME
        
        Replace the following:
        
          - `  NOTEBOOKS_PROJECT_NUMBER  ` : the ID of your Agent Platform Workbench project
          - `  REGION  ` : the region where you created your key ring and where you plan to create your Agent Platform Workbench instance
          - `  KEY_RING_NAME  ` : the key ring that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key)
          - `  KEY_NAME  ` : the name of the key that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key)

7.  Complete the rest of the instance creation dialog, and then click **Create** .

### gcloud

To use the gcloud CLI to create a Agent Platform Workbench instance with a customer-managed encryption key, run the following command. This example assumes that you want to create a Agent Platform Workbench instance with an `n1-standard-1` machine type and a 100 GB standard persistent boot disk.

    gcloud notebooks instances create notebook-vm-cmek \
        --location=REGION \
        --vm-image-family=IMAGE_FAMILY \
        --vm-image-project=cloud-notebooks-managed \
        --machine-type="n1-standard-1" \
        --boot-disk-type="PD_STANDARD" \
        --boot-disk-size=100 \
        --kms-key=KEY_NAME \
        --kms-project=KMS_PROJECT_ID \
        --kms-location=REGION \
        --kms-keyring=KEY_RING_NAME \
        --disk-encryption=CMEK \
        --metadata='proxy-mode=project_editors'

Replace the following:

  - `  REGION  ` : the region where you created your key ring and where you plan to create your Agent Platform Workbench instance
  - `  IMAGE_FAMILY  ` : the image family that you want to use to create your Agent Platform Workbench instance
  - `  KEY_NAME  ` : the name of the key that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key)
  - `  KMS_PROJECT_ID  ` : the ID of your Cloud KMS project
  - `  KEY_RING_NAME  ` : the key ring that you created in [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek#creating-key-ring-and-key)

## What's next

  - Learn more about [CMEK on Google Cloud](https://docs.cloud.google.com/kms/docs/cmek) .
  - Learn [how to use CMEK with other Google Cloud products](https://docs.cloud.google.com/kms/docs/using-other-products) .
