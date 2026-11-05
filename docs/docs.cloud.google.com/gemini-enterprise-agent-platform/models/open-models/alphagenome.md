---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome
title: AlphaGenome
description: Learn how to deploy and query AlphaGenome, a deep learning foundation model for predicting regulatory variant effects and genomic modalities on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Important:** AlphaGenome is a research tool and is **not** intended or cleared for clinical diagnostic use.

[Video](https://www.youtube.com/watch?v=Xbvloe13nak) *Video runtime: 30 minutes*

[AlphaGenome](https://doi.org/10.1038/s41586-025-10014-0) is a deep learning foundation model developed by Google DeepMind that predicts the functional regulatory effects of DNA sequences in the human genome. By analyzing DNA sequences up to 1 million base pairs (1 MB) at single-base resolution, the model predicts how genetic variations affect molecular and biological mechanisms across 11 genomic modalities: gene expression ( `RNA_SEQ` , `CAGE` , `PROCAP` ), chromatin accessibility ( `ATAC` , `DNASE` ), histone modifications and transcription factor binding ( `CHIP_HISTONE` , `CHIP_TF` ), RNA splicing ( `SPLICE_SITES` , `SPLICE_SITE_USAGE` , `SPLICE_JUNCTIONS` ), and 3D chromatin contact maps ( `CONTACT_MAPS` ).

This document describes the hardware and deployment requirements for AlphaGenome, and shows how to deploy and query the model on Gemini Enterprise Agent Platform.

> **GA with allowlist:** To access AlphaGenome, complete the [AlphaGenome request form](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/alphagenome-request) .

## Hardware and deployment requirements

Because of AlphaGenome's deep architecture and 1 MB context window, the model has strict hardware and memory requirements. This section covers the following topics:

- [Supported VM and GPU configurations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome#supported-configurations)
- [Supported accelerator and machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome#supported-accelerator-and-machine-types)
- [Quota requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/alphagenome#quota-requirements)

### Supported VM and GPU configurations

AlphaGenome requires at least one node. You can deploy the model to Agent Platform endpoints by using machine types equipped with NVIDIA A100 or H100 accelerators.

If you need additional capacity to handle increased request volumes, you can configure autoscaling on your Agent Platform endpoint to add nodes automatically. For more information, see [Scale inference nodes by using autoscaling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling) .

### Supported accelerator and machine types

Select from the following supported machine types that provide the required 80 GB of GPU memory:

- **NVIDIA H100 (80 GB)** : `a3-highgpu-1g` , `a3-highgpu-2g` , `a3-highgpu-4g` , `a3-highgpu-8g`
- **NVIDIA A100 (80 GB)** : `a2-ultragpu-1g` , `a2-ultragpu-2g` , `a2-ultragpu-4g` , `a2-ultragpu-8g`
- **NVIDIA H100 Mega (80 GB)** : `a3-megagpu-8g`

> **Note:** The 40 GB A100 `a2-highgpu` series isn't supported.

For detailed specifications, see [Configure compute resources for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) .

### Quota requirements

Before you deploy the model, ensure that your Google Cloud project has sufficient GPU serving quota in the target region for the following metrics:

- `aiplatform.googleapis.com/custom_model_serving_nvidia_h100_gpus`
- `aiplatform.googleapis.com/custom_model_serving_nvidia_a100_gpus`
- `aiplatform.googleapis.com/custom_model_serving_nvidia_h100_mega_gpus`
- `compute.googleapis.com/gpus_per_gpu_family`

## Deploy AlphaGenome

AlphaGenome is available as a self-deployed model from Model Garden. For detailed instructions on provisioning the endpoint infrastructure and deploying the model to a Google Cloud project, see [Deploy open models from Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/deploy-model-garden) .

Model Garden provides the following serving versions for AlphaGenome:

- **`alphagenome-004` (default, unified gRPC and HTTP)** : Serves all seven `DnaModelService` methods ( `predict_sequence` , `predict_interval` , `predict_variant` , `score_variant` , `score_interval` , `score_ism_variants` , and `output_metadata` ) from a unified container that supports both HTTP/2 gRPC streaming on port `8081` and HTTP streaming ( `streamRawPredict` ) on port `8080` :
  - **Public (shared endpoint) (gRPC)** : Select **Public (shared endpoint)** under **Endpoint access** when deploying in Model Garden to query the model over gRPC streaming ( `PredictionService.StreamDirectRawPredict` using `dna_client_grpc.create_vertex_client` ). Calling the model over gRPC transmits compressed binary tensor chunks directly without JSON or base64 serialization overhead, which reduces latency on 1 MB track predictions and avoids HTTP gateway timeouts on high-concurrency multi-variant workloads such as in silico saturation mutagenesis ( `score_ism_variants` ).
  - **Public (dedicated endpoint) (HTTP)** : Keep the default **Public (dedicated endpoint)** option when deploying in Model Garden to query the model over HTTP streaming ( `streamRawPredict` using `dna_client_http.create_http_client` ), which streams chunked binary protobuf payloads ( `proto_b64` ) without the 10 MB HTTP response size limit of shared endpoints.
  - **Fold selection** : Both gRPC and HTTP clients on `alphagenome-004` support model fold selection ( `ALL_FOLDS` by default, or individual folds `FOLD_0` through `FOLD_3` ) using the `model_version` parameter.
- **`alphagenome-003` (legacy HTTP)** : Serves predictions over HTTP/1.1 streaming ( `streamRawPredict` ) on port `8080` and remains available for backward compatibility with existing HTTP client deployments.

## Use AlphaGenome

You can interact with a deployed AlphaGenome endpoint programmatically by using the Python SDK (over gRPC on shared endpoints or HTTP on dedicated endpoints).

> **Note:** Access to the SDK wheel file is restricted. Work with your Google Cloud account team to get your service account added to the allowlist for access to the Google Cloud-specific Python SDK.

For the complete API reference, parameter definitions, and detailed schemas, see the [official AlphaGenome documentation](https://www.alphagenomedocs.com) .

### Prerequisites and authentication

Agent Platform uses Identity and Access Management (IAM) to manage access to deployed endpoints. Ensure that your execution environment (such as a local terminal, VM, or Colaboratory) is authenticated with a service account or user credentials that have the Agent Platform User ( `roles/aiplatform.user` ) IAM role.

### Usage ( `alphagenome-004` )

The following examples show how to query a deployed `alphagenome-004` endpoint using the Python SDK:

### Python

#### Install the SDK

The wheel file for the AlphaGenome Cloud SDK ( `alphagenome-004` ) is available in the [GoogleCloudPlatform GitHub repository](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/alphagenome/whl/alphagenome_cloud_sdk-0.4.2.12-py3-none-any.whl) . Download and install the wheel file by running the following commands:

```
# Download the wheel file
wget -q https://github.com/GoogleCloudPlatform/vertex-ai-samples/raw/main/notebooks/community/alphagenome/whl/alphagenome_cloud_sdk-0.4.2.12-py3-none-any.whl

# Install the wheel file
pip install alphagenome_cloud_sdk-0.4.2.12-py3-none-any.whl
```

#### Initialize the client

Before querying the model, initialize the client for your deployed `alphagenome-004` endpoint. Both the gRPC client ( `GrpcDnaClient` ) and the HTTP client ( `HttpDnaClient` ) implement the standard `alphagenome.models.dna_model.DnaModel` interface.

To connect to an `alphagenome-004` **shared (standard) endpoint** over gRPC streaming, pass your Agent Platform endpoint resource name to `dna_client_grpc.create_vertex_client` :

```
from alphagenome.models import dna_client
from alphagenome_cloud_sdk.models import dna_client_grpc

# Specify the standard (shared) endpoint resource name:
endpoint = "projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID"

# Optional: Specify `service_account` for service account impersonation, or
# `model_version` to select a specific fold ("ALL_FOLDS", "FOLD_0", "FOLD_1",
# "FOLD_2", or "FOLD_3").
dna_model = dna_client_grpc.create_vertex_client(
    endpoint=endpoint,
    # service_account="SERVICE_ACCOUNT_EMAIL",
    # model_version=dna_client.ModelVersion.ALL_FOLDS,
)
```

If you deployed `alphagenome-004` to a **dedicated endpoint** , use `dna_client_http.create_http_client` :

```
from alphagenome.models import dna_client
from alphagenome_cloud_sdk.models import dna_client_http

# Create the HTTP client pointing to the dedicated endpoint streamRawPredict URL.
dna_model = dna_client_http.create_http_client(
    vertex_ai_url="https://ENDPOINT_DNS/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:streamRawPredict",
    # service_account="SERVICE_ACCOUNT_EMAIL",
    # model_version=dna_client.ModelVersion.ALL_FOLDS,
)
```

#### Predict tracks for a DNA sequence

Use `predict_sequence` to predict genomic modalities for a raw DNA string:

> **Note:** The sequence must be padded to a supported context length (up to 1 MB).

```
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
    ],
)

# Access prediction values (shape: sequence_length, num_tracks)
dnase_signals = output.dnase.values
dnase_metadata = output.dnase.metadata
```

#### Predict tracks for a reference genome interval

Use `predict_interval` to predict modalities directly from a specific chromosome region in the reference genome:

```
from alphagenome.data.genome import Interval

# Define a genomic interval and resize it to the 1 MB context window
interval = Interval(
    chromosome='chr19',
    start=40991281,
    end=41018398,
    strand='.',
    name='CYP2B6',
).resize(dna_client.SEQUENCE_LENGTH_1MB)

output = dna_model.predict_interval(
    interval=interval,
    requested_outputs=[dna_client.OutputType.RNA_SEQ],
    ontology_terms=['UBERON:0001114'],  # Right liver lobe
)
```

#### Predict variant effects on genomic tracks

Use `predict_variant` to generate paired reference ( `reference` ) and mutated ( `alternate` ) track predictions across an interval:

```
from alphagenome.data import genome

interval = genome.Interval(
    chromosome='chr19',
    start=41003816,
    end=41005864,
    strand='.',
).resize(dna_client.SEQUENCE_LENGTH_1MB)

variant = genome.Variant(
    chromosome='chr19',
    position=41004840,
    reference_bases='C',
    alternate_bases='T',
)

variant_output = dna_model.predict_variant(
    interval=interval,
    variant=variant,
    requested_outputs=[dna_client.OutputType.RNA_SEQ],
    ontology_terms=['UBERON:0001114'],
)

ref_rna_values = variant_output.reference.rna_seq.values
alt_rna_values = variant_output.alternate.rna_seq.values
```

#### Score a variant effect

Use `score_variant` to summarize the predicted effect of a genetic variant comparing a reference ( `REF` ) sequence against an alternative ( `ALT` ) mutated sequence:

```
from alphagenome.data import genome
from alphagenome.models import variant_scorers

# Define the genetic variant
variant = genome.Variant(
    chromosome='chr22',
    position=36201698,
    reference_bases='A',
    alternate_bases='C',
)

# Select the recommended variant scoring method for RNA-Seq
variant_scorer = variant_scorers.RECOMMENDED_VARIANT_SCORERS['RNA_SEQ']

# Execute the scoring
variant_scores = dna_model.score_variant(
    interval=variant.reference_interval.resize(dna_client.SEQUENCE_LENGTH_1MB),
    variant=variant,
    variant_scorers=[variant_scorer],
)

# Output is returned as a list of AnnData objects containing raw and quantile scores
print("Scores shape:", variant_scores[0].X.shape)
```

#### Score a genomic interval

Use `score_interval` to compute gene-mask interval scores across a genomic region:

```
from alphagenome.data import genome
from alphagenome.models import interval_scorers

interval = genome.Interval(
    chromosome='chr19',
    start=40991281,
    end=41018398,
    strand='.',
).resize(dna_client.SEQUENCE_LENGTH_1MB)

interval_scorer = interval_scorers.RECOMMENDED_INTERVAL_SCORERS['RNA_SEQ']

interval_scores = dna_model.score_interval(
    interval=interval,
    interval_scorers=[interval_scorer],
)

print("Interval scores shape:", interval_scores[0].X.shape)
```

#### Run in silico saturation mutagenesis

Use `score_ism_variants` to evaluate all possible single-nucleotide variants across a target `ism_interval` :

```
from alphagenome.data import genome
from alphagenome.models import variant_scorers

# Define the 1 MB sequence context interval and a target 50 bp ISM window
sequence_interval = genome.Interval(
    chromosome='chr19',
    start=41003816,
    end=41005864,
).resize(dna_client.SEQUENCE_LENGTH_1MB)

ism_interval = genome.Interval(
    chromosome='chr19',
    start=41004815,
    end=41004865,
)

dnase_scorer = variant_scorers.RECOMMENDED_VARIANT_SCORERS['DNASE']

ism_scores = dna_model.score_ism_variants(
    interval=sequence_interval,
    ism_interval=ism_interval,
    variant_scorers=[dnase_scorer],
)

print("Number of variants scored:", len(ism_scores))
```

### Usage ( `alphagenome-003` )

### Python

#### Install the SDK

The Wheel file for the AlphaGenome Cloud SDK is available at the [GoogleCloudPlatform GitHub repository](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/alphagenome/whl/alphagenome_cloud_sdk-0.4.2.11-py3-none-any.whl) . You can download the Wheel file by running the following:

```
# Download the whl file using - 
wget -q https://github.com/GoogleCloudPlatform/vertex-ai-samples/raw/main/notebooks/community/alphagenome/whl/alphagenome_cloud_sdk-0.4.2.11-py3-none-any.whl

# Install the whl file
pip install alphagenome_cloud_sdk-0.4.2.11-py3-none-any.whl
```

#### Initialize the client

Before you can use the model, you must initialize the client:

```
from alphagenome.models import dna_client
from alphagenome_cloud_sdk.models import dna_client_http

# Create the HTTP client pointing to the Agent Platform endpoint.
# The `service_account` parameter is optional and only required if you are 
# choosing to authenticate via service account impersonation.
dna_model = dna_client_http.create_http_client(
    vertex_ai_url=vertex_ai_url,
    # service_account=service_account  # Uncomment to use service account impersonation
)
```

#### Predict tracks for a DNA sequence

Use `predict_sequence` to predict genomic modalities for a raw DNA string:

> **Note:** The sequence must be padded to exactly 1 MB.

```
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
```

#### Predict tracks for a reference genome interval

Use `predict_interval` to predict modalities direct from a specific chromosome region in the reference genome:

```
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
```

#### Score a variant effect (in silico mutagenesis)

Use `score_variant` to compare the predicted expression of a reference (REF) sequence versus an alternative (ALT) mutated sequence:

```
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
```

## Pricing

AlphaGenome requires a paid subscription. For information about AlphaGenome pricing, [contact a Google Cloud sales specialist](https://cloud.google.com/contact) or work with your Google Cloud account team.

You are responsible for the cost of infrastructure used to host the model, including the Agent Platform endpoint and the GPU instances the model is deployed on. For more information, see [Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .

## Limitations

AlphaGenome has the following limitations:

- **Research use only** : AlphaGenome is a research tool and isn't intended or cleared for clinical diagnostic use.
- **1 MB context horizon** : A single prediction query can't capture genomic interactions that occur over distances larger than 1 MB.
- **No fine-tuning support** : AlphaGenome doesn't support fine-tuning on private training datasets. The model is available for inference only.

## Scientific reference directory

To support the scientific and developer communities, the following table lists primary reference materials, literature, and resources for AlphaGenome:

| Resource type       | Title and link                                                                                                                                                                       | Description                                                                                                     |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| Peer-reviewed paper | [Advancing regulatory variant effect prediction with AlphaGenome, *Nature* (January 2026)](https://doi.org/10.1038/s41586-025-10014-0)                                               | The primary scientific publication detailing the model's architecture, evaluations, and performance benchmarks. |
| Pre-print article   | [AlphaGenome: advancing regulatory variant effect prediction with a unified DNA sequence model, bioRxiv (July 2025)](https://www.biorxiv.org/content/10.1101/2025.06.25.661532v2)    | The initial pre-peer-review manuscript.                                                                         |
| Announcement        | [AlphaGenome: AI for better understanding the genome, Google DeepMind blog (June 2025)](https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/)            | The high-level release blog post outlining the model's impact on genomics.                                      |
| API documentation   | [AlphaGenome documentation](https://www.alphagenomedocs.com)                                                                                                                         | Technical documentation for the Python SDK and HTTP API schemas.                                                |
| Video walkthrough   | [AlphaGenome: AI for better understanding the genome](https://www.youtube.com/watch?v=Xbvloe13nak)                                                                                   | Video walkthrough outlining the model capabilities and basic interaction flows. *(Video runtime: 30 minutes)*   |
| Quickstart notebook | [AlphaGenome quickstart Colab notebook](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/alphagenome/cloudai_alphagenome_vai_quickstart.ipynb) | A notebook providing executable examples of SDK initialization and variant effect scoring.                      |

## Support and feedback

You can get support for AlphaGenome in the following ways:

- **Genomic science and model output support** : For discussions about biology, model predictions, or interpretability, or to engage with Google DeepMind, join the public AlphaGenome Community Forum at [alphagenomecommunity.com](https://alphagenomecommunity.com) .
- **Infrastructure and platform support** : For questions about Google Cloud quotas, accelerators, client library issues, or billing, contact your Google Cloud account team or open a case with Cloud Customer Care.
