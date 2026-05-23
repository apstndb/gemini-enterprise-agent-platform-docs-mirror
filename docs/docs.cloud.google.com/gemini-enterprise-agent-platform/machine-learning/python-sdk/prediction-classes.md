---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/prediction-classes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/prediction-classes
title: Prediction classes
description: Learn about each inference class in the Vertex AI SDK.
data_source: docs.cloud.google.com
---

The Vertex AI SDK includes the following prediction classes. One class is for batch predictions. The others are related to online predictions or Vector Search predictions. For more information, see [Overview of getting predictions on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/predictions/overview) .

## Batch prediction class

A batch prediction is a group of asynchronous prediction requests. You request batch predictions from the model resource without needing to deploy the model to an endpoint. Batch predictions are suitable for when you don't need an immediate response and want to process data with a single request. [`BatchPredictionJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob) is the one class in the Vertex AI SDK that is specific to batch predictions.

### [`BatchPredictionJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob)

The [`BatchPredictionJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob) class represents a group of asynchronous prediction requests. There are two ways to create a batch prediction job:

1.  The preferred way to create a batch prediction job is to use the [`batch_predict`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_batch_predict) method on your trained [`Model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model) . This method requires the following parameters:
    
      - `instances_format` : The format of the batch prediction request file: `jsonl` , `csv` , `bigquery` , `tf-record` , `tf-record-gzip` , or `file-list` .
      - `prediction_format` : The format of the batch prediction response file: `jsonl` , `csv` , `bigquery` , `tf-record` , `tf-record-gzip` , or `file-list` .
      - `gcs_source:` A list of one or more Cloud Storage paths to your batch prediction requests.
      - `gcs_destination_prefix` : The Cloud Storage path to which Gemini Enterprise Agent Platform writes the predictions.
    
    The following code is an example of how you might call [`Model.batch_predict`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_batch_predict) :
    
        batch_prediction_job = model.batch_predict(
            instances_format="jsonl",
            predictions_format="jsonl",
            job_display_name="your_job_display_name_string",
            gcs_source=['gs://path/to/my/dataset.csv'],
            gcs_destination_prefix='gs://path/to/my/destination',
            model_parameters=None,
            starting_replica_count=1,
            max_replica_count=5,
            machine_type="n1-standard-4",
            sync=True
        )

