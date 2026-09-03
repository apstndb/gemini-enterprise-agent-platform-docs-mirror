---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling
title: Autonomous agent scheduling
description: Optimize your agentic workflows using the Gemini Enterprise Agent Platform deferred tier for off-peak scheduling.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

When deploying multi-step agentic workflows (such as large-scale document synthesis and long-running research), running background agents on real-time models can create unnecessary infrastructure pressure and trigger resource exhaustion (429) errors.

Gemini Enterprise Agent Platform offers a *deferred tier* , a throughput-optimized scheduler designed specifically for latency-tolerant workloads. Instead of treating long-running autonomous tasks with the same immediate urgency as a live chat query, the scheduler queues your complex multi-step agent workflows to off-peak hours to target high success rates and overall throughput.

When you submit a request using the deferred tier, the API accepts the task asynchronously and returns an interaction ID immediately. The deferred tier features the following:

  - **Discounted rate** : You receive a 50% discount on model inference pricing compared to a standard request, so you can manage your agent cost in production. For more information, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

  - **Higher throughput** : The deferred tier mitigates 429s (model capacity constraints) and rate limits by moving your heavy, asynchronous workloads off-peak, freeing up Standard Tier quota for your real-time production needs.

  - **Completion timeout** : The deferred tier targets completing 95% of tasks within 24 hours. If a task doesn't complete within this window, it expires and transitions to a `failed` state. The actual time spent in the queue depends on current regional cluster capacity and demand.

## Use cases

The deferred tier is a good fit for use cases that can tolerate hours of turnaround time, such as the following examples:

  - **Finance** : Daily or weekly equity and market research.

  - **Legal & compliance** : Multi-document regulatory and mergers and acquisitions due diligence.

  - **Strategy** : Continuous competitive intelligence and trend synthesis.

  - **Security** : Codebase vulnerability scanning and fix.

## Supported agents

