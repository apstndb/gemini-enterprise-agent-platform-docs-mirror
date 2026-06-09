---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/track-executions-artifacts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/track-executions-artifacts
title: Track executions and artifacts
description: Gemini Enterprise Agent Platform Experiments supports tracking both executions and artifacts.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform Experiments supports tracking both executions and artifacts . Executions are steps in an ML workflow that include but aren't limited to data preprocessing, training, and model evaluation. Executions can consume artifacts such as datasets and produce artifacts such as models.

### Create artifact

The following sample uses the `  create  ` method of the Artifact Class.

### Python

    from typing import Dict, Optional
    
    from google.cloud import aiplatform
    
    
    def create_artifact_sample(
        schema_title: str,
        project: str,
        location: str,
        uri: Optional[str] = None,
        resource_id: Optional[str] = None,
        display_name: Optional[str] = None,
        schema_version: Optional[str] = None,
        description: Optional[str] = None,
        metadata: Optional[Dict] = None,
    ):
        artifact = aiplatform.Artifact.create(
            schema_title=schema_title,
            uri=uri,
            resource_id=resource_id,
            display_name=display_name,
            schema_version=schema_version,
            description=description,
            metadata=metadata,
            project=project,
            location=location,
        )
        return artifact

  - `schema_title` : Required. Identifies the schema title used by the resource.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .
  - `uri` : Optional. URI of artifact's location.
  - `resource_id` : Optional. The `resource_id` portion of the Artifact name with the format. This is globally unique in a metadataStore:  
    `projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id>` .
  - `display_name` : Optional. The user-defined name of the resource.
  - `schema_version` : Optional. Specifies the version used by the resource. If not set, defaults to use the latest version.
  - `description` : Optional. Describes the purpose of the resource to be created.
  - `metadata` : Optional. Contains the metadata information that will be stored in the resource.

### Start execution

The following sample uses the `  start_execution  ` method.

### Python

    from typing import Any, Dict, List, Optional
    
    from google.cloud import aiplatform
    
    
    def start_execution_sample(
        schema_title: str,
        display_name: str,
        input_artifacts: List[aiplatform.Artifact],
        output_artifacts: List[aiplatform.Artifact],
        project: str,
        location: str,
        resource_id: Optional[str] = None,
        metadata: Optional[Dict[str, Any]] = None,
        schema_version: Optional[str] = None,
        resume: bool = False,
    ):
        aiplatform.init(project=project, location=location)
    
        with aiplatform.start_execution(
            schema_title=schema_title,
            display_name=display_name,
            resource_id=resource_id,
            metadata=metadata,
            schema_version=schema_version,
            resume=resume,
        ) as execution:
            execution.assign_input_artifacts(input_artifacts)
            execution.assign_output_artifacts(output_artifacts)
            return execution

  - `schema_title` : Identifies the schema title used by the resource.

  - `display_name` : The user-defined name of the resource.

  - `input_artifacts` : Artifacts to assign as input.

  - `output_artifacts` : Artifacts as outputs to this Execution.

  - `project` : Your project ID. You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

  - `resource_id` : Optional. The `resource_id` portion of the Artifact name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/\<metadata\_store\_id\>/artifacts/\<resource\_id\>.

  - `schema_version` : Optional. Specifies the version used by the resource. If not set, defaults to use the latest version.

  - `metadata` : Optional. Contains the metadata information that will be stored in the resource.

  - `resume` : bool.
    
    Note: When the optional `resume` parameter is specified as `TRUE` , the previously started run resumes. When not specified, `resume` defaults to `FALSE` and a new run is created.

### Notebook samples

  - [Compare models trained and evaluated locally](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)
