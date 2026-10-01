---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/batch-prediction-genai-embeddings
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/batch-prediction-genai-embeddings
title: Get batch embeddings inferences
description: Learn how to get batch inferences for text and multimodal embeddings in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Getting batch responses is a way to efficiently send large numbers of non-latency-sensitive embedding requests. Unlike online responses, where you are limited to one input request at a time, you can send many embedding requests in a single batch request. Similar to how batch inference is done for [tabular data in Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions) , you determine your output location, add your input, and your responses are asynchronously populated into your output location.

<span id="gemini-embedding-batch-prediction-preview"></span>

## Gemini Embedding batch prediction

Gemini Embedding batch prediction is built on [Gemini Batch Inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference) and uses an updated schema for input and output:

  - **Input and output storage:** Inputs and outputs must be formatted as [JSON Lines (JSONL)](https://jsonlines.org/) files stored in Cloud Storage. (BigQuery tables are not supported for Gemini embedding models.)
  - **Job limits:** Each batch job supports up to **1,000,000 rows** and an input file size of up to **1 GB** .
  - **Quotas and queuing:** There are no predefined concurrency quotas. Batch jobs are dynamically scheduled based on resource availability and can remain queued for up to 72 hours, with a target turnaround time of under 24 hours.

### Supported models and locations

The following table lists the supported Gemini embedding models and locations for batch inference:

| Model                | Model ID               | Supported locations                                                                    |
| -------------------- | ---------------------- | -------------------------------------------------------------------------------------- |
| Gemini Embedding 001 | `gemini-embedding-001` | `us-central1` , `us-east4` , `us-west1` , `us-west4` , `europe-west1` , `europe-west4` |
| Gemini Embedding 2   | `gemini-embedding-2`   | Global ( `global` ), US multi-region ( `us` ), EU multi-region ( `eu` )                |

For more information about regional and global endpoints, see [Locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

### Prepare your inputs

Upload your batch input data as a JSONL file to Cloud Storage, where each line is a single JSON object containing a `"request"` field.

> **Note:** The `"key"` field is not mandatory, but it is strongly recommended to add this field and assign a unique ID for each row so that you can map asynchronous output vectors back to your input rows.

#### Gemini Embedding 001

The `gemini-embedding-001` model supports a `task_type` and `title` configuration inside `embed_content_config` for each row.

    {"key": "id_1", "request": {"content": {"parts": [{"text": "Hello World"}]}, "embed_content_config": {"output_dimensionality": 768, "title": "some_title", "task_type": "RETRIEVAL_DOCUMENT"}}}
    {"key": "id_2", "request": {"content": {"parts": [{"text": "Hello World again"}]}, "embed_content_config": {"output_dimensionality": 768, "title": "some_title_2", "task_type": "RETRIEVAL_DOCUMENT"}}}

#### Gemini Embedding 2

The `gemini-embedding-2` model supports text, image, video, and audio inputs. Unlike `gemini-embedding-001` , `gemini-embedding-2` expects the task type and title to be inlined directly within the prompt text. If `task_type` or `title` are passed inside `embed_content_config` , they are silently ignored (matching online API behavior).

For multimodal input constraints and token and file limits, see [Multimodal Embeddings API limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings#api-limits) .

    {"key": "id_1", "request": {"content": {"parts": [{"text": "title: sample | text: Hello World"}]}, "embed_content_config": {"output_dimensionality": 768}}}
    {"key": "id_2", "request": {"content": {"parts": [{"fileData": {"fileUri": "gs://cloud-samples-data/generative-ai/image/benchmark.jpeg", "mimeType": "image/jpeg"}}]}, "embed_content_config": {"output_dimensionality": 768}}}

### Request a batch response

Depending on the number of input items that you submit, a batch job can take some time to complete. You can submit a batch embedding job using the REST API or the Google Gen AI SDK.

### REST

You can use the REST API to create a batch embedding job by sending a POST request to the `batchPredictionJobs` endpoint.

Before using any of the request data, make the following replacements:

  - ENDPOINT\_PREFIX : The region or multi-region prefix followed by `-` (for example, `us-central1-` , `us-` , or `eu-` ). If using the `global` endpoint, leave blank ( `aiplatform.googleapis.com` ).
  - PROJECT\_ID : The ID of your Google Cloud project.
  - LOCATION : A supported location for the model (for example, `us-central1` for `gemini-embedding-001` , or `global` , `us` , or `eu` for `gemini-embedding-2` ).
  - BP\_JOB\_NAME : A display name for your batch job.
  - MODEL\_ID : The publisher model ID ( `gemini-embedding-001` or `gemini-embedding-2` ).
  - INPUT\_URI : The Cloud Storage URI of your input JSONL file (for example, `gs://my-bucket/path/to/input.jsonl` ).
  - OUTPUT\_URI\_PREFIX : The Cloud Storage bucket and directory prefix where output JSONL files will be written (for example, `gs://my-bucket/path/to/output/` ).

HTTP method and URL:

    POST https://ENDPOINT_PREFIXaiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs

Request JSON body:

    {
      "displayName": "BP_JOB_NAME",
      "model": "publishers/google/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "displayName": "BP_JOB_NAME",
      "model": "publishers/google/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        }
      }
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://ENDPOINT_PREFIXaiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "displayName": "BP_JOB_NAME",
      "model": "publishers/google/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        }
      }
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://ENDPOINT_PREFIXaiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "BP_JOB_NAME",
      "model": "publishers/google/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2026-09-15T19:33:59.153782Z",
      "updateTime": "2026-09-15T19:33:59.153782Z",
      "modelVersionId": "1"
    }

#### Example curl commands

The response includes a unique identifier for the batch job ( BATCH\_JOB\_ID ). You can submit a batch job and poll for its status using `curl` :

**Create a batch job:**

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://ENDPOINT_PREFIXaiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs"

**Poll job status:**

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        "https://ENDPOINT_PREFIXaiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/BATCH_JOB_ID"

### Python

#### Install

    pip install --upgrade google-genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=us-central1
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    import time
    
    from google import genai
    from google.genai.types import CreateBatchJobConfig, JobState, HttpOptions
    
    client = genai.Client(http_options=HttpOptions(api_version="v1"))
    # TODO(developer): Update and un-comment below line
    # output_uri = "gs://your-bucket/your-prefix"
    
    # See the documentation: https://googleapis.github.io/python-genai/genai.html#genai.batches.Batches.create
    job = client.batches.create(
        model="text-embedding-005",
        # Source link: https://storage.cloud.google.com/cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl
        src="gs://cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl",
        config=CreateBatchJobConfig(dest=output_uri),
    )
    print(f"Job name: {job.name}")
    print(f"Job state: {job.state}")
    # Example response:
    # Job name: projects/.../locations/.../batchPredictionJobs/9876453210000000000
    # Job state: JOB_STATE_PENDING
    
    # See the documentation: https://googleapis.github.io/python-genai/genai.html#genai.types.BatchJob
    completed_states = {
        JobState.JOB_STATE_SUCCEEDED,
        JobState.JOB_STATE_FAILED,
        JobState.JOB_STATE_CANCELLED,
        JobState.JOB_STATE_PAUSED,
    }
    
    while job.state not in completed_states:
        time.sleep(30)
        job = client.batches.get(name=job.name)
        print(f"Job state: {job.state}")
        if job.state == JobState.JOB_STATE_FAILED:
            print(f"Error: {job.error}")
            break
    
    # Example response:
    # Job state: JOB_STATE_PENDING
    # Job state: JOB_STATE_RUNNING
    # Job state: JOB_STATE_RUNNING
    # ...
    # Job state: JOB_STATE_SUCCEEDED

### Go

Learn how to install or update the [Go](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://pkg.go.dev/google.golang.org/genai) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=us-central1
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    import (
        "context"
        "fmt"
        "io"
        "time"
    
        "google.golang.org/genai"
    )
    
    // generateBatchEmbeddings shows how to run a batch embeddings prediction job.
    func generateBatchEmbeddings(w io.Writer, outputURI string) error {
        // outputURI = "gs://your-bucket/your-prefix"
        ctx := context.Background()
    
        client, err := genai.NewClient(ctx, &genai.ClientConfig{
            HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
        })
        if err != nil {
            return fmt.Errorf("failed to create genai client: %w", err)
        }
        modelName := "text-embedding-005"
        // See the documentation: https://pkg.go.dev/google.golang.org/genai#Batches.Create
        job, err := client.Batches.Create(ctx,
            modelName,
            &genai.BatchJobSource{
                Format: "jsonl",
                // Source link: https://storage.cloud.google.com/cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl
                GCSURI: []string{"gs://cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl"},
            },
            &genai.CreateBatchJobConfig{
                Dest: &genai.BatchJobDestination{
                    Format: "jsonl",
                    GCSURI: outputURI,
                },
            },
        )
        if err != nil {
            return fmt.Errorf("failed to create batch job: %w", err)
        }
    
        fmt.Fprintf(w, "Job name: %s\n", job.Name)
        fmt.Fprintf(w, "Job state: %s\n", job.State)
        // Example response:
        //  Job name: projects/{PROJECT_ID}/locations/us-central1/batchPredictionJobs/9876453210000000000
        //  Job state: JOB_STATE_PENDING
    
        // See the documentation: https://pkg.go.dev/google.golang.org/genai#BatchJob
        completedStates := map[genai.JobState]bool{
            genai.JobStateSucceeded: true,
            genai.JobStateFailed:    true,
            genai.JobStateCancelled: true,
            genai.JobStatePaused:    true,
        }
    
        // Poll until job finishes
        for !completedStates[job.State] {
            time.Sleep(30 * time.Second)
            job, err = client.Batches.Get(ctx, job.Name, nil)
            if err != nil {
                return fmt.Errorf("failed to get batch job: %w", err)
            }
            fmt.Fprintf(w, "Job state: %s\n", job.State)
    
            if job.State == genai.JobStateFailed {
                fmt.Fprintf(w, "Error: %+v\n", job.Error)
                break
            }
        }
    
        //  Example response:
        //    Job state: JOB_STATE_PENDING
        //    Job state: JOB_STATE_RUNNING
        //    Job state: JOB_STATE_RUNNING
        //    ...
        //    Job state: JOB_STATE_SUCCEEDED
    
        return nil
    }

### Node.js

#### Install

    npm install @google/genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/js-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=us-central1
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    const {GoogleGenAI} = require('@google/genai');
    
    const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
    const GOOGLE_CLOUD_LOCATION =
      process.env.GOOGLE_CLOUD_LOCATION || 'us-central1';
    const OUTPUT_URI = 'gs://your-bucket/your-prefix';
    
    async function runBatchPredictionJob(
      outputUri = OUTPUT_URI,
      projectId = GOOGLE_CLOUD_PROJECT,
      location = GOOGLE_CLOUD_LOCATION
    ) {
      const client = new GoogleGenAI({
        vertexai: true,
        project: projectId,
        location: location,
        httpOptions: {
          apiVersion: 'v1',
        },
      });
    
      // See the documentation: https://googleapis.github.io/js-genai/release_docs/classes/batches.Batches.html
      let job = await client.batches.create({
        model: 'text-embedding-005',
        // Source link: https://storage.cloud.google.com/cloud-samples-data/batch/prompt_for_batch_gemini_predict.jsonl
        src: 'gs://cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl',
        config: {
          dest: outputUri,
        },
      });
    
      console.log(`Job name: ${job.name}`);
      console.log(`Job state: ${job.state}`);
    
      // Example response:
      //  Job name: projects/%PROJECT_ID%/locations/us-central1/batchPredictionJobs/9876453210000000000
      //  Job state: JOB_STATE_PENDING
    
      const completedStates = new Set([
        'JOB_STATE_SUCCEEDED',
        'JOB_STATE_FAILED',
        'JOB_STATE_CANCELLED',
        'JOB_STATE_PAUSED',
      ]);
    
      while (!completedStates.has(job.state)) {
        await new Promise(resolve => setTimeout(resolve, 30000));
        job = await client.batches.get({name: job.name});
        console.log(`Job state: ${job.state}`);
      }
    
      // Example response:
      //  Job state: JOB_STATE_PENDING
      //  Job state: JOB_STATE_RUNNING
      //  Job state: JOB_STATE_RUNNING
      //  ...
      //  Job state: JOB_STATE_SUCCEEDED
    
      return job.state;
    }

### Java

Learn how to install or update the [Java](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://central.sonatype.com/artifact/com.google.genai/google-genai) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=us-central1
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    import static com.google.genai.types.JobState.Known.JOB_STATE_CANCELLED;
    import static com.google.genai.types.JobState.Known.JOB_STATE_FAILED;
    import static com.google.genai.types.JobState.Known.JOB_STATE_PAUSED;
    import static com.google.genai.types.JobState.Known.JOB_STATE_SUCCEEDED;
    
    import com.google.genai.Client;
    import com.google.genai.types.BatchJob;
    import com.google.genai.types.BatchJobDestination;
    import com.google.genai.types.BatchJobSource;
    import com.google.genai.types.CreateBatchJobConfig;
    import com.google.genai.types.GetBatchJobConfig;
    import com.google.genai.types.HttpOptions;
    import com.google.genai.types.JobState;
    import java.util.EnumSet;
    import java.util.Set;
    import java.util.concurrent.TimeUnit;
    
    public class BatchPredictionEmbeddingsWithGcs {
    
      public static void main(String[] args) throws InterruptedException {
        // TODO(developer): Replace these variables before running the sample.
        String modelId = "text-embedding-005";
        String outputGcsUri = "gs://your-bucket/your-prefix";
        createBatchJob(modelId, outputGcsUri);
      }
    
      // Creates a batch prediction job with embedding model and Google Cloud Storage.
      public static JobState createBatchJob(String modelId, String outputGcsUri)
          throws InterruptedException {
        // Client Initialization. Once created, it can be reused for multiple requests.
        try (Client client =
            Client.builder()
                .location("us-central1")
                .vertexAI(true)
                .httpOptions(HttpOptions.builder().apiVersion("v1").build())
                .build()) {
    
          // See the documentation:
          // https://googleapis.github.io/java-genai/javadoc/com/google/genai/Batches.html
          BatchJobSource batchJobSource =
              BatchJobSource.builder()
                  // Source link:
                  // https://storage.cloud.google.com/cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl
                  .gcsUri("gs://cloud-samples-data/generative-ai/embeddings/embeddings_input.jsonl")
                  .format("jsonl")
                  .build();
    
          CreateBatchJobConfig batchJobConfig =
              CreateBatchJobConfig.builder()
                  .displayName("your-display-name")
                  .dest(BatchJobDestination.builder().gcsUri(outputGcsUri).format("jsonl").build())
                  .build();
    
          BatchJob batchJob = client.batches.create(modelId, batchJobSource, batchJobConfig);
    
          String jobName =
              batchJob.name().orElseThrow(() -> new IllegalStateException("Missing job name"));
          JobState jobState =
              batchJob.state().orElseThrow(() -> new IllegalStateException("Missing job state"));
          System.out.println("Job name: " + jobName);
          System.out.println("Job state: " + jobState);
          // Job name: projects/.../locations/.../batchPredictionJobs/6205497615459549184
          // Job state: JOB_STATE_PENDING
    
          // See the documentation:
          // https://googleapis.github.io/java-genai/javadoc/com/google/genai/types/BatchJob.html
          Set<JobState.Known> completedStates =
              EnumSet.of(JOB_STATE_SUCCEEDED, JOB_STATE_FAILED, JOB_STATE_CANCELLED, JOB_STATE_PAUSED);
    
          while (!completedStates.contains(jobState.knownEnum())) {
            TimeUnit.SECONDS.sleep(30);
            batchJob = client.batches.get(jobName, GetBatchJobConfig.builder().build());
            jobState =
                batchJob
                    .state()
                    .orElseThrow(() -> new IllegalStateException("Missing job state during polling"));
            System.out.println("Job state: " + jobState);
          }
          // Example response:
          // Job state: JOB_STATE_QUEUED
          // Job state: JOB_STATE_RUNNING
          // ...
          // Job state: JOB_STATE_SUCCEEDED
          return jobState;
        }
      }
    }

### Retrieve batch output

When a batch inference task is complete, the output JSONL files are stored in the Cloud Storage output directory that you specified in your request.

    {"key": "id_1", "request": {...}, "response": {"tokenCount": "2", "embedding": {"values": [-0.015, 0.024, ...]}}}
    {"key": "id_2", "request": {...}, "response": {"tokenCount": "3", "embedding": {"values": [-0.075, 0.031, ...]}}}

### Additional resources

  - For available configuration options on `gemini-embedding-001` , see the [Text Embeddings Guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings) .
  - For available configuration options on `gemini-embedding-2` , see the [Multimodal Embeddings Guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings) .
  - To learn more about Gemini batch inference features and quotas, see [Batch inference with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference) .

-----

## Legacy Embedding batch prediction

This section describes batch inference workflows for legacy text embedding models ( `text-embedding-004` , `text-embedding-005` , and `text-multilingual-embedding-002` ), which are built on a different architecture than Gemini embedding models.

> **Note:** If you are using Gemini embedding models ( `gemini-embedding-2` or `gemini-embedding-001` ), see [Gemini Embedding batch prediction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/batch-prediction-genai-embeddings#gemini-embedding-batch-prediction) for the required schema and Cloud Storage-only workflow.

### Text embeddings models that support batch inferences

All stable versions of legacy text embedding models support batch inferences and are fully supported for production environments. To view the full list of embedding models, see [Embedding model and versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-versions#embedding_models_and_versions) .

### Prepare your inputs for legacy models

The input for legacy batch requests is a list of prompts that can either be stored in a BigQuery table or as a [JSON Lines (JSONL)](https://jsonlines.org/) file in Cloud Storage. Each request can include up to 30,000 prompts.

#### JSONL example

This section shows examples of how to format JSONL input and output for legacy models.

##### JSONL input example

    {"content":"Give a short description of a machine learning model:"}
    {"content":"Best recipe for banana bread:"}

##### JSONL output example

    {"instance":{"content":"Give..."},"predictions": [{"embeddings":{"statistics":{"token_count":8,"truncated":false},"values":[0.2,....]}}],"status":""}
    {"instance":{"content":"Best..."},"predictions": [{"embeddings":{"statistics":{"token_count":3,"truncated":false},"values":[0.1,....]}}],"status":""}

#### BigQuery example

This section shows examples of how to format BigQuery input and output for legacy models.

##### BigQuery input example

This example shows a single column BigQuery table.

| content                                                 |
| ------------------------------------------------------- |
| "Give a short description of a machine learning model:" |
| "Best recipe for banana bread:"                         |

##### BigQuery output example

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>content</th>
<th>predictions</th>
<th>status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>"Give a short description of a machine learning model:"</td>
<td><pre dir="ltr" data-is-upgraded="" data-syntax="JSON" translate="no"><code>[
  {
    &quot;embeddings&quot;: {
      &quot;statistics&quot;: {
        &quot;token_count&quot;: 8,
        &quot;truncated&quot;: false
      },
      &quot;values&quot;: [0.1, ...]
    }
  }
]</code></pre></td>
<td></td>
</tr>
<tr class="even">
<td>"Best recipe for banana bread:"</td>
<td><pre dir="ltr" data-is-upgraded="" data-syntax="JSON" translate="no"><code>[
  {
    &quot;embeddings&quot;: {
      &quot;statistics&quot;: {
        &quot;token_count&quot;: 3,
        &quot;truncated&quot;: false
      },
      &quot;values&quot;: [0.2, ...]
    }
  }
]</code></pre></td>
<td></td>
</tr>
</tbody>
</table>

### Request a batch response for legacy models

Depending on the number of input items that you've submitted, a batch generation task can take some time to complete.

### REST

You can use the REST API to get text embeddings in batch for legacy models by sending a POST request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - LOCATION : The location to send your request (for example, `us-central1` ).
  - PROJECT\_ID : The ID of your Google Cloud project.
  - BP\_JOB\_NAME : The job name.
  - MODEL\_ID : The model ID of the legacy embedding model (for example, `text-embedding-005` ).
  - INPUT\_URI : The input source URI. This is either a BigQuery table URI or a JSONL file URI in Cloud Storage.
  - OUTPUT\_URI : Output target URI.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs

Request JSON body:

    {
        "name": "BP_JOB_NAME",
        "displayName": "BP_JOB_NAME",
        "model": "publishers/google/models/text-embedding-005",
        "inputConfig": {
          "instancesFormat":"bigquery",
          "bigquerySource":{
            "inputUri" : "INPUT_URI"
          }
        },
        "outputConfig": {
          "predictionsFormat":"bigquery",
          "bigqueryDestination":{
            "outputUri": "OUTPUT_URI"
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
        "name": "BP_JOB_NAME",
        "displayName": "BP_JOB_NAME",
        "model": "publishers/google/models/text-embedding-005",
        "inputConfig": {
          "instancesFormat":"bigquery",
          "bigquerySource":{
            "inputUri" : "INPUT_URI"
          }
        },
        "outputConfig": {
          "predictionsFormat":"bigquery",
          "bigqueryDestination":{
            "outputUri": "OUTPUT_URI"
        }
      }
    }
    
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
        "name": "BP_JOB_NAME",
        "displayName": "BP_JOB_NAME",
        "model": "publishers/google/models/text-embedding-005",
        "inputConfig": {
          "instancesFormat":"bigquery",
          "bigquerySource":{
            "inputUri" : "INPUT_URI"
          }
        },
        "outputConfig": {
          "predictionsFormat":"bigquery",
          "bigqueryDestination":{
            "outputUri": "OUTPUT_URI"
        }
      }
    }
    
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/123456789",
      "displayName": "BP_JOB_NAME",
      "model": "projects/PROJECT_ID/locations/LOCATION/models/text-embedding-005",
      "inputConfig": {
        "instancesFormat": "bigquery",
        "bigquerySource": {
          "inputUri": "INPUT_URI"
        }
      },
      "modelParameters": {},
      "outputConfig": {
        "predictionsFormat": "bigquery",
        "bigqueryDestination": {
          "outputUri": "OUTPUT_URI"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2023-07-12T20:46:52.148717Z",
      "updateTime": "2023-07-12T20:46:52.148717Z",
      "labels": {
        "owner": "sample_owner",
        "product": "llm"
      },
      "modelVersionId": "1",
      "modelMonitoringStatus": {}
    }

#### Example curl command

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs"

### Retrieve batch output for legacy models

When a legacy batch inference task is complete, the output is stored in the Cloud Storage bucket or BigQuery table that you specified in your request.

## What's next

  - Learn how to [get text embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings) .
  - Learn how to [get multimodal embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings) .
