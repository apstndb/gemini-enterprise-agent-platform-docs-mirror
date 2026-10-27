---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation
title: Generate images with Gemini
description: Generate images with Gemini, using Google's image generation AI.
data_source: docs.cloud.google.com
---

> To see an example of image generation with Gemini, run the "Gemini Nano Banana 2.1 in Gemini Enterprise Agent Platform" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/vision/getting-started/gemini_nano_banana_2_1_image_gen.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fvision%2Fgetting-started%2Fgemini_nano_banana_2_1_image_gen.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fvision%2Fgetting-started%2Fgemini_nano_banana_2_1_image_gen.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/vision/getting-started/gemini_nano_banana_2_1_image_gen.ipynb)

You can use Gemini to generate images from a text prompt. Supported interfaces include the Google Cloud console and the Agent Platform API.

The following Gemini models support image generation:

#### Click to expand supported models

- [`gemini-nano-banana-2.1`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/nano-banana-2-1)
- [`gemini-3.1-flash-lite-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite-image)
- [`gemini-3.1-flash-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)
- [`gemini-3-pro-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)
- [`gemini-2.5-flash-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-image)

For more information about Gemini model capabilities, see [Gemini models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#gemini-models) .

## Generate images

The following shows how to generate images using either Agent Studio or using the API.

For more information about best practices for prompting, see [Design multimodal prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/design-multimodal-prompts#fundamentals) .

### Console

To generate images with Gemini, do the following:

1.  Open [**Agent Studio \> Create prompt**](https://console.cloud.google.com/agent-platform/studio/multimodal;mode=prompt) .
2.  Click **Switch model** and select one of the displayed models.
3.  In the **Outputs** panel, select **Image and text** from the drop-down menu.
4.  Write a description of the image you want to generate in the text area of the **Write a prompt** text area.
5.  Click the **Prompt** ( send ) button.

Gemini generates an image based on your description. This process takes a few seconds, but can be comparatively slower depending on capacity.

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
import os
from io import BytesIO

from google import genai
from google.genai.types import GenerateContentConfig, Modality
from PIL import Image

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3.1-flash-image",
    contents=("Generate an image of the Eiffel tower with fireworks in the background."),
    config=GenerateContentConfig(
        response_modalities=[Modality.TEXT, Modality.IMAGE],
    ),
)
for part in response.candidates[0].content.parts:
    if part.text:
        print(part.text)
    elif part.inline_data:
        image = Image.open(BytesIO((part.inline_data.data)))
        # Ensure the output directory exists
        output_dir = "output_folder"
        os.makedirs(output_dir, exist_ok=True)
        image.save(os.path.join(output_dir, "example-image-eiffel-tower.png"))
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
    "os"

    "google.golang.org/genai"
)

// generateMMFlashWithText demonstrates how to generate both text and image outputs.
func generateMMFlashWithText(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-flash-image"
    contents := []*genai.Content{
        {
            Parts: []*genai.Part{
                {Text: "Generate an image of the Eiffel tower with fireworks in the background."},
            },
            Role: genai.RoleUser,
        },
    }

    resp, err := client.Models.GenerateContent(ctx,
        modelName,
        contents,
        &genai.GenerateContentConfig{
            ResponseModalities: []string{
                string(genai.ModalityText),
                string(genai.ModalityImage),
            },
            CandidateCount: int32(1),
            SafetySettings: []*genai.SafetySetting{
                {Method: genai.HarmBlockMethodProbability},
                {Category: genai.HarmCategoryDangerousContent},
                {Threshold: genai.HarmBlockThresholdBlockMediumAndAbove},
            },
        },
    )
    if err != nil {
        return fmt.Errorf("failed to generate content: %w", err)
    }

    if len(resp.Candidates) == 0 || resp.Candidates[0].Content == nil {
        return fmt.Errorf("no candidates returned")
    }
    var fileName string
    for _, part := range resp.Candidates[0].Content.Parts {
        if part.Text != "" {
            fmt.Fprintln(w, part.Text)
        } else if part.InlineData != nil {
            fileName = "example-image-eiffel-tower.png"
            if err := os.WriteFile(fileName, part.InlineData.Data, 0o644); err != nil {
                return fmt.Errorf("failed to save image: %w", err)
            }
        }
    }
    fmt.Fprintln(w, fileName)

    // Example response:
    // I will generate an image of the Eiffel Tower at night, with a vibrant display of
    // colorful fireworks exploding in the dark sky behind it.
    // ....
    return nil
}
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
const fs = require('fs');
const {GoogleGenAI, Modality} = require('@google/genai');

const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
const GOOGLE_CLOUD_LOCATION =
  process.env.GOOGLE_CLOUD_LOCATION || 'us-central1';

async function generateImage(
  projectId = GOOGLE_CLOUD_PROJECT,
  location = GOOGLE_CLOUD_LOCATION
) {
  const client = new GoogleGenAI({
    vertexai: true,
    project: projectId,
    location: location,
  });

  const response = await client.models.generateContentStream({
    model: 'gemini-2.5-flash-image',
    contents:
      'Generate an image of the Eiffel tower with fireworks in the background.',
    config: {
      responseModalities: [Modality.TEXT, Modality.IMAGE],
    },
  });

  const generatedFileNames = [];
  let imageIndex = 0;

  for await (const chunk of response) {
    const text = chunk.text;
    const data = chunk.data;
    if (text) {
      console.debug(text);
    } else if (data) {
      const outputDir = 'output-folder';
      if (!fs.existsSync(outputDir)) {
        fs.mkdirSync(outputDir, {recursive: true});
      }
      const fileName = `${outputDir}/generate_content_streaming_image_${imageIndex++}.png`;
      console.debug(`Writing response image to file: ${fileName}.`);
      try {
        fs.writeFileSync(fileName, data);
        generatedFileNames.push(fileName);
      } catch (error) {
        console.error(`Failed to write image file ${fileName}:`, error);
      }
    }
  }

  // Example response:
  //  I will generate an image of the Eiffel Tower at night, with a vibrant display of
  //  colorful fireworks exploding in the dark sky behind it. The tower will be
  //  illuminated, standing tall as the focal point of the scene, with the bursts of
  //  light from the fireworks creating a festive atmosphere.

  return generatedFileNames;
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
import com.google.genai.types.Blob;
import com.google.genai.types.Candidate;
import com.google.genai.types.Content;
import com.google.genai.types.GenerateContentConfig;
import com.google.genai.types.GenerateContentResponse;
import com.google.genai.types.Part;
import com.google.genai.types.SafetySetting;
import java.awt.image.BufferedImage;
import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import javax.imageio.ImageIO;

public class ImageGenMmFlashWithText {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String modelId = "gemini-2.5-flash-image";
    String outputFile = "resources/output/example-image-eiffel-tower.png";
    generateContent(modelId, outputFile);
  }

  // Generates an image with text input
  public static void generateContent(String modelId, String outputFile) throws IOException {
    // Client Initialization. Once created, it can be reused for multiple requests.
    try (Client client = Client.builder().location("global").vertexAI(true).build()) {

      GenerateContentConfig contentConfig =
          GenerateContentConfig.builder()
              .responseModalities("TEXT", "IMAGE")
              .candidateCount(1)
              .safetySettings(
                  SafetySetting.builder()
                      .method("PROBABILITY")
                      .category("HARM_CATEGORY_DANGEROUS_CONTENT")
                      .threshold("BLOCK_MEDIUM_AND_ABOVE")
                      .build())
              .build();

      GenerateContentResponse response =
          client.models.generateContent(
              modelId,
              "Generate an image of the Eiffel tower with fireworks in the background.",
              contentConfig);

      // Get parts of the response
      List<Part> parts =
          response
              .candidates()
              .flatMap(candidates -> candidates.stream().findFirst())
              .flatMap(Candidate::content)
              .flatMap(Content::parts)
              .orElse(new ArrayList<>());

      // For each part print text if present, otherwise read image data if present and
      // write it to the output file
      for (Part part : parts) {
        if (part.text().isPresent()) {
          System.out.println(part.text().get());
        } else if (part.inlineData().flatMap(Blob::data).isPresent()) {
          BufferedImage image =
              ImageIO.read(new ByteArrayInputStream(part.inlineData().flatMap(Blob::data).get()));
          ImageIO.write(image, "png", new File(outputFile));
        }
      }

      System.out.println("Content written to: " + outputFile);
      // Example response:
      // Here is the Eiffel Tower with fireworks in the background...
      //
      // Content written to: resources/output/example-image-eiffel-tower.png
    }
  }
}
```

### REST

Run the following command in the terminal to create or overwrite this file in the current directory:

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://${API_ENDPOINT}:generateContent \
  -d '{
    "contents": {
      "role": "USER",
      "parts": [
        {
          "text": "Create a tutorial explaining how to make a peanut butter and jelly sandwich in three easy steps."
        }
      ]
    },
    "generationConfig": {
      "responseModalities": ["TEXT", "IMAGE"],
      "imageConfig": {
        "aspectRatio": "16:9",
      },
     },
     "safetySettings": {
      "method": "PROBABILITY",
      "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
      "threshold": "BLOCK_MEDIUM_AND_ABOVE"
    },
  }' 2>/dev/null >response.json
```

Gemini generates an image based on your description. This process takes a few seconds, but can be comparatively slower depending on capacity.

## Generate interleaved images and text

You can use Gemini to generate interleaved images with text responses. For example, you can generate images for each step of a generated recipe without having to make separate requests to the model.

The following Gemini models support generating interleaved images and text:

#### Click to expand supported models

- [`gemini-nano-banana-2.1`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/nano-banana-2-1)
- [`gemini-3.1-flash-lite-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite-image)
- [`gemini-3.1-flash-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)
- [`gemini-3-pro-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)
- [`gemini-2.5-flash-image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-image)

### Console

To generate interleaved images with text responses, do the following:

1.  Open [**Agent Studio \> Create prompt**](https://console.cloud.google.com/agent-platform/studio/multimodal;mode=prompt) .
2.  Click **Switch model** and select one of the displayed models.
3.  In the **Outputs** panel, select **Image and text** from the drop-down menu.
4.  Write a description of the image you want to generate in the text area of the **Write a prompt** text area. For example, "Create a tutorial explaining how to make a peanut butter and jelly sandwich in three steps. For each step, provide a title with the number of the step, an explanation, and also generate an image, generate each image in a 1:1 aspect ratio."
5.  Click the **Prompt** ( send ) button.

Gemini generates a response based on your description. This process takes a few seconds, but can be comparatively slower depending on capacity.

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
from google.genai.types import GenerateContentConfig, Modality
from PIL import Image
from io import BytesIO

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3.1-flash-image",
    contents=(
        "Generate an illustrated recipe for a paella."
        "Create images to go alongside the text as you generate the recipe"
    ),
    config=GenerateContentConfig(response_modalities=[Modality.TEXT, Modality.IMAGE]),
)
with open("output_folder/paella-recipe.md", "w") as fp:
    for i, part in enumerate(response.candidates[0].content.parts):
        if part.text is not None:
            fp.write(part.text)
        elif part.inline_data is not None:
            image = Image.open(BytesIO((part.inline_data.data)))
            image.save(f"output_folder/example-image-{i+1}.png")
            fp.write(f"![image](example-image-{i+1}.png)")
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
import com.google.genai.types.Blob;
import com.google.genai.types.Candidate;
import com.google.genai.types.Content;
import com.google.genai.types.GenerateContentConfig;
import com.google.genai.types.GenerateContentResponse;
import com.google.genai.types.Part;
import java.awt.image.BufferedImage;
import java.io.BufferedWriter;
import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import javax.imageio.ImageIO;

public class ImageGenMmFlashTextAndImageWithText {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String modelId = "gemini-2.5-flash-image";
    String outputFile = "resources/output/paella-recipe.md";
    generateContent(modelId, outputFile);
  }

  // Generates text and image with text input
  public static void generateContent(String modelId, String outputFile) throws IOException {
    // Client Initialization. Once created, it can be reused for multiple requests.
    try (Client client = Client.builder().location("global").vertexAI(true).build()) {

      GenerateContentResponse response =
          client.models.generateContent(
              modelId,
              Content.fromParts(
                  Part.fromText("Generate an illustrated recipe for a paella."),
                  Part.fromText(
                      "Create images to go alongside the text as you generate the recipe.")),
              GenerateContentConfig.builder().responseModalities("TEXT", "IMAGE").build());

      try (BufferedWriter writer = new BufferedWriter(new FileWriter(outputFile))) {

        // Get parts of the response
        List<Part> parts =
            response
                .candidates()
                .flatMap(candidates -> candidates.stream().findFirst())
                .flatMap(Candidate::content)
                .flatMap(Content::parts)
                .orElse(new ArrayList<>());

        int index = 1;
        // For each part print text if present, otherwise read image data if present and
        // write it to the output file
        for (Part part : parts) {
          if (part.text().isPresent()) {
            writer.write(part.text().get());
          } else if (part.inlineData().flatMap(Blob::data).isPresent()) {
            BufferedImage image =
                ImageIO.read(new ByteArrayInputStream(part.inlineData().flatMap(Blob::data).get()));
            ImageIO.write(
                image, "png", new File("resources/output/example-image-" + index + ".png"));
            writer.write("![image](example-image-" + index + ".png)");
          }
          index++;
        }

        System.out.println("Content written to: " + outputFile);

        // Example response:
        // A markdown page for a Paella recipe(`paella-recipe.md`) has been generated.
        // It includes detailed steps and several images illustrating the cooking process.
        //
        // Content written to:  resources/output/paella-recipe.md
      }
    }
  }
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
    "os"
    "path/filepath"

    "google.golang.org/genai"
)

