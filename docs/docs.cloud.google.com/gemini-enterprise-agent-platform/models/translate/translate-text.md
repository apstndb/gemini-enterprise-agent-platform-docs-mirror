---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/translate/translate-text
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/translate/translate-text
title: Translate text
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

For translation tasks, Generative AI on Gemini Enterprise Agent Platform offers two specialized translation models from the Cloud Translation API:

  - **Translation LLM** - Google's newest highest quality LLM-style translation offering. Achieves the highest quality translation while serving at reasonable latencies (\~3x faster than Gemini 2.0 Flash).

  - **Cloud Translation Neural Machine Translation (NMT) model** - Google's premier real-time translation offering achieving \~100ms latency translations. It achieves the highest quality of all models benchmarked serving at comparable latencies and continues to see ongoing quality advancements. NMT can achieve latencies up to 20x faster than Gemini 2.0 Flash.

## Key advantages & differentiators of the Translation LLM

  - **Unmatched Translation Quality** - Translation LLM offers the highest translation quality achieving significantly higher performance on benchmarks compared to other benchmarked models. Translation LLM is **far more likely to significantly rewrite a sentence to make it sound more natural** in the target language, rather than giving less natural "word-for-word" translations that are often seen in other translation models.
  - **Superior Quality/Latency Trade off -** Translation LLM provides LLM-powered translations at latencies significantly better than Gemini 2.0 Flash. Although Translation LLM has higher latencies than the NMT model, it typically provides higher quality responses for a broad range of applications.

## Model feature comparison

