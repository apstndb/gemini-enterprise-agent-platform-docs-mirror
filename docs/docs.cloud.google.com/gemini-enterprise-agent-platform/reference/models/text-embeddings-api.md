---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api
title: Text embeddings API
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Text embeddings API converts textual data into numerical vectors. These vector representations are designed to capture the semantic meaning and context of the words they represent.

## Supported models

You can get text embeddings by using the following models:

| Model name                        | Description                                                                                                                                                                                                                                                                                                                                        | Output Dimensions | Max sequence length | Supported text languages                                                                                                                                 |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `gemini-embedding-001`            | State-of-the-art performance across English, multilingual and code tasks. It unifies the previously specialized models like `text-embedding-005` and `text-multilingual-embedding-002` and achieves better performance in their respective domains. Read our [Tech Report](https://deepmind.google/research/publications/157741/) for more detail. | up to 3072        | 2048 tokens         | [Supported text languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api#supported_text_languages) |
| `text-embedding-005`              | Specialized in English and code tasks.                                                                                                                                                                                                                                                                                                             | up to 768         | 2048 tokens         | English                                                                                                                                                  |
| `text-multilingual-embedding-002` | Specialized in multilingual tasks.                                                                                                                                                                                                                                                                                                                 | up to 768         | 2048 tokens         | [Supported text languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api#supported_text_languages) |

For superior embedding quality, `gemini-embedding-001` is our large model designed to provide the highest performance.

## Syntax

### curl

    PROJECT_ID = PROJECT_ID
    REGION = us-central1
    MODEL_ID = MODEL_ID
    
    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://${REGION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${REGION}/publishers/google/models/${MODEL_ID}:predict -d \
      '{
        "instances": [
          ...
        ],
        "parameters": {
          ...
        }
      }'

### Python

    PROJECT_ID = PROJECT_ID
    REGION = us-central1
    MODEL_ID = MODEL_ID
    
    import vertexai
    from vertexai.language_models import TextEmbeddingModel
    
    vertexai.init(project=PROJECT_ID, location=REGION)
    
    model = TextEmbeddingModel.from_pretrained(MODEL_ID)
    embeddings = model.get_embeddings(...)

## Parameter list

Top-level fields

`instances`

A list of objects containing the following fields:

  - **`content`**

  - **`title`** (optional)

  - **`task_type`** (optional)

`parameters`

An object containing the following fields:

  - **`autoTruncate`** (optional)

  - **`outputDimensionality`** (optional)

`instance` fields

`content`

`string`

The text that you want to generate embeddings for.

`task_type`

Optional: `string`

Used to convey intended downstream application to help the model produce better embeddings. If left blank, the default used is `RETRIEVAL_QUERY` .

  - `RETRIEVAL_QUERY`
  - `RETRIEVAL_DOCUMENT`
  - `SEMANTIC_SIMILARITY`
  - `CLASSIFICATION`
  - `CLUSTERING`
  - `QUESTION_ANSWERING`
  - `FACT_VERIFICATION`
  - `CODE_RETRIEVAL_QUERY`

For more information about task types, see [Choose an embeddings task type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/task-types) .

`title`

Optional: `string`

Used to help the model produce better embeddings. Only valid with `task_type=RETRIEVAL_DOCUMENT` .

#### `task_type`

The following table describes the `task_type` parameter values and their use cases:

| `task_type`            | Description                                                                                                                       |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `RETRIEVAL_QUERY`      | Specifies the given text is a query in a search or retrieval setting. Use RETRIEVAL\_DOCUMENT for the document side.              |
| `RETRIEVAL_DOCUMENT`   | Specifies the given text is a document in a search or retrieval setting.                                                          |
| `SEMANTIC_SIMILARITY`  | Specifies the given text is used for Semantic Textual Similarity (STS).                                                           |
| `CLASSIFICATION`       | Specifies that the embedding is used for classification.                                                                          |
| `CLUSTERING`           | Specifies that the embedding is used for clustering.                                                                              |
| `QUESTION_ANSWERING`   | Specifies that the query embedding is used for answering questions. Use RETRIEVAL\_DOCUMENT for the document side.                |
| `FACT_VERIFICATION`    | Specifies that the query embedding is used for fact verification. Use RETRIEVAL\_DOCUMENT for the document side.                  |
| `CODE_RETRIEVAL_QUERY` | Specifies that the query embedding is used for code retrieval for Java and Python. Use RETRIEVAL\_DOCUMENT for the document side. |

**Retrieval Tasks** :

Query: Use task\_type= `RETRIEVAL_QUERY` to indicate that the input text is a search query. Corpus: Use task\_type= `RETRIEVAL_DOCUMENT` to indicate that the input text is part of the document collection being searched.

**Similarity Tasks** :

Semantic similarity: Use task\_type= `SEMANTIC_SIMILARITY` for both input texts to assess their overall meaning similarity.

> **Note:** `SEMANTIC_SIMILARITY` is not intended for retrieval use cases, such as document search and information retrieval. For these use cases, use `RETRIEVAL_DOCUMENT` , `RETRIEVAL_QUERY` , `QUESTION_ANSWERING` , and `FACT_VERIFICATION` .

`parameters` fields

`autoTruncate`

Optional: `bool`

When set to true, input text will be truncated. When set to false, an error is returned if the input text is longer than the maximum length supported by the model. Defaults to true.

`outputDimensionality`

Optional: `int`

Used to specify output embedding size. If set, output embeddings will be truncated to the size specified.

### Request body

    {
      "instances": [
        {
          "task_type": "RETRIEVAL_DOCUMENT",
          "title": "document title",
          "content": "I would like embeddings for this text!"
        },
      ]
    }

### Response body

    {
      "predictions": [
        {
          "embeddings": {
            "statistics": {
              "truncated": boolean,
              "token_count": integer
            },
            "values": [ number ]
          }
        }
      ]
    }

Response elements

`predictions`

A list of objects with the following fields:

  - **`embeddings`** : The result generated from input text. Contains the following fields:
    
      - **`values`**
    
      - **`statistics`**

`embeddings` fields

`values`

A list of `float` s. The `values` field contains a numerical encoding (embedding vector) of the semantic content present in the given input text.

`statistics`

The statistics computed from the input text. Contains:

  - **`truncated`** : Indicates whether the input text was truncated due to being longer than the maximum number of tokens allowed by the model.

  - **`token_count`** : Number of tokens of the input text.

#### Sample response

    {
      "predictions": [
        {
          "embeddings": {
            "values": [
              0.0058424929156899452,
              0.011848051100969315,
              0.032247550785541534,
              -0.031829461455345154,
              -0.055369812995195389,
              ...
            ],
            "statistics": {
              "token_count": 4,
              "truncated": false
            }
          }
        }
      ]
    }

## Examples

### Embed a text string

The following example shows how to obtain the embedding of a text string.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - TEXT : The text that you want to generate embeddings for. **Limit:** five texts of up to 2,048 tokens per text for all models except `textembedding-gecko@001` . The max input token length for `textembedding-gecko@001` is 3072. For `gemini-embedding-001` , each request can only include a single input text. For more information, see [Text embedding limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#text-embedding-limits) .
  - AUTO\_TRUNCATE : If set to `false` , text that exceeds the token limit causes the request to fail. The default value is `true` .

HTTP method and URL:

    POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/gemini-embedding-001:predict

Request JSON body:

    {
      "instances": [
        { "content": "TEXT"}
      ],
      "parameters": { 
        "autoTruncate": AUTO_TRUNCATE 
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/gemini-embedding-001:predict"

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
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/gemini-embedding-001:predict" | Select-Object -Expand Content

You should receive a JSON response similar to the following. Note that `values` has been truncated to save space.

#### Response

    {
      "predictions": [
        {
          "embeddings": {
            "statistics": {
              "truncated": false,
              "token_count": 6
            },
            "values": [ ... ]
          }
        }
      ]
    }

Note the following in the URL for this sample:

  - Use the [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.models/generateContent) method to request that the response is returned after it's fully generated. To reduce the perception of latency to a human audience, stream the response as it's being generated by using the [`streamGenerateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.models/streamGenerateContent) method.
  - The multimodal model ID is located at the end of the URL before the method (for example, `gemini-2.5-flash` ). This sample might support other models as well.
  - When you use a regional API endpoint (for example, `us-central1` ), the region from the endpoint URL determines where the request is processed. Any conflicting location in the resource path is ignored.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from __future__ import annotations
    
    from vertexai.language_models import TextEmbeddingInput, TextEmbeddingModel
    
    
    def embed_text() -> list[list[float]]:
        """Embeds texts with a pre-trained, foundational model.
    
        Returns:
            A list of lists containing the embedding vectors for each input text
        """
    
        # A list of texts to be embedded.
        texts = ["banana muffins? ", "banana bread? banana muffins?"]
        # The dimensionality of the output embeddings.
        dimensionality = 3072
        # The task type for embedding. Check the available tasks in the model's documentation.
        task = "RETRIEVAL_DOCUMENT"
    
        model = TextEmbeddingModel.from_pretrained("gemini-embedding-001")
        kwargs = dict(output_dimensionality=dimensionality) if dimensionality else {}
    
        embeddings = []
        # gemini-embedding-001 takes one input at a time
        for text in texts:
            text_input = TextEmbeddingInput(text, task)
            embedding = model.get_embeddings([text_input], **kwargs)
            print(embedding)
            # Example response:
            # [[0.006135190837085247, -0.01462465338408947, 0.004978656303137541, ...]]
            embeddings.append(embedding[0].values)
    
        return embeddings

### Go

Before trying this sample, follow the Go setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "fmt"
     "io"
    
     aiplatform "cloud.google.com/go/aiplatform/apiv1"
     "cloud.google.com/go/aiplatform/apiv1/aiplatformpb"
    
     "google.golang.org/api/option"
     "google.golang.org/protobuf/types/known/structpb"
    )
    
    // embedTexts shows how embeddings are set for gemini-embedding-001 model
    func embedTexts(w io.Writer, project, location string) error {
     // location := "us-central1"
     ctx := context.Background()
    
     apiEndpoint := fmt.Sprintf("%s-aiplatform.googleapis.com:443", location)
     dimensionality := 3072
     model := "gemini-embedding-001"
     texts := []string{"banana muffins? ", "banana bread? banana muffins?"}
    
     client, err := aiplatform.NewPredictionClient(ctx, option.WithEndpoint(apiEndpoint))
     if err != nil {
         return err
     }
     defer client.Close()
    
     endpoint := fmt.Sprintf("projects/%s/locations/%s/publishers/google/models/%s", project, location, model)
     allEmbeddings := make([][]float32, 0, len(texts))
     // gemini-embedding-001 takes 1 input at a time
     for _, text := range texts {
         instances := make([]*structpb.Value, 1)
         instances[0] = structpb.NewStructValue(&structpb.Struct{
             Fields: map[string]*structpb.Value{
                 "content":   structpb.NewStringValue(text),
                 "task_type": structpb.NewStringValue("QUESTION_ANSWERING"),
             },
         })
    
         params := structpb.NewStructValue(&structpb.Struct{
             Fields: map[string]*structpb.Value{
                 "outputDimensionality": structpb.NewNumberValue(float64(dimensionality)),
             },
         })
    
         req := &aiplatformpb.PredictRequest{
             Endpoint:   endpoint,
             Instances:  instances,
             Parameters: params,
         }
         resp, err := client.Predict(ctx, req)
         if err != nil {
             return err
         }
    
         // Process the prediction for the single text
         // The response will contain one prediction because we sent one instance.
         if len(resp.Predictions) == 0 {
             return fmt.Errorf("no predictions returned for text \"%s\"", text)
         }
    
         prediction := resp.Predictions[0]
         embeddingValues := prediction.GetStructValue().Fields["embeddings"].GetStructValue().Fields["values"].GetListValue().Values
    
         currentEmbedding := make([]float32, len(embeddingValues))
         for j, value := range embeddingValues {
             currentEmbedding[j] = float32(value.GetNumberValue())
         }
         allEmbeddings = append(allEmbeddings, currentEmbedding)
     }
    
     if len(allEmbeddings) > 0 {
         fmt.Fprintf(w, "Dimensionality: %d. Embeddings length: %d", len(allEmbeddings[0]), len(allEmbeddings))
     } else {
         fmt.Fprintln(w, "No texts were processed.")
     }
     return nil
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import static java.util.stream.Collectors.toList;
    
    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.PredictRequest;
    import com.google.cloud.aiplatform.v1.PredictResponse;
    import com.google.cloud.aiplatform.v1.PredictionServiceClient;
    import com.google.cloud.aiplatform.v1.PredictionServiceSettings;
    import com.google.protobuf.Struct;
    import com.google.protobuf.Value;
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.List;
    import java.util.OptionalInt;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;
    
    public class PredictTextEmbeddingsSample {
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        // Details about text embedding request structure and supported models are available in:
        // https://cloud.google.com/vertex-ai/docs/generative-ai/embeddings/get-text-embeddings
        String endpoint = "us-central1-aiplatform.googleapis.com:443";
        String project = "YOUR_PROJECT_ID";
        String model = "gemini-embedding-001";
        predictTextEmbeddings(
            endpoint,
            project,
            model,
            List.of("banana bread?", "banana muffins?"),
            "QUESTION_ANSWERING",
            OptionalInt.of(3072));
      }
    
      // Gets text embeddings from a pretrained, foundational model.
      public static List<List<Float>> predictTextEmbeddings(
          String endpoint,
          String project,
          String model,
          List<String> texts,
          String task,
          OptionalInt outputDimensionality)
          throws IOException {
        PredictionServiceSettings settings =
            PredictionServiceSettings.newBuilder().setEndpoint(endpoint).build();
        Matcher matcher = Pattern.compile("^(?<Location>\\w+-\\w+)").matcher(endpoint);
        String location = matcher.matches() ? matcher.group("Location") : "us-central1";
        EndpointName endpointName =
            EndpointName.ofProjectLocationPublisherModelName(project, location, "google", model);
    
        List<List<Float>> floats = new ArrayList<>();
        // You can use this prediction service client for multiple requests.
        try (PredictionServiceClient client = PredictionServiceClient.create(settings)) {
          // gemini-embedding-001 takes one input at a time.
          for (int i = 0; i < texts.size(); i++) {
            PredictRequest.Builder request = 
                PredictRequest.newBuilder().setEndpoint(endpointName.toString());
            if (outputDimensionality.isPresent()) {
              request.setParameters(
                  Value.newBuilder()
                      .setStructValue(
                          Struct.newBuilder()
                              .putFields(
                                  "outputDimensionality", valueOf(outputDimensionality.getAsInt()))
                              .build()));
            }
            request.addInstances(
                Value.newBuilder()
                    .setStructValue(
                        Struct.newBuilder()
                            .putFields("content", valueOf(texts.get(i)))
                            .putFields("task_type", valueOf(task))
                            .build()));
            PredictResponse response = client.predict(request.build());
    
            for (Value prediction : response.getPredictionsList()) {
              Value embeddings = prediction.getStructValue().getFieldsOrThrow("embeddings");
              Value values = embeddings.getStructValue().getFieldsOrThrow("values");
              floats.add(
                  values.getListValue().getValuesList().stream()
                      .map(Value::getNumberValue)
                      .map(Double::floatValue)
                      .collect(toList()));
            }
          }
          return floats;
        }
      }
    
      private static Value valueOf(String s) {
        return Value.newBuilder().setStringValue(s).build();
      }
    
      private static Value valueOf(int n) {
        return Value.newBuilder().setNumberValue(n).build();
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    async function main(
      project,
      model = 'gemini-embedding-001',
      texts = 'banana bread?;banana muffins?',
      task = 'QUESTION_ANSWERING',
      dimensionality = 0,
      apiEndpoint = 'us-central1-aiplatform.googleapis.com'
    ) {
      const aiplatform = require('@google-cloud/aiplatform');
      const {PredictionServiceClient} = aiplatform.v1;
      const {helpers} = aiplatform; // helps construct protobuf.Value objects.
      const clientOptions = {apiEndpoint: apiEndpoint};
      const location = 'us-central1';
      const endpoint = `projects/${project}/locations/${location}/publishers/google/models/${model}`;
    
      async function callPredict() {
        const instances = texts
          .split(';')
          .map(e => helpers.toValue({content: e, task_type: task}));
    
        const client = new PredictionServiceClient(clientOptions);
        const parameters = helpers.toValue(
          dimensionality > 0 ? {outputDimensionality: parseInt(dimensionality)} : {}
        );
        const allEmbeddings = []
        // gemini-embedding-001 takes one input at a time.
        for (const instance of instances) {
          const request = {endpoint, instances: [instance], parameters};
          const [response] = await client.predict(request);
          const predictions = response.predictions;
    
          const embeddings = predictions.map(p => {
            const embeddingsProto = p.structValue.fields.embeddings;
            const valuesProto = embeddingsProto.structValue.fields.values;
            return valuesProto.listValue.values.map(v => v.numberValue);
          });
    
          allEmbeddings.push(embeddings[0])
        }
    
    
        console.log('Got embeddings: \n' + JSON.stringify(allEmbeddings));
      }
    
      callPredict();
    }

## Supported text languages

All text embedding models support and have been evaluated on English-language text. The `text-multilingual-embedding-002` model additionally supports and has been evaluated on the following languages:

  - **Evaluated languages:** `Arabic (ar)` , `Bengali (bn)` , `English (en)` , `Spanish (es)` , `German (de)` , `Persian (fa)` , `Finnish (fi)` , `French (fr)` , `Hindi (hi)` , `Indonesian (id)` , `Japanese (ja)` , `Korean (ko)` , `Russian (ru)` , `Swahili (sw)` , `Telugu (te)` , `Thai (th)` , `Yoruba (yo)` , `Chinese (zh)`
  - **Supported languages** : `Afrikaans` , `Albanian` , `Amharic` , `Arabic` , `Armenian` , `Azerbaijani` , `Basque` , `Belarusiasn` , `Bengali` , `Bulgarian` , `Burmese` , `Catalan` , `Cebuano` , `Chichewa` , `Chinese` , `Corsican` , `Czech` , `Danish` , `Dutch` , `English` , `Esperanto` , `Estonian` , `Filipino` , `Finnish` , `French` , `Galician` , `Georgian` , `German` , `Greek` , `Gujarati` , `Haitian Creole` , `Hausa` , `Hawaiian` , `Hebrew` , `Hindi` , `Hmong` , `Hungarian` , `Icelandic` , `Igbo` , `Indonesian` , `Irish` , `Italian` , `Japanese` , `Javanese` , `Kannada` , `Kazakh` , `Khmer` , `Korean` , `Kurdish` , `Kyrgyz` , `Lao` , `Latin` , `Latvian` , `Lithuanian` , `Luxembourgish` , `Macedonian` , `Malagasy` , `Malay` , `Malayalam` , `Maltese` , `Maori` , `Marathi` , `Mongolian` , `Nepali` , `Norwegian` , `Pashto` , `Persian` , `Polish` , `Portuguese` , `Punjabi` , `Romanian` , `Russian` , `Samoan` , `Scottish Gaelic` , `Serbian` , `Shona` , `Sindhi` , `Sinhala` , `Slovak` , `Slovenian` , `Somali` , `Sotho` , `Spanish` , `Sundanese` , `Swahili` , `Swedish` , `Tajik` , `Tamil` , `Telugu` , `Thai` , `Turkish` , `Ukrainian` , `Urdu` , `Uzbek` , `Vietnamese` , `Welsh` , `West Frisian` , `Xhosa` , `Yiddish` , `Yoruba` , `Zulu` .

The `gemini-embedding-001` model supports the following languages:

`Arabic` , `Bengali` , `Bulgarian` , `Chinese (Simplified and Traditional)` , `Croatian` , `Czech` , `Danish` , `Dutch` , `English` , `Estonian` , `Finnish` , `French` , `German` , `Greek` , `Hebrew` , `Hindi` , `Hungarian` , `Indonesian` , `Italian` , `Japanese` , `Korean` , `Latvian` , `Lithuanian` , `Norwegian` , `Polish` , `Portuguese` , `Romanian` , `Russian` , `Serbian` , `Slovak` , `Slovenian` , `Spanish` , `Swahili` , `Swedish` , `Thai` , `Turkish` , `Ukrainian` , `Vietnamese` , `Afrikaans` , `Amharic` , `Assamese` , `Azerbaijani` , `Belarusian` , `Bosnian` , `Catalan` , `Cebuano` , `Corsican` , `Welsh` , `Dhivehi` , `Esperanto` , `Basque` , `Persian` , `Filipino (Tagalog)` , `Frisian` , `Irish` , `Scots Gaelic` , `Galician` , `Gujarati` , `Hausa` , `Hawaiian` , `Hmong` , `Haitian Creole` , `Armenian` , `Igbo` , `Icelandic` , `Javanese` , `Georgian` , `Kazakh` , `Khmer` , `Kannada` , `Krio` , `Kurdish` , `Kyrgyz` , `Latin` , `Luxembourgish` , `Lao` , `Malagasy` , `Maori` , `Macedonian` , `Malayalam` , `Mongolian` , `Meiteilon (Manipuri)` , `Marathi` , `Malay` , `Maltese` , `Myanmar (Burmese)` , `Nepali` , `Nyanja (Chichewa)` , `Odia (Oriya)` , `Punjabi` , `Pashto` , `Sindhi` , `Sinhala (Sinhalese)` , `Samoan` , `Shona` , `Somali` , `Albanian` , `Sesotho` , `Sundanese` , `Tamil` , `Telugu` , `Tajik` , `Uyghur` , `Urdu` , `Uzbek` , `Xhosa` , `Yiddish` , `Yoruba` , `Zulu` .

## Model versions

To use a current stable model, specify the model version number, for example `gemini-embedding-001` . Specifying a model without a version number, isn't recommended, as it is merely a legacy pointer to another model and isn't stable.

For more information, see [Model versions and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-versions) .

## What's next

For detailed documentation, see the following:

  - [Text Embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings)
