---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/export-metadata-annotations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/export-metadata-annotations
title: Export metadata and annotations from a dataset
description: Export metadata and annotations from a dataset.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform lets you export the metadata and annotation sets from a `Dataset` resource. This capability can be useful if you want to maintain a record of a specific collection of annotation changes, additions, or deletions.

When you export a `Dataset` , Agent Platform creates one or more [JSON Lines](https://jsonlines.org/) files that contain your `Dataset` 's metadata and annotations, and saves these JSON Lines files to a Cloud Storage directory of your choice.

You can export image `Dataset` resources. You cannot export tabular `Dataset` resources.

Exporting a `Dataset` doesn't create additional copies of the image data that your `Dataset` is based on. The JSON Lines files created by the export processes include the original Cloud Storage URIs for your data that you specified when you [imported that data into the `Dataset`](https://docs.cloud.google.com/vertex-ai/docs/datasets/create-dataset-api#import-data) .

## Export a `Dataset` using the Google Cloud console or the API

You can use the Google Cloud console or the Agent Platform API to export a `Dataset` . Follow the steps in the corresponding tab:

### Console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  In the **Region** drop-down list, select the location where the `Dataset` is stored.

3.  Find the row of the `Dataset` . You can export metadata and annotations for all [annotation sets](https://docs.cloud.google.com/vertex-ai/docs/datasets/create-annotation-set) or for a specific annotation set:
    
      - **If you want to export metadata and annotations for all of the `Dataset` 's annotation sets,** then click **View more more\_vert** and then click **Export dataset** .
        
        This tells Agent Platform to create a set of JSON Lines files for each annotation set.
    
      - **If you want to export metadata and annotations for a specific annotation set,** then do the following:
        
        1.  Click **Expand node arrow\_drop\_down** to show rows for each of the `Dataset` 's annotation sets.
        
        2.  In the row of the annotation set that you want to export, click **View more more\_vert** and then click **Export annotation set** .
        
        This tells Agent Platform to create a set of JSON Lines files for the annotation set that you specified.

4.  In the **Export data** dialog, enter a Cloud Storage directory where you want Agent Platform to save the exported JSON Lines files. Click **Export** .

### REST

### Get the `Dataset` 's ID

To export a `Dataset` , you must know the numerical ID of the `Dataset` . If you know the display name of the `Dataset` but not the ID, expand the following section to learn how to get the ID using the API:

#### Get a Dataset's ID from its display name

Before using any of the request data, make the following replacements:

  - LOCATION : The location where the `Dataset` is stored. For example, `us-central1` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_DISPLAY\_NAME : The display name of the `Dataset` .

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets?filter=displayName=DATASET_DISPLAY_NAME

To send your request, choose one of these options:

#### curl

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets?filter=displayName=DATASET_DISPLAY_NAME"

#### PowerShell

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets?filter=displayName=DATASET_DISPLAY_NAME" | Select-Object -Expand Content

The following example response has been truncated with `...` to emphasize where you can find your `Dataset` 's ID: it is the number that takes the place of DATASET\_ID .

    {
      "datasets": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID",
          "displayName": "DATASET_DISPLAY_NAME",
          ...
        }
      ]
    }

Alternatively, you can get the `Dataset` 's ID from the Google Cloud console: Go to the Agent Platform **Datasets** page and find the number in the **ID** column.

### Export one or more annotation sets

Before using any of the request data, make the following replacements:

  - LOCATION : The location where the `Dataset` is stored. For example, `us-central1` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_ID : The numerical ID of the `Dataset` .

  - EXPORT\_DIRECTORY : Cloud Storage URI (beginning with `gs://` ) of a directory where you want Agent Platform to save the exported JSON Lines files. This must be in a Cloud Storage bucket that you have access to, but the directory does not need to exist yet.

  - FILTER : A filter string that determines which [annotation sets](https://docs.cloud.google.com/vertex-ai/docs/datasets/create-annotation-set) get exported.
    
      - **If you want to export metadata and annotations for all of the `Dataset` 's annotation sets,** replace FILTER with an empty string (or omit the `annotationsFilter` field from the request body entirely). This tells Agent Platform to create a set of JSON Lines files for each annotation set.
    
      - **If you want to export metadata and annotations for a specific annotation set,** replace FILTER with the following:
        
            labels.aiplatform.googleapis.com/annotation_set_name=ANNOTATION_SET_ID
        
        This tells Agent Platform to create a set of JSON Lines files for the annotation set with the numerical ID ANNOTATION\_SET\_ID .
        
        To find the numerical ID of the annotation set that you want to specify, view the annotation set in the Google Cloud console and look for the value following `annotationSetId` in the URL.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:export

Request JSON body:

    {
      "exportConfig": {
        "gcsDestination": {
          "outputUriPrefix": "EXPORT_DIRECTORY"
        },
        "annotationsFilter": "FILTER"
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:export"

#### PowerShell

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:export" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.ExportDataOperationMetadata",
        "genericMetadata": {
          "createTime": "2021-02-17T00:54:58.827429Z",
          "updateTime": "2021-02-17T00:54:58.827429Z"
        },
        "gcsOutputDirectory": "EXPORT_DIRECTORY/export-data-DATASET_DISPLAY_NAME-2021-02-17T00:54:58.734772Z"
      }
    }

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/vertex-ai/docs/general/long-running-operations) .

## Exported files explained

Within the export directory that you specified in the previous section, Agent Platform creates a new directory labeled with the `Dataset` 's display name and a timestamp; for example, `export-data- DATASET_DISPLAY_NAME -2021-02-17T00:54:58.734772Z` . Within this directory, you can find a subdirectory for each annotation set that you exported.

For each annotation set, you can find one or more JSON Lines files. Each row of each JSON Lines file represents a data item from the annotation set. Each data item may contain metadata and annotations that you specified when you imported the data to Agent Platform, as well as metadata and annotations that you added after importing the data. For example, if you [requested data labeling](https://docs.cloud.google.com/vertex-ai/docs/datasets/data-labeling-job) for your `Dataset` or if you manually added labels or annotations to the `Dataset` in the Google Cloud console, then this information is included in the exported files.

If you export multiple annotation sets, the same data items might appear in multiple JSON Lines files. For example, if you export an image `Dataset` with multiple annotation sets, one JSON Lines file might contain a data item with a single-label classification annotation; another JSON Lines file for a different annotation set might contain the same data item, but with an object detection annotation instead.

The format of the exported files matches the format of the JSON Lines import files that you can use to [import data intoAgent Platform](https://docs.cloud.google.com/vertex-ai/docs/datasets/create-dataset-api#import-data) . This format depends on the data type (image or tabular) and objective (such as object tracking, entity extraction, or classification). For example, if you export an annotation set for single-label image classification, then each line of each JSON Lines file is formatted according to the [`gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml` schema file](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml) , as described in [Preparing image data](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data) .

> **Note:** If you export a dataset with *no* annotations, verify the fields established by the export before attempting to import the data for a specific objective. For example, if you export an image dataset with no annotations, the exported JSON lines file contains an empty `classificationAnnotations` array. This field is only applicable to specific objectives and their corresponding YAML schema files. For more information, see [prepare training data page](https://docs.cloud.google.com/vertex-ai/docs/training-overview) .

## What's next

  - Learn how to [label data using the Google Cloud console](https://docs.cloud.google.com/vertex-ai/docs/datasets/label-using-console) .
  - Read more about [working with datasets in Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/training-overview) .
