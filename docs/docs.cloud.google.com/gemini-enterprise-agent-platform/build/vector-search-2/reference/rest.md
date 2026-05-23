---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest
title: Vector Search API
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Vector Search API provides a fully-managed, highly performant, and scalable vector database designed to power next-generation search, recommendation, and generative AI applications. It allows you to store, index, and query your data and its corresponding vector embeddings through a simple, intuitive interface. With Vector Search, you can define custom schemas for your data, insert objects with associated metadata, automatically generate embeddings from your data, and perform fast approximate nearest neighbor (ANN) searches to find semantically similar items at scale.

## Service: vectorsearch.googleapis.com

To call this service, we recommend that you use the Google-provided [client libraries](https://cloud.google.com/apis/docs/client-libraries-explained) . If your application needs to use your own libraries to call this service, use the following information when you make the API requests.

### Discovery document

A [Discovery Document](https://developers.google.com/discovery/v1/reference/apis) is a machine-readable specification for describing and consuming REST APIs. It is used to build client libraries, IDE plugins, and other tools that interact with Google APIs. One service may provide multiple discovery documents. This service provides the following discovery documents:

  - <https://vectorsearch.googleapis.com/$discovery/rest?version=v1>
  - <https://vectorsearch.googleapis.com/$discovery/rest?version=v1beta>

### Service endpoint

A [service endpoint](https://cloud.google.com/apis/design/glossary#api_service_endpoint) is a base URL that specifies the network address of an API service. One service might have multiple service endpoints. This service has the following service endpoint and all URIs below are relative to this service endpoint:

  - `https://vectorsearch.googleapis.com`

## REST Resource: [v1.projects.locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations)

Methods

`  get  `

`GET /v1/{name}`  
Gets information about a location.

`  list  `

`GET /v1/{name}/locations`  
Lists information about the supported locations for this service.

## REST Resource: [v1.projects.locations.collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections)

Methods

`  create  `

`POST /v1/{parent}/collections`  
Creates a new Collection in a given project and location.

`  delete  `

`DELETE /v1/{name}`  
Deletes a single Collection.

`  exportDataObjects  `

`POST /v1/{name}:exportDataObjects`  
Initiates a Long-Running Operation to export DataObjects from a Collection.

`  get  `

`GET /v1/{name}`  
Gets details of a single Collection.

`  importDataObjects  `

`POST /v1/{name}:importDataObjects`  
Initiates a Long-Running Operation to import DataObjects into a Collection.

`  list  `

`GET /v1/{parent}/collections`  
Lists Collections in a given project and location.

`  patch  `

`PATCH /v1/{collection.name}`  
Updates the parameters of a single Collection.

## REST Resource: [v1.projects.locations.collections.dataObjects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects)

Methods

`  aggregate  `

`POST /v1/{parent}/dataObjects:aggregate`  
Aggregates data objects.

`  batchCreate  `

`POST /v1/{parent}/dataObjects:batchCreate`  
Creates a batch of dataObjects.

`  batchDelete  `

`POST /v1/{parent}/dataObjects:batchDelete`  
Deletes dataObjects in a batch.

`  batchSearch  `

`POST /v1/{parent}/dataObjects:batchSearch`  
Batch searches data objects.

`  batchUpdate  `

`POST /v1/{parent}/dataObjects:batchUpdate`  
Updates dataObjects in a batch.

`  create  `

`POST /v1/{parent}/dataObjects`  
Creates a dataObject.

`  delete  `

`DELETE /v1/{name}`  
Deletes a dataObject.

`  get  `

`GET /v1/{name}`  
Gets a data object.

`  patch  `

`PATCH /v1/{dataObject.name}`  
Updates a dataObject.

`  query  `

`POST /v1/{parent}/dataObjects:query`  
Queries data objects.

`  search  `

`POST /v1/{parent}/dataObjects:search`  
Searches data objects.

## REST Resource: [v1.projects.locations.collections.indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes)

Methods

`  create  `

`POST /v1/{parent}/indexes`  
Creates a new Index in a given project and location.

`  delete  `

`DELETE /v1/{name}`  
Deletes a single Index.

`  get  `

`GET /v1/{name}`  
Gets details of a single Index.

`  list  `

`GET /v1/{parent}/indexes`  
Lists Indexes in a given project and location.

`  patch  `

`PATCH /v1/{index.name}`  
Updates the parameters of a single Index.

## REST Resource: [v1.projects.locations.operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.operations)

Methods

`  cancel  `

`POST /v1/{name}:cancel`  
Starts asynchronous cancellation on a long-running operation.

`  delete  `

`DELETE /v1/{name}`  
Deletes a long-running operation.

`  get  `

`GET /v1/{name}`  
Gets the latest state of a long-running operation.

`  list  `

`GET /v1/{name}/operations`  
Lists operations that match the specified filter in the request.

## REST Resource: [v1beta.projects.locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations)

Methods

`  get  `

`GET /v1beta/{name}`  
Gets information about a location.

`  list  `

`GET /v1beta/{name}/locations`  
Lists information about the supported locations for this service.

## REST Resource: [v1beta.projects.locations.collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections)

Methods

`  create  `

`POST /v1beta/{parent}/collections`  
Creates a new Collection in a given project and location.

`  delete  `

`DELETE /v1beta/{name}`  
Deletes a single Collection.

`  exportDataObjects  `

`POST /v1beta/{name}:exportDataObjects`  
Initiates a Long-Running Operation to export DataObjects from a Collection.

`  get  `

`GET /v1beta/{name}`  
Gets details of a single Collection.

`  importDataObjects  `

`POST /v1beta/{name}:importDataObjects`  
Initiates a Long-Running Operation to import DataObjects into a Collection.

`  list  `

`GET /v1beta/{parent}/collections`  
Lists Collections in a given project and location.

`  patch  `

`PATCH /v1beta/{collection.name}`  
Updates the parameters of a single Collection.

## REST Resource: [v1beta.projects.locations.collections.dataObjects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects)

Methods

`  aggregate  `

`POST /v1beta/{parent}/dataObjects:aggregate`  
Aggregates data objects.

`  batchCreate  `

`POST /v1beta/{parent}/dataObjects:batchCreate`  
Creates a batch of dataObjects.

`  batchDelete  `

`POST /v1beta/{parent}/dataObjects:batchDelete`  
Deletes dataObjects in a batch.

`  batchSearch  `

`POST /v1beta/{parent}/dataObjects:batchSearch`  
Batch searches data objects.

`  batchUpdate  `

`POST /v1beta/{parent}/dataObjects:batchUpdate`  
Updates dataObjects in a batch.

`  create  `

`POST /v1beta/{parent}/dataObjects`  
Creates a dataObject.

`  delete  `

`DELETE /v1beta/{name}`  
Deletes a dataObject.

`  get  `

`GET /v1beta/{name}`  
Gets a data object.

`  patch  `

`PATCH /v1beta/{dataObject.name}`  
Updates a dataObject.

`  query  `

`POST /v1beta/{parent}/dataObjects:query`  
Queries data objects.

`  search  `

`POST /v1beta/{parent}/dataObjects:search`  
Searches data objects.

## REST Resource: [v1beta.projects.locations.collections.indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.indexes)

Methods

`  create  `

`POST /v1beta/{parent}/indexes`  
Creates a new Index in a given project and location.

`  delete  `

`DELETE /v1beta/{name}`  
Deletes a single Index.

`  get  `

`GET /v1beta/{name}`  
Gets details of a single Index.

`  list  `

`GET /v1beta/{parent}/indexes`  
Lists Indexes in a given project and location.

`  patch  `

`PATCH /v1beta/{index.name}`  
Updates the parameters of a single Index.

## REST Resource: [v1beta.projects.locations.operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.operations)

Methods

`  cancel  `

`POST /v1beta/{name}:cancel`  
Starts asynchronous cancellation on a long-running operation.

`  delete  `

`DELETE /v1beta/{name}`  
Deletes a long-running operation.

`  get  `

`GET /v1beta/{name}`  
Gets the latest state of a long-running operation.

`  list  `

`GET /v1beta/{name}/operations`  
Lists operations that match the specified filter in the request.
