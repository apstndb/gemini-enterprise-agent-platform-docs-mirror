---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions
title: Get online inferences from a custom trained model
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=-9fU1xwBQYU)

This page shows you how to get online (real-time) inferences from your custom trained models using the Google Cloud CLI or the Agent Platform API.

## Format your input for online inference

This section shows how to format and encode your inference input instances as JSON, which is required if you are using the [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) or [`explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain) method. This isn't required if you are [`rawPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict) method. For information on which method to choose, see [Send request to endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#send-request) .

If you're using the Agent Platform SDK for Python to send inference requests, specify the list of instances without the `instances` field. For example, specify `[ ["the","quick","brown"], ... ]` instead of `{ "instances": [ ["the","quick","brown"], ... ] }` .

If your model uses a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) , your input must be formatted as JSON, and there is an additional `parameters` field that can be used for your container. Learn more about [format inference input with custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#inference) .

### Format instances as JSON strings

The basic format for online inference is a list of data instances. These can be either plain lists of values or members of a JSON object, depending on how you configured your inputs in your training application. TensorFlow models can accept more complex inputs, while most scikit-learn and XGBoost models expect a list of numbers as input.

This example shows an input tensor and an instance key to a TensorFlow model:

``` 
 {"values": [1, 2, 3, 4], "key": 1}
```

The makeup of the JSON string can be complex as long as it follows these rules:

  - The top level of instance data must be a JSON object: a dictionary of key-value pairs.

  - Individual values in an instance object can be strings, numbers, or lists. You can't embed JSON objects.

  - Lists must contain only items of the same type (including other lists). You may not mix string and numerical values.

You pass input instances for online inference as the message body for the `projects.locations.endpoints.predict` call. Learn more about the [request body's formatting requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#request-response-examples) .

Make each instance an item in a JSON array, and provide the array as the `instances` field of a JSON object. For example:

    {"instances": [
      {"values": [1, 2, 3, 4], "key": 1},
      {"values": [5, 6, 7, 8], "key": 2}
    ]}

### Encode binary data for inference input

> **Note:** This following section only applies to prediction with TensorFlow.

Binary data can't be formatted as the UTF-8 encoded strings that JSON supports. If you have binary data in your inputs, you must use base64 encoding to represent it. The following special formatting is required:

  - Your encoded string must be formatted as a JSON object with a single key named `b64` . In Python 3, base64 encoding outputs a byte sequence. You must convert this to a string to make it JSON serializable:
    
        {'image_bytes': {'b64': base64.b64encode(jpeg_data).decode()}}

  - In your TensorFlow model code, you must name the aliases for your binary input and output tensors so that they end with '\_bytes'.

## Request and response examples

This section describes the format of the inference request body and of the response body, with examples for TensorFlow, scikit-learn, and XGBoost.

### Request body details

### TensorFlow

The request body contains data with the following structure (JSON representation):

    {
      "instances": [
        <value>|<simple/nested list>|<object>,
        ...
      ]
    }

The `instances[]` object is required, and must contain the list of instances to get inferences for.

The structure of each element of the instances list is determined by your model's input definition. Instances can include named inputs (as objects) or can contain only unlabeled values.

Not all data includes named inputs. Some instances are simple JSON values (boolean, number, or string). However, instances are often lists of simple values, or complex nested lists.

Below are some examples of request bodies.

CSV data with each row encoded as a string value:

    {"instances": ["1.0,true,\\"x\\"", "-2.0,false,\\"y\\""]}

Plain text:

    {"instances": ["the quick brown fox", "the lazy dog"]}

Sentences encoded as lists of words (vectors of strings):

    {
      "instances": [
        ["the","quick","brown"],
        ["the","lazy","dog"],
        ...
      ]
    }

Floating point scalar values:

    {"instances": [0.0, 1.1, 2.2]}

Vectors of integers:

    {
      "instances": [
        [0, 1, 2],
        [3, 4, 5],
        ...
      ]
    }

Tensors (in this case, two-dimensional tensors):

    {
      "instances": [
        [
          [0, 1, 2],
          [3, 4, 5]
        ],
        ...
      ]
    }

Images, which can be represented different ways. In this encoding scheme the first two dimensions represent the rows and columns of the image, and the third dimension contains lists (vectors) of the R, G, and B values for each pixel:

    {
      "instances": [
        [
          [
            [138, 30, 66],
            [130, 20, 56],
            ...
          ],
          [
            [126, 38, 61],
            [122, 24, 57],
            ...
          ],
          ...
        ],
        ...
      ]
    }

### Data encoding

JSON strings must be encoded as UTF-8. To send binary data, you must base64-encode the data and mark it as binary. To mark a JSON string as binary, replace it with a JSON object with a single attribute named `b64` :

    {"b64": "..."} 

The following example shows two serialized `tf.Examples` instances, requiring base64 encoding (fake data, for illustrative purposes only):

    {"instances": [{"b64": "X5ad6u"}, {"b64": "IA9j4nx"}]}

The following example shows two JPEG image byte strings, requiring base64 encoding (fake data, for illustrative purposes only):

    {"instances": [{"b64": "ASa8asdf"}, {"b64": "JLK7ljk3"}]}

### Multiple input tensors

Some models have an underlying TensorFlow graph that accepts multiple input tensors. In this case, use the names of JSON name/value pairs to identify the input tensors.

For a graph with input tensor aliases "tag" (string) and "image" (base64-encoded string):

    {
      "instances": [
        {
          "tag": "beach",
          "image": {"b64": "ASa8asdf"}
        },
        {
          "tag": "car",
          "image": {"b64": "JLK7ljk3"}
        }
      ]
    }

For a graph with input tensor aliases "tag" (string) and "image" (3-dimensional array of 8-bit ints):

    {
      "instances": [
        {
          "tag": "beach",
          "image": [
            [
              [138, 30, 66],
              [130, 20, 56],
              ...
            ],
            [
              [126, 38, 61],
              [122, 24, 57],
              ...
            ],
            ...
          ]
        },
        {
          "tag": "car",
          "image": [
            [
              [255, 0, 102],
              [255, 0, 97],
              ...
            ],
            [
              [254, 1, 101],
              [254, 2, 93],
              ...
            ],
            ...
          ]
        },
        ...
      ]
    }

### scikit-learn

The request body contains data with the following structure (JSON representation):

    {
      "instances": [
        <simple list>,
        ...
      ]
    }

The `instances[]` object is required, and must contain the list of instances to get inferences for. In the following example, each input instance is a list of floats:

    {
      "instances": [
        [0.0, 1.1, 2.2],
        [3.3, 4.4, 5.5],
        ...
      ]
    }

The dimension of input instances must match what your model expects. For example, if your model requires three features, then the length of each input instance must be 3.

### XGBoost

The request body contains data with the following structure (JSON representation):

    {
      "instances": [
        <simple list>,
        ...
      ]
    }

The `instances[]` object is required, and must contain the list of instances to get inferences for. In the following example, each input instance is a list of floats:

    {
      "instances": [
        [0.0, 1.1, 2.2],
        [3.3, 4.4, 5.5],
        ...
      ]
    }

The dimension of input instances must match what your model expects. For example, if your model requires three features, then the length of each input instance must be 3.

Agent Platform doesn't support sparse representation of input instances for XGBoost.

The online inference service interprets zeros and `NaN` s differently. If the value of a feature is zero, use `0.0` in the corresponding input. If the value of a feature is missing, use `"NaN"` in the corresponding input.

The following example represents an inference request with a single input instance, where the value of the first feature is 0.0, the value of the second feature is 1.1, and the value of the third feature is missing:

    {"instances": [[0.0, 1.1, "NaN"]]}

### PyTorch

If your model uses a [PyTorch prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers#pytorch) , TorchServe's default handlers expect each instance to be wrapped in a `data` field. For example:

    {
      "instances": [
        { "data": , <value> },
        { "data": , <value> }
      ]
    }

### Response body details

If the call is successful, the response body contains one inference entry per instance in the request body, given in the same order:

    {
      "predictions": [
        {
          object
        }
      ],
      "deployedModelId": string
    }

If inference fails for any instance, the response body contains no inferences. Instead, it contains a single error entry:

    {
      "error": string
    }

The `predictions[]` object contains the list of inferences, one for each instance in the request.

On error, the `error` string contains a message describing the problem. The error is returned instead of an inference list if an error occurred while processing any instance.

Even though there is one inference per instance, the format of an inference isn't directly related to the format of an instance. Inferences take whatever format is specified in the outputs collection defined in the model. The collection of inferences is returned in a JSON list. Each member of the list can be a simple value, a list, or a JSON object of any complexity. If your model has more than one output tensor, each inference will be a JSON object containing a name-value pair for each output. The names identify the output aliases in the graph.

### Response body examples

### TensorFlow

The following examples show some possible responses:

  - A simple set of predictions for three input instances, where each prediction is an integer value:
    
        {"predictions":
           [5, 4, 3],
           "deployedModelId": 123456789012345678
        }

  - A more complex set of predictions, each containing two named values that correspond to output tensors, named `label` and `scores` respectively. The value of `label` is the predicted category ("car" or "beach") and `scores` contains a list of probabilities for that instance across the possible categories.
    
        {
          "predictions": [
            {
              "label": "beach",
              "scores": [0.1, 0.9]
            },
            {
              "label": "car",
              "scores": [0.75, 0.25]
            }
          ],
          "deployedModelId": 123456789012345678
        }

  - A response when there is an error processing an input instance:
    
        {"error": "Divide by zero"}

### scikit-learn

The following examples show some possible responses:

  - A simple set of predictions for three input instances, where each prediction is an integer value:
    
        {"predictions":
           [5, 4, 3],
           "deployedModelId": 123456789012345678
        }

  - A response when there is an error processing an input instance:
    
        {"error": "Divide by zero"}

### XGBoost

The following examples show some possible responses:

  - A simple set of predictions for three input instances, where each prediction is an integer value:
    
        {"predictions":
           [5, 4, 3],
           "deployedModelId": 123456789012345678
        }

  - A response when there is an error processing an input instance:
    
        {"error": "Divide by zero"}

## Send a request to an endpoint

There are four ways to send a request:

  - [Inference request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#predict-request) : send a request to [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) to get an online inference.

  - [Raw inference request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#raw-inference-request) : sends a request to [`rawPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict) , which lets you use an arbitrary HTTP payload rather than following the guidelines described in the [Format your input](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#formatting-inference-input) sections of this page. You might want to get raw inferences if:
    
      - You are [using a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) which receives requests and sends responses that differ from the guidelines.
      - You require lower latency. `rawPredict` skips the serialization steps and directly forwards the request to the inference container.
      - You are serving inferences with [NVIDIA Triton](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-nvidia-triton) .

  - [Explanation request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#explain-request) : sends a request to [`explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain) . If you have [configured your `Model` for Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-feature-based) , then you can [get online explanations](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/getting-explanations) . Online explanation requests have the same format as online inference requests, and they return similar responses; the only difference is that online explanation responses include feature attributions as well as inferences.

  - [Invoke request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#invoke-request) : forwards an arbitrary request to the model server. For example, "/invoke/foo/bar" would be forwarded as "/foo/bar" to the model server. This feature is in public preview and only supports HTTP calls on dedicated endpoints. To create an invoke enabled model, follow directions to [use arbitrary custom routes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-arbitrary-custom-routes) .

### Send an online inference request to a dedicated public endpoint

> To learn more, run the " Model Garden - Gemma (Deployment)" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_gemma_deployment_on_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_gemma_deployment_on_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_gemma_deployment_on_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_gemma_deployment_on_vertex.ipynb)

Dedicated endpoints facilitate communication using both HTTP and gRPC protocols. For gRPC requests, the inclusion of the `x-vertex-ai-endpoint-id` header is mandatory to ensure accurate endpoint identification. The following APIs are supported through these dedicated endpoints:

  - Predict
  - RawPredict
  - StreamRawPredict
  - Chat Completion (Model Garden only)
  - Invoke

Dedicated endpoints use a new URL path. You can retrieve this path from the [`dedicatedEndpointDns`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) field in the REST API, or from [`Endpoint.dedicated_endpoint_dns`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#properties) in the Agent Platform SDK for Python.

To send an inference to a dedicated endpoint using the Agent Platform SDK for Python, set the `use_dedicated_endpoint` parameter to `True` :

    endpoint.predict(instances=instances, use_dedicated_endpoint=True)

### Send an online inference request to a shared public endpoint

### gcloud

The following example uses the [`gcloud ai endpoints predict` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/predict) :

1.  Write the following JSON object to file in your local environment. The filename doesn't matter, but for this example, name the file `request.json` .
    
        {
         "instances": INSTANCES
        }
    
    Replace the following:
    
      - INSTANCES : A JSON array of instances that you want to get inferences for. The format of each instance depends on which inputs your trained ML model expects. For more information, see [Formatting your input for online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#formatting-inference-input) .

2.  Run the following command:
    
        gcloud ai endpoints predict ENDPOINT_ID \
          --region=LOCATION_ID \
          --json-request=request.json
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers).
  - ENDPOINT\_ID : The ID for the endpoint.
  - INSTANCES : A JSON array of instances that you want to get inferences for. The format of each instance depends on which inputs your trained ML model expects. For more information, see [Formatting your input for online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#formatting-inference-input) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict

Request JSON body:

    {
      "instances": INSTANCES
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict" | Select-Object -Expand Content

If successful, you receive a JSON response similar to the following. In the response, expect the following replacements:

  - PREDICTIONS : A JSON array of predictions, one for each instance that you included in the request body.
  - DEPLOYED\_MODEL\_ID : The ID of the [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel) that served the predictions.

<!-- end list -->

    {
      "predictions": PREDICTIONS,
      "deployedModelId": "DEPLOYED_MODEL_ID"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.PredictRequest;
    import com.google.cloud.aiplatform.v1.PredictResponse;
    import com.google.cloud.aiplatform.v1.PredictionServiceClient;
    import com.google.cloud.aiplatform.v1.PredictionServiceSettings;
    import com.google.protobuf.ListValue;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    import java.util.List;
    
    public class PredictCustomTrainedModelSample {
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String instance = "[{ “feature_column_a”: “value”, “feature_column_b”: “value”}]";
        String project = "YOUR_PROJECT_ID";
        String endpointId = "YOUR_ENDPOINT_ID";
        predictCustomTrainedModel(project, endpointId, instance);
      }
    
      static void predictCustomTrainedModel(String project, String endpointId, String instance)
          throws IOException {
        PredictionServicPredictionServiceSettingsceSettings =
            PredictionServicPredictionServiceSettings          .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PredictionServicPredictionServiceClientceClient =
            PredictionServicPredictionServiceClientonServiceSettings)) {
          String location = "us-central1";
          EndpointName endEndpointNameEndpointName.of(EndpointNameation, endpointId);
    
          ListValue.BuildeListValueue = ListValue.newBuiListValue     JsonFormat.parseJsonFormatinstance, listValue);
          List<Value> instanListValuelistValue.getValuesList();
    
          PredictRequest pPredictRequest=
              PredictRequest.nPredictRequest            .setEndpoint(endpointName.toSendpointName.toString().addAllInstances(instanceList)
                  .build();
          PredictResponse PredictResponse = predictionServiceClient.predict(predictRequest);
    
          System.out.println("Predict Custom Trained model Response");
          System.out.format("\tDeployed Model Id: %s\n", predictResponse.predictResponse.getDeployedModelId()out.println("Predictions");
          for (Value predictionValueedictResponse.predictResponse.getPredictionsList()em.out.format("\tPrediction: %s\n", prediction);
          }
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const filename = "YOUR_PREDICTION_FILE_NAME";
    // const endpointId = "YOUR_ENDPOINT_ID";
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    const util = require('util');
    const {readFile} = require('fs');
    const readFileAsync = util.promisify(readFile);
    
    // Imports the Google Cloud Prediction Service Client library
    const {PredictionServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const predictionServiceClient = new PredictionServiceClient(clientOptions);
    
    async function predictCustomTrainedModel() {
      // Configure the parent resource
      const endpoint = `projects/${project}/locations/${location}/endpoints/${endpointId}`;
      const parameters = {
        structValue: {
          fields: {},
        },
      };
      const instanceDict = await readFileAsync(filename, 'utf8');
      const instanceValue = JSON.parse(instanceDict);
      const instance = {
        structValue: {
          fields: {
            Age: {stringValue: instanceValue['Age']},
            Balance: {stringValue: instanceValue['Balance']},
            Campaign: {stringValue: instanceValue['Campaign']},
            Contact: {stringValue: instanceValue['Contact']},
            Day: {stringValue: instanceValue['Day']},
            Default: {stringValue: instanceValue['Default']},
            Deposit: {stringValue: instanceValue['Deposit']},
            Duration: {stringValue: instanceValue['Duration']},
            Housing: {stringValue: instanceValue['Housing']},
            Job: {stringValue: instanceValue['Job']},
            Loan: {stringValue: instanceValue['Loan']},
            MaritalStatus: {stringValue: instanceValue['MaritalStatus']},
            Month: {stringValue: instanceValue['Month']},
            PDays: {stringValue: instanceValue['PDays']},
            POutcome: {stringValue: instanceValue['POutcome']},
            Previous: {stringValue: instanceValue['Previous']},
          },
        },
      };
    
      const instances = [instance];
      const request = {
        endpoint,
        instances,
        parameters,
      };
    
      // Predict request
      const [response] = await predictionServiceClient.predict(request);
    
      console.log('Predict custom trained model response');
      console.log(`\tDeployed model id : ${response.deployedModelId}`);
      const predictions = response.predictions;
      console.log('\tPredictions :');
      for (const prediction of predictions) {
        console.log(`\t\tPrediction : ${JSON.stringify(prediction)}`);
      }
    }
    predictCustomTrainedModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def endpoint_predict_sample(
        project: str, location: str, instances: list, endpoint: str
    ):
        aiplatform.init(project=project, location=location)
    
        endpoint = aiplatform.Endpoint(endpoint)
    
        prediction = endpoint.predict(instances=instances)
        print(prediction)
        return prediction

### Send an online raw inference request

### gcloud

The following examples use the [`gcloud ai endpoints raw-predict` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/raw-predict) :

  - To request inference with the JSON object in REQUEST specified on the command line:
    
    ``` 
     gcloud ai endpoints raw-predict ENDPOINT_ID \
         --region=LOCATION_ID \
         --request=REQUEST
     
    ```

  - To request inferences with an image stored in the file `image.jpeg` and the appropriate `Content-Type` header:
    
    ``` 
     gcloud ai endpoints raw-predict ENDPOINT_ID \
         --region=LOCATION_ID \
         --http-headers=Content-Type=image/jpeg \
         --request=@image.jpeg
     
    ```
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.
      - REQUEST : The contents of the request that you want to get inferences for. The format of the request depends on what your custom container expects, which may not necessarily be a JSON object.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform_v1
    
    
    def sample_raw_predict():
        # Create a client
        client = aiplatform_v1.PredictionServiceClient()
    
        # Initialize request argument(s)
        request = aiplatform_v1.RawPredictRequest(
            endpoint="endpoint_value",
        )
    
        # Make the request
        response = client.raw_predict(request=request)
    
        # Handle the response
        print(response)

The response includes the following HTTP headers:

  - `X-Vertex-AI-Endpoint-Id` : ID of the `Endpoint` that served this inference.

  - `X-Vertex-AI-Deployed-Model-Id` : ID of the Endpoint's `DeployedModel` that served this inference.

> **Note:** If your container receives requests or sends responses that differ from the guidelines, then the container isn't compatible with [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) or [Gemini Enterprise Agent Platform Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) .

### Send an online explanation request

### gcloud

The following example uses the [`gcloud ai endpoints explain` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/explain) :

1.  Write the following JSON object to file in your local environment. The filename doesn't matter, but for this example, name the file `request.json` .
    
        {
         "instances": INSTANCES
        }
    
    Replace the following:
    
      - INSTANCES : A JSON array of instances that you want to get inferences for. The format of each instance depends on which inputs your trained ML model expects. For more information, see [Formatting your input for online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#formatting-inference-input) .

2.  Run the following command:
    
        gcloud ai endpoints explain ENDPOINT_ID \
          --region=LOCATION_ID \
          --json-request=request.json
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.
    
    Optionally, if you want to send an explanation request to a specific `DeployedModel` on the `Endpoint` , you can specify the `--deployed-model-id` flag:
    
        gcloud ai endpoints explain ENDPOINT_ID \
          --region=LOCATION \
          --deployed-model-id=DEPLOYED_MODEL_ID \
          --json-request=request.json
    
    In addition to the placeholders described previously, replace the following:
    
      - DEPLOYED\_MODEL\_ID Optional: The ID of the deployed model for which you want to get explanations. The ID is included in the `predict` method's response. If you need to request explanations for a particular model and you have more than one model deployed to the same endpoint, you can use this ID to ensure that the explanations are returned for that particular model.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID :
  - ENDPOINT\_ID : The ID for the endpoint.
  - INSTANCES : A JSON array of instances that you want to get inferences for. The format of each instance depends on which inputs your trained ML model expects. For more information, see [Formatting your input for online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions#formatting-inference-input) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:explain

Request JSON body:

    {
      "instances": INSTANCES
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:explain"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:explain" | Select-Object -Expand Content

If successful, you receive a JSON response similar to the following. In the response, expect the following replacements:

  - PREDICTIONS : A JSON array of predictions, one for each instance that you included in the request body.
  - EXPLANATIONS : A JSON array of [explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#Explanation) , one for each prediction.
  - DEPLOYED\_MODEL\_ID : The ID of the [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel) that served the predictions.

<!-- end list -->

    {
      "predictions": PREDICTIONS,
      "explanations": EXPLANATIONS,
      "deployedModelId": "DEPLOYED_MODEL_ID"
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def explain_tabular_sample(
        project: str, location: str, endpoint_id: str, instance_dict: Dict
    ):
    
        aiplatform.init(project=project, location=location)
    
        endpoint = aiplatform.Endpoint(endpoint_id)
    
        response = endpoint.explain(instances=[instance_dict], parameters={})
    
        for explanation in response.explanations:
            print(" explanation")
            # Feature attributions.
            attributions = explanation.attributions
            for attribution in attributions:
                print("  attribution")
                print("   baseline_output_value:", attribution.baseline_output_value)
                print("   instance_output_value:", attribution.instance_output_value)
                print("   output_display_name:", attribution.output_display_name)
                print("   approximation_error:", attribution.approximation_error)
                print("   output_name:", attribution.output_name)
                output_index = attribution.output_index
                for output_index in output_index:
                    print("   output_index:", output_index)
    
        for prediction in response.predictions:
            print(prediction)

### Send an online invoke request

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Invoke route allows access to all non-root request paths in the deployment. For example, `/invoke/foo/bar` will be forwarded as `/foo/bar` to the model server. There are two ways to access the route.

#### custom route request to a dedicated endpoint

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def invoke_tabular_sample(
        project: str,
        location: str,
        endpoint_id: str,
        request_path: str,
        http_request_body: Dict[str, Any],
        stream: bool = False,
    ):
        aiplatform.init(project=project, location=location)
    
        dedicated_endpoint = aiplatform.Endpoint(endpoint_id)
        if stream:
            for chunk in dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
                stream=True,
            ):
                print(chunk)
        else:
            response = dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
            )
            print(response)

#### direct custom route request to deployed model

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def invoke_direct_deployed_model_inference_tabular_sample(
        project: str,
        location: str,
        endpoint_id: str,
        request_path: str,
        http_request_body: Dict[str, Any],
        deployed_model_id: str,
        stream: bool = False,
    ):
        aiplatform.init(project=project, location=location)
    
        dedicated_endpoint = aiplatform.Endpoint(endpoint_id)
        if stream:
            for chunk in dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
                deployed_model_id=deployed_model_id,
                stream=True,
            ):
                print(chunk)
        else:
            response = dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
                deployed_model_id=deployed_model_id,
            )
            print(response)

## What's next

  - Learn about [Online inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging) .
