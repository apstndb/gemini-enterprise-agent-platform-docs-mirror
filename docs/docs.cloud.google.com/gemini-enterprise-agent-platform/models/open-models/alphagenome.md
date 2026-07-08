---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome
title: AlphaGenome
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Important:** AlphaGenome is a research tool and is **not** intended or cleared for clinical diagnostic use.

[Video](https://www.youtube.com/watch?v=Xbvloe13nak) *Video runtime: 30 minutes*

[AlphaGenome](https://doi.org/10.1038/s41586-025-10014-0) is a state-of-the-art deep learning model developed by Google DeepMind. It is designed to decipher the functional regulatory code of the human genome. By analyzing large-scale DNA sequences (up to 1 million base pairs) at single-base resolution, the model predicts how genetic variations affect molecular and biological mechanisms such as gene expression, chromatin accessibility, and RNA splicing.

This document covers how to deploy and use AlphaGenome, as well as the hardware and deployment requirements for using the model.

## Hardware and deployment requirements

Because of AlphaGenome's deep architecture and 1 MB context window, the model has strict hardware and memory requirements. This section covers:

  - [Supported VM and GPU configurations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome#supported-configurations)
  - [Supported accelerator and machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome#supported-accelerator-and-machine-types)
  - [Quota requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome#quota-requirements)

### Supported VM and GPU configurations

AlphaGenome requires a minimum of one node and can be deployed to Agent Platform endpoints using specific machine types equipped with NVIDIA A100 or H100 accelerators.

Agent Platform endpoints scale seamlessly. If additional capacity is required to handle increased request volumes, administrators can configure autoscaling to continuously add nodes as needed. For more information, see [Scale inference nodes by using autoscaling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling) .

### Supported accelerator and machine types

Administrators must select from the following supported machine types that provide the required 80 GB GPU memory:

  - **NVIDIA H100 (80 GB)** : `a3-highgpu-1g` , `a3-highgpu-2g` , `a3-highgpu-4g` , `a3-highgpu-8g`
  - **NVIDIA A100 (80 GB)** : `a2-ultragpu-1g` , `a2-ultragpu-2g` , `a2-ultragpu-4g` , `a2-ultragpu-8g`
  - **NVIDIA H100 Mega (80 GB)** : `a3-megagpu-8g`

> **Note:** The 40 GB A100 `a2-highgpu` series isn't supported.

For detailed specifications, see [Configure compute resources for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) .

### Quota requirements

Before deploying, administrators must ensure that the Google Cloud project has adequate GPU serving quota assigned in the target region:

  - `aiplatform.googleapis.com/custom_model_serving_nvidia_h100_gpus`
  - `aiplatform.googleapis.com/custom_model_serving_nvidia_a100_gpus`
  - `compute.googleapis.com/gpus_per_gpu_family`

## Deploy AlphaGenome

AlphaGenome is available as a self-deployed model from Model Garden. For detailed instructions on provisioning the endpoint infrastructure and deploying the model to a Google Cloud project, see [Deploy open models from Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/deploy-model-garden) .

## Use AlphaGenome

Users can interact with the deployed AlphaGenome endpoint programmatically using either the Python SDK or the REST API.

> **Note:** Access to the SDK wheel file is restricted. Work with your Google Cloud account team to get your service account added to the allowlist for access to the Google Cloud-specific Python SDK.

For the complete API reference, parameter definitions, and detailed schemas, see the [official AlphaGenome documentation](https://www.alphagenomedocs.com) .

### Prerequisites and authentication

Access to the deployed endpoint is managed using Google Cloud Identity and Access Management. Ensure the execution environment (such as a local terminal, VM, or Colab) is authenticated with credentials (either a service account or end-user credentials) that have the Agent Platform User ( `roles/aiplatform.user` ) role.

    # Set your endpoint URL. AlphaGenome requires the `streamRawPredict` action.
    # Ensure your URL ends with :streamRawPredict
    export ENDPOINT_URL="https://<your-endpoint-url>:streamRawPredict"
    
    # (Optional) If you choose to impersonate a service account, set this variable
    export SERVICE_ACCOUNT="your-service-account-email@your-project.iam.gserviceaccount.com"

### Usage

### Python

#### Install the SDK

Run the following commands to install the AlphaGenome Cloud SDK. Refer to the product welcome package for the wheel file location.

    # Copy the SDK wheel file and install
    gcloud storage cp "gs://alphagenome-whl/alphagenome_cloud_sdk-0.4.2.10-py3-none-any.whl" .
    pip install alphagenome_cloud_sdk-0.4.2.10-py3-none-any.whl

#### Initialize the client

Before you can use the model, you must initialize the client:

    from alphagenome.models import dna_client
    from alphagenome_cloud_sdk.models import dna_client_http
    
    # Create the HTTP client pointing to the Agent Platform endpoint.
    # The `service_account` parameter is optional and only required if you are 
    # choosing to authenticate via service account impersonation.
    dna_model = dna_client_http.create_http_client(
        vertex_ai_url=vertex_ai_url,
        # service_account=service_account  # Uncomment to use service account impersonation
    )

#### Predict tracks for a DNA sequence

Use `predict_sequence` to predict genomic modalities for a raw DNA string:

> **Note:** The sequence must be padded to exactly 1 MB.

    # Pad a synthetic sequence to 1 MB using 'N' for unknown/padding bases
    padded_sequence = 'GATTACA'.center(dna_client.SEQUENCE_LENGTH_1MB, 'N')
    
    output = dna_model.predict_sequence(
        sequence=padded_sequence,
        requested_outputs=[
            dna_client.OutputType.CAGE,   # Transcription Start Sites
            dna_client.OutputType.DNASE,  # Chromatin Accessibility
        ],
        ontology_terms=[
            'UBERON:0002048',             # Lung tissue ontology term
        ]
    )
    
    # Access prediction values (shape: sequence_length, num_tracks)
    dnase_signals = output.dnase.values
    dnase_metadata = output.dnase.metadata

#### Predict tracks for a reference genome interval

Use `predict_interval` to predict modalities direct from a specific chromosome region in the reference genome:

    from alphagenome.data.genome import Interval
    
    # Define a genomic interval and resize it to the 1Mb context window
    interval = Interval(
        chromosome='chr19',
        start=40991281,
        end=41018398,
        strand='.',
        name='CYP2B6'
    ).resize(dna_client.SEQUENCE_LENGTH_1MB)
    
    output = dna_model.predict_interval(
        interval=interval,
        requested_outputs=[dna_client.OutputType.RNA_SEQ],
        ontology_terms=['UBERON:0001114']  # Right liver lobe
    )

#### Score a variant effect (in silico mutagenesis)

Use `score_variant` to compare the predicted expression of a reference (REF) sequence versus an alternative (ALT) mutated sequence:

    from alphagenome.data import genome
    from alphagenome.models import variant_scorers
    
    # Define the genetic variant
    variant = genome.Variant(
        chromosome='chr22',
        position=36201698,
        reference_bases='A',
        alternate_bases='C',
    )
    
    # Select the variant scoring method for RNA-Seq
    variant_scorer = variant_scorers.RECOMMENDED_VARIANT_SCORERS['RNA_SEQ']
    
    # Execute the scoring
    variant_scores = dna_model.score_variant(
        interval=variant.reference_interval.resize(dna_client.SEQUENCE_LENGTH_1MB),
        variant=variant,
        variant_scorers=[variant_scorer],
        fix_negative_strand=True
    )
    
    # Output is returned as an AnnData object containing raw and quantile scores
    print("Scores shape:", variant_scores[0].X.shape)

### REST

Clients can query the deployed endpoint using standard REST client tools like curl:

    # Generate an OAuth2 access token using your current credentials
    # If using service account impersonation, append: --impersonate-service-account=$SERVICE_ACCOUNT
    export TOKEN=$(gcloud auth print-access-token)
    
    curl -X POST \
      -H "Authorization: Bearer $TOKEN" \
      -H "Content-Type: application/json" \
      -d '{
        "model": "google/alpha-genome-001",
        "instances": [
          {
            "request_type": "predict_interval",
            "data": {
              "interval": {
                "chromosome": "chr19",
                "start": "41003816",
                "end": "41005864",
                "strand": "STRAND_UNSTRANDED"
              },
              "organism": "ORGANISM_HOMO_SAPIENS",
              "requestedOutputs": ["OUTPUT_TYPE_ATAC"]
            }
          }
        ]
      }' \
      $ENDPOINT_URL

## Pricing

AlphaGenome is a paid model with a licensing fee. For information about AlphaGenome pricing, [contact a Google Cloud sales specialist](https://cloud.google.com/contact) or work with your Google Cloud account team.

You are responsible for the cost of infrastructure used to host the model, including the Agent Platform endpoint and the GPU instances the model is deployed on. For more information, see [Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .

## Limitations

AlphaGenome has the following limitations:

  - **Research use only** : AlphaGenome is a research tool and is not intended or cleared for clinical diagnostic use.
  - **1 MB context horizon** : Genomic interactions occurring over distances larger than 1 MB cannot be captured in a single prediction query.
  - **No fine-tuning support** : Fine-tuning the foundation AlphaGenome model on private training datasets is not supported. The model is available for inference only.

## Scientific reference directory

To support the scientific and developer communities, the following table lists primary reference materials, literature, and resources for AlphaGenome:

| Resource type       | Title and link                                                                                                                                                                       | Description                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| Peer-reviewed paper | [Advancing regulatory variant effect prediction with AlphaGenome, *Nature* (January 2026)](https://doi.org/10.1038/s41586-025-10014-0)                                               | The primary scientific publication detailing the model's architecture, evaluations, and performance benchmarks. |
| Pre-print article   | [AlphaGenome: advancing regulatory variant effect prediction with a unified DNA sequence model, bioRxiv (July 2025)](https://www.biorxiv.org/content/10.1101/2025.06.25.661532v2)    | The initial pre-peer-review manuscript.                                                                         |
| Announcement        | [AlphaGenome: AI for better understanding the genome, Google DeepMind blog (June 2025)](https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/)            | The high-level release blog post outlining the model's impact on genomics.                                      |
| API documentation   | [AlphaGenome documentation](https://www.alphagenomedocs.com)                                                                                                                         | Technical documentation for the Python SDK and HTTP API schemas.                                                |
| Video walkthrough   | [AlphaGenome: AI for better understanding the genome](https://www.youtube.com/watch?v=Xbvloe13nak)                                                                                   | Video walkthrough outlining the model capabilities and basic interaction flows. *(Video runtime: 30 minutes)*   |
| Quickstart notebook | [AlphaGenome quickstart Colab notebook](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/alphagenome/cloudai_alphagenome_vai_quickstart.ipynb) | A notebook providing executable examples of SDK initialization and variant effect scoring.                      |

## Support and feedback

You can get support for AlphaGenome in the following ways:

  - **Genomic science and model output support** : For discussions about biology, model predictions, interpretability, or to engage with Google DeepMind, join the public AlphaGenome and EDM Community Forum at [alphagenomecommunity.com](https://alphagenomecommunity.com) .
  - **Infrastructure and platform support** : For questions regarding Google Cloud quotas, accelerators, issue with client library, billing, etc., engage with your account team or open a ticket with the standard Google Cloud Support team.