You can configure autonomous agent scheduling for the [Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .

## Create a deferred task

The following example shows how to [start a Deep Research task](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research#start-research-task) using the deferred tier with `client.interactions.create()` :

    import time
    from google import genai
    
    client = genai.Client(
        enterprise=True,
        project="PROJECT_ID",
        location="global",
    )
    
    PROMPT = "Analyze the latest market trends in renewable energy storage."
    DEEP_RESEARCH_AGENT = "deep-research-preview-04-2026"
    
    interaction = client.interactions.create(
        input=PROMPT,
        agent=DEEP_RESEARCH_AGENT,  # Agent identifier
        service_tier="deferred",  # Run on deferred tier for off-peak scheduling
        background=True,  # Return immediately instead of waiting for the answer
        store=True,  # Persist interaction state to poll or stream later
        stream=False,  # `stream` must be set to False during task creation
    )
    
    print(f"Interaction ID: {interaction.id}")
    print(f"Status:         {interaction.status}")
    print(f"Service tier:   {interaction.service_tier}")

The method returns immediately with `status="in_progress"` and `service_tier="deferred"` .

## Monitor task progress

While awaiting off-peak capacity and actively running, the interaction `status` remains `in_progress` . As the agent executes planning, search, and analysis steps, new items append to the `steps` list.

You can track the task status programmatically by polling the interaction periodically or streaming updates.

### Polling

Poll the interaction periodically (such as every 15–30 seconds) until the interaction reaches one of the terminal states: `completed` , `failed` , or `cancelled` .

    TERMINAL_STATES = ("completed", "failed", "cancelled")
    POLL_INTERVAL_SECONDS = 15
    TIMEOUT_MINUTES = 60
    
    started = time.time()
    deadline = started + TIMEOUT_MINUTES * 60
    
    while True:
      current = client.interactions.get(interaction.id)
      elapsed = int(time.time() - started)
      steps = getattr(current, "steps", None) or []
      print(f"[{elapsed:>4}s] status={current.status} steps={len(steps)}")
    
      if current.status in TERMINAL_STATES:
        break
      if time.time() >= deadline:
        raise TimeoutError(
            f"Still {current.status} after {TIMEOUT_MINUTES} min. The interaction "
            "continues running server-side; re-run the check to resume polling."
        )
      time.sleep(POLL_INTERVAL_SECONDS)
    
    print(f"\nFinished in {int(time.time() - started)}s with status={current.status}.")

### Streaming

You can stream updates in real time once the interaction enters `in_progress` status by setting `stream=True` alongside `background=True` and `store=True` . The stream pushes events such as intermediate thoughts, text deltas, and status updates as they occur.

If the connection drops while the task is still `in_progress` , you can reconnect to the stream using `client.interactions.get()` with `stream=True` and pass the last received event ID to `last_event_id` . If you omit `last_event_id` , the API replays every event from the beginning.

    INTERACTION_ID = interaction.id  # from the create step
    MAX_RECONNECTS = 5
    STREAM_TIMEOUT = 300  # seconds
    
    print(
        f"streaming interaction: {INTERACTION_ID} (status={interaction.status})\n"
    )
    
    def render(event):
      """Prints one SSE event. Returns True once the interaction has finished."""
      if event.event_type == "step.delta":
        delta = event.delta
        if delta.type == "text":
          print(delta.text, end="", flush=True)
        elif delta.type == "thought_summary":
          summary = (getattr(delta.content, "text", "") or "").strip()
          if summary:
            print(f"\n[thinking] {summary[:200]}", flush=True)
        elif delta.type.endswith("_call"):
          queries = getattr(getattr(delta, "arguments", None), "queries", None)
          print(
              f"\n[{delta.type}] {', '.join(queries) if queries else ''}",
              flush=True,
          )
      elif event.event_type == "interaction.status_update":
        print(f"[status] {event.status}", flush=True)
      elif event.event_type == "interaction.completed":
        print(f"\n\n[status] {event.interaction.status}", flush=True)
        return True
      elif event.event_type == "error":
        print(f"\n[error] {event.error.message}", flush=True)
        return True
      return False
    
    last_event_id = None
    finished = False
    
    for attempt in range(MAX_RECONNECTS):
      try:
        # stream=True turns the GET into a live subscription. last_event_id=None on
        # the first pass, so the server starts from the beginning of the run.
        for event in client.interactions.get(
            INTERACTION_ID,
            stream=True,
            last_event_id=last_event_id,
            timeout=STREAM_TIMEOUT,
        ):
          last_event_id = event.event_id or last_event_id
          finished = render(event) or finished
      except Exception as e:  # pylint: disable=broad-except
        # A dropped connection loses nothing: the run continues server-side and the
        # next iteration reattaches from last_event_id.
        print(f"\n[stream dropped: {type(e).__name__}] reattaching...", flush=True)
    
      if finished:
        break
      # The server also closes the stream when the run ends, without an error.
      if (
          client.interactions.get(INTERACTION_ID, timeout=STREAM_TIMEOUT).status
          != "in_progress"
      ):
        break
    else:
      print(f"\n[gave up after {MAX_RECONNECTS} reconnects]")
    
    print(f"\n\nStreamed interaction: {INTERACTION_ID}")

## Cancel a task

You can cancel a task while its status is `queued` , `in_progress` , or `requires_action` . When you cancel a task, its status transitions to `cancelled` .

To cancel a task, use `client.interactions.cancel()` :

    client.interactions.cancel(INTERACTION_ID)

## Retrieve the final output and token usage

When the interaction reaches the `completed` state, the full transcript is available in the `steps` list. The final answer is the text content of the last step that produced output.

Because the interaction is stored ( `store=True` ), you can fetch the result at any time using the interaction ID from any session:

    def get_final_text(completed_interaction):
      """Returns the text of the last step that produced output."""
      for step in reversed(getattr(completed_interaction, "steps", None) or []):
        text = "".join(
            part.text for part in (getattr(step, "content", None) or [])
            if getattr(part, "text", None)
        )
        if text:
          return text
      return ""
    
    
    final = client.interactions.get(interaction.id)
    print(f"Status: {final.status}\n")
    print(get_final_text(final) or "(No text output)")
    
    if final.usage:
      print(
          f"\nToken usage:\n"
          f"  Input tokens:  {final.usage.total_input_tokens}\n"
          f"  Output tokens: {final.usage.total_output_tokens}\n"
          f"  Total tokens:  {final.usage.total_tokens}"
      )
