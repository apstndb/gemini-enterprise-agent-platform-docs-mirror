---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts
title: Export model artifacts for inference and explanation
description: Export model artifacts for inference and explanation using a prebuilt container.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform offers [prebuilt containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) to serve inferences and explanations from models trained using the following machine learning (ML) frameworks:

  - TensorFlow
  - PyTorch
  - XGBoost
  - scikit-learn

To use one of these prebuilt containers, you must save your model as one or more *model artifacts* that comply with the requirements of the prebuilt container. These requirements apply whether or not your model artifacts are created on Agent Platform.

If you use a [custom container to serve inferences](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) , you don't need to comply with the requirements in this page, but you can still use them as guidelines.

## Framework-specific requirements for exporting to prebuilt containers

Depending on [which ML framework you plan to use for inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) , you must export model artifacts in different formats. The following sections describe the acceptable model formats for each ML framework.

### TensorFlow

If you [use TensorFlow to train a model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers#tensorflow) , export your model as a [TensorFlow SavedModel directory](https://www.tensorflow.org/guide/saved_model) .

There are several ways to export SavedModels from TensorFlow training code. The following list describes a few ways that work for various TensorFlow APIs:

  - If you use Keras for training, [use `tf.keras.Model.save` to export a SavedModel](https://www.tensorflow.org/guide/keras/save_and_serialize#whole-model_saving_loading) .

  - If you use an Estimator for training, [use `tf.estimator.Estimator.export_saved_model` to export a SavedModel](https://www.tensorflow.org/guide/estimator#savedmodels_from_estimators) .

  - Otherwise, [use `tf.saved_model.save`](https://www.tensorflow.org/guide/saved_model#saving_a_custom_model) or [use `tf.compat.v1.saved_model.SavedModelBuilder`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/saved_model/builder) .
    
    If you aren't using Keras or an Estimator, make sure to [use the `serve` tag and `serving_default` signature when you export your SavedModel](https://www.tensorflow.org/tfx/serving/serving_basic#train_and_export_tensorflow_model) in order to make sure Agent Platform can use your model artifacts to serve inferences. Keras and Estimator handle this automatically. Learn more about [specifying signatures during export](https://www.tensorflow.org/guide/saved_model#specifying_signatures_during_export) .

To serve inferences using these artifacts, create a `Model` with the [prebuilt container for inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#tensorflow) matching the version of TensorFlow that you used for training.

#### TensorFlow for Vertex Explainable AI

If you want to [get explanations](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) from a `Model` that uses a TensorFlow prebuilt container to serve inferences, read the [additional requirements for exporting a TensorFlow model for Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/tensorflow#exporting) .

#### Enable server-side request batching for TensorFlow

If you want to enable request batching for a `Model` that uses a TensorFlow prebuilt container to serve inferences, include config/batching\_parameters\_config in the same Cloud Storage directory as `saved_model.pb` file. To configure the batching config file, see the [TensorFlow's official documentation](https://www.tensorflow.org/tfx/serving/serving_config#batching_configuration) .

### PyTorch

You must package your model artifacts into a model archive ( `.mar` ) file. This archive must include a handler script, either [default](https://pytorch.org/serve/#default-handlers) or [custom](https://pytorch.org/serve/custom_service.html) , that defines how the model processes inference requests. For more advanced workflows, you should consider using custom containers instead of relying on the prebuilt PyTorch serving image.

The prebuilt PyTorch images expect the archive to be named `model.mar` , so make sure you set the model-name to 'model' when creating the archive.

For information about optimizing the memory usage, latency or throughput of a PyTorch model served with TorchServe, see the [PyTorch performance guide](https://github.com/pytorch/serve/blob/master/docs/performance_guide.md) .

### XGBoost

If you use an [XGBoost prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers#xgboost) to train a model, you can export the trained model in the following ways:

  - Use [`xgboost.Booster` 's `save_model` method](https://xgboost.readthedocs.io/en/latest/python/python_api.html#xgboost.Booster.save_model) to export a file named `model.bst` .
  - Use the [`joblib` library](https://joblib.readthedocs.io/en/latest/index.html) to export a file named `model.joblib` .

Your model artifact's filename must exactly match one of these options.

The following examples show how to train and export a model:

> **Note:** These examples assume that you train your model on Agent Platform and use the [`AIP_MODEL_DIR` environment variable set by Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) .

### xgboost.Booster

    import os
    
    from google.cloud import storage
    from sklearn import datasets
    import xgboost as xgb
    
    digits = datasets.load_digits()
    dtrain = xgb.DMatrix(digits.data, label=digits.target)
    bst = xgb.train({}, dtrain, 20)
    
    artifact_filename = 'model.bst'
    
    # Save model artifact to local filesystem (doesn't persist)
    local_path = artifact_filename
    bst.save_model(local_path)
    
    # Upload model artifact to Cloud Storage
    model_directory = os.environ['AIP_MODEL_DIR']
    storage_path = os.path.join(model_directory, artifact_filename)
    blob = storage.blob.Blob.from_string(storage_path, client=storage.Client())
    blob.upload_from_filename(local_path)

### joblib

    import os
    
    from google.cloud import storage
    from sklearn import datasets
    import joblib
    import xgboost as xgb
    
    digits = datasets.load_digits()
    dtrain = xgb.DMatrix(digits.data, label=digits.target)
    bst = xgb.train({}, dtrain, 20)
    
    artifact_filename = 'model.joblib'
    
    # Save model artifact to local filesystem (doesn't persist)
    local_path = artifact_filename
    joblib.dump(bst, local_path)
    
    # Upload model artifact to Cloud Storage
    model_directory = os.environ['AIP_MODEL_DIR']
    storage_path = os.path.join(model_directory, artifact_filename)
    blob = storage.blob.Blob.from_string(storage_path, client=storage.Client())
    blob.upload_from_filename(local_path)

To serve inferences using this artifact, create a `Model` with the [prebuilt container for inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#xgboost) matching the version of XGBoost that you used for training.

### scikit-learn

If you [use a `scikit-learn` prebuilt model to train a model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers#scikit-learn) , you can export it by using the [`joblib` library](https://joblib.readthedocs.io/en/latest/index.html) to export a file named `model.joblib` .

Your model artifact's filename must exactly match one of these options. You can export standard scikit-learn estimators or [scikit-learn pipelines](https://scikit-learn.org/stable/modules/compose.html) .

The following example shows how to train and export a model:

> **Note:** These examples assume that you train your model on Agent Platform and use the [`AIP_MODEL_DIR` environment variable set by Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) .

### joblib

    import os
    
    from google.cloud import storage
    from sklearn import datasets
    from sklearn.ensemble import RandomForestClassifier
    import joblib
    
    digits = datasets.load_digits()
    classifier = RandomForestClassifier()
    classifier.fit(digits.data, digits.target)
    
    artifact_filename = 'model.joblib'
    
    # Save model artifact to local filesystem (doesn't persist)
    local_path = artifact_filename
    joblib.dump(classifier, local_path)
    
    # Upload model artifact to Cloud Storage
    model_directory = os.environ['AIP_MODEL_DIR']
    storage_path = os.path.join(model_directory, artifact_filename)
    blob = storage.blob.Blob.from_string(storage_path, client=storage.Client())
    blob.upload_from_filename(local_path)

To serve inferences using this artifact, create a `Model` with the [prebuilt container for inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers#scikit-learn) matching the version of scikit-learn that you used for training.

## What's next

  - Read about [additional requirements for your training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) that you must consider when performing serverless training on Agent Platform.

  - Learn how to [create a custom `TrainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) in order to run your custom training code and create a `Model` from the resulting model artifacts.

  - Learn how to [import a `Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) from model artifacts in Cloud Storage. This applies to model artifacts that you [create using a `CustomJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) or a [`HyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) , as well as model artifacts that you train outside of Agent Platform.
