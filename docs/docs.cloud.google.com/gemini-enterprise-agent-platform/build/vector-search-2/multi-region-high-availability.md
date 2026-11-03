---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/multi-region-high-availability
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/multi-region-high-availability
title: Multi-Region High-Availability
description: Multi-Region High-Availability
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## High-Availability Deployment

When using the Agent Retrieval service in the `us` multi-region, you benefit from a stronger serving availability SLA, and continuous uptime even in the event of a regional outage.

The `us` multi-region provides the same API as the rest of Agent Retrieval, with some [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/multi-region-high-availability#limitations) . Your data in the `us` multi-region location is replicated to regions across the continental United States, and all active indexes in the `us` multi-region have redundant servers provisioned in each of these regions. Under normal operating conditions, your queries are served from the region to which your network client has optimal latency. In the event of an outage or loss of serving capacity, google's load balancer will redirect your query to the nearest available region. Setup and maintenance of the load balancing and replication is entirely managed by Agent Retrieval.

NOTE: Given the commitment of hardware and engineering resources necessary to support Agent Retrieval with high-availability, customer projects may be onboarded to the high-availability multi-region only after being specifically vetted and allow-listed. To be considered for access to the high-availability multi-region, fill out [the linked request form](https://forms.gle/Nd8YHTPirwczNtrq6) .

## Onboarding

You must request to be allow-listed for access to the high-availability multi-region.

After you receive confirmation that your project has been allow-listed for access to the high-availability multi-region, you can create new collections, data objects, and indexes in the `us` multi-region location. Follow the standard Agent Retrieval API documentation, substituting `us` where you would normally specify a single region (such as `us-central1` or `europe-central2` ).

All data uploaded and operations performed in the `us` multi-region benefit from the enhanced replication, redundancy, and higher availability.

## Billing

Billing rates for the multi-region location are higher than for the standard single-region, reflecting the increased costs of replication and higher operational priority.

For details, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/pricing#agent-retrieval) .

## Limitations

**Storage optimized is not implemented.** Only Performance Optimized tier indexes may be deployed in the multi-region location.

**SearchDataObjects calls to indexes over unnormalized embedding vectors may report unexpected distance metrics** in the multi-region location. The retrieval and ranking of datapoints from these indexes will be correct (within the limitations of an approximate nearest neighbor index). We recommend that you always provide normalized embedding vectors, or rely on automatic embedding generation.

**Only the DOT_PRODUCT_DISTANCE is supported** in the multi-region location.

**Sparse embeddings are not supported** in the multi-region location. For vector search requests where specific tokens must be present in certain fields, the `$search` operator may be used in the request's filter expression.

**The `Index.dedicated_infrastructure.autoscaling_spec` field in CreateIndex and UpdateIndex requests is not used** in the multi-region location.

**The `SearchHint.IndexHint.dense_scann_params` field in SearchDataObjectsRequests are not used** in the multi-region location. The multi-region ANN indexes are tuned to provide approximately 95% recall, though recall may vary based on specifics of your data.

## Migrate from a regional deployment

If you have data in a regional Agent Retrieval collection, the following high-level workflow can be used to clone that data into the `us` location:

- Export your collection data into a bucket in the region which hosts the collection, removing etags;
- Import from the bucket into a collection hosted in the `us` location.

## Before you start

Ensure you have:

- A bucket in the source region, to be used as the export staging area.
- The `gcloud` CLI installed.
- IAM permission read on the source collection, write on the destination, read and write on the bucket.
- A destination collection already created in `us` with the same schema as the source.

`PROJECT_ID` : the project which contains the collection to be migrated. The following commands assume the source and destination project are the same.

`SOURCE_LOCATION` : the location of the source collection, such as `us-central1` .

`SOURCE_COLLECTION` : the name of the collection to be migrated.

`STAGING_BUCKET` : the path to a directory within a bucket to which you want the collection data exported, such as `gs://your-bucket-id` .

### Steps

Each snippet is copy-pasteable. Replace the placeholders at the top of each block with values specific to your project, source location, collection and buckets.

#### 1. Export from source region

```
cat > request.json <<EOF
{
  "gcsDestination": {
    "exportUri": "STAGING_BUCKET/export/",
    "format": "JSONL"
  },
  "field_filter": {
    "excluded_fields": {
      "fields": ["etag"]
    }
  }
}
EOF

curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json; charset=utf-8" \
  -d @request.json \
  "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/SOURCE_LOCATION/collections/SOURCE_COLLECTION:exportDataObjects"
```

The response includes an operation name like `projects/.../locations/us-central1/operations/operation-...` . Poll it until `"done": true` .

`EXPORT_OPERATION_NAME`

```
gcloud vector-search operations describe "EXPORT_OPERATION_NAME" \
  --location="SOURCE_LOCATION"
```

#### 2. Import into us

`DEST_COLLECTION` : the name of the collection after migration (can be the same as the original name).

```
gcloud vector-search collections import-data-objects "DEST_COLLECTION" \
  --location="us" \
  --project="PROJECT_ID" \
  --gcs-import-contents-uri="STAGING_BUCKET/export/" \
  --gcs-import-error-uri="STAGING_BUCKET/import-errors/" \
  --gcs-import-output-uri="STAGING_BUCKET/import-output/" \
  --async
```

Poll the returned operation the same way as the export:

`IMPORT_OPERATION_NAME`

```
gcloud vector-search operations describe "IMPORT_OPERATION_NAME" \
  --location="us"
```

#### 3. Verify the import

- Check `gs://your-bucket-uscentral1/import-errors/` for any rejected records.
- Compare record counts between source and destination.
- Run a handful of known queries against both and compare results.