// generateMMFlashTxtImgWithText demonstrates how to generate an illustrated recipe
// combining text and image outputs into a markdown file.
func generateMMFlashTxtImgWithText(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-flash-image"
    contents := []*genai.Content{
        {
            Parts: []*genai.Part{
                {Text: "Generate an illustrated recipe for a paella. " +
                    "Create images to go alongside the text as you generate the recipe."},
            },
            Role: genai.RoleUser,
        },
    }

    resp, err := client.Models.GenerateContent(ctx,
        modelName,
        contents,
        &genai.GenerateContentConfig{
            ResponseModalities: []string{
                string(genai.ModalityText),
                string(genai.ModalityImage),
            },
            CandidateCount: int32(1),
        },
    )
    if err != nil {
        return fmt.Errorf("failed to generate content: %w", err)
    }

    if len(resp.Candidates) == 0 || resp.Candidates[0].Content == nil {
        return fmt.Errorf("no candidates returned")
    }

    outputFolder := ""

    // Create the markdown file
    mdFile := filepath.Join(outputFolder, "paella-recipe.md")
    fp, err := os.Create(mdFile)
    if err != nil {
        return fmt.Errorf("failed to create markdown file: %w", err)
    }
    defer fp.Close()

    for i, part := range resp.Candidates[0].Content.Parts {
        if part.Text != "" {
            if _, err := fp.WriteString(part.Text); err != nil {
                return fmt.Errorf("failed to write text: %w", err)
            }
        } else if part.InlineData != nil {
            imgFile := filepath.Join(outputFolder, fmt.Sprintf("example-image-%d.png", i+1))
            if err := os.WriteFile(imgFile, part.InlineData.Data, 0644); err != nil {
                return fmt.Errorf("failed to save image: %w", err)
            }
            if _, err := fp.WriteString(fmt.Sprintf("![image](%s)", filepath.Base(imgFile))); err != nil {
                return fmt.Errorf("failed to write image reference: %w", err)
            }
        }
    }

    fmt.Fprintln(w, mdFile)

    // Example response:
    //  A markdown page for a Paella recipe (`paella-recipe.md`) has been generated.
    //  It includes detailed steps and several images illustrating the cooking process.
    return nil
}
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
const fs = require('fs');
const {GoogleGenAI, Modality} = require('@google/genai');

