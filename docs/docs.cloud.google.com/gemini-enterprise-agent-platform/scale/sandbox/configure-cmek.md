---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-cmek
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-cmek
title: Configure Customer-Managed Encryption Keys (CMEK) for sandboxes
description: Learn how to configure Customer-Managed Encryption Keys (CMEK) to protect data at rest in Gemini Enterprise Agent Platform sandboxes.
data_source: docs.cloud.google.com
---

Encrypt a sandbox's data at rest with a Cloud Key Management Service key that you own and control.

## Overview

By default, Google Cloud encrypts your data at rest with Google-owned and Google-managed encryption keys. [Customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/kms/docs/cmek) let you create and manage a [Cloud Key Management Service](https://docs.cloud.google.com/kms/docs) encryption key so you can audit its use, rotate it, and disable or destroy it to make the protected data unreadable.

The Gemini Enterprise Agent Platform sandbox runs your agent's code, browser, or custom container in an isolated environment. That environment writes customer content to disk and can be checkpointed to snapshots, which CMEK protects when you enable it on the sandbox's parent Gemini Enterprise Agent Platform instance.

You can only configure CMEK for Gemini Enterprise Agent Platform sandboxes when you create the Gemini Enterprise Agent Platform instance. The CMEK key secures the Gemini Enterprise Agent Platform instance and its sub-resources, including the sandbox environments, templates, and snapshots.

## What CMEK encrypts for the sandbox

Enabling CMEK on the parent Gemini Enterprise Agent Platform instance encrypts the sandbox's at-rest surfaces with your key:

  - **GKE node boot disk / root filesystem:** Files the session writes at runtime and in-memory state paged to disk (node boot-disk CMEK).
  - **Snapshot Cloud Storage bucket:** Disk and memory checkpoints of a sandbox (snapshots) (bucket default encryption).

Resource metadata (names, labels, state, connection info), and environment variables and service-account emails aren't encrypted with the CMEK key.

To encrypt [custom container images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers) , set CMEK on your own Artifact Registry repository.

## Limitations and considerations

  - Only single-region keys are supported for CMEK on Gemini Enterprise Agent Platform. Multi-region, dual-region, and global keys are not supported.
  - The key is immutable when you create the Gemini Enterprise Agent Platform instance. To use a different key, you need to create a new Gemini Enterprise Agent Platform instance. Rotating to new versions of the same key is supported and applied automatically.
  - If you disable or destroy the key version, or revoke the Encrypter/Decrypter role, sandboxes can't be provisioned or resumed, and snapshot writes fail. Restore key access to recover the sandbox resources.

## Before you begin

  - Have or create a Cloud Key Management Service [key ring and key](https://docs.cloud.google.com/kms/docs/resource-hierarchy) . As a best practice, keep keys in a separate project from your Gemini Enterprise Agent Platform workloads, managed by a different administrator.

  - Confirm you hold the roles to create and manage keys ( `roles/cloudkms.admin` ) and to create the Gemini Enterprise Agent Platform instance.

  - Create an Agent Runtime service agent, if you haven't already:
    
        # Create the service agent if needed
        gcloud beta services identity create \
            --service=aiplatform.googleapis.com \
            --project=PROJECT_ID

## Create a Cloud Key Management Service key

Create a single-region key in the same region as your Gemini Enterprise Agent Platform instance:

    # Key ring (once per region)
    gcloud kms keyrings create sandbox-keyring \
        --location=REGION
    
    # Key
    gcloud kms keys create sandbox-key \
        --location=REGION \
        --keyring=sandbox-keyring \
        --purpose=encryption

Replace the following:

  - `REGION` : The Google Cloud region of your Gemini Enterprise Agent Platform instance (for example, `us-central1` ).

## Grant the Agent Platform service agent access to your key

Grant the Agent Runtime service agent the Cloud Key Management Service CryptoKey Encrypter/Decrypter role ( `roles/cloudkms.cryptoKeyEncrypterDecrypter` ) on the key:

    # Grant Encrypter/Decrypter on the key
    gcloud kms keys add-iam-policy-binding sandbox-key \
        --location=REGION \
        --keyring=sandbox-keyring \
        --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-aiplatform-re.iam.gserviceaccount.com" \
        --role="roles/cloudkms.cryptoKeyEncrypterDecrypter"

Replace the following:

  - `PROJECT_NUMBER` : Your Google Cloud project number.

## Enable CMEK on the Agent Platform instance

Set `encryption_spec.kms_key_name` when you create the Gemini Enterprise Agent Platform instance. Every sandbox template and sandbox you create under it inherits this key.

### Python SDK

    import vertexai
    
    client = vertexai.Client(project="PROJECT_ID", location="REGION",
                            http_options={"api_version": "v1beta1"})
    agent_instance = client.agent_engines.create(
        config={
            "encryption_spec": {
                "kms_key_name":
                    "projects/PROJECT_ID/locations/REGION/keyRings/sandbox-keyring/cryptoKeys/sandbox-key"
            }
        },
    )

### REST

Using the REST API, set the same value at `reasoningEngines.encryptionSpec.kmsKeyName` on create:

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/reasoningEngines \
      -d '{
        "display_name": "cmek-protected-engine",
        "encryption_spec": {
          "kms_key_name": "projects/PROJECT_ID/locations/REGION/keyRings/sandbox-keyring/cryptoKeys/sandbox-key"
        }
      }'

## Create a sandbox and verify CMEK configuration

1.  [Create your sandbox template and sandbox](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers) under the CMEK-protected Gemini Enterprise Agent Platform instance.
2.  Confirm the Gemini Enterprise Agent Platform instance reports your key in `encryption_spec.kms_key_name` by [getting the instance details](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#get) .
3.  Optionally, check [Cloud Key Management Service audit logs](https://docs.cloud.google.com/kms/docs/audit-logging) to confirm encrypt and decrypt operations occur as sandboxes start and snapshots are written.

## What's next

  - Read [Customer-managed encryption keys for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) .
  - See [Deploy agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) for enabling CMEK on the Agent Runtime.
  - Review [CMEK integrations](https://docs.cloud.google.com/kms/docs/cmek) and [key rotation](https://docs.cloud.google.com/kms/docs/key-rotation) in Cloud Key Management Service.
  - Read the [Sandbox overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox) and [Manage snapshots](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-snapshots) .
