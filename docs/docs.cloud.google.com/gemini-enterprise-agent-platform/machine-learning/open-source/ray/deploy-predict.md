---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/deploy-predict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/deploy-predict
title: Deploy a model on Gemini Enterprise Agent Platform to get inferences
description: Deploy a model for online inference requests after training the model on a Ray cluster on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> To see an example of getting started with PyTorch on Ray on , run the "Get started with PyTorch on Ray on " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fget_started_with_pytorch_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fget_started_with_pytorch_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb)

After training a model on a Ray cluster on Gemini Enterprise Agent Platform, deploy the model for online inference requests using the following process:

> **Note:** To get batch inferences from the trained models, use the following process: upload the model to Model Registry and then follow the [Get batch inferences from a custom trained model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions) instructions.

  - Export the model from the [Ray checkpoint](https://docs.ray.io/en/latest/tune/tutorials/tune-trial-checkpoints.html) .

  - Upload the model to [Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .

  - Deploy the model to an endpoint.

  - Make inference requests.

Before you begin, make sure to read the [Ray on Agent Platform overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray) and [set up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/set-up) all the prerequisite tools you need.

The steps in this section assume that you use the Ray on Agent Platform SDK in an interactive Python environment.

## Gemini Enterprise Agent Platform online inference and Ray inference compared

| Feature                   | [Gemini Enterprise Agent Platform online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/deploy-predict) (Recommended) | Ray Inference (Ray Serve)                                                                           |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Scalability               | Autoscaling based on traffic (highly scalable even for LLM models)                                                                                                                | Highly scalable with distributed backends and custom resource management                            |
| Infrastructure Management | Fully managed by Google Cloud, less operational overhead                                                                                                                          | Requires more manual setup and management on your infrastructure or Kubernetes cluster              |
| API/Supported Features    | REST and gRPC APIs, online and batch inferences, explainability features, batching, caching, streaming                                                                            | REST and gRPC APIs, real-time and batch inference, model composition, batching, caching, streaming  |
| Model Format              | Supports various frameworks such as TensorFlow, PyTorch, scikit-learn, XGBoost using prebuilt containers or any custom container                                                  | Supports various frameworks such as TensorFlow, PyTorch, scikit-learn.                              |
| Ease of Use               | Easier to set up and manage, integrated with other Gemini Enterprise Agent Platform features                                                                                      | More flexible and customizable, but requires deeper knowledge of Ray                                |
| Cost                      | Cost depends on machine types, accelerators, and number of replicas                                                                                                               | Cost depends on your infrastructure choices                                                         |
| Specialized Features      | Model monitoring, A/B testing, traffic splitting, Gemini Enterprise Agent Platform Model Registry and Gemini Enterprise Agent Platform Pipelines integration                      | Advanced model composition, ensemble models, custom inference logic, integration with Ray ecosystem |

## Import and initialize Ray on Agent Platform client

If you're already connected to your Ray cluster on Gemini Enterprise Agent Platform, restart your kernel and run the following code. The `runtime_env` variable is necessary at connection time to run online inference commands.

    import ray
    import vertexai
    
    # The CLUSTER_RESOURCE_NAME is the one returned from vertex_ray.create_ray_cluster.
    address = 'vertex_ray://{}'.format(CLUSTER_RESOURCE_NAME)
    
    # Initialize Agent Platform to retrieve projects for downstream operations.
    vertexai.init(staging_bucket=BUCKET_URI)
    
    # Shutdown cluster and reconnect with required dependencies in the runtime_env.
    ray.shutdown()

Where:

  - CLUSTER\_RESOURCE\_NAME : The full resource name for the Ray on Agent Platform cluster that must be unique across your project.

  - BUCKET\_URI is the Cloud Storage bucket to store the model artifacts.

## Train and export the model to Model Registry

Export the Gemini Enterprise Agent Platform model from the Ray checkpoint and upload the model to Model Registry.

### TensorFlow

    import numpy as np
    from ray.air import session, CheckpointConfig, ScalingConfig
    from ray.air.config import RunConfig
    from ray.train import SyncConfig
    from ray.train.tensorflow import TensorflowCheckpoint, TensorflowTrainer
    from ray import train
    import tensorflow as tf
    
    from vertex_ray.predict import tensorflow
    
    # Required dependencies at runtime
    runtime_env = {
      "pip": [
          "ray==2.47.1", # pin the Ray version to prevent it from being overwritten
          "tensorflow",
          "IPython",
          "numpy",
      ],
    }
    
    # Initialize  Ray on Agent Platform client for remote cluster connection
    ray.init(address=address, runtime_env=runtime_env)
    
    # Define a TensorFlow model.
    
    def create_model():
      model = tf.keras.Sequential([tf.keras.layers.Dense(1, activation="linear", input_shape=(4,))])
      model.compile(optimizer="Adam", loss="mean_squared_error", metrics=["mse"])
      return model
    
    def train_func(config):
      n = 100
      # Create a fake dataset
      # data   : X - dim = (n, 4)
      # target : Y - dim = (n, 1)
      X = np.random.normal(0, 1, size=(n, 4))
      Y = np.random.uniform(0, 1, size=(n, 1))
    
      strategy = tf.distribute.experimental.MultiWorkerMirroredStrategy()
      with strategy.scope():
          model = create_model()
          print(model)
    
      for epoch in range(config["num_epochs"]):
          model.fit(X, Y, batch_size=20)
          tf.saved_model.save(model, "temp/my_model")
          checkpoint = TensorflowCheckpoint.from_saved_model("temp/my_model")
          train.report({}, checkpoint=checkpoint)
    
    trainer = TensorflowTrainer(
      train_func,
      train_loop_config={"num_epochs": 5},
      scaling_config=ScalingConfig(num_workers=1),
      run_config=RunConfig(
          storage_path=f'{BUCKET_URI}/ray_results/tensorflow',
          checkpoint_config=CheckpointConfig(
              num_to_keep=1  # Keep all checkpoints.
          ),
          sync_config=SyncConfig(
              sync_artifacts=True,
          ),
      ),
    )
    
    # Train the model.
    result = trainer.fit()
    
    # Register the trained model to Model Registry.
    vertex_model = tensorflow.register_tensorflow(
      result.checkpoint,
    )

### sklearn

    from vertex_ray.predict import sklearn
    from ray.train.sklearn import SklearnCheckpoint
    
    vertex_model = sklearn.register_sklearn(
      result.checkpoint,
    )

### XGBoost

    from vertex_ray.predict import xgboost
    from ray.train.xgboost import XGBoostTrainer
    
    # Initialize  Ray on Agent Platform client for remote cluster connection
    ray.init(address=address, runtime_env=runtime_env)
    
    # Define an XGBoost model.
    train_dataset = ray.data.from_pandas(
    pd.DataFrame([{"x": x, "y": x + 1} for x in range(32)]))
    
    run_config = RunConfig(
    storage_path=f'{BUCKET_URI}/ray_results/xgboost',
    checkpoint_config=CheckpointConfig(
        num_to_keep=1  # Keep all checkpoints.
    ),
    sync_config=SyncConfig(sync_artifacts=True),
    )
    
    trainer = XGBoostTrainer(
    label_column="y",
    params={"objective": "reg:squarederror"},
    scaling_config=ScalingConfig(num_workers=3),
    datasets={"train": train_dataset},
    run_config=run_config,
    )
    # Train the model.
    result = trainer.fit()
    
    # Register the trained model to Model Registry.
    vertex_model = xgboost.register_xgboost(
    result.checkpoint,
    )

### PyTorch

  - Convert the Ray checkpoints to a model.

  - Build `model.mar` .

  - Create LocalModel using `model.mar` .

  - Upload to Model Registry.

> To see an example of getting started with Ray on Vertex AI, run the "Get started with Ray on " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fget_started_with_pytorch_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fget_started_with_pytorch_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb)

## Deploy the model for online inferences

Deploy the model to the online endpoint. For more information, see [Deploy the model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

    DEPLOYED_NAME = model.display_name + "-endpoint"
    TRAFFIC_SPLIT = {"0": 100}
    MACHINE_TYPE = "n1-standard-4"
    
    endpoint = vertex_model.deploy(
        deployed_model_display_name=DEPLOYED_NAME,
        traffic_split=TRAFFIC_SPLIT,
        machine_type=MACHINE_TYPE,
    )

Where:

  - (Optional) DEPLOYED\_NAME : The display name of the deployed model. If you don't provide a name upon creation, the system uses the model's `display_name` .

  - (Optional) TRAFFIC\_SPLIT : A map from a deployed model's ID to the percentage of this endpoint's traffic that should be forwarded to that deployed model. If a deployed model's ID isn't listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or the map must be empty if the endpoint doesn't accept any traffic at the moment. The key for the model being deployed is `"0"` . For example, `{"0": 100}` .

  - (Optional) MACHINE\_TYPE : [Specify the compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#specify) .

## Make an inference request

Send an inference request to the endpoint. For more information, see [Get online inferences from a custom trained model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) .

    pred_request = [
        [ 1.7076793 , 0.23412449, 0.95170785, -0.10901471],
        [-0.81881499, 0.43874669, -0.25108584, 1.75536031]
    ]
    
    endpoint.predict(pred_request)

You should get output like the following:

    Prediction(predictions=[0.7891440987586975, 0.5843208432197571],
     deployed_model_id='3829557218101952512',
     model_version_id='1',
     model_resource_name='projects/123456789/locations/us-central1/models/123456789101112',
     explanations=None)

## What's next

  - [View logs for your Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/view-logs)

  - [Delete a Ray cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/delete-cluster)
