---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/runtime-contract
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/runtime-contract
title: Agent Platform runtime contract
description: Learn about the HTTP runtime contract for deploying custom containers on Agent Runtime.
data_source: docs.cloud.google.com
---

Agent Runtime is designed to be independent of the application framework. If you choose to deploy your agent using a custom container or a Dockerfile, your container must adhere to the runtime contract to successfully serve queries.

For more information about deployment methods, see [Deploy an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .

## Constraints and requirements

To deploy a custom container on Agent Runtime, the container must listen for HTTP requests on `0.0.0.0` on port `8080` .

### Endpoints (Optional)

Your container can expose any custom HTTP endpoints. You can invoke these custom endpoints by sending requests to the deployed agent's underlying API. For more information, see [Use deployed agents through their underlying API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent#use_deployed_agents_through_their_underlying_api) .

While these endpoints are optional at the API level, implementing them enables the following integration features:

  - **Python SDK support** : Implementing both `/api/reasoning_engine` and `/api/stream_reasoning_engine` lets you use your deployed agent through the [Agent Platform Python SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent#sdk) .
  - **Playground support** : Implementing `/api/stream_reasoning_engine` is required if you want to interact with your agent through the Google Cloud console playground. For more information, see [Playground support](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent#playground_support) .

If you want to use these features, you must implement the following endpoints:

  - `/api/reasoning_engine` : Used for serving queries sent to the `reasoningEngines/query` REST API or the Python SDK's synchronous and asynchronous query methods.
  - `/api/stream_reasoning_engine` : Used for serving queries sent to the `reasoningEngines/streamQuery` REST API or the Python SDK's streaming query methods.

## Class methods and execution modes

When deploying a custom container, you must declare the supported class methods in the `classMethods` list of the deployment specification. These class methods correspond to the operations you defined when developing your agent (see [Registering custom methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-a-custom-agent#custom-methods) and [Query the agent using supported operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-a-custom-agent#query-operations) ). Each declared method has a `name` and an `api_mode` which determines how it is routed:

| API Mode                         | Execution Type           | Routing Endpoint               |
| :------------------------------- | :----------------------- | :----------------------------- |
| `""` (empty string) or `"async"` | Unary (Request-Response) | `/api/reasoning_engine`        |
| `"stream"` or `"async_stream"`   | Streaming                | `/api/stream_reasoning_engine` |

When a client invokes a method, the Agent Runtime service sends a `POST` request to the corresponding routing endpoint in your container. The JSON body of the request contains the `class_method` field (matching the method name) and the `input` field.

### Required methods for integration

To use the Python SDK or the Google Cloud console playground, your container must implement the specific methods that these integrations expect:

  - **SDK standard query** : Requires `query` (mode `""` or `"async"` ) and `stream_query` (mode `"stream"` or `"async_stream"` ).
  - **Playground** : Requires `stream_query` (mode `"stream"` or `"async_stream"` ).

### ADK integration

If you are deploying an agent built with the Agent Development Kit (ADK), you can build your own proxy container in the programming language and server framework of your choice. To support the full set of ADK features, your container must implement the methods defined by the ADK contract. For more information, see [Use an ADK agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-adk-agent) and [Register and manage an ADK agent](https://docs.cloud.google.com/gemini/enterprise/docs/register-and-manage-an-adk-agent) .

You can consult the `AdkApp` template as a reference implementation. For more information, see the [AdkApp reference documentation](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.agent_engines.AdkApp) and the [AdkApp source code](https://github.com/googleapis/python-aiplatform/blob/main/vertexai/agent_engines/templates/adk.py) .

If you want Google to automatically handle updates when you update your version of ADK, you should use the tooling provided by ADK for deploying agents instead of writing your own API server. For more information, see the [ADK deployment documentation](https://adk.dev/deploy/agent-runtime/deploy/) .

## API specifications

Both `/api/reasoning_engine` and `/api/stream_reasoning_engine` receive HTTP `POST` requests with a JSON body containing the following fields:

  - `class_method` (string): The method name of the underlying agent to be invoked (for example, `query` or `stream_query` ).
  - `input` (JSON object): The arguments to be passed to the specified class method.

### `/api/reasoning_engine` (Unary)

  - **Request method** : `POST`
  - **Request body** : `json { "class_method": "query", "input": { "message": "What is the capital of France?" } }`
  - **Response** : A JSON object containing the output of the agent execution. `json { "output": "The capital of France is Paris." }`

### `/api/stream_reasoning_engine` (Streaming)

  - **Request method** : `POST`
  - **Request body** : `json { "class_method": "stream_query", "input": { "message": "Tell me a short story." } }`
  - **Response** : A stream of line-delimited JSON (ndjson), where each line is a JSON-encoded chunk of the response. `json {"output": "Once"} {"output": " upon"} {"output": " a time..."}`

## Example API server (Python)

The following is an example of a FastAPI server in Python that implements the Agent Platform runtime contract. This server wraps an example agent ( `SimpleAgent` ) and handles routing and encoding. You can replace `SimpleAgent` with your own agent implementation.

To run this example, ensure you have `fastapi` , `uvicorn` , and `pydantic` installed.

    import inspect
    import json
    import logging
    import os
    import uvicorn
    from fastapi import FastAPI, encoders, responses
    from pydantic import BaseModel
    
    app = FastAPI()
    
    # Define the request body structure
    class QueryRequest(BaseModel):
        input: dict | None = None
        class_method: str
    
    # Example Agent implementation
    class SimpleAgent:
        def query(self, message: str) -> str:
            return f"Echo: {message}"
    
        async def stream_query(self, message: str):
            words = message.split()
            for word in words:
                yield {"output": word + " "}
    
    agent = SimpleAgent()
    
    def _encode_chunk_to_json(chunk):
        """Encodes a chunk to a JSON string with a newline."""
        try:
            json_chunk = encoders.jsonable_encoder(chunk)
            return json.dumps(json_chunk) + "\n"
        except Exception:
            logging.exception("Failed to encode chunk")
            return None
    
    async def json_generator(output):
        async for chunk in output:
            encoded_chunk = _encode_chunk_to_json(chunk)
            if encoded_chunk is None:
                break
            yield encoded_chunk
    
    async def _invoke_callable_or_raise(invocation_callable, invocation_payload):
        if inspect.iscoroutinefunction(invocation_callable):
            return await invocation_callable(**invocation_payload)
        else:
            return invocation_callable(**invocation_payload)
    
    @app.post("/api/reasoning_engine")
    async def query_endpoint(request: QueryRequest) -> responses.JSONResponse:
        try:
            method = getattr(agent, request.class_method)
        except AttributeError:
            return responses.JSONResponse(
                status_code=400,
                content={"error": f"Method {request.class_method} not found on agent"}
            )
    
        output = await _invoke_callable_or_raise(method, request.input or {})
    
        try:
            json_serialized_content = encoders.jsonable_encoder({"output": output})
        except ValueError as encoding_error:
            logging.exception("Failed to JSON-encode response: %s", encoding_error)
            raise encoding_error
        return responses.JSONResponse(content=json_serialized_content)
    
    @app.post("/api/stream_reasoning_engine")
    async def stream_query_endpoint(request: QueryRequest) -> responses.StreamingResponse:
        try:
            method = getattr(agent, request.class_method)
        except AttributeError:
            return responses.StreamingResponse(
                content=iter([json.dumps({"error": f"Method {request.class_method} not found"})]),
                status_code=400,
                media_type="application/json"
            )
    
        output = await _invoke_callable_or_raise(method, request.input or {})
        return responses.StreamingResponse(
            content=json_generator(output),
            media_type="application/json",
        )
    
    if __name__ == "__main__":
        # The container must listen on 0.0.0.0 and port 8080
        uvicorn.run(app, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))
