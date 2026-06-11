---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook
title: Create a notebook
description: Create and prepare a notebook (IPYNB) file as part of a tutorial that shows you how to use the Agent Platform SDK for Python to create a custom-trained model.
data_source: docs.cloud.google.com
---

In this tutorial, you use the Vertex AI SDK in a [Jupyter](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html) notebook to get predictions by using a Vertex AI Workbench instance.

This section shows you how to create a Jupyter notebook in a Vertex AI Workbench instance. Vertex AI Workbench instances are Jupyter notebook-based development environments for the entire data science workflow. Vertex AI Workbench instances are prepackaged with JupyterLab and have a preinstalled suite of deep learning packages, including support for the TensorFlow and PyTorch frameworks. For more information, see [Introduction to Vertex AI Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/introduction) .

After you create a notebook in Vertex AI Workbench, you run sequential portions of Python code to do most of the work to generate your predictions.

## Before you begin

## Create a Vertex AI Workbench instance

To create a Vertex AI Workbench instance, do the following:

1.  In the Google Cloud console, open your Google Cloud project if it's not already open.

2.  In the Google Cloud console, go to the Vertex AI Workbench **Instances** page.

3.  If the option to enable the **Notebooks API** appears, click **Enable** . It might take a few moments for the enabling process to complete.

4.  Click add\_box **Create new** .

5.  In the **New instance** dialog, for **Name** , enter a name for your instance.

6.  For **Region** , select **us-central1 (Iowa)** .

7.  For **Zone** , select **us-central1-a** .

8.  Click **Create** . If you want to learn more about your instance, after it appears in your list of instances click its name to see its properties.

## Prepare your notebook

Your Vertex AI Workbench instance is already authenticated to use your Google Cloud project. However, you must install and initialize the Agent Platform SDK for Python. This section walks you through these steps.

After you create your notebook, you use it to enter and run the sequential snippets of code in this tutorial. Each snippet of code must be run individually and in order.

### Create and open your notebook

Your notebook is where you run the code in this tutorial. It's a file with the extension `.ipynb` . When you create it, it's untitled. You can rename it after it's open. To create and open your notebook, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your instance's name, click **Open JupyterLab** .
    
    Your Vertex AI Workbench instance opens the JupyterLab environment.

3.  In JupyterLab, select **File \> New \> Notebook** .
    
    Your new notebook file opens and the **Select kernel** dialog appears.

4.  In the **Select kernel** dialog, select the **Python 3** kernel.

5.  In the left-navigation pane of JupyterLab, find your new notebook, named *Untitled.ipynb* . To rename it, right-click the notebook name, click **Rename** , and enter a new name.

### Install the Agent Platform SDK for Python

