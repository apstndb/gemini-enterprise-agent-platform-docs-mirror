---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/orchestration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/orchestration
title: Task orchestration
description: Orchestrate long-horizon robotics tasks with Gemini Robotics ER 2 by combining spatial reasoning with custom robot APIs.
data_source: docs.cloud.google.com
---

> **Note:** This page is part of the [Gemini Robotics ER 2](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er) documentation. Complete the [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er#before-you-begin) setup before you run these examples.

Gemini Robotics ER 2 can plan tasks and reason about space, inferring which actions to take and which objects to move to complete a goal. This page shows an example for [driving a pick-and-place](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/orchestration#calling-custom-robot-api) operation through a custom robot API to orchestrate the task of placing an item into a bowl.

For full runnable code, see the [Robotics cookbook](https://github.com/google-gemini/robotics-samples/blob/main/Getting%20Started/gemini_robotics_er.ipynb) .

## Call a custom robot API

This example demonstrates task orchestration with a custom robot API. It introduces a mock API designed for a pick-and-place operation. The task is to pick up a blue block and place it in an orange bowl:

![An image of the block and bowl](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/images/robot-api-example.png)

This example uses the following mock robot API and tool definitions. Instead of returning the sequence of actions as text, the model calls these functions through the Google Gen AI SDK function-calling interface:

### Python

```
from google import genai
from google.genai import types

client = genai.Client(
    enterprise=True,
    project="your-project-id",
    location="global",
)

def move(x, y, high):
    print(f"Mock Robot: Moving to coordinates: {x}, {y}, {'high above table' if high else 'down at table level'}")

def setGripperState(opened):
    print(f"Mock Robot: {'Opening gripper' if opened else 'Closing gripper'}")

robot_origin_y = 300
robot_origin_x = 500

move_declaration = types.FunctionDeclaration(
    name="move",
    description="Moves the arm to the given coordinates.",
    parameters=types.Schema(
        type=types.Type.OBJECT,
        properties={
            "x": types.Schema(type=types.Type.INTEGER, description="X coordinate relative to the origin"),
            "y": types.Schema(type=types.Type.INTEGER, description="Y coordinate relative to the origin"),
            "high": types.Schema(type=types.Type.BOOLEAN, description="Set to True to lift the robot arm above the scene. Set to False to place the gripper on the surface."),
        },
        required=["x", "y", "high"],
    ),
)

set_gripper_state_declaration = types.FunctionDeclaration(
    name="setGripperState",
    description="Opens or closes the robot's gripper.",
    parameters=types.Schema(
        type=types.Type.OBJECT,
        properties={
            "opened": types.Schema(type=types.Type.BOOLEAN, description="True opens the gripper, False closes the gripper."),
        },
        required=["opened"],
    ),
)

robot_tools = types.Tool(function_declarations=[move_declaration, set_gripper_state_declaration])
```

The following example sends the prompt and image to the model along with the tool definitions. It then runs an agentic loop: after each model response, it executes any requested function calls ( `move` , `setGripperState` ), sends the results back to the model, and repeats until the model stops calling functions or the step limit is reached.

### Python

```
with open("robot-api-example.png", "rb") as f:
    img_bytes = f.read()

prompt = (
    "You are a robotic arm with six degrees-of-freedom. "
    f"The origin point for calculating the moves is at normalized point y={robot_origin_y}, x={robot_origin_x}. "
    "Use this as the new (0,0) for calculating moves, allowing x and y to be negative.\n\n"
    "Find the blue block and the orange bowl. Calculate their coordinates relative to the origin.\n"
    "Perform a pick and place operation where you pick up the blue block and place it into the orange bowl. "
    "Call the appropriate sequence of functions to complete this operation."
)

contents = [
    types.Content(role="user", parts=[
        types.Part.from_bytes(data=img_bytes, mime_type="image/png"),
        types.Part(text=prompt),
    ])
]

print("\n--- Executing Orchestrated Plan ---")

max_steps = 15  # Safety limit to prevent infinite loops
step_count = 0

# The agentic loop
while step_count < max_steps:
    step_count += 1

    response = client.models.generate_content(
        model="gemini-robotics-er-2-preview",
        contents=contents,
        config=types.GenerateContentConfig(
            tools=[robot_tools],
            thinking_config=types.ThinkingConfig(
                thinking_level=types.ThinkingLevel.LOW
            ),
        ),
    )

    # Add the model response to the conversation history
    contents.append(response.candidates[0].content)

    # Check for function calls
    function_calls = [
        part for part in response.candidates[0].content.parts if part.function_call
    ]

    if not function_calls:
        # The model is done calling functions
        print("Sequence complete.")
        print(f"Model Summary: {response.text}")
        break

    # Execute function calls and collect results
    function_response_parts = []
    for part in function_calls:
        fc = part.function_call
        if fc.name == "move":
            move(**fc.args)
        elif fc.name == "setGripperState":
            setGripperState(**fc.args)

        function_response_parts.append(
            types.Part.from_function_response(
                name=fc.name,
                response={"status": "success"},
            )
        )

    # Send the function results back to the model
    contents.append(types.Content(role="user", parts=function_response_parts))
```

The following shows a possible output of the model based on the prompt and the mock robot API. The output includes the results of the robot function calls that the model sequenced together:

```
--- Executing Orchestrated Plan ---
Mock Robot: Opening gripper
Mock Robot: Moving to coordinates: 160, 440, high above table
Mock Robot: Moving to coordinates: 160, 440, down at table level
Mock Robot: Closing gripper
Mock Robot: Moving to coordinates: 160, 440, high above table
Mock Robot: Moving to coordinates: -250, 60, high above table
Mock Robot: Moving to coordinates: -250, 60, down at table level
Mock Robot: Opening gripper
Mock Robot: Moving to coordinates: -250, 60, high above table
Sequence complete.
Model Summary: I have completed the task of picking up the blue block and placing it into the orange bowl.
```

## What's next

To learn more about Gemini Robotics ER 2, see the following resources:

- [Video understanding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/video-understanding) : track task progress from video.
- [Spatial reasoning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/spatial) : pointing, tracking, and bounding box examples.
- [Agentic capabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/agentic) : code execution, instrument reading, and image annotation.
- [Gemini Robotics ER 2 overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er) : capabilities and quickstart.
- [Gemini Robotics ER 2 model information](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/robotics-er-2) : technical specifications, token limits, and supported capabilities.
