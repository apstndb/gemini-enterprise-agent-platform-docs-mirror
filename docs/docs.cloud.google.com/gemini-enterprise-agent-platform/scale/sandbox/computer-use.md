---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use
title: Computer Use
description: Guide on how to use Computer Use sandboxes in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides a sandbox environment for AI Agents, and so the "Agentic AI Services" Service Specific Terms apply. To utilize this feature, you will need to enable full network access for your AI Agent so please consider applicable safeguards (including human supervision) and your organization's policies before doing so. For built-in computer use safeguards, consider the Agent Platform [Computer Use Tool](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/computer-use#safety-and-security) .
> 
> Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

Agent Platform Computer Use sandboxes provide a secure, isolated browser environment that your agents can interact with. These sandboxes allow agents to automate tasks that mimic human interactions (such as clicking, navigating sites, and taking screenshots).

## How it works

When you create a Computer Use sandbox, Gemini Enterprise Agent Platform provisions a containerized environment that runs a web browser agent. You can control the browser in two ways:

  - **API requests** : Send commands to the sandbox to perform actions like navigating to a URL, clicking on elements, or typing text.
  - **Browser control** : Connect to the browser by using a standard Chrome DevTools Protocol (CDP) connection, letting you use browser automation tools (such as Playwright) to automate the browser.

### Considerations

During Preview, Agent Platform Computer Use Sandbox latency is optimized for low traffic volumes. Higher traffic volumes might temporarily encounter elevated latency.

### Control the browser using API

You can send API requests to the sandbox to perform common browser actions. The sandbox handles the execution of these actions within its isolated environment.

Supported actions include:

  - Navigating to a URL.
  - Clicking at specific coordinates.
  - Typing text into fields.
  - Taking screenshots.

For an example of how to send commands, see the [Computer Use quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use-quickstart) .

### Control the browser using a CDP connection

For more advanced automation, you can connect to the sandbox browser over a Chrome DevTools Protocol (CDP) connection. This method lets you use standard browser automation tools, such as Playwright, to interact with the webpage.

To connect Playwright to the sandbox:

1.  Generate the WebSocket URL and required headers for your sandbox by using the Python SDK `generate_browser_ws_headers` method.
    
    ``` 
      service_account_email = "SERVICE_ACCOUNT_EMAIL"
      ws_url, ws_headers = client.agent_engines.sandboxes.generate_browser_ws_headers(
          sandbox_environment=sandbox,
          service_account_email=service_account_email,
      )
    ```

2.  Use Playwright's `connect_over_cdp` method to establish a connection.
    
    Use the generated WebSocket URL and headers to connect over CDP using Playwright:
    
    ``` 
      import asyncio
      from playwright.async_api import async_playwright
      import nest_asyncio
      nest_asyncio.apply()
    
      async def connect_over_cdp(ws_url, ws_headers):
          async with async_playwright() as p:
              try:
                  browser = await p.chromium.connect_over_cdp(
                      endpoint_url=ws_url,
                      headers=ws_headers
                  )
                  print("Successfully connected to browser over CDP.")
    
                  # You can now interact with the browser
                  page = browser.contexts[0].pages[0]
                  await page.goto("https://www.example.com")
                  print(f"Page title: {await page.title()}")
    
                  await browser.close()
                  print("Browser connection closed.")
              except Exception as e:
                  print(f"An error occurred: {e}")
    
      # Run CDP connection
      asyncio.run(connect_over_cdp(ws_url, ws_headers))
    ```

## Live streaming view

Computer Use sandboxes support a live streaming view (VNC), letting you to visually monitor the agent's actions in real-time. You can debug and observe the agent's behavior.

For example, you can use noVNC to connect to the sandbox through WebSocket.

## What's next

  - [Computer Use quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use-quickstart)
  - Explore [Snapshots](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/snapshots) for sandbox lifecycle management.
