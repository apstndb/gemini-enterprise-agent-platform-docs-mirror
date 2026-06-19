---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/cmek
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/cmek
title: Customer Managed Encryption Keys (CMEK) in Agent Retrieval
description: Learn how CMEK works with Agent Retrieval (formerly Vector Search 2.0)
data_source: docs.cloud.google.com
---

Agent Retrieval (formerly Vector Search 2.0) lets you protect your data at rest using cryptographic keys managed through [Google Cloud Key Management Service (KMS)](https://docs.cloud.google.com/third_party/devsite/cloud/en/kms/docs/key-management-service) . This integration provides control over the keys used to encrypt core customer content, including the ability to rotate and revoke those keys.

By default, data is encrypted using Google-managed platform defaults. CMEK provides you with direct control over the encryption keys.

> **Note:** Manual and automatic re-encryption (rewrapping core content to a new key version without downtime) is not supported.

For more information, go to the [Customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) documentation.

## Prerequisites and constraints

The following prerequisites and constraints must be met in order to use CMEK with a [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) :

  - The Cloud KMS key must reside in the same Google Cloud region as the [Collection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) it protects. For example, a Collection in the `us-central1` region must use a KMS key located in `us-central1` .

  - You must grant your Per-Product-Per-Project (P4) Service Account the `cryptoKeyEncrypterDecrypter` role on your KMS key. The P4 Service Account follows this format: `service-${CONSUMER_PROJECT_NUMBER}@gcp-sa-vectorsearch.iam.gserviceaccount.com`

> **Warning:** Previous key versions must not be deleted immediately to void encrypted data to be lost. Keep them for at least 30 days.

## Creating a CMEK-protected Collection

After you meet all pre-requistites, you can use the gcloud CLI, REST API, or Python SDK to create a new Collection with CMEK enabled.

### Using the gcloud CLI

Specify the fully qualified resource ID of your KMS key using the `--kms-key` argument:

    gcloud vector-search collections create [COLLECTION_ID] \
        --kms-key projects/[KMS_PROJECT_ID]/locations/[REGION]/keyRings/[KEY_RING]/cryptoKeys/[KEY]

### Using the REST API

Include the `encryption_spec` in the body of your `POST` request:

    {
      "encryption_spec": {
        "crypto_key_name": "projects/[PROJECT_ID]/locations/[REGION]/keyRings/[KEY_RING]/cryptoKeys/[KEY]"
      }
    }

### Using the Python SDK

Using the Python SDK:

``` 
   
request = vectorsearch_v1beta.CreateCollectionRequest(
    parent=f"projects/{PROJECT_ID}/locations/{LOCATION}",
    collection_id=collection_id,
    collection={
        "data_schema": {...},
        "vector_schema": {...},
        # Specifies the customer-managed encryption key spec for a Collection
        "encryption_spec": {
            "crypto_key_name": f"projects/{PROJECT_ID}/locations/{LOCATION}/keyRings/{KEY_RING}/cryptoKeys/{KEY}"
        }
    },
)

operation = vector_search_service_client.create_collection(request=request)
operation.result()
```

## Migrating Data Objects from a non-CMEK Collection into a CMEK-enabled Collection

CMEK cannot be enabled for existing Collections. You must instead migrate Data Objects into a new Collection with CMEK enabled.

To do so:

1.  Export your Data Objects from an existing Collection into a Cloud Storage bucket.

2.  [Create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/cmek#create) a new Collection with CMEK enabled.

3.  [Import your Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#import) into the Collection.

## Key rotation

When a key is rotated in KMS, new data is encrypted using the primary key version, while existing data remains encrypted with the previous version. For more details, see [Key rotation](https://cloud.google.com/kms/docs/key-rotation) .

## Key revocation

Revoking or disabling a key immediately disables the Collection. Associated ANN indexes are automatically undeployed and in-memory data is purged. Read, write, and search operations on the Collection will fail.

Collections aren't automatically re-enabled if the key is restored.

> **Note:** For emergency recovery, contact support. Data is recoverable if the key is restored no later than 7 days after revocation.

## CMEK-supported resources

The current Vertex AI resources covered by CMEK are as follows. CMEK support for Preview features is in Preview status as well.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Resource</th>
<th style="text-align: left;">Material encrypted</th>
<th style="text-align: left;">Documentation links</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets">Dataset</a></td>
<td style="text-align: left;">All user imported data (for example, text content) for <code dir="ltr" translate="no">DataItems</code> and <code dir="ltr" translate="no">Annotations</code> .<br />
<br />
User created content such as <code dir="ltr" translate="no">AnnotationSpecs, ColumnSpecs</code> .</td>
<td style="text-align: left;"><a href="https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/create-dataset">Create a dataset for training classification and regression models</a><br />
<br />
<a href="https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/create-dataset">Create a dataset for training forecast models</a></td>
</tr>
<tr class="even">
<td style="text-align: left;"><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes">Index</a></td>
<td style="text-align: left;">All data files used for Vector Search indexes stored in Cloud Storage, Pub/Sub, and internal storage. Index and IndexEndpoint must be created with the same key.<br />
<br />
All indexes within a Collection must be created with the same key.</td>
<td style="text-align: left;"><a href="https://docs.cloud.google.com/vertex-ai/docs/vector-search/create-manage-index">Manage indexes</a> in Vector Search :<br />
<br />
<a href="https://docs.cloud.google.com/vertex-ai/docs/vector-search-2/indexes/indexes">Manage indexes in Vector Search 2</a></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections">Collections</a></td>
<td style="text-align: left;"><em>Collections</em> are used to store related Data Objects.</td>
<td style="text-align: left;"><a href="https://docs.cloud.google.com/vertex-ai/docs/vector-search-2/collections/collections">Manage collections in Vector Search 2</a></td>
</tr>
<tr class="even">
<td style="text-align: left;"><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects">DataObjects</a></td>
<td style="text-align: left;">Collections store data as individual JSON objects called Data Objects.</td>
<td style="text-align: left;"><a href="https://docs.cloud.google.com/vertex-ai/docs/vector-search-2/data-objects/data-objects">Manage Data Objects in Vector Search 2</a></td>
</tr>
</tbody>
</table>
