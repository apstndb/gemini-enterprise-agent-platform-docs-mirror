---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/jwt-auth
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/jwt-auth
title: JSON Web Token authentication
description: Set up a Vector Search index endpoint with JWT authentication, controlling access by allowing only clients using authorized Google service accounts to interact with the endpoint using signed JWTs.
data_source: docs.cloud.google.com
---

Vector Search supports authenticated index endpoints using [self-signed JSON Web Tokens (JWTs)](https://docs.cloud.google.com/docs/authentication/token-types#sa-jwts) . To control access to the index endpoint, it's configured to accept only signed JWTs issued by specifically authorized Google service accounts. This means only clients using those designated accounts can interact with the endpoint.

This page outlines the required steps for setting up an index endpoint with JSON Web Token (JWT) authentication and running queries against it.

## Limitations

  - JWT authentication is supported only for private endpoints with [VPC peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/vpc) or [Private Service Connect (PSC)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect) .
  - JWT authentication is supported only for data plane RPC APIs (such as MatchService) that are invoked by using gRPC. The RPC examples in this page use the open source [`grpc_cli`](https://github.com/grpc/grpc/blob/master/doc/command_line_tool.md) tool to send gRPC requests to the deployed index server.
  - Admin APIs for creation, deployment, and management of indexes are secured by using [predefined IAM roles](https://docs.cloud.google.com/iam/docs/understanding-roles) .

## Creating and using a JWT to query an index

Follow these steps to create an index endpoint and query it with a self-signed JWT.

### Create an index

Create a Vector Search index by following the instructions in [Create an index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/create-manage-index) .

### Create a private endpoint

Create a private endpoint by following the instructions in one of the following documentation pages:

  - [Set up a VPC Network Peering connection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/vpc)
  - [Vector Search Private Service Connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect)

### Create a service account

Create a service account and grant it the [Service Account Token Creator](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountTokenCreator) IAM role.

1.  Enable the IAM Service Account Credentials API and create a service account:
    
        gcloud services enable iamcredentials.googleapis.com --project="PROJECT_ID"
        gcloud iam service-accounts create SERVICE_ACCOUNT_ID --project="PROJECT_ID"
    
    Replace the following values:
    
      - PROJECT\_ID : The project to create your service account in.
      - SERVICE\_ACCOUNT\_ID : The ID for the service account.
    
    Learn more about [creating a service account](https://docs.cloud.google.com/iam/docs/service-accounts-create) .

2.  Use one of the following commands to grant the `iam.serviceAccountTokenCreator` IAM role to your service account:
    
      - The following command gives you permission to create JWTs by using the service account from a Compute Engine VM that has the service account attached to it:
        
            gcloud iam service-accounts add-iam-policy-binding \
               "SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
               --role "roles/iam.serviceAccountTokenCreator" \
               --member "serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
               --project "PROJECT_ID"
        
        Replace the following values:
        
          - SERVICE\_ACCOUNT\_ID : The ID for the service account.
          - PROJECT\_ID : The project to create your service account in.
    
      - The following command grants permission to create JWTs by using the service account from your own Google Account (on your workstation):
        
            gcloud iam service-accounts add-iam-policy-binding \
               "SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
               --role "roles/iam.serviceAccountTokenCreator" \
               --member "user:EMAIL_ADDRESS" \
               --project PROJECT_ID
        
        Replace the following values:
        
          - SERVICE\_ACCOUNT\_ID : The ID for the service account.
          - PROJECT\_ID : The project to create your service account in.
          - EMAIL\_ADDRESS : Your email address.

### Deploy the index to the endpoint with JWT auth config

1.  Deploy the index to the private endpoint as shown in the following example:
    
        gcloud ai index-endpoints deploy-index INDEX_ENDPOINT_ID \
           --index=INDEX_ID \
           --deployed-index-id=DEPLOYED_INDEX_ID \
           --display-name=DEPLOYED_INDEX_NAME \
           --audiences=AUDIENCES \
           --allowed-issuers="SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
           --project=PROJECT_ID \
           --region=LOCATION
    
    Replace the following values:
    
      - INDEX\_ENDPOINT\_ID : The ID of the index endpoint.
      - INDEX\_ID : The ID of the index.
      - DEPLOYED\_INDEX\_ID : A user specified string to uniquely identify the deployed index. It must start with a letter and contain only letters, numbers or underscores. See [DeployedIndex.id](https://cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.DeployedIndex) for format guidelines.
      - DEPLOYED\_INDEX\_NAME : Display name of the deployed index.
      - AUDIENCES : A descriptive string that identifies the expected audience for your service, workload or app, for example, `"123456-my-app"` .
      - SERVICE\_ACCOUNT\_ID : The ID for the service account.
      - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - LOCATION : The region where you are using Agent Platform.

### Query the index with a self-signed JWT

At a high level, the required steps are as follows:

1.  Create a JWT payload.
2.  Sign the token by using the service account created earlier.
3.  Query the index by using a gRPC call, passing the token in the authorization header.

### Python

#### Create and Sign the JWT payload

This example uses the Python IAM API Credentials library's [`sign_jwt` method](https://docs.cloud.google.com/python/docs/reference/iam/latest/google.cloud.iam_credentials_v1.services.iam_credentials.IAMCredentialsClient#google_cloud_iam_credentials_v1_services_iam_credentials_IAMCredentialsClient_sign_jwt) to obtain a signed token. To learn more about how to install and use this library, see the [IAM API Client Libraries documentation](https://docs.cloud.google.com/iam/docs/reference/libraries#credentials-install) .

``` 
   from google.cloud import iam_credentials_v1
   from datetime import datetime, timezone
   import json

   def sign_jwt(issuer: str, audience: str):
      client = iam_credentials_v1.IAMCredentialsClient()
      payload = {
            'aud': audience,
            'sub': audience,
            'iss': issuer,
            'iat': int(datetime.now(timezone.utc).timestamp()),
            'exp': int(datetime.now(timezone.utc).timestamp()) + 600,
      }
      response = client.sign_jwt(name="projects/-/serviceAccounts/" + issuer,
                                 payload=json.dumps(payload))
      return response.signed_jwt

   sign_jwt("SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com",
            "AUDIENCES")
```

### Command-line

#### Create the JWT payload

Vector Search authentication accepts JWTs that are signed with a pre-authorized service account, for a predefined audience. The service account and audience must be specified by the caller when an index is deployed to a private endpoint. Once an index is deployed with these settings, all gRPC API requests to that endpoint are required to include an authorization header containing a JWT that's signed by the issuer (a service account) and targeted at the provided audience. The signed JWT is passed as a bearer token in the `authorization` header of the gRPC request. In addition to being signed by the service account, the JWT must include the following claims:

  - The `iss` (allowed issuer) claim should be the service account email address, for example:
    
        "iss": "SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com"

  - The `aud` (audience) and `sub` (subject) claims should both be set to the same value. This is a descriptive string that identifies the expected audience for your service, workload or app, for example:
    
        "aud": "123456-my-app",
        "sub": "123456-my-app"
    
    This value must match the `--audiences` argument that was passed at index deployment time.

  - The `iat` (issued at) claim should be set to the time the token is issued. The `exp` (expiration time) claim should be set to a short time later (about an hour). These values are expressed in Unix epoch time, for example:
    
        "iat": 1698966927, // unix time since epoch eg via date +%s
        "exp": 1698967527 // iat + a few mins (eg 600 seconds)

The following example shows these claims in a single JWT payload:

    {
       "iss": "SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com",
       "aud": "123456-my-app",
       "sub": "123456-my-app",
       "iat": 1698956084,
       "exp": 1698960084
    }

The JWT payload is signed by using the service account specified in the `iss` claim.

#### Create the JWT

1.  Make sure that you (the caller) can use the `roles/iam.serviceAccountTokenCreator` role on the service account.

2.  Create a JSON file named `jwt_in.json` that contains the raw JWT:
    
        SA="serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com"
        cat << EOF > jwt_in.json
        {
          "aud": "AUDIENCES",
          "sub": "AUDIENCES",
          "iss": "${SA}",
          "iat": $(date +%s),
          "exp": $(expr $(date +%s) + 600)
        }
        EOF
    
    Replace the following values:
    
      - SERVICE\_ACCOUNT\_ID : The ID for the service account.
      - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - AUDIENCES : A descriptive string that identifies the expected audience for your service, workload or app, for example, `"123456-my-app"` .

#### Sign the JWT (REST API)

1.  Using the [`jq` tool](https://jqlang.github.io/jq/) , create the `curl` request payload by encoding the JWT into a string:
    
        cat jwt_in.json | jq -Rsa >request.json

2.  Sign the token by passing the request payload to the [signJwt](https://docs.cloud.google.com/iam/docs/reference/credentials/rest/v1/projects.serviceAccounts/signJwt) REST API method.
    
        SA="serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com"
        curl -X POST \
           -H "Authorization: Bearer $(gcloud auth print-access-token)" \
           -H "Content-Type: application/json; charset=utf-8" \
           -d @request.json \
           "https://iamcredentials.googleapis.com/v1/projects/-/serviceAccounts/$SA:signJwt"
    
    Replace the following values:
    
      - SERVICE\_ACCOUNT\_ID : The ID for the service account.
      - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
    
    Store the returned `signedJwt` value into an environment variable called `signedJwt` .

#### Sign the JWT (gcloud CLI)

Alternatively, you can sign the JWT by passing the `jwt_in.json` file directly to the gcloud CLI [`sign-jwt`](https://docs.cloud.google.com/sdk/gcloud/reference/iam/service-accounts/sign-jwt) method.

    gcloud iam service-accounts sign-jwt jwt_in.json jwt_out \
       --iam-account=SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com

Replace the following values:

  - SERVICE\_ACCOUNT\_ID : The ID for the service account.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

The signed JWT is returned in the `jwt_out` output file. Store it into an environment variable called `signedJwt` .

#### Send the signed JWT to the index endpoint

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def vector_search_match_jwt(
        project: str,
        location: str,
        index_endpoint_name: str,
        deployed_index_id: str,
        queries: List[List[float]],
        num_neighbors: int,
        signed_jwt: str,
    ) -> List[List[aiplatform.matching_engine.matching_engine_index_endpoint.MatchNeighbor]]:
        """Query the vector search index.
    
        Args:
            project (str): Required. Project ID
            location (str): Required. The region name
            index_endpoint_name (str): Required. Index endpoint to run the query
            against. The endpoint must be a private endpoint.
            deployed_index_id (str): Required. The ID of the DeployedIndex to run
            the queries against.
            queries (List[List[float]]): Required. A list of queries. Each query is
            a list of floats, representing a single embedding.
            num_neighbors (int): Required. The number of neighbors to return.
            signed_jwt (str): Required. The signed JWT token for the private
            endpoint. The endpoint must be configured to accept tokens from JWT's
            issuer and encoded audience.
    
        Returns:
            List[List[aiplatform.matching_engine.matching_engine_index_endpoint.MatchNeighbor]] - A list of nearest neighbors for each query.
        """
        # Initialize the Vertex AI client
        aiplatform.init(project=project, location=location)
    
        # Create the index endpoint instance from an existing endpoint.
        my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint(
            index_endpoint_name=index_endpoint_name
        )
    
        # Query the index endpoint for matches.
        resp = my_index_endpoint.match(
            deployed_index_id=deployed_index_id,
            queries=queries,
            num_neighbors=num_neighbors,
            signed_jwt=signed_jwt,
        )
        return resp

### Command-line

From a Compute Engine VM in the same VPC network, call the `MatchService` `gRPC` endpoint, passing the `signedJwt` token in the `authorization` header, as shown in the following example:

    ./grpc_cli call ${TARGET_IP}:10000 google.cloud.aiplatform.container.v1.MatchService.Match \
       '{deployed_index_id: "${DEPLOYED_INDEX_ID}", float_val: [-0.1,..]}' \
       --metadata "authorization: Bearer $signedJwt"

To run this command, you'll need the following environment variables to be set:

  - TARGET\_IP is the IP address for your deployed index server. To learn how to retrieve this value, see [Query indexes to get nearest neighbors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/query-index-vpc) .
  - DEPLOYED\_INDEX\_ID : A user specified string to uniquely identify the deployed index. It must start with a letter and contain only letters, numbers or underscores. See [DeployedIndex.id](https://cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.DeployedIndex) for format guidelines.

`signedJwt` is the environment variable containing your signed JWT.

## Troubleshooting

The following table lists some common `gRPC` error messages.

| gRPC Error Message                                     | Reason                                                              |
| ------------------------------------------------------ | ------------------------------------------------------------------- |
| Authorization header not found for index ' INDEX\_ID ' | The gRPC metadata doesn't contain an authorization header           |
| JWT is invalid format                                  | The token is malformed and can't be parsed correctly                |
| JWT authentication failed                              | The token is expired or isn't signed by the correct service account |
| JWT issuer should be in the allowed issuers list       | The token `iss` isn't in `auth_config` allowed issuers              |
| Permission check fail for index ' INDEX\_ID '          | The token `aud` or `sub` claim isn't in `auth_config` audiences     |

## What's next

  - To learn more about JWT and token claim structure, see [RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519) .
  - Learn more about how to [Create a self-signed JSON Web Token (JWT)](https://docs.cloud.google.com/iam/docs/create-short-lived-credentials-direct#sa-credentials-jwt)
  - Learn how to [Update and rebuild your index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/update-rebuild-index)
  - Learn how to [Monitor an index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/monitor)