const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
const GOOGLE_CLOUD_LOCATION =
  process.env.GOOGLE_CLOUD_LOCATION || 'us-central1';

async function savePaellaRecipe(response) {
  const parts = response.candidates[0].content.parts;

  let mdText = '';
  const outputDir = 'output-folder';

  for (let i = 0; i < parts.length; i++) {
    const part = parts[i];

    if (part.text) {
      mdText += part.text + '\n';
    } else if (part.inlineData) {
      if (!fs.existsSync(outputDir)) {
        fs.mkdirSync(outputDir, {recursive: true});
      }
      const imageBytes = Buffer.from(part.inlineData.data, 'base64');
      const imagePath = `example-image-${i + 1}.png`;
      const saveImagePath = `${outputDir}/${imagePath}`;

      fs.writeFileSync(saveImagePath, imageBytes);
      mdText += `![image](./${imagePath})\n`;
    }
  }
  const mdFile = `${outputDir}/paella-recipe.md`;

  fs.writeFileSync(mdFile, mdText);
  console.log(`Saved recipe to: ${mdFile}`);
}

async function generateImage(
  projectId = GOOGLE_CLOUD_PROJECT,
  location = GOOGLE_CLOUD_LOCATION
) {
  const client = new GoogleGenAI({
    vertexai: true,
    project: projectId,
    location: location,
  });

  const response = await client.models.generateContent({
    model: 'gemini-2.5-flash-image',
    contents:
      'Generate an illustrated recipe for a paella. Create images to go alongside the text as you generate the recipe',
    config: {
      responseModalities: [Modality.TEXT, Modality.IMAGE],
    },
  });
  console.log(response);

  await savePaellaRecipe(response);

  return response;
}
// Example response:
//  A markdown page for a Paella recipe(`paella-recipe.md`) has been generated.
//  It includes detailed steps and several images illustrating the cooking process.
```

### REST

Run the following command in the terminal to create or overwrite this file in the current directory:

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://${API_ENDPOINT}:generateContent \
  -d '{
    "contents": {
      "role": "USER",
      "parts": [
        {
          "text": "Generate an illustrated recipe for a paella. Create images to
          go alongside the text as you generate the recipe."
        }
      ]
    },
    "generationConfig": {
      "responseModalities": ["TEXT", "IMAGE"],
      "imageConfig": {
        "aspectRatio": "16:9",
      },
    },
    "safetySettings": {
      "method": "PROBABILITY",
      "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
      "threshold": "BLOCK_MEDIUM_AND_ABOVE"
    },
  }' 2>/dev/null >response.json
```

