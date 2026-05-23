---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/create-loadbalancer
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/create-loadbalancer
title: 'Step 3: Create a load balancer'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this step, you create an [Application Load Balancer](https://docs.cloud.google.com/load-balancing/docs/application-load-balancer) to distribute the traffic to backend instances hosted on Cloud Run. In the load balancer configuration, you define the routing rules, which determine how the load balancer directs the traffic. Routing rules include host rules and path matches, which constitute the configuration components of an external Application Load Balancer's [URL map](https://docs.cloud.google.com/load-balancing/docs/url-map-concepts) .

Note that to complete this step, you must have a valid domain name or a valid self-managed certificate.

## Create a load balancer for the Cloud Run service

1.  In the Google Cloud console, go to the **Load balancing** page.

2.  Click **Create load balancer** .

3.  In the **Type of load balancer** section, click **Application Load Balancer (HTTP/HTTPS)** , and then click **Next** .

4.  In the **Public facing or internal** section, click **Public facing (external)** , and then click **Next** .

5.  In the **Global or single region deployment** section, click **Best for global workloads** , and then click **Next** .

6.  In the **Load balancer generation** section, click **Global external Application Load Balancer** , and then click **Next** .

7.  Click **Configure** .

8.  In the **Load Balancer name** field, enter `gemini-streamlit-app-lb` .

9.  Configure the load balancer by completing the **Frontend configuration** , **Backend configuration** , and **Routing rules** sections.

### Frontend Configuration

1.  Specify the following **Frontend configuration** :
    
      - **Name** : Enter `gemini-streamlit-app-frontend` .
    
      - **Protocol** : Select **HTTPS (includes HTTP/2 and HTTP/3)** .
    
      - **Network Service Tier** : Set the **IP address** by [reserving a new external static IP address](https://docs.cloud.google.com/load-balancing/docs/https/setup-global-ext-https-serverless#ip-address) . While reserving the new IP address, specify `genai-app-ip` as the **Name** .
    
      - **Certificate** : Perform the following steps to create a new Google-managed certificate:
        
        1.  Click **Create a new certificate** .
        
        2.  Specify the following details:
            
              - **Name** : Enter `my-genai-app-certificate` .
            
              - **Create mode** : Click **Create Google-managed certificate** .
            
              - **Domains** : Enter the domain name for provisioning the certificate.
        
        3.  Click **Create** .
        
        For more information about Google-managed SSL certificates, see [Use Google-managed SSL certificates](https://docs.cloud.google.com/load-balancing/docs/ssl-certificates/google-managed-certs) .
    
    <!-- end list -->
    
      - Select the **Enable HTTP to HTTPS redirect** checkbox.

2.  Click **Done** .

3.  Click **Backend configuration** to configure the backend.

### Backend configuration

1.  Click the **Backend services & backend buckets** list and then click CEnter the following details:
    
      - **Name** : Enter `gemini-streamlit-app-backend` .
    
      - **Backend type** : Click **Serverless network endpoint group** .
    
      - **Backends** : On the **New Backend** card, perform the following steps:
        
        1.  Click the **Serverless network endpoint groups** list, and then click **Create serverless network endpoint group** .
        
        2.  Enter the following details:
            
              - **Name** : Enter `streamlit-app-neg` .
            
              - **Region** : Select `us-central1` .
            
              - **Serverless network endpoint group type** : Select **Cloud Run** .
            
              - **Select service** : Select the `gemini-streamlit-cloudrun` Cloud Run service.
        
        3.  Click **Create** .
        
        4.  Click **Done** .

2.  Clear the **Enable Cloud CDN** checkbox.

3.  In the **Policy name** box, enter `default-security-policy-gemini-app-backend` .

4.  Click **Create** , and then click **OK** .

5.  Click **Routing rules** to configure the routing rules.

### Routing rules

1.  Click **Advanced host and path rule** .

2.  In the **Host and path rules** section, click **(Default) Route traffic to backend "" for any unmatched hosts** , and then enter the following details:
    
      - **Action** : Select **Route traffic to a single backend** .
    
      - **Backend** : Select `gemini-streamlit-app-backend` .
        
        > **Note:** This rule handles the traffic for any unmatched host.

3.  Click **Done** .

4.  Click **Add host and path rule** to add a new rule.

5.  Under **New host and path rule** , enter the following details:
    
      - **Hosts** : Enter the domain name used while creating the Google-managed certificate.
    
      - **Path Matcher** : Copy the following URL map configuration:
        
            defaultService: projects/PROJECT_ID/global/backendServices/gemini-streamlit-app-backend
            name: matcher1
            routeRules:
              - matchRules:
                  - prefixMatch: /gemini-streamlit-app
                priority: PRIORITY
                routeAction:
                  weightedBackendServices:
                    - backendService: projects/PROJECT_ID/global/backendServices/gemini-streamlit-app-backend
                      weight: 100
        
        Replace the following:
        
          - PROJECT\_ID : Your Google Cloud project ID.
        
          - PRIORITY : Specify the priority of the backend service by which the route rules are evaluated. In this scenario, set this to any value because you created only one backend service.

6.  Click **Done** .

7.  Click **Review and finalize** to review the configuration and create the load balancer.

### Review and finalize

1.  Review the load balancer configuration.

2.  To create the load balancer, click **Create** .

## Add the IP address to the domain DNS records

Update the DNS records of your domain to point to the reserved IP address that was created for your load balancer. You might have to contact the administrator of your domain to complete this step.