2.  The second way to create a batch prediction job is to call the [`BatchPredictionJob.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob#google_cloud_aiplatform_BatchPredictionJob_create) method. The [`BatchPredictionJob.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob#google_cloud_aiplatform_BatchPredictionJob_create) method requires four parameters:
    
      - `job_display_name` : A name you that you assign to the batch prediction job. Note that while `job_display_name` is required for [`BatchPredictionJob.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob#google_cloud_aiplatform_BatchPredictionJob_create) , it is optional for [`Model.batch_predict`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_batch_predict) .
      - `model_name` : The fully-qualified name or ID of the trained [`Model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model) you use for the batch prediction job.
      - `instances_format` : The format of the batch prediction request file: `jsonl` , `csv` , `bigquery` , `tf-record` , `tf-record-gzip` , or `file-list` .
      - `predictions_format` : The format of the batch prediction response file: `jsonl` , `csv` , `bigquery` , `tf-record` , `tf-record-gzip` , or `file-list` .

## Online prediction classes

Online predictions are synchronous requests made to a model endpoint. You must deploy your model to an endpoint before you can make an online prediction request. Use online predictions when you want predictions that are generated based on application input or when you need a fast prediction response.

### [`Endpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint)

Before you can get online predictions from your model, you must deploy your model to an endpoint. When you deploy a model to an endpoint, you associate the physical machine resources with the model so it can serve online predictions.

You can deploy more than one model to one endpoint. You can also deploy one model to more than one endpoint. For more information, see [Considerations for deploying models](https://docs.cloud.google.com/vertex-ai/docs/general/deployment) .

To create an [`Endpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint) resource, you deploy your model. When you call the [`Model.deploy`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelModel#google_cloud_aiplatform_Model_deploy) method, it creates and returns an [`Endpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint) .

The following is a sample code snippet that shows how to create a custom training job, create and train a model, and then deploy the model to an endpoint.

    # Create your custom training job
    
    job = aiplatform.CustomTrainingJob(
        display_name="my_custom_training_job",
        script_path="task.py",
        container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8:latest",
        requirements=["google-cloud-bigquery>=2.20.0", "db-dtypes"],
        model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-8:latest"
    )
    
    # Start the training and create your model
    model = job.run(
        dataset=dataset,
        model_display_name="my_model_name",
        bigquery_destination=f"bq://{project_id}"
    )
    
    # Create an endpoint and deploy your model to that endpoint
    endpoint = model.deploy(deployed_model_display_name="my_deployed_model")
    
    # Get predictions using test data in a DataFrame named 'df_my_test_data'
    predictions = endpoint.predict(instances=df_my_test_data)

### [`PrivateEndpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint)

A private endpoint is like an [`Endpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint) resource, except predictions are sent across a secure network to the Gemini Enterprise Agent Platform online prediction service. Use a private endpoint if your organization wants to keep all traffic private.

To use a private endpoint, you must configure Gemini Enterprise Agent Platform to peer with a Virtual Private Cloud (VPC). A VPC is required for the private prediction endpoint to connect directly with Gemini Enterprise Agent Platform. For more information, see [Set up VPC network peering](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-peering) and [Use private endpoints for online prediction](https://docs.cloud.google.com/vertex-ai/docs/predictions/using-private-endpoints) .

### [`ModelDeploymentMonitoringJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelDeploymentMonitoringJob)

Use the [`ModelDeploymentMonitoringJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelDeploymentMonitoringJob) resource to monitor your model and receive alerts if it deviates in a way that might impact the quality of your model's predictions.

When the input data deviates from the data used to train your model, the model's performance can deteriorate, even if the model hasn't changed. Model monitoring analyzes input date for feature *skew* and *drift* :

  - *Skew* occurs when the production feature data distribution deviates from the feature data used to train the model.
  - *Drift* occurs when the production feature data changes significantly over time.

For more information, see [Introduction to Gemini Enterprise Agent Platform model monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) . For an example of how to implement Gemini Enterprise Agent Platform monitoring with the Vertex AI SDK, see the [Gemini Enterprise Agent Platform model monitoring with explainable AI feature attributions](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) notebook on GitHub.

## Vector Search prediction classes

Vector Search is a managed service that builds similarity indexes, or vectors, to perform similarity matching. There are two high-level steps to perform similarity matching:

1.  Create a vector representation of your data. Data can be text, images, video, audio, or tabular data.

2.  Vector Search uses the endpoints of the vectors you create to perform a high scale, low latency search for similar vectors.

For more information, see [Vector Search overview](https://docs.cloud.google.com/vertex-ai/docs/vector-search/overview) and the [Create a Vector Search index](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_for_indexing.ipynb) notebook on GitHub.

### [`MatchingEngineIndex`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndex)

The [`MatchingEngineIndex`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndex) class represents the indexes, or vectors, you create that Vector Search uses to perform its similarity search.

There are two search algorithms you can use for your index:

1.  `TreeAhConfig` uses a shallow the tree-AH algorithm (shallow tree using asymmetric hashing). Use [`MatchingEngineIndex.create_tree_ah_index`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndex#google_cloud_aiplatform_MatchingEngineIndex_create_tree_ah_index) to create an index that uses the tree-AH algorithm algorithm.
2.  `BruteForceConfig` uses a standard linear search) Use [`MatchingEngineIndex.create_brute_force_index`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndex#google_cloud_aiplatform_MatchingEngineIndex_create_brute_force_index) to create an index that uses a standard linear search.

For more information about how you can configure your indexes, see [Configure indices](https://docs.cloud.google.com/vertex-ai/docs/vector-search/configuring-indexes) .

The following code is an example of creating an index that uses the tree-AH algorithm:

    my_tree_ah_index = aiplatform.Index.create_tree_ah_index(
        display_name="my_display_name",
        contents_delta_uri="gs://my_bucket/embeddings",
        dimensions=1,
        approximate_neighbors_count=150,
        distance_measure_type="SQUARED_L2_DISTANCE",
        leaf_node_embedding_count=100,
        leaf_nodes_to_search_percent=50,
        description="my description",
        labels={ "label_name": "label_value" }
    )

The following code is an example of creating an index that uses the brute force algorithm:

    my_brute_force_index = aiplatform.Index.create_brute_force_index(
        display_name="my_display_name",
        contents_delta_uri="gs://my_bucket/embeddings",
        dimensions=1,
        approximate_neighbors_count=150,
        distance_measure_type="SQUARED_L2_DISTANCE",
        description="my description",
        labels={ "label_name": "label_value" }
    )

### [`MatchingEngineIndexEndpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndexEndpoint)

Use the [`MatchingEngineIndexEndpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndexEndpoint) class to create and retrieve an endpoint. After you deploy a model to your endpoint, you get an IP address that you use to run your queries.

The following code is an example of creating a matching engine index endpoint and then deploying a matching engine index to it:

    my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint.create(
        display_name="sample_index_endpoint",
        description="index endpoint description",
        network="projects/123456789123/global/networks/my_vpc"
    )
    
    my_index_endpoint = my_index_endpoint.deploy_index(
        index=my_tree_ah_index, deployed_index_id="my_matching_engine_index_id"
    )

## What's next

  - Learn about the [Vertex AI SDK](https://docs.cloud.google.com/vertex-ai/docs/python-sdk/use-vertex-ai-python-sdk) .