Gemini generates an image based on your description. This process takes a few seconds, but can be comparatively slower depending on capacity.

## Save generated images to Cloud Storage

Instead of returning raw base64-encoded image bytes inline in the response, you can configure `generateContent` and `streamGenerateContent` requests to write generated images directly to a Cloud Storage bucket and return the object URI in `fileData.fileUri` .

The following Gemini models support Cloud Storage output persistence:

- [Gemini Nano Banana 2.1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/nano-banana-2-1) ( `gemini-nano-banana-2.1` )
- [Gemini 3.1 Flash Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image) ( `gemini-3.1-flash-image` )
- [Gemini 3.1 Flash-Lite Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite-image) ( `gemini-3.1-flash-lite-image` )
- [Gemini 3 Pro Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image) ( `gemini-3-pro-image` )

### Prerequisites

Before sending a request with Cloud Storage output persistence, verify that the principal authenticating the request has the following Identity and Access Management permission on the destination Cloud Storage bucket:

- `storage.objects.create` (included in roles such as the Storage Object Creator role, `roles/storage.objectCreator` )

Before generating images, the service verifies `storage.objects.create` permission on the target Cloud Storage bucket using the caller's credentials. If the Cloud Storage bucket does not exist, the caller lacks write permission, or a VPC Service Controls perimeter blocks the write, the request fails before generation with a `403 PERMISSION_DENIED` error.

