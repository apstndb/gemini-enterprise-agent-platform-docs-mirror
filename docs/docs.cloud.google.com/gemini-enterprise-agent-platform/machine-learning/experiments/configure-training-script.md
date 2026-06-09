---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/configure-training-script
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/configure-training-script
title: Configure your training script
description: Configure your training script to write TensorBoard logs. For existing TensorBoard users, this requires no change to your model training code.
data_source: docs.cloud.google.com
---

Your training script must be configured to write TensorBoard logs. For existing TensorBoard users, this requires no change to your model training code.

To configure your training script in TensorFlow 2.x, create a TensorBoard callback and set the `log_dir` variable to any location which can connect to Google Cloud.

The TensorBoard callback is then included in the TensorFlow `model.fit` callbacks list.

    import tensorflow as tf
    
    def train_tensorflow_model_with_tensorboard(log_dir):
        (x_train, y_train), (x_test, y_test) = tf.keras.datasets.mnist.load_data()
        x_train, x_test = x_train / 255.0, x_test / 255.0
    
        def create_model():
            return tf.keras.models.Sequential(
                [
                    tf.keras.layers.Flatten(input_shape=(28, 28)),
                    tf.keras.layers.Dense(512, activation="relu"),
                ]
            )
    
        model = create_model()
        model.compile(
            optimizer="adam",
            loss="sparse_categorical_crossentropy",
            metrics=["accuracy"]
        )
    
        tensorboard_callback = tf.keras.callbacks.TensorBoard(
            log_dir=log_dir,
            histogram_freq=1
        )
    
        model.fit(
            x=x_train,
            y=y_train,
            epochs=5,
            validation_data=(x_test, y_test),
            callbacks=[tensorboard_callback],
        )

The TensorBoard logs are created in the specified directory and can be uploaded to a Vertex AI TensorBoard experiment by following the [Upload TensorBoard Logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-upload-existing-logs#one-time-logging) instructions for uploading.

For more examples, see the [TensorBoard open source docs](https://www.tensorflow.org/tensorboard/get_started)

## What's next

  - Check out automatic log streaming
      - [Train using a custom training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training)
      - [Train using Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-with-pipelines)
