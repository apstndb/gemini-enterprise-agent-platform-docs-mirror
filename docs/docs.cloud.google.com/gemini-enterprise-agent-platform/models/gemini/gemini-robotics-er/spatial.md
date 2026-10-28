---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/spatial
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/spatial
title: Spatial reasoning
description: 'Use Gemini Robotics ER 2 for spatial reasoning: point to objects, track them in video, detect bounding boxes, and plan trajectories.'
data_source: docs.cloud.google.com
---

> **Note:** This page is part of the [Gemini Robotics ER 2](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er) documentation. Complete the [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er#before-you-begin) setup before you run these examples.

Gemini Robotics ER 2 can point to objects, track them in video, detect them with bounding boxes, and generate movement trajectories. All examples on this page use natural language prompts with `generate_content` .

For full runnable code, see the [Robotics cookbook](https://github.com/google-gemini/robotics-samples/blob/main/Getting%20Started/gemini_robotics_er.ipynb) .

## Point to objects

The following example finds specific objects in an image and returns their normalized `[y, x]` coordinates:

### Python

```
from google import genai
from google.genai import types

PROMPT = """
          Point to no more than 10 items in the image. The label returned
          should be an identifying name for the object detected.
          The answer should follow the json format: [{"point": <point>,
          "label": <label1>}, ...]. The points are in [y, x] format
          normalized to 0-1000.
        """
client = genai.Client(
    enterprise=True,
    project="your-project-id",
    location="global",
)

# Load your image
with open("my-image.png", 'rb') as f:
    image_bytes = f.read()

image_response = client.models.generate_content(
    model="gemini-robotics-er-2-preview",
    contents=[
        types.Part.from_bytes(
            data=image_bytes,
            mime_type='image/png',
        ),
        PROMPT
    ],
    config = types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(
            thinking_level=types.ThinkingLevel.HIGH
        )
    )
)

print(image_response.text)
```

### REST

```
# First, ensure you have the image file locally.
# Encode the image to base64
IMAGE_BASE64=$(base64 -w 0 my-image.png)

# Set your Google Cloud project and location.
export PROJECT_ID="your-project-id"
export LOCATION="global"
export MODEL="gemini-robotics-er-2-preview"

curl -X POST \
  "https://aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/publishers/google/models/${MODEL}:generateContent" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "contents": [
      {
        "parts": [
          {
            "inlineData": {
              "mimeType": "image/png",
              "data": "'"${IMAGE_BASE64}"'"
            }
          },
          {
            "text": "Point to no more than 10 items in the image. The label returned should be an identifying name for the object detected. The answer should follow the json format: [{\"point\": [y, x], \"label\": <label1>}, ...]. The points are in [y, x] format normalized to 0-1000."
          }
        ]
      }
    ],
    "generationConfig": {
      "thinkingConfig": {
        "thinkingLevel": "HIGH"
      }
    }
  }'
```

The output will be a JSON array containing objects, each with a `point` (normalized `[y, x]` coordinates) and a `label` identifying the object.

### JSON

```
[
  {"point": [376, 508], "label": "small banana"},
  {"point": [287, 609], "label": "larger banana"},
  {"point": [223, 303], "label": "pink starfruit"},
  {"point": [435, 172], "label": "paper bag"},
  {"point": [270, 786], "label": "green plastic bowl"},
  {"point": [488, 775], "label": "metal measuring cup"},
  {"point": [673, 580], "label": "dark blue bowl"},
  {"point": [471, 353], "label": "light blue bowl"},
  {"point": [492, 497], "label": "bread"},
  {"point": [525, 429], "label": "lime"}
]
```

The following image is an example of how these points can be displayed:

![An example that displays the points of objects in an image](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/images/point-to-object.png)

## Track objects in a video

Gemini Robotics ER 2 can also analyze video frames to track objects over time.

### Python

```
from google import genai
from google.genai import types

client = genai.Client(
    enterprise=True,
    project="your-project-id",
    location="global",
)

# Load your video
with open("my-video.mp4", 'rb') as f:
    video_bytes = f.read()

prompt = """
          Point to the red ball in every frame where it appears.
          The answer should follow the json format: [{"point": [y, x],
          "label": <label>}, ...]. The points are in [y, x] format
          normalized to 0-1000. Return one entry per frame that contains
          the object.
        """

image_response = client.models.generate_content(
  model="gemini-robotics-er-2-preview",
  contents=[
    types.Part.from_bytes(
      data=video_bytes,
      mime_type='video/mp4',
    ),
    prompt
  ],
  config = types.GenerateContentConfig(
      thinking_config=types.ThinkingConfig(
          thinking_level=types.ThinkingLevel.HIGH
      )
  )
)

print(image_response.text)
```

## Object detection and bounding boxes

In addition to points, you can prompt the model to return 2D bounding boxes, which provide more spatial detail for detected objects.

### Python

```
from google import genai
from google.genai import types

client = genai.Client(
    enterprise=True,
    project="your-project-id",
    location="global",
)

with open("my-image.png", 'rb') as f:
    image_bytes = f.read()

prompt = """
          Detect all objects in this image and return bounding boxes.
          The answer should follow the JSON format:
          [{"label": <label>, "y": <y_min>, "x": <x_min>,
            "y2": <y_max>, "x2": <x_max>}, ...]
          where coordinates are normalized to 0-1000.
        """

image_response = client.models.generate_content(
  model="gemini-robotics-er-2-preview",
  contents=[
    types.Part.from_bytes(
      data=image_bytes,
      mime_type='image/png',
    ),
    prompt
  ],
  config = types.GenerateContentConfig(
      thinking_config=types.ThinkingConfig(
          thinking_level=types.ThinkingLevel.LOW
      )
  )
)

print(image_response.text)
```

## Trajectories

Gemini Robotics ER 2 can generate sequences of points that define a trajectory, useful for guiding robot movement.

This example requests a trajectory to move a red pen to an organizer, including an estimate of the intermediate waypoints. The code has been reduced to show only the prompt.

### Python

```
prompt = """
          Generate a trajectory for the robotic arm to pick up the red pen
          and place it in the organizer. Return a list of waypoints as JSON:
          [{"step": <int>, "point": [y, x], "action": <description>}, ...]
          where coordinates are normalized to 0-1000.
        """
```

## Make room for a laptop

This example shows how Gemini Robotics ER 2 can reason about a space. The prompt asks the model to identify which object needs to be moved to create space for another item.

### Python

```
from google import genai
from google.genai import types

client = genai.Client(
    enterprise=True,
    project="your-project-id",
    location="global",
)

# Load your image
with open('path/to/image-with-objects.jpg', 'rb') as f:
    image_bytes = f.read()

prompt = """
          Point to the object that I need to remove to make room for my laptop
          The answer should follow the JSON format: [{"point": <point>,
          "label": <label1>}, ...]. The points are in [y, x] format normalized to 0-1000.
        """

image_response = client.models.generate_content(
  model="gemini-robotics-er-2-preview",
  contents=[
    types.Part.from_bytes(
      data=image_bytes,
      mime_type='image/jpeg',
    ),
    prompt
  ],
  config = types.GenerateContentConfig(
      thinking_config=types.ThinkingConfig(
          thinking_level=types.ThinkingLevel.HIGH
      )
  )
)

print(image_response.text)
```

The response contains a 2D coordinate of the object that answers the user's question, in this case, the object that should move to make room for a laptop.

```
[
  {"point": [672, 301], "label": "The object that I need to remove to make room for my laptop"}
]
```

![An example that shows which object needs to be moved for another object](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/images/spatial-reasoning.png)

## Pack a lunch

The model can also provide instructions for multi-step tasks and point to relevant objects for each step. This example shows how the model plans a series of steps to pack a lunch bag.

### Python

```
from google import genai
from google.genai import types

client = genai.Client(
    enterprise=True,
    project="your-project-id",
    location="global",
)

# Load your image and set up your prompt
with open('path/to/image-of-lunch.jpg', 'rb') as f:
    image_bytes = f.read()

prompt = """
          Explain how to pack the lunch box and lunch bag. Point to each
          object that you refer to. Each point should be in the format:
          [{"point": [y, x], "label": }], where the coordinates are
          normalized between 0-1000.
        """

image_response = client.models.generate_content(
  model="gemini-robotics-er-2-preview",
  contents=[
    types.Part.from_bytes(
      data=image_bytes,
      mime_type='image/jpeg',
    ),
    prompt
  ],
  config = types.GenerateContentConfig(
      thinking_config=types.ThinkingConfig(
          thinking_level=types.ThinkingLevel.HIGH
      )
  )
)

print(image_response.text)
```

The response of this prompt is a set of step by step instructions on how to pack a lunch bag from the image input.

**Input image**

![An image of a lunch box and items to put into it](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/images/packing-lunch.png)

**Model output**

```
Based on the image, here is a plan to pack the lunch box and lunch bag:

1.  **Pack the fruit into the lunch box.** Place the apple, banana, red grapes, and green grapes into the blue lunch box.
2.  **Add the spoon to the lunch box.** Put the blue spoon inside the lunch box as well.
3.  **Close the lunch box.** Secure the lid on the blue lunch box.
4.  **Place the lunch box inside the lunch bag.** Put the closed blue lunch box into the brown lunch bag.
5.  **Pack the remaining items into the lunch bag.** Place the blue snack bar and the brown snack bar into the brown lunch bag.

Here is the list of objects and their locations:
*   [{"point": [899, 440], "label": "apple"}]
*   [{"point": [814, 363], "label": "banana"}]
*   [{"point": [727, 470], "label": "red grapes"}]
*   [{"point": [675, 608], "label": "green grapes"}]
*   [{"point": [706, 529], "label": "blue lunch box"}]
*   [{"point": [864, 517], "label": "blue spoon"}]
*   [{"point": [499, 401], "label": "blue snack bar"}]
*   [{"point": [614, 705], "label": "brown snack bar"}]
*   [{"point": [448, 501], "label": "brown lunch bag"}]
```

## What's next

To learn more about Gemini Robotics ER 2, see the following resources:

- [Agentic capabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/agentic) : code execution, instrument reading, and image annotation.
- [Task orchestration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/orchestration) : long-horizon tasks with custom robot APIs.
- [Video understanding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er/video-understanding) : moment finding and progress classification.
- [Gemini Robotics ER 2 overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er) : capabilities and quickstart.
- [Gemini Robotics ER 2 model information](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/robotics-er-2) : technical specifications, token limits, and supported capabilities.