### Send a request with Cloud Storage output

To write generated images directly to Cloud Storage, configure both of the following fields in your `generateContent` or `streamGenerateContent` request:

- Set `outputConfig.outputUriPrefix` to your destination Cloud Storage bucket or folder prefix (for example, `gs:// `` BUCKET_NAME `` / `` PREFIX `` /` ).
- Set `generationConfig.responseFormat[].image.delivery` to `"URI"` .

The following REST request generates an image and writes it directly to a Cloud Storage bucket:

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-nano-banana-2.1:generateContent" \
  -d '{
    "contents": [
      {
        "role": "USER",
        "parts": [
          {
            "text": "Create an architectural rendering of a sustainable glass greenhouse in alpine snow."
          }
        ]
      }
    ],
    "generationConfig": {
      "responseModalities": ["TEXT", "IMAGE"],
      "responseFormat": [
        {
          "image": {
            "delivery": "URI"
          }
        }
      ]
    },
    "outputConfig": {
      "outputUriPrefix": "gs://BUCKET_NAME/PREFIX/"
    }
  }'
```

Replace the following:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` BUCKET_NAME ` : The name of the destination Cloud Storage bucket.
- ` PREFIX ` : Optional folder path prefix inside the Cloud Storage bucket (for example, `outputs` ).

The service writes each generated image part to Cloud Storage using the naming pattern `gs:// `` BUCKET `*`NAME`*` `` `*`/ `` PREFIX `` /image`*` `` GENERATION `*`ID`*` `` `*`. `` EXTENSION`* *(appending* `CANDIDATE `*`INDEX`* *when a response contains multiple candidates, and* `IMAGE_INDEX` when a candidate contains multiple images) and returns the URI in `fileData` :