After you open your notebook, you must install the Agent Platform SDK for Python. You use the Agent Platform SDK for Python to make Agent Platform API calls that create your dataset, create your model, train and deploy your model, and make predictions with your model. For more information, see [Use the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .

When you install Agent Platform SDK for Python, other Google Cloud SDKs on which it's dependent are also installed. Two of those SDKs are used in this tutorial:

  - Cloud Storage - When you use the Agent Platform SDK for Python to make Agent Platform API calls, Gemini Enterprise Agent Platform stores artifacts in a Cloud Storage bucket. The bucket is referred to as a *staging bucket* . You specify the staging bucket when you [initialize the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook#initialize-vertex_sdk_python) . For more information, see [Python client for Google Cloud storage API](https://docs.cloud.google.com/python/docs/reference/storage/latest) .

  - BigQuery - Gemini Enterprise Agent Platform trains your model using a BigQuery public dataset. The BigQuery SDK must be installed to access and download the dataset used in this tutorial. For more information, see [BigQuery API client libraries](https://docs.cloud.google.com/bigquery/docs/reference/libraries) .

To install the Agent Platform SDK for Python and its dependent SDKs, run the following code.

    # Install the Agent Platform SDK
    ! pip3 install --upgrade --quiet google-cloud-aiplatform

The `--quiet` flag suppresses output so that only errors display, if there are any. The exclamation mark ( `!` ) indicates that this is a shell command.

Because this is the first code you're running in your new notebook, you enter it into the blank code cell at the top of your notebook. After you enter code in a code cell, click play\_arrow **Run the selected cells and advance** or use the keyboard shortcut `Shift + Enter` to run the code.

![Run code to install the SDK.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/images/run-code-to-install-sdks.png)

As you proceed through this tutorial, run code in the empty code cell that automatically appears below the most recently run code. If you want to manually add a new code cell, click the notebook file's add **Insert a cell below** button.

![Add new code cell.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/images/add-new-code-cell.png)

### Set your project ID and region

In this step, you assign your project ID and your region to variables so they can be easily referenced later in this tutorial.

#### Set your project ID

To set your project ID, do the following:

1.  Locate your Google Cloud project ID. For more information, see [Find your project ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/prerequisites#find-project-id) .

2.  Run the following in a code cell in your notebook. In the code, replace PROJECT\_ID with the project ID you just located. The output this command generates is `Updated property [core/project].`
    
        project_id = "PROJECT_ID"  # @param {type:"string"}

#### Set your region

This tutorial uses the `us-central1` region. To set your region, do the following:

1.  Run the following code to set the `region` variable that's used by Gemini Enterprise Agent Platform to `us-central1` . This command doesn't generate output. For more information, see [Choose your location](https://docs.cloud.google.com/vertex-ai/docs/general/locations#choosing_your_location) .
    
        region = "us-central1"  # @param {type: "string"}

### Create a Cloud Storage bucket

This tutorial requires a Cloud Storage bucket that's used by Gemini Enterprise Agent Platform to stage artifacts. Gemini Enterprise Agent Platform stores the data associated with the dataset you create and model resources in the staging bucket. This data is retained and available across sessions. In this tutorial, Gemini Enterprise Agent Platform also stores your dataset in the staging bucket. You specify your staging bucket when you [initialize the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook#initialize-vertex_sdk_python) .

Every Cloud Storage bucket name must be globally unique. If you choose a name that's been used, the command to create your bucket fails. The following code uses a datetime stamp and your project name to create a unique bucket name. You append the bucket name to `gs://` to create the URI for your Cloud Storage bucket. The `echo` shell command shows you the URI so you can verify it created correctly.

1.  To set your bucket's name and URI, run the following code. The last line displays the URI of your Cloud Storage bucket.
    
        bucket_name = "bucket-name-placeholder"  # @param {type:"string"}
        bucket_uri = f"gs://{bucket_name}"
        
        from datetime import datetime
        timestamp = datetime.now().strftime("%Y%m%d%H%M%S")
        
        if bucket_name == "" or bucket_name is None or bucket_name == "bucket-name-placeholder":
            bucket_name = project_id + "aip-" + timestamp
            bucket_uri = "gs://" + bucket_name
        ! echo $bucket_uri

2.  To create a bucket using the Cloud Storage client library and the bucket URI, run the following code. This code doesn't generate output.
    
        from google.cloud import storage
        client = storage.Client(project=project_id)
        
        # Create a bucket
        bucket = client.create_bucket(bucket_name, location=region)

3.  To verify your bucket created successfully, run the following:
    
        print("Bucket {} created.".format(bucket.name))

### Initialize the Agent Platform SDK for Python

To initialize the Agent Platform SDK for Python, you first import its library, `aiplatform` . Next, you call `aiplatform.init` and pass in values for the following parameters:

  - `project` - The `project` specifies which Google Cloud project to use when you use the Agent Platform SDK for Python to make calls to the Agent Platform API. In this tutorial you specify your Google Cloud project with its name. You can also specify your project with its project number.

  - `location` - The `location` specifies which Google Cloud region to use when you make API calls. If you don't specify a location, the Agent Platform SDK for Python uses `us-central1` .

  - `staging_bucket` - The `staging_bucket` specifies which Cloud Storage bucket is used to stage artifacts when you use the Agent Platform SDK for Python. You specify the bucket with a URI that starts with `gs://` . In this tutorial, you use the URI created earlier in [Create a Cloud Storage bucket](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook#create-storage-bucket) .

To set your Google Cloud project, region, and staging bucket, run the following command. This command doesn't generate output.

    from google.cloud import aiplatform
    
    # Initialize the Agent Platform SDK
    aiplatform.init(project=project_id, location=region, staging_bucket=bucket_uri)

### Initialize BigQuery

This tutorial uses a BigQuery public dataset of penguins to train a model. After Gemini Enterprise Agent Platform trains the model, you specify parameters that represent characteristics of penguins, and the model uses those characteristics to predict the species of penguin they represent. For more information about public datasets, see [BigQuery public datasets](https://cloud.google.com/bigquery/public-data) .

Before you use the BigQuery dataset, you must initialize BigQuery with your project ID. To do this, run the following command. This command doesn't generate output.

    from google.cloud import bigquery
    
    # Set up BigQuery client
    bq_client = bigquery.Client(project=project_id)
