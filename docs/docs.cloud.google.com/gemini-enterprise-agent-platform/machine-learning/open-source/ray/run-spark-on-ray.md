---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/run-spark-on-ray
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/run-spark-on-ray
title: Run Spark on Ray cluster on Gemini Enterprise Agent Platform
description: Install and configure RayDP to run Spark on a Ray cluster on Agent Platform.
data_source: docs.cloud.google.com
---

> To see an example of getting started with Spark on Ray on Agent Platform, run the "Spark on Ray on Agent Platform" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/spark_on_ray_on_vertex_ai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fspark_on_ray_on_vertex_ai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fspark_on_ray_on_vertex_ai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/spark_on_ray_on_vertex_ai.ipynb)

> **Note:** While [Managed Service for Apache Spark](https://cloud.google.com/dataproc) is the preferred service for running Spark, RayDP is recommended when you need to unify your stack for both ETL and ML. RayDP runs Spark on your Ray cluster, which enables a seamless and efficient transition from Spark data processing to Ray ML without the overhead of saving and reloading data between separate environments.

The [RayDP](https://github.com/oap-project/raydp) Python library makes it possible to run Spark on a Ray cluster. This document covers installing, configuring and running RayDP on Ray on Agent Platform (Ray cluster on Gemini Enterprise Agent Platform).

## Installation

Ray on Agent Platform enables users to run their applications using the open source [Ray framework](https://docs.ray.io/en/latest/ray-overview/index.html) . RayDP provides APIs for running Spark on Ray. The prebuilt container images available to create a Ray cluster on Gemini Enterprise Agent Platform don't come with RayDP pre-installed. This means you must create a [custom Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/create-cluster#custom-image) image for your Ray cluster on Gemini Enterprise Agent Platform to run RayDP applications on Ray cluster on Gemini Enterprise Agent Platform. The following section explains how to build a RayDP custom image.

### Build a Ray on Gemini Enterprise Agent Platform custom container image

Use this dockerfile to create a custom container image for Ray on Gemini Enterprise Agent Platform that has RayDP installed.

    FROM us-docker.pkg.dev/vertex-ai/training/ray-cpu.2-9.py310:latest
    
    RUN apt-get update -y \
        && pip install --no-cache-dir raydp pyarrow==14.0

You can use the latest Ray cluster on Gemini Enterprise Agent Platform prebuilt image for creating the RayDP custom image. You can also install other Python packages that you anticipate you'll use in your applications. The `pyarrow==14.0` is due to a dependency constraint of Ray 2.9.3.

### Build and push the custom container image

Create a Docker repository in [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) before you build your custom image (see [Work with container images](https://docs.cloud.google.com/artifact-registry/docs/docker) for how to create and configure your Docker repository). After you create the docker repository, build and push the custom container image using the Dockerfile.

    docker build . -t [LOCATION]-docker.pkg.dev/[PROJECT_ID]/[DOCKER_REPOSITORY]/[IMAGE_NAME]
    docker push [LOCATION]-docker.pkg.dev/[PROJECT_ID]/[DOCKER_REPOSITORY]/[IMAGE_NAME]

Where:

  - `LOCATION` : The Cloud Storage location (for example, us-central1) that you created in your Artifact Registry.
  - `PROJECT_ID` : Your Google Cloud project ID.
  - `DOCKER_REPOSITORY` : The name of the docker repository that you created.
  - `IMAGE_NAME` : The name of your custom container images.

### Create a Ray cluster on Gemini Enterprise Agent Platform

Use the custom container image built in the previous step to create a Ray cluster on Gemini Enterprise Agent Platform. You can use the Agent Platform SDK for Python for creating a Ray cluster on Gemini Enterprise Agent Platform.

If you haven't done so yet, install the required Python libraries.

    pip install --quiet google-cloud-aiplatform \
                 ray[all]==2.9.3 \
                 google-cloud-aiplatform[ray]

Configure Head and Worker nodes and create the cluster using Agent Platform SDK for Python. For example:

    import logging
    import ray
    from google.cloud import aiplatform
    from google.cloud.aiplatform import vertex_ray
    from vertex_ray import Resources
    
    head_node_type = Resources(
        machine_type="n1-standard-16",
        node_count=1,
        custom_image=[CUSTOM_CONTAINER_IMAGE_URI],
    )
    
    worker_node_types = [Resources(
        machine_type="n1-standard-8",
        node_count=2,
        custom_image=[CUSTOM_CONTAINER_IMAGE_URI],
    )]
    
    ray_cluster_resource_name = vertex_ray.create_ray_cluster(
        head_node_type=head_node_type,
        worker_node_types=worker_node_types,
        cluster_name=[CLUSTER_NAME],
    )

Where:

  - `CUSTOM_CONTAINER_IMAGE_URI` : The URI of the custom container image pushed to Artifact Registry.
  - `CLUSTER_NAME` : The name of your Ray cluster on Gemini Enterprise Agent Platform.

## Spark on Ray cluster on Gemini Enterprise Agent Platform

Before you run your Spark application, create a Spark session using the RayDP API. You can use the Ray client for doing this interactively or use the Ray job API. The Ray job API is recommended, especially for production and long-running applications. The RayDP API provides parameters to configure the Spark session, as well as supporting [Spark Configuration](https://spark.apache.org/docs/latest/configuration.html) . Learn more about the RayDP API for creating Spark Session see [Spark master actors node affinity](https://github.com/oap-project/raydp/blob/master/doc/spark_on_ray.md) .

### RayDP with Ray client

You can use Ray [Task](https://docs.ray.io/en/latest/ray-core/tasks.html#ray-remote-functions) or [Actor](https://docs.ray.io/en/latest/ray-core/actors.html) to create a Spark cluster and session on the Ray cluster on Gemini Enterprise Agent Platform. Ray Task, or Actor, is required to use a [Ray Client](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/ray-client.html) to create a Spark session on the Ray cluster on Gemini Enterprise Agent Platform. The following code shows how a Ray Actor can create a Spark Session, run a Spark application, and stop a Spark cluster on a Ray cluster on Gemini Enterprise Agent Platform using RayDP.

To interactively connect to the Ray cluster on Gemini Enterprise Agent Platform, see [Connect to a Ray cluster through Ray Client](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/develop-application#sdk)

    @ray.remote
    class SparkExecutor:
      import pyspark
    
      spark: pyspark.sql.SparkSession = None
    
      def __init__(self):
    
        import ray
        import raydp
    
        self.spark = raydp.init_spark(
          app_name="RAYDP ACTOR EXAMPLE",
          num_executors=1,
          executor_cores=1,
          executor_memory="500M",
        )
    
      def get_data(self):
        df = self.spark.createDataFrame(
            [
                ("sue", 32),
                ("li", 3),
                ("bob", 75),
                ("heo", 13),
            ],
            ["first_name", "age"],
        )
        return df.toJSON().collect()
    
      def stop_spark(self):
        import raydp
        raydp.stop_spark()
    
    s = SparkExecutor.remote()
    data = ray.get(s.get_data.remote())
    print(data)
    ray.get(s.stop_spark.remote())

### RayDP with Ray Job API

Ray client is useful for small experiments that require interactive connection with the Ray cluster. The [Ray Job API](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/index.html#ray-jobs-api) is the recommended way to run long-running and production jobs on a Ray cluster. This also applies to running Spark applications on the Ray cluster on Gemini Enterprise Agent Platform.

Create a Python script that contains your Spark application code. For example:

    import pyspark
    import raydp
    
    def get_data(spark: pyspark.sql.SparkSession):
        df = spark.createDataFrame(
            [
                ("sue", 32),
                ("li", 3),
                ("bob", 75),
                ("heo", 13),
            ],
            ["first_name", "age"],
        )
        return df.toJSON().collect()
    
    def stop_spark():
        raydp.stop_spark()
    
    if __name__ == '__main__':
        spark = raydp.init_spark(
          app_name="RAYDP JOB EXAMPLE",
            num_executors=1,
            executor_cores=1,
            executor_memory="500M",
        )
        print(get_data(spark))
        stop_spark()

Submit the job to run the python script using Ray Job API. For example:

    from ray.job_submission import JobSubmissionClient
    
    client = JobSubmissionClient(RAY_ADDRESS)
    
    job_id = client.submit_job(
      # Entrypoint shell command to execute
      entrypoint="python [SCRIPT_NAME].py",
      # Path to the local directory that contains the python script file.
      runtime_env={
        "working_dir": ".",
      }
    )

Where:

  - `SCRIPT_NAME` : The filename of the script that you created.

## Reading Cloud Storage files from Spark application

It's common practice to store data files in a Google Cloud Storage bucket. You can read these files in multiple ways from a Spark application that's running on the Ray cluster on Gemini Enterprise Agent Platform. This section explains two techniques for reading Cloud Storage files from Spark applications running on Ray Cluster on Gemini Enterprise Agent Platform.

### Use the Google Cloud Storage Connector

You can use the Google Cloud Connector for Hadoop to read files from a Cloud Storage bucket from your Spark application. After you create a Spark session using RayDP, you can read files using a few configuration parameter. The following code shows how to read a CSV file stored in a Cloud Storage bucket from a Spark application on the Ray cluster on Gemini Enterprise Agent Platform.

    import raydp
    
    spark = raydp.init_spark(
      app_name="RayDP Cloud Storage Example 1",
      configs={
          "spark.jars": "https://storage.googleapis.com/hadoop-lib/gcs/gcs-connector-hadoop3-2.2.22.jar",
          "spark.hadoop.fs.AbstractFileSystem.gs.impl": "com.google.cloud.hadoop.fs.gcs.GoogleHadoopFS",
          "spark.hadoop.fs.gs.impl": "com.google.cloud.hadoop.fs.gcs.GoogleHadoopFileSystem",
      },
      num_executors=2,
      executor_cores=4,
      executor_memory="500M",
    )
    
    spark_df = spark.read.csv([GCS_FILE_URI], header = True, inferSchema = True)

Where:

  - `GCS_FILE_URI` : The URI of a file stored in a Cloud Storage bucket. For example: gs://my-bucket/my-file.csv.

### Use Ray data

The Google Cloud connector provides a way to read files from a Google Cloud bucket and it may be sufficient for most use cases. You might want to use Ray Data to read files from the Google Cloud bucket when you need to use Ray's distributed processing for reading data, or when you face issues reading Google Cloud file with Google Cloud connector. This could possibly happen because of Java dependency conflicts when some other application dependencies are added to the Spark Java classpath using either `spark.jars.packages` or `spark.jars` .

    import raydp
    import ray
    
    spark = raydp.init_spark(
      app_name="RayDP Cloud Storage Example 2",
      configs={
          "spark.jars.packages": "com.microsoft.azure:synapseml_2.12:0.11.4-spark3.3",
          "spark.jars.repositories": "https://mmlspark.azureedge.net/maven",
          "spark.jars": "https://storage.googleapis.com/hadoop-lib/gcs/gcs-connector-hadoop3-2.2.22.jar",
          "spark.hadoop.fs.AbstractFileSystem.gs.impl": "com.google.cloud.hadoop.fs.gcs.GoogleHadoopFS",
          "spark.hadoop.fs.gs.impl": "com.google.cloud.hadoop.fs.gcs.GoogleHadoopFileSystem",
      },
      num_executors=2,
      executor_cores=4,
      executor_memory="500M",
    )
    
    # This doesn't work even though the Cloud Storage connector Jar and other parameters have
    been added to the Spark configuration.
    #spark.read.csv([GCS_FILE_URI], header = True, inferSchema = True)
    
    ray_dataset = ray.data.read_csv(GCS_FILE_URI)
    spark_df = ray_dataset.to_spark(spark)

## Pyspark Pandas UDF on Ray cluster on Gemini Enterprise Agent Platform

[Pyspark Pandas UDFs](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.functions.pandas_udf.html) sometimes require additional code when you use them in your Spark application running on a Ray cluster on Gemini Enterprise Agent Platform. This is usually required when the Pandas UDF uses a Python library that isn't available on the Ray cluster on Gemini Enterprise Agent Platform. You can package the [Python dependencies](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/sdk.html#dependency-management) of an application using the runtime environment with the Ray Job API. After you submit the Ray job to the cluster, Ray installs those dependencies in the Python virtual environment that it creates for running the job. The [Pandas UDFs](https://spark.apache.org/docs/latest/api/python/user_guide/python_packaging.html) , however, don't use the same virtual environment. Instead, they use the default Python System environment. If that dependency isn't available in the System environment, you might need to install it within your Pandas UDF. In the following example, install the `statsmodels` library within the UDF.

    import pandas as pd
    import pyspark
    import raydp
    from pyspark.sql.functions import pandas_udf
    from pyspark.sql.types import StringType
    
    def test_udf(spark: pyspark.sql.SparkSession):
        import pandas as pd
    
        df = spark.createDataFrame(pd.read_csv("https://www.datavis.ca/gallery/guerry/guerry.csv"))
        return df.select(func('Lottery','Literacy', 'Pop1831')).collect()
    
    @pandas_udf(StringType())
    def func(s1: pd.Series, s2: pd.Series, s3: pd.Series) -> str:
        import numpy as np
        import subprocess
        import sys
        subprocess.check_call([sys.executable, "-m", "pip", "install", "statsmodels"])
        import statsmodels.api as sm
        import statsmodels.formula.api as smf
    
        d = {'Lottery': s1,
             'Literacy': s2,
             'Pop1831': s3}
        data = pd.DataFrame(d)
    
        # Fit regression model (using the natural log of one of the regressors)
        results = smf.ols('Lottery ~ Literacy + np.log(Pop1831)', data=data).fit()
        return results.summary().as_csv()
    
    if __name__ == '__main__':
    
        spark = raydp.init_spark(
          app_name="RayDP UDF Example",
          num_executors=2,
          executor_cores=4,
          executor_memory="1500M",
        )
    
        print(test_udf(spark))
    
        raydp.stop_spark()