```
{
  "candidates": [
    {
      "content": {
        "role": "model",
        "parts": [
          {
            "fileData": {
              "mimeType": "image/png",
              "fileUri": "gs://my-bucket/outputs/image_1234567890.png"
            }
          }
        ]
      }
    }
  ]
}
```

When you configure Cloud Storage output delivery, the service handles responses as follows:

- **Mixed text and image responses** : Text parts in a `TEXT` and `IMAGE` response remain inline in `parts[].text` . Only generated image parts are written to Cloud Storage and returned as `parts[].fileData` objects.
- **Thinking images** : When `generationConfig.thinkingConfig.includeThoughts` is set to `true` , intermediate thinking images ( `parts[].thought: true` ) are also written to Cloud Storage using the `thought `*`image`*` `` GENERATION_ID` prefix and returned as `parts[].fileData` objects.
- **Streaming responses ( `streamGenerateContent` )** : Each generated image is written to Cloud Storage before the response chunk referencing its `fileData.fileUri` is sent.
- **No-image responses** : If a request returns only text or is blocked by safety filters, no object is written to Cloud Storage.
- **Encryption and retention** : Written objects inherit the destination Cloud Storage bucket's encryption configuration, including Customer-managed encryption keys (CMEK), and follow the Cloud Storage bucket's lifecycle management rules.

### Limitations

Cloud Storage output has the following limitation:

- **Multi-turn editing with cross-project Cloud Storage buckets** : The service writes generated images using the credentials of the principal that sent the request. However, when a later request in a multi-turn conversation references a generated image by its `fileData.fileUri` , the service reads the object using the Gemini Enterprise Agent Platform service agent of the calling project ( `service- `` PROJECT_NUMBER `` @gcp-sa-aiplatform.iam.gserviceaccount.com` ). If the destination Cloud Storage bucket is in a different project and the service agent doesn't have the `storage.objects.get` permission on that Cloud Storage bucket, the follow-up request fails with a `403 PERMISSION_DENIED` error even though the original write succeeded.

  To use generated images as input in multi-turn editing, grant the service agent read access to the destination Cloud Storage bucket (for example, the Storage Object Viewer role, `roles/storage.objectViewer` ).

## What's next

See the following links for more information about Gemini image generation:

- [Edit images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images)

- [Gemini image generation best practices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-best-practices)

- [Gemini image generation limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-generation-limitations)

- [Gemini image generation and responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-image-responsible-ai)
