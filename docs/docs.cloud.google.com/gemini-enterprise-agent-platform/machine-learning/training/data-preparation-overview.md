---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview
title: Data preparation overview
description: Provides an overview of the options available when preparing your dataset.
data_source: docs.cloud.google.com
---

There are several options for developing your training data.

  - [Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview#cloud-storage-fuse)
  - [Network File System](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview#network-file-system)
  - [Managed dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview#managed-dataset)
  - [BigQuery](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview#bigquery)

What choice you make depends on numerous factors.

## Cloud Storage as a Mounted File System (Cloud Storage FUSE)

Consider using Cloud Storage as a Mounted File System (Cloud Storage FUSE) for the following reasons:

  - When training data is unstructured, such as image, text, or video: Cloud Storage is a natural fit for storing these types of large, often individual files.
  - When training data is structured in formats like TFRecord: Cloud Storage is commonly used for these ML-specific formats.
  - When you are working with very large files: Cloud Storage FUSE streams the data to your training job instead of requiring the entire file to be downloaded to the replicas. This can lead to faster data loading and job start-up times for large datasets.
  - When performing distributed training: Cloud Storage FUSE provides high throughput for large file sequential reads, which is beneficial in distributed training scenarios where multiple workers need to access data in parallel.
  - When you prefer the convenience of accessing Cloud Storage data as if it were a local file system without needing to make explicit API calls in your training code.
  - When your primary need is scalable storage and you are less concerned about the very lowest latency for random access to numerous small files.

### Specific to Ray on Agent Platform

  - You can store your data in Cloud Storage buckets, which Ray on Agent Platform can access.
  - Ray can directly read data from Cloud Storage. For example, when running [Spark on Ray](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/run-spark-on-ray) , you can read files from Cloud Storage.
  - Agent Platform uses Cloud Storage FUSE to mount Cloud Storage buckets as local file systems within your training jobs running on Ray. This lets your Ray applications access data as if it were on a local disk using standard file I/O operations.
  - For optimal performance, it's recommended that you use Cloud Storage buckets in the same region where you're running your Ray cluster.

### Learn more

  - [Use Cloud Storage FUSE](https://docs.cloud.google.com/vertex-ai/docs/training/cloud-storage-file-system)

## Network File System (NFS) share

  - When you require very high throughput and low latency access to remote files, as if they were stored locally. This can be important for certain types of data or complex file interactions during training.
  - When you need to make remote files readily available to all nodes in a compute cluster, such as a Ray cluster on Agent Platform.
  - When your application benefits from a more standard file system interface with potentially stronger POSIX compliance compared to Cloud Storage FUSE.
  - You have an existing NFS infrastructure within your Virtual Private Cloud that you want to use.
  - You need to share files or directories across multiple jobs or clusters with consistent, low-latency access, and managing permissions at the file system level is preferred.

### Specific to Ray on Agent Platform

  - You can mount NFS shares to your Ray cluster on Agent Platform, making remote files accessible as if they were local.
  - This is beneficial for high-throughput and low-latency access to shared file systems.
  - You can set up NFS mounts when creating your Ray cluster using the Agent Platform SDK for Python, specifying the server, path, and mount point. Once mounted, your Ray code can read and write to these NFS volumes using standard file operations.

### Learn more

  - [Use NFS shares](https://docs.cloud.google.com/vertex-ai/docs/training/train-nfs-share)

## Managed dataset

  - Centralized data management and governance: Managed datasets provide a central location to organize and manage your datasets within Agent Platform. This helps with tracking and governance of your data assets across different projects and experiments.
  - Data Labeling: You can create labeling tasks and manage annotation sets directly within the managed dataset.
  - Tracking Data Lineage: Managed datasets automatically track the lineage of your data to the models trained on it. This is crucial for understanding the data sources used for specific models and for ensuring reproducibility and governance.
  - Comparing Custom and AutoML Models: Managed datasets let you train both custom models and AutoML models using the same data. This facilitates a direct comparison of their performance on the same dataset, helping you choose the best approach for your problem.
  - Generating Data Statistics and Visualizations: Agent Platform can automatically generate statistics and visualizations for the data within a managed dataset. This can aid in exploratory data analysis and help you understand the characteristics of your data.
  - Automatic Data Splitting: When using managed datasets in training pipelines, Agent Platform can automatically split your data into training, validation, and test sets based on specified fractions, filters, predefined splits, or timestamps. This simplifies the data preparation process.
  - Utilizing Dataset Versions: Managed datasets enables versioning, which lets you to track changes to your data over time and revert to previous versions if needed.

### Specific to Ray on Vertex AI

  - If you use a managed dataset in a Agent Platform training pipeline that utilizes Ray for distributed training, the data from the managed dataset is made available to the training containers, which your Ray application can then access (via mounted Cloud Storage or BigQuery if the dataset is linked to those sources). The environment variables `AIP_TRAINING_DATA_URI` , `AIP_VALIDATION_DATA_URI` , and `AIP_TEST_DATA_URI` would point to the data.

### Learn more

  - [Use managed datasets](https://docs.cloud.google.com/vertex-ai/docs/training/using-managed-datasets)

## BigQuery

  - When connecting to data within Agent Platform components: Many Agent Platform tools and services directly integrate with BigQuery. You can query data in BigQuery from within JupyterLab. This lets you directly interact with your BigQuery data for exploration, visualization, and model development without needing to move it to another storage system.
  - When building training pipelines: When building training pipelines in Agent Platform, you can use data directly from BigQuery. For example, a pipeline can fetch data from BigQuery, preprocess it, and then train a model.
  - Continuous model training pipelines: For setting up continuous model training, you might trigger pipeline runs based on new data arriving in a BigQuery table. This enables automation of model retraining. You can configure an Eventarc trigger to initiate a pipeline when a new job is inserted into a specific BigQuery table.
  - Model monitoring: BigQuery can be used as a source for monitoring feature skew and drift of your deployed models. For skew detection, you can specify the BigQuery URI of your training dataset. Also, BigQuery can store the logs from online inference endpoints, which can then be used as a data source for continuous monitoring. For this, your BigQuery table should ideally have a timestamp column.
  - BigQuery ML integration: You can use BigQuery datasets when leveraging BigQuery ML for building machine learning models using SQL. Vertex AI Workbench enables interactive exploratory analysis of BigQuery data and the use of BigQuery ML within a notebook environment.
  - Data exploration and preparation: Before training, you can use BigQuery to explore and visualize your data. You can also perform data transformations using SQL queries directly in BigQuery before using the data for training.
  - Accessing public datasets: BigQuery hosts many public datasets, such as the Chicago Taxi Trips dataset, which you can readily use for experimentation and training in Vertex AI Workbench.

### Specific to Ray on Vertex AI

  - Ray on Vertex AI has capabilities to read data directly from BigQuery. You can use the Agent Platform SDK for Python within a Ray task to execute BigQuery queries and materialize the results for use in your Ray applications.
  - When reading from BigQuery, be aware of the maximum query response size, which is 10 GB.
  - You can also write data from your Ray applications back to BigQuery using the Agent Platform SDK for Python.

### Learn more

  - [Agent Platform for BigQuery users](https://docs.cloud.google.com/vertex-ai/docs/beginner/bqml)
  - [Build a pipeline for continuous model training](https://docs.cloud.google.com/vertex-ai/docs/pipelines/continuous-training-tutorial)
  - [Use Ray on Vertex AI with BigQuery](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/bigquery-integration)