| Feature              | Translation LLM (Powered by Gemini)                                                                                                                                                                                                                                                                                                            | NMT model                                                                                                                                                                                                                                                                                     |
| :------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Description          | A translation-specialized Large Language Model powered by Gemini, fine-tuned for translation. Available with Generative AI on Gemini Enterprise Agent Platform and the Cloud Translation - Advanced API.                                                                                                                                       | Google's Neural Machine Translation model, available through Cloud Translation - Advanced and Cloud Translation - Basic APIs . Optimized for simplicity and scale.                                                                                                                            |
| Quality              | **Highest quality** translation. Outperforms NMT, Gemini 2.0 Flash, and Gemini 2.5 Pro in quality. More likely to rewrite sentences for natural flow. Shows significant error reduction.                                                                                                                                                       | Medium to high quality depending on the language pair. Among the best-performing real-time NMT models for many language-domain combinations.                                                                                                                                                  |
| Latency              | Latency is significantly better than Gemini 2.0 Flash, but still slower than NMT.                                                                                                                                                                                                                                                              | **Fastest Real Time Translation** . Low latency, suitable for chat and real-time applications. Achieves latencies up to 20x faster than Gemini 2.0 Flash                                                                                                                                      |
| Language support     | Supported languages include Arabic, Chinese, Czech, Dutch, English, French, German, Hindi, Indonesian, Italian, Japanese, Korean, Polish, Portuguese, Russian, Spanish, Thai, Turkish, Ukrainian, and Vietnamese. Refer to [supported languages](https://docs.cloud.google.com/translate/docs/languages#adaptive_translation) for a full list. | Supports languages include Cantonese, Fijian, and Balinese. Translations from any language to any other language in the supported list are possible. Refer to [supported languages](https://docs.cloud.google.com/translate/docs/languages#neural_machine_translation_model) for a full list. |
| Customization        | Support for - **Advanced Glossaries** , **Supervised Fine-tuning** on Gemini Enterprise Agent Platform for domain/customer-specific adaptations, **Adaptive translation** for real-time style customization with a few examples.                                                                                                               | Support for - **Glossaries** to control terminology, and training **Custom Models** with AutoML Translation in Cloud Translation - Advanced API.                                                                                                                                              |
| Translation features | HTML translation                                                                                                                                                                                                                                                                                                                               | HTML, Batch, and Formatted document translation                                                                                                                                                                                                                                               |
| API Integration      | Cloud Translation - Advanced API, Gemini Enterprise API                                                                                                                                                                                                                                                                                        | Cloud Translation - Basic API, Cloud Translation - Advanced API, Gemini Enterprise API                                                                                                                                                                                                        |

## Usage

This section shows you how to use Gemini Enterprise Agent Platform Studio to rapidly translate text from one language to another. You can use the Translation LLM or the NMT model to translate text by using the Google Cloud console or API. Note that the languages that each model supports can vary. Before you request translations, check that the model you're using [supports your source and target languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/translate/translate-text#supported-languages) .

### Console

1.  In the Agent Platform section of the Google Cloud console, go to the **Translate text** page in **Gemini Enterprise Agent Platform Studio** .

2.  In the **Run settings** pane, select a translation model in the **Model** field.

3.  To change the model settings (such as temperature), expand **Advanced** .

4.  Set the source and target languages.

5.  In the input field, enter the text to translate.

6.  Click **Submit** .

7.  To get the code or curl command that demonstrate how to request translations, click code **Get code** .

Note that in Gemini Enterprise Agent Platform Studio, the Translation LLM lets you provide example translations to tailor model responses to more closely match your style, tone, and industry domain. The model uses your examples as few-shot context before translating your text.

### API

Select the model to use for your translations.

### Translation LLM

Use the Agent Platform API and Translation LLM to translate text.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_NUMBER\_OR\_ID : The numeric or alphanumeric ID of your Google Cloud project
  - LOCATION : The location where you want to run this operation. For example, `us-central1` .
  - SOURCE\_LANGUAGE\_CODE : The language code of the input text. Set to one of the language codes listed in [adaptive translation](https://docs.cloud.google.com/translate/docs/languages#adaptive_translation) .
  - TARGET\_LANGUAGE\_CODE : The target language to translate the input text to. Set to one of the language codes listed in [adaptive translation](https://docs.cloud.google.com/translate/docs/languages#adaptive_translation) .
  - SOURCE\_TEXT : Text in the source language to translate.
  - MIME\_TYPE (Optional): The format of the source text, such as `text/html` or `text/plain` . By default, the MIME type is set to `text/plain` .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/cloud-translate-text:predict

Request JSON body:

    {
      "instances": [
        {
          "source_language_code": "SOURCE_LANGUAGE_CODE",
          "target_language_code": "TARGET_LANGUAGE_CODE",
          "contents": [
            "SOURCE_TEXT"
          ],
          "mimeType": "MIME_TYPE",
          "model": "projects/PROJECT_ID/locations/LOCATION/models/general/translation-llm"
        }
      ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "x-goog-user-project: PROJECT_NUMBER_OR_ID" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/cloud-translate-text:predict"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred"; "x-goog-user-project" = "PROJECT_NUMBER_OR_ID" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/cloud-translate-text:predict" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "predictions": [
        {
          "translations": [
            {
              "translatedText": "TRANSLATED_TEXT",
              "model": "projects/PROJECT_ID/locations/LOCATION/models/general/translation-llm"
            }
          ]
        }
      ]
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

``` 
async function translate() {
  const request = {
    instances: [{
      source_language_code: SOURCE_LANGUAGE_CODE,
      target_language_code: TARGET_LANGUAGE_CODE,
      contents: [SOURCE_TEXT],
      model: "projects/PROJECT_ID/locations/LOCATION/models/general/translation-llm"
    }]
  };
  const {google} = require('googleapis');
  const aiplatform = google.cloud('aiplatform');
  const endpoint = aiplatform.predictionEndpoint('projects/PROJECT_ID/locations/LOCATION/publishers/google/models/cloud-translate-text');

  const [response] = await endpoint.predict(request)
  console.log('Translating')
  console.log(response)
}
      
```

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

``` 
from google.cloud import aiplatform

def translate():
  # Create a client
  client_options = {"api_endpoint": "LOCATION-aiplatform.googleapis.com"}
  client = aiplatform.gapic.PredictionServiceClient(client_options=client_options)
  
  # Initialize the request
  endpoint_id = f"projects/PROJECT_ID/locations/LOCATION/publishers/google/models/cloud-translate-text"
  instances=[{
    "model": "projects/PROJECT_ID/locations/LOCATION/models/general/translation-llm",
    "source_language_code": 'SOURCE_LANGUAGE_CODE',
    "target_language_code": 'TARGET_LANGUAGE_CODE',
    "contents": ["SOURCE_TEXT"],
  }]

  # Make the request
  response = client.predict(instances=instances, endpoint=endpoint_id)
  # Handle the response
  print(response)
      
```

### NMT

Use the Cloud Translation API and the NMT model to translate text.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_NUMBER\_OR\_ID : the numeric or alphanumeric ID of your Google Cloud project.
  - SOURCE\_LANGUAGE : (Optional) The language code of the input text. For supported language codes, see [Language support](https://docs.cloud.google.com/translate/docs/languages) .
  - TARGET\_LANGUAGE : The target language to translate the input text to. Set to one of the supported [language codes](https://docs.cloud.google.com/translate/docs/languages) .
  - SOURCE\_TEXT : The text to translate.

HTTP method and URL:

    POST https://translation.googleapis.com/v3/projects/PROJECT_ID:translateText

Request JSON body:

    {
      "sourceLanguageCode": "SOURCE_LANGUAGE",
      "targetLanguageCode": "TARGET_LANGUAGE",
      "contents": ["SOURCE_TEXT1", "SOURCE_TEXT2"]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "x-goog-user-project: PROJECT_NUMBER_OR_ID" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://translation.googleapis.com/v3/projects/PROJECT_ID:translateText"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred"; "x-goog-user-project" = "PROJECT_NUMBER_OR_ID" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://translation.googleapis.com/v3/projects/PROJECT_ID:translateText" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "translations": [
        {
          "translatedText": "TRANSLATED_TEXT1"
        },
        {
          "translatedText": "TRANSLATED_TEXT2"
        }
      ]
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample
     */
    // const projectId = 'YOUR_PROJECT_ID';
    // const location = 'global';
    // const text = 'text to translate';
    
    // Imports the Google Cloud Translation library
    const {TranslationServiceClient} = require('@google-cloud/translate');
    
    // Instantiates a client
    const translationClient = new TranslationServiceClient();
    
    async function translateText() {
      // MIME type of the content to translate
      // Supported MIME types:
      // https://cloud.google.com/translate/docs/supported-formats
      const mimeType = 'text/plain';
    
      // Construct request
      const request = {
        parent: `projects/${projectId}/locations/${location}`,
        contents: [text],
        mimeType: mimeType,
        sourceLanguageCode: 'en',
        targetLanguageCode: 'sr-Latn',
      };
    
      // Run request
      const [response] = await translationClient.translateText(request);
    
      for (const translation of response.translations) {
        console.log(`Translation: ${translation.translatedText}`);
      }
    }
    
    translateText();

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import os
    
    # Import the Google Cloud Translation library.
    from google.cloud import translate_v3
    
    PROJECT_ID = os.environ.get("GOOGLE_CLOUD_PROJECT")
    
    
    def translate_text(
        text: str = "YOUR_TEXT_TO_TRANSLATE",
        source_language_code: str = "en-US",
        target_language_code: str = "fr",
    ) -> translate_v3.TranslationServiceClient:
        """Translate Text from a Source language to a Target language.
        Args:
            text: The content to translate.
            source_language_code: The code of the source language.
            target_language_code: The code of the target language.
                For example: "fr" for French, "es" for Spanish, etc.
                Find available languages and codes here:
                https://cloud.google.com/translate/docs/languages#neural_machine_translation_model
        """
    
        # Initialize Translation client.
        client = translate_v3.TranslationServiceClient()
        parent = f"projects/{PROJECT_ID}/locations/global"
    
        # MIME type of the content to translate.
        # Supported MIME types:
        # https://cloud.google.com/translate/docs/supported-formats
        mime_type = "text/plain"
    
        # Translate text from the source to the target language.
        response = client.translate_text(
            contents=[text],
            parent=parent,
            mime_type=mime_type,
            source_language_code=source_language_code,
            target_language_code=target_language_code,
        )
    
        # Display the translation for the text.
        # For example, for "Hello! How are you doing today?":
        # Translated text: Bonjour comment vas-tu aujourd'hui?
        for translation in response.translations:
            print(f"Translated text: {translation.translated_text}")
    
        return response

## Custom translations

Customize responses from the Translation LLM by providing your own example translations. Custom translations only work with the Translation LLM.

You can request customized translation through the Gemini Enterprise Agent Platform Studio console or API with one difference. The console supports custom translations only when you provide examples in a TMX or TSV file. The API supports custom translations only when you provide examples (up to 5 sentence pairs) inline as part of the translation request.

### Data requirements

If you provide example translations in a file for the Google Cloud console, the examples must be written as segment pairs in a TMX or TSV file. Each pair includes a source language segment and its translated counterpart. For more information, see [Prepare example translations](https://docs.cloud.google.com/translate/docs/advanced/custom-translations#file-prep) in the Cloud Translation documentation.

To get the most accurate results, include specific examples from a wide variety of scenarios. You must include at least five sentence pairs but no more than 10,000 pairs. Also, a segment pair can be at most a total of 512 characters.

### Console

1.  In the Agent Platform section of the Google Cloud console, go to the **Translate text** page in **Gemini Enterprise Agent Platform Studio** .

2.  In the **Run settings** pane, configure your translation settings.
    
    1.  In the **Model** field, select **Translation LLM** .
    2.  To change the temperature, expand **Advanced** .

3.  Click **Add examples** .
    
    1.  Select a local file or a file from Cloud Storage. Gemini Enterprise Agent Platform Studio determines the source and target languages from your file.
    2.  Select the number of examples for the model to use before generating a response.
    
    The number of examples you select counts toward the input character limit per request of 3,000.

4.  In the input field, enter the text to translate.

5.  Click **Submit** .
    
    Agent Platform automatically selects your specified number of reference sentences that are most similar to your input. The translation model identifies patterns from your examples and then applies those patterns when generating a response.
    
    The output limit per request is 3,000 characters. Any text beyond this limit is dropped.

6.  To get the code or curl command that demonstrate how to request translations, click code **Get code** .

### API

To request custom translations, include up to five reference sentence pairs in your translation request. The translation model uses all of them to identify patterns from your examples and then applies those patterns when generating a response.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_NUMBER\_OR\_ID : The numeric or alphanumeric ID of your Google Cloud project
  - LOCATION : The location where you want to run this operation. For example, `us-central1` .
  - REFERENCE\_SOURCE : A sentence in the source language that is part of a reference sentence pair.
  - REFERENCE\_TARGET : A sentence in the target language that is part of a reference sentence pair.
  - SOURCE\_LANGUAGE : The language code of the input text.
  - TARGET\_LANGUAGE : The target language to translate the input text to.
  - SOURCE\_TEXT : Text in the source language to translate.
  - MIME\_TYPE (Optional): The format of the source text, such as `text/html` or `text/plain` . By default, the MIME type is set to `text/plain` .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/translate-llm:predict

Request JSON body:

    {
      "instances": [
        {
          "reference_sentence_config": {
            "reference_sentence_pair_lists": [
              {
                "reference_sentence_pairs": [
                  {
                    "source_sentence": "REFERENCE_SOURCE_1_1",
                    "target_sentence": "REFERENCE_TARGET_1_1"
                  },
                  {
                    "source_sentence": "REFERENCE_SOURCE_1_2",
                    "target_sentence": "REFERENCE_SOURCE_1_2"
                  }
                ]
              }
            ],
            "source_language_code": "SOURCE_LANGUAGE_CODE",
            "target_language_code": "TARGET_LANGUAGE_CODE"
          },
          "content": [
            "SOURCE_TEXT"
          ],
          "mimeType": "MIME_TYPE"
        }
      ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "x-goog-user-project: PROJECT_NUMBER_OR_ID" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/translate-llm:predict"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred"; "x-goog-user-project" = "PROJECT_NUMBER_OR_ID" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/translate-llm:predict" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "predictions": [
        {
          "languageCode": "TARGET_LANGUAGE",
          "translations": [
            {
              "translatedText": "TRANSLATED_TEXT"
            }
          ]
        }
      ]
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

``` 
async function translate() {
  const request = {
    instances: [{
        "reference_sentence_config": {
          "reference_sentence_pair_lists": [{
            "reference_sentence_pairs": [{
              "source_sentence": 'SAMPLE_REFERENCE_SOURCE_1',
              "target_sentence": 'SAMPLE_REFERENCE_TARGET_1'
            },
            "reference_sentence_pairs": {
              "source_sentence": 'SAMPLE_REFERENCE_SOURCE_2',
              "target_sentence": 'SAMPLE_REFERENCE_TARGET_2'
            }]
          }],
          "source_language_code": 'SOURCE_LANGUAGE_CODE',
          "target_language_code": 'TARGET_LANGUAGE_CODE'
        },
        "contents": ["SOURCE_TEXT"]
    }]
  };
  const {google} = require('googleapis');
  const aiplatform = google.cloud('aiplatform');
  const endpoint = aiplatform.predictionEndpoint('projects/PROJECT_ID/locations/LOCATION/publishers/google/models/translate-llm');

  const [response] = await endpoint.predict(request)
  console.log('Translating')
  console.log(response)
}
  
```

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

``` 
from google.cloud import aiplatform
from google.protobuf.json_format import MessageToDict

def translate():
  # Create a client
  client_options = {"api_endpoint": "LOCATION-aiplatform.googleapis.com"}
  client = aiplatform.gapic.PredictionServiceClient(client_options=client_options)

  # Initialize the request
  endpoint_id = f"projects/PROJECT_ID/locations/LOCATION/publishers/google/models/translate-llm"
  instances=[{
      "reference_sentence_config": {
        "reference_sentence_pair_lists": [{
          "reference_sentence_pairs": [{
            "source_sentence": 'SAMPLE_REFERENCE_SOURCE_1',
            "target_sentence": 'SAMPLE_REFERENCE_TARGET_1'
          },
          {
            "source_sentence": 'SAMPLE_REFERENCE_SOURCE_2',
            "target_sentence": 'SAMPLE_REFERENCE_TARGET_2'
          }]
        }],
        "source_language_code": 'SOURCE_LANGUAGE_CODE',
        "target_language_code": 'TARGET_LANGUAGE_CODE'
      },
      "content": ["SOURCE_TEXT"]
  }]
  # Make the request
  response = client.predict(
      endpoint=endpoint_id, instances=instances,
  )
  # Handle the response
  print(response)

  # The predictions are a google.protobuf.Value representation of the model's predictions.
  predictions = MessageToDict(response._pb)['predictions']
  for prediction in predictions:
      print(prediction['translations'])
  
```

You can also use the Cloud Translation API to create a dataset and import your example sentence pairs. When you use the Cloud Translation API to request translations, you can include your dataset to customize responses. The dataset persists and can be reused with multiple translation requests. For more information, see [Request adaptive translations](https://docs.cloud.google.com/translate/docs/advanced/adaptive-translation#api) in the Cloud Translation documentation.

## Supported languages

### Translation LLM

With the Translation LLM, you can translate to and from any of the following languages.

| Language name            | Language code |
| ------------------------ | ------------- |
| Afrikaans                | `af`          |
| Albanian                 | `sq`          |
| Amharic                  | `am`          |
| Arabic (Saudi Arabia)    | `ar-SA`       |
| Arabic                   | `ar`          |
| Armenian                 | `hy`          |
| Azerbaijani              | `az`          |
| Basque                   | `eu`          |
| Belarusian               | `be`          |
| Bengali (India)          | `bn-IN`       |
| Bengali                  | `bn`          |
| Bosnian (Cyrillic)       | `bs-Cyrl`     |
| Bosnian                  | `bs`          |
| Bulgarian                | `bg`          |
| Burmese                  | `my`          |
| Catalan                  | `ca`          |
| Chinese (China)          | `zh-CN`       |
| Chinese (Hong Kong)      | `zh-HK`       |
| Chinese (Simplified)     | `zh-Hans`     |
| Chinese (Taiwan)         | `zh-TW`       |
| Chinese (Traditional)    | `zh-Hant`     |
| Chinese                  | `zh`          |
| Croatian                 | `hr`          |
| Czech                    | `cs`          |
| Danish                   | `da`          |
| Dutch (Belgium)          | `nl-BE`       |
| Dutch                    | `nl`          |
| English (Australia)      | `en-AU`       |
| English (Canada)         | `en-CA`       |
| English (New Zealand)    | `en-NZ`       |
| English (Philippines)    | `en-PH`       |
| English (South Africa)   | `en-ZA`       |
| English (United Kingdom) | `en-GB`       |
| English (United States)  | `en-US`       |
| English                  | `en`          |
| Estonian                 | `et`          |
| Filipino                 | `fil`         |
| Finnish                  | `fi`          |
| French (Canada)          | `fr-CA`       |
| French (Switzerland)     | `fr-CH`       |
| French                   | `fr`          |
| Frisian                  | `fy`          |
| Galician                 | `gl`          |
| Georgian                 | `ka`          |
| German                   | `de`          |
| Greek                    | `el`          |
| Guarani                  | `gn`          |
| Gujarati                 | `gu`          |
| Hausa                    | `ha`          |
| Hebrew                   | `he`          |
| Hebrew                   | `iw`          |
| Hindi                    | `hi`          |
| Hungarian                | `hu`          |
| Icelandic                | `is`          |
| Igbo                     | `ig`          |
| Indonesian               | `id`          |
| Irish                    | `ga`          |
| Italian                  | `it`          |
| Japanese                 | `ja`          |
| Kannada                  | `kn`          |
| Khmer                    | `km`          |
| Korean                   | `ko`          |
| Kyrgyz                   | `ky`          |
| Lao                      | `lo`          |
| Latvian                  | `lv`          |
| Lingala                  | `ln`          |
| Lithuanian               | `lt`          |
| Luxembourgish            | `lb`          |
| Macedonian               | `mk`          |
| Malay                    | `ms`          |
| Malayalam                | `ml`          |
| Maltese                  | `mt`          |
| Marathi                  | `mr`          |
| Mongolian                | `mn`          |
| Nepali                   | `ne`          |
| Norwegian Bokmal         | `nb`          |
| Norwegian                | `no`          |
| Odia                     | `or`          |
| Persian                  | `fa`          |
| Polish                   | `pl`          |
| Portuguese (Brazil)      | `pt-BR`       |
| Portuguese (Portugal)    | `pt-PT`       |
| Portuguese               | `pt`          |
| Punjabi (Pakistan)       | `pa-PK`       |
| Punjabi                  | `pa`          |
| Romanian                 | `ro`          |
| Russian                  | `ru`          |
| Scots Gaelic             | `gd`          |
| Serbian                  | `sr`          |
| Slovak                   | `sk`          |
| Slovenian                | `sl`          |
| Somali                   | `so`          |
| Spanish (Argentina)      | `es-AR`       |
| Spanish (Chile)          | `es-CL`       |
| Spanish (Colombia)       | `es-CO`       |
| Spanish (Costa Rica)     | `es-CR`       |
| Spanish (Ecuador)        | `es-EC`       |
| Spanish (El Salvador)    | `es-SV`       |
| Spanish (Guatemala)      | `es-GT`       |
| Spanish (Haiti)          | `es-HT`       |
| Spanish (Honduras)       | `es-HN`       |
| Spanish (Latin America)  | `es-419`      |
| Spanish (Mexico)         | `es-MX`       |
| Spanish (Nicaragua)      | `es-NI`       |
| Spanish (Panama)         | `es-PA`       |
| Spanish (Paraguay)       | `es-PY`       |
| Spanish (Peru)           | `es-PE`       |
| Spanish (Puerto Rico)    | `es-PR`       |
| Spanish (Spain)          | `es-ES`       |
| Spanish (United States)  | `es-US`       |
| Spanish (Uruguay)        | `es-UY`       |
| Spanish (Venezuela)      | `es-VE`       |
| Spanish                  | `es`          |
| Swahili                  | `sw`          |
| Swedish                  | `sv`          |
| Tagalog                  | `tl`          |
| Tajik                    | `tg`          |
| Tamil                    | `ta`          |
| Telugu                   | `te`          |
| Thai                     | `th`          |
| Turkish                  | `tr`          |
| Ukrainian                | `uk`          |
| Urdu                     | `ur`          |
| Uzbek                    | `uz`          |
| Vietnamese               | `vi`          |
| Welsh                    | `cy`          |
| Zulu                     | `zu`          |

### NMT

For information about which languages the the Cloud Translation NMT model support, refer to the following documentation:

  - [Translation NMT model language support](https://docs.cloud.google.com/translate/docs/languages#neural_machine_translation_model)
