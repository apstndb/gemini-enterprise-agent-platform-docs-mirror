---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/grounding
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/grounding
title: Grounding API
description: Understand grounding in generative AI. Connect model output to verifiable sources using Google Search, Google Maps, RAG Engine on Gemini Enterprise Agent Platform, or Agent Search.
data_source: docs.cloud.google.com
---

In generative AI, grounding is the ability to connect model output to verifiable sources of information. If you provide models with access to specific data sources, then grounding tethers their output to these data and reduces the chances of inventing content.

With Gemini Enterprise Agent Platform, you can ground model outputs in the following ways:

  - Ground with Google Search - ground a model with publicly-available web data.
  - Ground with Google Maps - ground a model with geospatial data from Google Maps.
  - Ground to your data - ground a model with your data from Agent Search as a data store.

For more information about grounding, see [Grounding overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview) .

## Supported models

#### Click to expand supported models

  - [Gemini 3 Pro Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)
  - [Gemini 3.1 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)
  - [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
  - [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
  - [Gemini 3.1 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image) preview
  - [Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro) preview
  - [Gemini 3 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash) preview
  - [Gemini 3 Pro Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image-preview) preview
  - [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash) preview
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite) preview
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
  - [Gemini 2.5 Flash with Gemini Live API native audio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api)

## Parameter list

See [examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/grounding#examples) for implementation details.

#### `googleSearch`

Ground the response with publicly-available web data from Google Search.

#### `googleMaps`

Ground the response with publicly-available geospatial data from Google Maps.

The API input includes the following parameter:

Input parameter

`enable_widget`

Required: `boolean`

Flag that can be set to `true` or `false` . A value of `true` returns a token using the API response that you can use with the Google Maps context widget user interface.

The API response structure includes the following parameter:

Response parameter

`grounding_metadata`

Required: `Object`

The primary field that contains grounding information.

**`grounding_support`** : A sub-field indicating the level of grounding support.

**`grounding_chunks.maps`** : A sub-field containing the places sources used to generate the grounded response.

  - **`place_answer_sources.review_snippets`** : A sub-field within `grounding_chunks.maps` that appears when a place answer is used to answer a query. Place answers provide deeper contextual information about a specific place using data, such as user reviews. The place answer is backed by a list of sources like user reviews.

#### Attributes

A place or user review source has the following attributes:

Attributes

`title`

Required: `Object`

The title of the source.

`uri`

Required: `string`

A URI linking to the source.

`place_id`

Required: `string`

A unique identifier for the place.

`review_id`

Required: `string`

A unique identifier for review.

#### `retrieval`

Ground the response with private data from Agent Search as a data store. Defines a retrieval tool that the model can call to access external knowledge.

Parameters

`vertexAiSearch`

Required: `VertexAISearch`

Ground with Agent Search data sources.

#### `VertexAISearch`

Parameters

`datastore`

Required: `string`

Fully-qualified data store resource ID from Agent Search, in the following format: `projects/{project}/locations/{location}/collections/default_collection/dataStores/{datastore}`

## Examples

This section provides examples for grounding a response on public web data using Google Search and grounding a response on private data using Agent Search.

### Ground response on public web data using Google Search

Ground the response with Google Search public data. Include the `google_search_retrieval` tool in the request. No additional parameters are required.

### Python

#### Install

    pip install --upgrade google-genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    from google import genai
    from google.genai.types import (
        GenerateContentConfig,
        GoogleSearch,
        HttpOptions,
        Tool,
    )
    
    client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents="When is the next total solar eclipse in the United States?",
        config=GenerateContentConfig(
            tools=[
                # Use Google Search Tool
                Tool(
                    google_search=GoogleSearch(
                        # Optional: Domains to exclude from results
                        exclude_domains=["domain.com", "domain2.com"]
                    )
                )
            ],
        ),
    )
    
    print(response.text)
    # Example response:
    # 'The next total solar eclipse in the United States will occur on ...'

### Go

Learn how to install or update the [Go](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://pkg.go.dev/google.golang.org/genai) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    import (
        "context"
        "fmt"
        "io"
    
        genai "google.golang.org/genai"
    )
    
    // generateWithGoogleSearch shows how to generate text using Google Search.
    func generateWithGoogleSearch(w io.Writer) error {
        ctx := context.Background()
    
        client, err := genai.NewClient(ctx, &genai.ClientConfig{
            HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
        })
        if err != nil {
            return fmt.Errorf("failed to create genai client: %w", err)
        }
    
        modelName := "gemini-2.5-flash"
        contents := []*genai.Content{
            {Parts: []*genai.Part{
                {Text: "When is the next total solar eclipse in the United States?"},
            },
                Role: genai.RoleUser},
        }
        config := &genai.GenerateContentConfig{
            Tools: []*genai.Tool{
                {GoogleSearch: &genai.GoogleSearch{ExcludeDomains: []string{"example.com", "example.org"}}},
            },
        }
    
        resp, err := client.Models.GenerateContent(ctx, modelName, contents, config)
        if err != nil {
            return fmt.Errorf("failed to generate content: %w", err)
        }
    
        respText := resp.Text()
    
        fmt.Fprintln(w, respText)
    
        // Example response:
        // The next total solar eclipse in the United States will occur on March 30, 2033, but it will only ...
    
        return nil
    }

### Java

Learn how to install or update the [Java](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://central.sonatype.com/artifact/com.google.genai/google-genai) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    import com.google.genai.Client;
    import com.google.genai.types.GenerateContentConfig;
    import com.google.genai.types.GenerateContentResponse;
    import com.google.genai.types.GoogleSearch;
    import com.google.genai.types.HttpOptions;
    import com.google.genai.types.Tool;
    
    public class ToolsGoogleSearchWithText {
    
      public static void main(String[] args) {
        // TODO(developer): Replace these variables before running the sample.
        String modelId = "gemini-2.5-flash";
        generateContent(modelId);
      }
    
      // Generates content with Google Search tool
      public static String generateContent(String modelId) {
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests.
        try (Client client =
            Client.builder()
                .location("global")
                .vertexAI(true)
                .httpOptions(HttpOptions.builder().apiVersion("v1").build())
                .build()) {
    
          // Create a GenerateContentConfig and set Google Search tool
          GenerateContentConfig contentConfig =
              GenerateContentConfig.builder()
                  .tools(Tool.builder().googleSearch(GoogleSearch.builder().build()).build())
                  .build();
    
          GenerateContentResponse response =
              client.models.generateContent(
                  modelId, "When is the next total solar eclipse in the United States?", contentConfig);
    
          System.out.print(response.text());
          // Example response:
          // The next total solar eclipse in the United States will occur on...
          return response.text();
        }
      }
    }

### Node.js

#### Install

    npm install @google/genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/js-genai/) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    const {GoogleGenAI} = require('@google/genai');
    
    const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
    const GOOGLE_CLOUD_LOCATION = process.env.GOOGLE_CLOUD_LOCATION || 'global';
    
    async function generateGoogleSearch(
      projectId = GOOGLE_CLOUD_PROJECT,
      location = GOOGLE_CLOUD_LOCATION
    ) {
      const client = new GoogleGenAI({
        vertexai: true,
        project: projectId,
        location: location,
      });
    
      const response = await client.models.generateContent({
        model: 'gemini-2.5-flash',
        contents: 'When is the next total solar eclipse in the United States?',
        config: {
          tools: [
            {
              googleSearch: {},
            },
          ],
        },
      });
    
      console.log(response.text);
    
      // Example response:
      //    'The next total solar eclipse in United States will occur on ...'
    
      return response.text;
    }

### Ground response on private data using Agent Search

Ground the response with data from a Agent Search data store. For more information, see [Agent Search](https://docs.cloud.google.com/generative-ai-app-builder/docs) .

Before you ground a response with private data, [create a data store](https://docs.cloud.google.com/generative-ai-app-builder/docs/create-data-store-es) and a [search app](https://docs.cloud.google.com/generative-ai-app-builder/docs/create-engine-es) .

WARNING: For the time being, this "grounding" interface does not support Agent Search "chunk mode".

### Gen AI SDK for Python

    from google import genai
    from google.genai.types import (
        GenerateContentConfig,
        HttpOptions,
        Retrieval,
        Tool,
        VertexAISearch,
    )
    
    client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
    # Load Data Store ID from Vertex AI Search
    # datastore = "projects/111111111111/locations/global/collections/default_collection/dataStores/data-store-id"
    
    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents="How do I make an appointment to renew my driver's license?",
        config=GenerateContentConfig(
            tools=[
                # Use Vertex AI Search Tool
                Tool(
                    retrieval=Retrieval(
                        vertex_ai_search=VertexAISearch(
                            datastore=datastore,
                        )
                    )
                )
            ],
        ),
    )
    
    print(response.text)
    # Example response:
    # 'The process for making an appointment to renew your driver's license varies depending on your location. To provide you with the most accurate instructions...'

## What's next

For detailed documentation, see the following:

  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview)
  - [Generate content with the Gemini API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference)
