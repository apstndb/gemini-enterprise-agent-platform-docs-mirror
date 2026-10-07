---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking
title: Thinking
description: Learn how to configure thinking in Gemini models on Gemini Enterprise Agent Platform, including thinking levels, token budgets, thought summaries, and reasoning states.
data_source: docs.cloud.google.com
---

Thinking models generate an internal "thinking" process before returning a response. This capability helps the model perform complex multi-step planning, solve mathematical problems, and generate accurate code.

This page explains how to:

- [Configure thinking levels and token budgets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#configure-thinking)
- [View thought summaries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#thought-summaries)
- [Preserve reasoning state across multi-turn conversations using thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#signatures)

## Supported models

Thinking is supported in the following models:

#### Click to expand supported models

- [Gemini Omni Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-flash-preview) preview
- [Gemini Omni 1.1 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash) preview
- [Gemini Nano Banana 2.1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/nano-banana-2-1)
- [Gemini 3.8 Flash Cyber](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-cyber)
- [Gemini 3.8 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash)
- [Gemini 3.7 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash)
- [Gemini 3.6 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash)
- [Gemini 3.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite)
- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro) preview
- [Gemini 3.1 Flash-Lite Image (Nano Banana 2 Lite)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite-image)
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 3.1 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)
- [Gemini 3 Pro Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)
- [Gemini 3 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash) preview
- [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
- [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

## Control model thinking

Thinking is enabled by default in supported Gemini models. In Agent Studio, you can inspect the full thinking process alongside the generated response.

How you configure thinking depends on the model version:

- [Gemini 3 and later models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#gemini-3-and-later-models)
- [Gemini 2.5 and earlier models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#gemini-2-5-and-earlier-models)

### Gemini 3 and later models

Gemini 3 models use the `thinking_level` parameter. This parameter sets discrete reasoning tiers so you can optimize between latency and reasoning depth.

### Console

1.  Go to [Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal) and select **New \> Chat** and expand the model panel.

2.  In the **Model settings** panel, select a supported model from the **Model** menu.

3.  Select a value from the **Thinking level** drop-down menu.

### Python

```
from google import genai
from google.genai import types

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3.5-flash",
    contents="How does AI work?",
    config=types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(
            # Options: MINIMAL, LOW, MEDIUM, HIGH
            thinking_level=types.ThinkingLevel.THINKING_LEVEL_VALUE
        )
    ),
)

print(response.text)
```

> **Warning:** The `thinking_budget` parameter is deprecated for Gemini 3 and later models. Using `thinking_budget` with these models can cause intermittent `400: INVALID_ARGUMENT` errors.
>
> Specifying both `thinking_level` and `thinking_budget` in the same request returns an error. Remove `thinking_budget` from your requests when using Gemini 3 models to avoid these errors.

#### Thinking level values

You can set `thinking_level` to one of the following values:

- **`MINIMAL`** : Uses the fewest possible tokens for thinking. Best for straightforward tasks that do not require extended reasoning. `MINIMAL` requires [thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/thought-signatures) in multi-turn conversations; if omitted, the model returns a `400: INVALID_ARGUMENT` error.
- **`LOW`** : Uses fewer thinking tokens for faster responses. Best for high-throughput applications with low task complexity.
- **`MEDIUM`** : Balances reasoning quality and latency. Suitable for tasks with moderate complexity that benefit from intermediate reasoning steps.
- **`HIGH`** : Uses the maximum thinking capacity. Best for complex prompts requiring deep reasoning, multi-step problem solving, formal code verification, or multi-turn tool execution.

#### Supported thinking levels by model

The following table lists supported `thinking_level` values and default configurations by model:

| Model                                                                                                                                                 | Supported `thinking_level` values     | Default   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|-----------|
| [Gemini Nano Banana 2.1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/nano-banana-2-1)                                | `MINIMAL` , `MEDIUM` , `HIGH`         | `MEDIUM`  |
| [Gemini 3.8 Flash Cyber](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-cyber)                                | `LOW` , `MEDIUM` , `HIGH`             | `MEDIUM`  |
| [Gemini 3.8 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash)                                            | `LOW` , `MEDIUM` , `HIGH`             | `MEDIUM`  |
| [Gemini 3.7 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash)                                            | `LOW` , `MEDIUM` , `HIGH`             | `MEDIUM`  |
| [Gemini 3.6 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash)                                            | `MINIMAL` , `LOW` , `MEDIUM` , `HIGH` | `MEDIUM`  |
| [Gemini 3.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite)                                  | `MINIMAL` , `LOW` , `MEDIUM` , `HIGH` | `MINIMAL` |
| [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)                                            | `MINIMAL` , `LOW` , `MEDIUM` , `HIGH` | `MEDIUM`  |
| [Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro) preview                                        | `LOW` , `MEDIUM` , `HIGH`             | `HIGH`    |
| [Gemini 3.1 Flash-Lite Image (Nano Banana 2 Lite)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite-image) | `MINIMAL` , `HIGH`                    | `MINIMAL` |
| [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)                                  | `MINIMAL` , `LOW` , `MEDIUM` , `HIGH` | `MINIMAL` |
| [Gemini 3.1 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)                                | `MINIMAL` , `HIGH`                    | `MINIMAL` |
| [Gemini 3 Pro Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)                                        | `HIGH`                                | `HIGH`    |
| [Gemini 3 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash) preview                                        | `MINIMAL` , `LOW` , `MEDIUM` , `HIGH` | `HIGH`    |

### Gemini 2.5 and earlier models

> **Caution:** Don't use the `thinking_level` parameter with Gemini 2.5 and earlier models. Your requests will return an error if this parameter is present.

For Gemini 2.5 and earlier models, configure thinking using the `thinking_budget` parameter. This parameter sets a soft limit on the number of tokens the model can use during internal reasoning.

### Console

1.  Go to [Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal) and select **New \> Chat** .

2.  In the **Model settings** panel, select a supported model from the **Model** menu.

3.  In the **Thinking budget** selector, select **Manual** and use the slider to adjust the token limit.

### Python

#### Install

```
pip install --upgrade google-genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
from google import genai
from google.genai.types import GenerateContentConfig, ThinkingConfig

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3.5-flash",
    contents="solve x^2 + 4x + 4 = 0",
    config=GenerateContentConfig(
        thinking_config=ThinkingConfig(
            thinking_budget=1024,  # Use `0` to turn off thinking
        )
    ),
)

print(response.text)
# Example response:
#     To solve the equation $x^2 + 4x + 4 = 0$, you can use several methods:
#     **Method 1: Factoring**
#     1.  Look for two numbers that multiply to the constant term (4) and add up to the coefficient of the $x$ term (4).
#     2.  The numbers are 2 and 2 ($2 \times 2 = 4$ and $2 + 2 = 4$).
#     ...
#     ...
#     All three methods yield the same solution. This quadratic equation has exactly one distinct solution (a repeated root).
#     The solution is **x = -2**.

# Token count for `Thinking`
print(response.usage_metadata.thoughts_token_count)
# Example response:
#     886

# Total token count
print(response.usage_metadata.total_token_count)
# Example response:
#     1525
```

### Node.js

#### Install

```
npm install @google/genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/js-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
const {GoogleGenAI} = require('@google/genai');

const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
const GOOGLE_CLOUD_LOCATION = process.env.GOOGLE_CLOUD_LOCATION || 'global';

async function generateWithThoughts(
  projectId = GOOGLE_CLOUD_PROJECT,
  location = GOOGLE_CLOUD_LOCATION
) {
  const client = new GoogleGenAI({
    vertexai: true,
    project: projectId,
    location: location,
  });

  const response = await client.models.generateContent({
    model: 'gemini-2.5-flash',
    contents: 'solve x^2 + 4x + 4 = 0',
    config: {
      thinkingConfig: {
        thinkingBudget: 1024,
      },
    },
  });

  console.log(response.text);
  // Example response:
  //  To solve the equation $x^2 + 4x + 4 = 0$, you can use several methods:
  //  **Method 1: Factoring**
  //  1.  Look for two numbers that multiply to the constant term (4) and add up to the coefficient of the $x$ term (4).
  //  2.  The numbers are 2 and 2 ($2 \times 2 = 4$ and $2 + 2 = 4$).
  //  ...
  //  ...
  //  All three methods yield the same solution. This quadratic equation has exactly one distinct solution (a repeated root).
  //  The solution is **x = -2**.

  // Token count for `Thinking`
  console.log(response.usageMetadata.thoughtsTokenCount);
  // Example response:
  //  886

  // Total token count
  console.log(response.usageMetadata.totalTokenCount);
  // Example response:
  //  1525
  return response.text;
}
```

### Go

Learn how to install or update the [Go](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://pkg.go.dev/google.golang.org/genai) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
import (
    "context"
    "fmt"
    "io"

    "google.golang.org/genai"
)

// generateThinkingBudgetContentWithText demonstrates how to generate text including the model's thought process.
func generateThinkingBudgetContentWithText(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-flash"
    thinkingBudget := int32(1024) //Use `0` to turn off thinking
    contents := []*genai.Content{
        {
            Parts: []*genai.Part{
                {Text: "solve x^2 + 4x + 4 = 0"},
            },
            Role: "user",
        },
    }

    resp, err := client.Models.GenerateContent(ctx,
        modelName,
        contents,
        &genai.GenerateContentConfig{
            ThinkingConfig: &genai.ThinkingConfig{
                ThinkingBudget: &thinkingBudget,
            },
        },
    )
    if err != nil {
        return fmt.Errorf("generate content failed: %w", err)
    }

    if resp.UsageMetadata != nil {
        fmt.Fprintf(w, "Thoughts token count: %d\n", resp.UsageMetadata.ThoughtsTokenCount)
        //Example response:
        //  908
        fmt.Fprintf(w, "Total token count: %d\n", resp.UsageMetadata.TotalTokenCount)
        //Example response:
        //  1364
    }

    fmt.Fprintln(w, resp.Text())

    // Example response:
    //    To solve the equation $x^2 + 4x + 4 = 0$, you can use several methods:
    //    **Method 1: Factoring**
    //    1.  Look for two numbers that multiply to the constant term (4) and add up to the coefficient of the $x$ term (4).
    //    2.  The numbers are 2 and 2 ($2 \times 2 = 4$ and $2 + 2 = 4$).
    //    ...
    //    ...
    //    Both methods yield the same result.
    //    The solution to the equation $x^2 + 4x + 4 = 0$ is **$x = -2$**.

    return nil
}
```

### Java

Learn how to install or update the [Java](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://central.sonatype.com/artifact/com.google.genai/google-genai) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
import com.google.genai.Client;
import com.google.genai.types.GenerateContentConfig;
import com.google.genai.types.GenerateContentResponse;
import com.google.genai.types.HttpOptions;
import com.google.genai.types.ThinkingConfig;

public class ThinkingBudgetWithTxt {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String modelId = "gemini-2.5-flash";
    generateContent(modelId);
  }

  // Generates text controlling the thinking budget
  public static String generateContent(String modelId) {
    // Initialize client that will be used to send requests. This client only needs to be created
    // once, and can be reused for multiple requests.
    try (Client client =
        Client.builder()
            .location("global")
            .vertexAI(true)
            .httpOptions(HttpOptions.builder().apiVersion("v1").build())
            .build()) {

      GenerateContentConfig contentConfig =
          GenerateContentConfig.builder()
              .thinkingConfig(ThinkingConfig.builder().thinkingBudget(1024).build())
              .build();

      GenerateContentResponse response =
          client.models.generateContent(modelId, "solve x^2 + 4x + 4 = 0", contentConfig);

      System.out.println(response.text());
      // Example response:
      // To solve the equation $x^2 + 4x + 4 = 0$, we can use several methods:
      //
      // **Method 1: Factoring (Recognizing a Perfect Square Trinomial)**
      //
      // Notice that the left side of the equation is a perfect square trinomial. It fits the form
      // $a^2 + 2ab + b^2 = (a+b)^2$...
      // ...
      // The solution is $x = -2$.

      response
          .usageMetadata()
          .ifPresent(
              metadata -> {
                System.out.println("Token count for thinking: " + metadata.thoughtsTokenCount());
                System.out.println("Total token count: " + metadata.totalTokenCount());
              });
      // Example response:
      // Token count for thinking: Optional[885]
      // Total token count: Optional[1468]
      return response.text();
    }
  }
}
```

If you do not specify a budget, the model sets the token budget dynamically up to 8,192 tokens. To explicitly enable dynamic budgeting in the API, set `thinking_budget` to `-1` .

> **Note:** The thinking budget is a *soft limit* . The actual number of thinking tokens generated might vary slightly. If your application requires lower latency, set a lower budget or set the budget to `0` .

#### Supported thinking budgets by model

The following table lists minimum, maximum, and default token limits for each model:

| Model                 | Minimum tokens | Maximum tokens | Default                   |
|-----------------------|----------------|----------------|---------------------------|
| Gemini 2.5 Flash      | 1              | 24,576         | Auto (up to 8,192 tokens) |
| Gemini 2.5 Pro        | 128            | 32,768         | Auto (up to 8,192 tokens) |
| Gemini 2.5 Flash-Lite | 512            | 24,576         | Auto (up to 8,192 tokens) |

#### Turn off thinking

You can turn off thinking for Gemini 2.5 Flash and Gemini 2.5 Flash-Lite by setting `thinking_budget` to `0` . Although thinking content is not returned in the response, the generated text might still show reasoning-style output.

You can't turn off thinking for Gemini 2.5 Pro.

## View thought summaries

*Thought summaries* display intermediate reasoning steps alongside the model's final response. Thought summaries are supported in Gemini 2.5 and later models.

### Console

Thought summaries are enabled by default in Agent Studio. To view the summarized reasoning steps, expand the **Thoughts** panel.

### Python

#### Install

```
pip install --upgrade google-genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
from google import genai
from google.genai.types import GenerateContentConfig, ThinkingConfig

client = genai.Client()
response = client.models.generate_content(
    model="gemini-3.1-pro-preview",
    contents="solve x^2 + 4x + 4 = 0",
    config=GenerateContentConfig(
        thinking_config=ThinkingConfig(include_thoughts=True)
    ),
)

print(response.text)
# Example Response:
#     Okay, let's solve the quadratic equation x² + 4x + 4 = 0.
#     ...
#     **Answer:**
#     The solution to the equation x² + 4x + 4 = 0 is x = -2. This is a repeated root (or a root with multiplicity 2).

for part in response.candidates[0].content.parts:
    if part and part.thought:  # show thoughts
        print(part.text)
# Example Response:
#     **My Thought Process for Solving the Quadratic Equation**
#
#     Alright, let's break down this quadratic, x² + 4x + 4 = 0. First things first:
#     it's a quadratic; the x² term gives it away, and we know the general form is
#     ax² + bx + c = 0.
#
#     So, let's identify the coefficients: a = 1, b = 4, and c = 4. Now, what's the
#     most efficient path to the solution? My gut tells me to try factoring; it's
#     often the fastest route if it works. If that fails, I'll default to the quadratic
#     formula, which is foolproof. Completing the square? It's good for deriving the
#     formula or when factoring is difficult, but not usually my first choice for
#     direct solving, but it can't hurt to keep it as an option.
#
#     Factoring, then. I need to find two numbers that multiply to 'c' (4) and add
#     up to 'b' (4). Let's see... 1 and 4 don't work (add up to 5). 2 and 2? Bingo!
#     They multiply to 4 and add up to 4. This means I can rewrite the equation as
#     (x + 2)(x + 2) = 0, or more concisely, (x + 2)² = 0. Solving for x is now
#     trivial: x + 2 = 0, thus x = -2.
#
#     Okay, just to be absolutely certain, I'll run the quadratic formula just to
#     double-check. x = [-b ± √(b² - 4ac)] / 2a. Plugging in the values, x = [-4 ±
#     √(4² - 4 * 1 * 4)] / (2 * 1). That simplifies to x = [-4 ± √0] / 2. So, x =
#     -2 again – a repeated root. Nice.
#
#     Now, let's check via completing the square. Starting from the same equation,
#     (x² + 4x) = -4. Take half of the b-value (4/2 = 2), square it (2² = 4), and
#     add it to both sides, so x² + 4x + 4 = -4 + 4. Which simplifies into (x + 2)²
#     = 0. The square root on both sides gives us x + 2 = 0, therefore x = -2, as
#      expected.
#
#     Always, *always* confirm! Let's substitute x = -2 back into the original
#     equation: (-2)² + 4(-2) + 4 = 0. That's 4 - 8 + 4 = 0. It checks out.
#
#     Conclusion: the solution is x = -2. Confirmed.
```

### Node.js

#### Install

```
npm install @google/genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/js-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
const {GoogleGenAI} = require('@google/genai');

const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
const GOOGLE_CLOUD_LOCATION = process.env.GOOGLE_CLOUD_LOCATION || 'global';

async function generateWithThoughts(
  projectId = GOOGLE_CLOUD_PROJECT,
  location = GOOGLE_CLOUD_LOCATION
) {
  const client = new GoogleGenAI({
    vertexai: true,
    project: projectId,
    location: location,
  });

  const response = await client.models.generateContent({
    model: 'gemini-2.5-pro',
    contents: 'solve x^2 + 4x + 4 = 0',
    config: {
      thinkingConfig: {
        includeThoughts: true,
      },
    },
  });

  console.log(response.text);
  // Example Response:
  //  Okay, let's solve the quadratic equation x² + 4x + 4 = 0.
  //  ...
  //  **Answer:**
  //  The solution to the equation x² + 4x + 4 = 0 is x = -2. This is a repeated root (or a root with multiplicity 2).

  for (const part of response.candidates[0].content.parts) {
    if (part && part.thought) {
      console.log(part.text);
    }
  }

  // Example Response:
  // **My Thought Process for Solving the Quadratic Equation**
  //
  // Alright, let's break down this quadratic, x² + 4x + 4 = 0. First things first:
  // it's a quadratic; the x² term gives it away, and we know the general form is
  // ax² + bx + c = 0.
  //
  // So, let's identify the coefficients: a = 1, b = 4, and c = 4. Now, what's the
  // most efficient path to the solution? My gut tells me to try factoring; it's
  // often the fastest route if it works. If that fails, I'll default to the quadratic
  // formula, which is foolproof. Completing the square? It's good for deriving the
  // formula or when factoring is difficult, but not usually my first choice for
  // direct solving, but it can't hurt to keep it as an option.
  //
  // Factoring, then. I need to find two numbers that multiply to 'c' (4) and add
  // up to 'b' (4). Let's see... 1 and 4 don't work (add up to 5). 2 and 2? Bingo!
  // They multiply to 4 and add up to 4. This means I can rewrite the equation as
  // (x + 2)(x + 2) = 0, or more concisely, (x + 2)² = 0. Solving for x is now
  // trivial: x + 2 = 0, thus x = -2.
  //
  // Okay, just to be absolutely certain, I'll run the quadratic formula just to
  // double-check. x = [-b ± √(b² - 4ac)] / 2a. Plugging in the values, x = [-4 ±
  // √(4² - 4 * 1 * 4)] / (2 * 1). That simplifies to x = [-4 ± √0] / 2. So, x =
  // -2 again – a repeated root. Nice.
  //
  // Now, let's check via completing the square. Starting from the same equation,
  // (x² + 4x) = -4. Take half of the b-value (4/2 = 2), square it (2² = 4), and
  // add it to both sides, so x² + 4x + 4 = -4 + 4. Which simplifies into (x + 2)²
  // = 0. The square root on both sides gives us x + 2 = 0, therefore x = -2, as
  //  expected.
  //
  // Always, *always* confirm! Let's substitute x = -2 back into the original
  // equation: (-2)² + 4(-2) + 4 = 0. That's 4 - 8 + 4 = 0. It checks out.
  //
  // Conclusion: the solution is x = -2. Confirmed.

  return response.text;
}
```

### Go

Learn how to install or update the [Go](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://pkg.go.dev/google.golang.org/genai) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
import (
    "context"
    "fmt"
    "io"

    "google.golang.org/genai"
)

// generateContentWithThoughts demonstrates how to generate text including the model's thought process.
func generateContentWithThoughts(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-pro"
    contents := []*genai.Content{
        {
            Parts: []*genai.Part{
                {Text: "solve x^2 + 4x + 4 = 0"},
            },
            Role: "user",
        },
    }

    resp, err := client.Models.GenerateContent(ctx,
        modelName,
        contents,
        &genai.GenerateContentConfig{
            ThinkingConfig: &genai.ThinkingConfig{
                IncludeThoughts: true,
            },
        },
    )
    if err != nil {
        return fmt.Errorf("failed to generate content: %w", err)
    }

    if len(resp.Candidates) == 0 || resp.Candidates[0].Content == nil {
        return fmt.Errorf("no content was generated")
    }

    // The response may contain both the final answer and the model's thoughts.
    // Iterate through the parts to print them separately.
    fmt.Fprintln(w, "Answer:")
    for _, part := range resp.Candidates[0].Content.Parts {
        if part.Text != "" && !part.Thought {
            fmt.Fprintln(w, part.Text)
        }
    }
    fmt.Fprintln(w, "\nThoughts:")
    for _, part := range resp.Candidates[0].Content.Parts {
        if part.Thought {
            fmt.Fprintln(w, part.Text)
        }
    }

    // Example response:
    //  Answer:
    //  Of course! We can solve this quadratic equation in a couple of ways.
    //
    //### Method 1: Factoring (the easiest method for this problem)
    //
    //1.  **Recognize the pattern.** The expression `x² + 4x + 4` is a perfect square trinomial. It fits the pattern `a² + 2ab + b² = (a + b)²`. In this case, `a = x` and `b = 2`.
    //
    //2.  **Factor the equation.**
    //    `x² + 4x + 4 = (x + 2)(x + 2) = (x + 2)²`
    //
    //3.  **Solve for x.** Now set the factored expression to zero:
    //    `(x + 2)² = 0`
    //
    //    Take the square root of both sides:
    //    `x + 2 = 0`
    //
    //    Subtract 2 from both sides:
    //    `x = -2`
    //
    //This type of solution is called a "repeated root" or a "double root" because the factor `(x+2)` appears twice.
    //
    //---
    //
    //### Method 2: Using the Quadratic Formula
    //
    //You can use the quadratic formula for any equation in the form `ax² + bx + c = 0`.
    //
    //The formula is: `x = [-b ± sqrt(b² - 4ac)] / 2a`
    //
    //1.  **Identify a, b, and c.**
    //    *   a = 1
    //    *   b = 4
    //    *   c = 4
    //
    //2.  **Plug the values into the formula.**
    //    `x = [-4 ± sqrt(4² - 4 * 1 * 4)] / (2 * 1)`
    //
    //3.  **Simplify.**
    //    `x = [-4 ± sqrt(16 - 16)] / 2`
    //    `x = [-4 ± sqrt(0)] / 2`
    //    `x = -4 / 2`
    //
    //4.  **Solve for x.**
    //    `x = -2`
    //Alright, the user wants to solve the quadratic equation `x² + 4x + 4 = 0`. My first instinct is to see if I can factor it; that's often the fastest approach if it works.  Looking at the coefficients, I see `a = 1`, `b = 4`, and `c = 4`.  Factoring is clearly the most direct path here. I need to find two numbers that multiply to 4 (c) and add up to 4 (b). Hmm, let's see… 1 and 4? Nope, that adds to 5.  2 and 2? Perfect!  2 times 2 is 4, and 2 plus 2 is also 4.
    //
    //So, `x² + 4x + 4` factors nicely into `(x + 2)(x + 2)`.  Ah, a perfect square trinomial! That's useful to note. Now, I can write the equation as `(x + 2)² = 0`.  Taking the square root of both sides gives me `x + 2 = 0`.  And finally, subtracting 2 from both sides, I get `x = -2`.  That's the solution.
    //
    //Just to be thorough, and maybe to offer an alternative explanation, let's verify this using the quadratic formula. It's `x = [-b ± √(b² - 4ac)] / 2a`. Plugging in my values:  `x = [-4 ± √(4² - 4 * 1 * 4)] / (2 * 1)`.  That simplifies to `x = [-4 ± √(16 - 16)] / 2`, or `x = [-4 ± 0] / 2`.  Therefore, `x = -2`. The discriminant being zero tells me I have exactly one real, repeated root.  Great. So, whether I factor or use the quadratic formula, the answer is the same.
    return nil
}
```

### Java

Learn how to install or update the [Java](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://central.sonatype.com/artifact/com.google.genai/google-genai) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
import com.google.genai.Client;
import com.google.genai.types.Candidate;
import com.google.genai.types.Content;
import com.google.genai.types.GenerateContentConfig;
import com.google.genai.types.GenerateContentResponse;
import com.google.genai.types.HttpOptions;
import com.google.genai.types.ThinkingConfig;

public class ThinkingIncludeThoughtsWithTxt {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String modelId = "gemini-2.5-pro";
    generateContent(modelId);
  }

  // Generates text including thoughts in the response
  public static String generateContent(String modelId) {
    // Initialize client that will be used to send requests. This client only needs to be created
    // once, and can be reused for multiple requests.
    try (Client client =
        Client.builder()
            .location("global")
            .vertexAI(true)
            .httpOptions(HttpOptions.builder().apiVersion("v1").build())
            .build()) {

      GenerateContentConfig contentConfig =
          GenerateContentConfig.builder()
              .thinkingConfig(ThinkingConfig.builder().includeThoughts(true).build())
              .build();

      GenerateContentResponse response =
          client.models.generateContent(modelId, "solve x^2 + 4x + 4 = 0", contentConfig);

      System.out.println(response.text());
      // Example response:
      // We can solve the equation x² + 4x + 4 = 0 using a couple of common methods.
      //
      // ### Method 1: Factoring (The Easiest Method for this Problem)
      // **Recognize the pattern:** The pattern for a perfect square trinomial
      // is a² + 2ab + b² = (a + b)².
      // ...
      // ### Final Answer:
      // The solution is **x = -2**.

      // Get parts of the response and print thoughts
      response
          .candidates()
          .flatMap(candidates -> candidates.stream().findFirst())
          .flatMap(Candidate::content)
          .flatMap(Content::parts)
          .ifPresent(
              parts -> {
                parts.forEach(
                    part -> {
                      if (part.thought().orElse(false)) {
                        part.text().ifPresent(System.out::println);
                      }
                    });
              });
      // Example response:
      // Alright, let's break down this quadratic equation, x² + 4x + 4 = 0. My initial thought is,
      // "classic quadratic."  I'll need to find the values of 'x' that make this equation true. The
      // equation is in standard form, and since the coefficients are relatively small, I
      // immediately suspect that factoring might be the easiest route.  It's worth checking.
      //
      // First, I assessed what I had. *a* is 1, *b* is 4, and *c* is 4. I consider my toolkit.
      // Factoring is the likely first choice, then I can use the quadratic formula as a backup,
      // because that ALWAYS works, and I could use graphing. However, for this, factoring seems the
      // cleanest approach.
      //
      // Okay, factoring. I need two numbers that multiply to *c* (which is 4) and add up to *b*
      // (also 4).  I quickly run through the factor pairs of 4: (1, 4), (-1, -4), (2, 2), (-2, -2).
      //  Aha! 2 and 2 fit the bill. They multiply to 4 *and* add up to 4.  Therefore, I can rewrite
      // the equation as (x + 2)(x + 2) = 0.  That simplifies to (x + 2)² = 0. Perfect square
      // trinomial – nice and tidy. Seeing that pattern from the outset can save a step or two. Now,
      // to solve for *x*:  if (x + 2)² = 0, then x + 2 must equal 0.  Therefore, x = -2. Done.
      //
      // But, for the sake of a full explanation, let's use the quadratic formula as a second
      // method. It's a reliable way to double-check the answer, plus it's good practice.  I plug my
      // *a*, *b*, and *c* values into the formula: x = [-b ± √(b² - 4ac)] / (2a). That gives me  x
      // = [-4 ± √(4² - 4 * 1 * 4)] / (2 * 1). Simplifying under the radical, I get x = [-4 ± √(16 -
      // 16)] / 2. So, x = [-4 ± √0] / 2. The square root of 0 is zero, which is very telling!  When
      // the discriminant (b² - 4ac) is zero, you get one real solution, a repeated root. This means
      // x = -4 / 2, which simplifies to x = -2.  Exactly the same as before.
      //
      // Therefore, the answer is x = -2.  Factoring was the most straightforward route.  For
      // completeness, I showed the solution via the quadratic formula, too. Both approaches lead to
      // the same single solution.  This is a repeated root – a double root, if you will.
      //
      // And to be absolutely sure...let's check our answer! Substitute -2 back into the original
      // equation. (-2)² + 4(-2) + 4 = 4 - 8 + 4 = 0.  Yep, 0 = 0. The solution is correct.
      return response.text();
    }
  }
}
```

A response might return a thought signature without thought summary text in the following situations:

- **Low-complexity requests** : The request required minimal reasoning steps.
- **Disabled summaries** : Thought summaries were not requested or were turned off.
- **Non-text modalities** : Reasoning over certain modalities (such as image analysis) might not produce text summaries.

Your application must handle empty or missing thought summary fields gracefully while preserving any accompanying thought signatures.

## Thought signatures

*Thought signatures* are encrypted representations of the model's internal reasoning state. They maintain context across multi-turn conversations, especially when using [function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .

To preserve the reasoning context across multi-turn interactions, pass the thought signatures returned in earlier responses back into subsequent requests, regardless of the thinking level configured.

If you use the official Google Google Gen AI SDK (Python, Node.js, Go, or Java), thought signatures are managed automatically when using standard chat sessions or when appending complete response objects to your message history.

For implementation patterns, requirements, and examples, see [Thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/thought-signatures) .

## Pricing

You are billed for tokens generated during the thinking process. For models where thinking is enabled by default—such as Gemini 3 Pro and Gemini 2.5 Pro—these thinking tokens are included in your billable usage.

For full rate details, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## What's next

Guide

### [Thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/thought-signatures)

Learn how to preserve the Gemini reasoning state during multi-turn and multi-step conversations using thought signatures.

Guide

### [Thinking prompting guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking/prompting-guide)

Explore prompt engineering techniques and best practices tailored for Gemini thinking models.

Console

### [Google Cloud console](https://console.cloud.google.com/agent-platform/studio/multimodal)

Try prompting Gemini for yourself in the Google Cloud console.
