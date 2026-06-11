---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/cloud-storage-file-system
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/cloud-storage-file-system
title: Use Cloud Storage as a mounted file system
description: Use Cloud Storage FUSE to load training data to a Cloud Storage bucket and access that data from your Gemini Enterprise Agent Platform serverless training job like a mounted file system.
data_source: docs.cloud.google.com
---

[Cloud Storage FUSE](https://docs.cloud.google.com/storage/docs/gcs-fuse) lets you load training data to a Cloud Storage bucket and access that data from your Gemini Enterprise Agent Platform serverless training job like a mounted file system. Using Cloud Storage FUSE has the following benefits:

  - Training data is streamed to your training job instead of downloaded to replicas, which can make data loading and setup tasks faster when the job starts running.
  - Training jobs can handle input and output at scale without making API calls, handling responses, or integrating with client-side libraries.
  - Cloud Storage FUSE provides high throughput for large file sequential reads and in distributed training scenarios.

## Use cases

We recommend using Cloud Storage for storing training data in the following situations:

  - Your training data is unstructured data, such as image, text, and video.
  - Your training data is structured data in a format such as TFRecord.
  - Your training data contains large files, such as raw video.
  - You use distributed training.

## How it works

Serverless training jobs can access your Cloud Storage buckets as subdirectories of the root `/gcs` directory. For example, if your training data is located at `gs://example-bucket/data.csv` , you can read and write to the bucket from your Python training application as follows:

**Read to the bucket**

    with open('/gcs/example-bucket/data.csv', 'r') as f:
      lines = f.readlines()

**Write to the bucket**

    with open('/gcs/example-bucket/epoch3.log', 'a') as f:
      f.write('success!\n')

## Bucket access permissions

By default, a serverless training job can access any Cloud Storage bucket within the same Google Cloud project by using the [Gemini Enterprise Agent Platform Custom Code Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) . To control access to buckets, you can assign a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) to the job. In this case, access to a Cloud Storage bucket is granted based on the permissions associated with the Cloud Storage roles of the custom service account.

For example, if you want to give the serverless training job read and write access to Bucket-A but only read access to Bucket-B, you can assign a custom service account that has the following roles to the job:

  - `roles/storage.objectAdmin` for Bucket-A
  - `roles/storage.objectViewer` for Bucket-B

If the training job attempts to write to Bucket-B, a "permission denied" error is returned.

For more information on Cloud Storage roles, see [IAM roles for Cloud Storage](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) .

## Best practices

  - Avoid renaming directories. A renaming operation is not atomic in Cloud Storage FUSE. If the operation is interrupted, some files remain in the old directory.
  - Avoid unnecessarily closing ( `close()` ) or flushing files ( `flush()` ). Closing or flushing files pushes the file to Cloud Storage, which incurs a cost.

### Performance optimization guidelines

To get optimal read throughput when using Cloud Storage as a file system, we recommend implementing the following guidelines:

  - To reduce the latency introduced by looking up and opening objects in a bucket, store data in larger and fewer files.
  - Use [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) to maximize bandwidth utilization.
  - Cache frequently accessed files to improve read performance. For details, see [Overview of caching in Cloud Storage FUSE](https://docs.cloud.google.com/storage/docs/gcsfuse-cache) .
  - Use local storage for checkpointing and logs instead of Cloud Storage.

## Limitations

To learn about the limitations of Cloud Storage FUSE, including the differences between Cloud Storage FUSE and POSIX file systems, see [Limitations and differences from POSIX file systems](https://docs.cloud.google.com/storage/docs/gcs-fuse#differences-and-limitations) .

## Use Cloud Storage FUSE

To use Cloud Storage FUSE for serverless training, do the following:

1.  [Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) . Note that dual-region and multi-region buckets are not supported for serverless training.

2.  Upload your training data to the bucket. For details, see [About object uploads](https://docs.cloud.google.com/storage/docs/uploads) .
    
    To learn about other options for transferring data to Cloud Storage, see [Data transfer options](https://docs.cloud.google.com/storage-transfer/docs/transfer-options) .

3.  [Install Cloud Storage FUSE](https://docs.cloud.google.com/storage/docs/gcsfuse-install) .

4.  [Use the Cloud Storage file system](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/cloud-storage-file-system) .

## What's next

  - [See Cloud Storage FUSE documentation](https://docs.cloud.google.com/storage/docs/gcs-fuse) .
  - [Learn about Cloud Storage FUSE pricing](https://docs.cloud.google.com/storage/docs/gcs-fuse#charges) .
  - [Prepare your training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) for use on Gemini Enterprise Agent Platform.
