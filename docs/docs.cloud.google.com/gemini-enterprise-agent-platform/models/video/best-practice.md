---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice
title: Best practices for generating videos
description: Learn best practices for generating videos on Gemini Enterprise Agent Platform
data_source: docs.cloud.google.com
---

This guide provides best practices to help you generate high-quality Gemini Omni and Veo videos.

For more information about writing effective prompts, see [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide) .

## Use clear and specific prompts

Clear and direct prompts that eliminate ambiguity help generate better video output.

  - **Not recommended** : "I envision a scene where, like, the main focus, a dude, is kinda sad, and it's like, dark, and the camera is sort of, from below, you know?"

  - **Recommended** : "Low-angle close-up shot of a man with a somber expression. The scene is dimly lit, conveying a melancholic mood"

## Avoid quotation marks

To prevent the model from rendering text in the video, use a colon ( `:` ) after the speaker's action to denote speech and avoid using quotation marks ( `"` ).

  - **Not recommended** : A woman says: "My name is Clara."

  - **Recommended** : A woman says: My name is Clara.

## Use multiple aspect ratios

Use aspect ratios to increase your video's performance on multiple platforms. Different platforms are optimized for different aspect ratios. Understanding your platforms' aspect ratios is critical for marketing and advertising.

The following are key aspect ratios and their primary uses:

  - **16:9** : Also called "landscape" or "widescreen", considered the standard for televisions, monitors, most video displays, YouTube, presentations, and mobile phones in landscape mode. The 16:9 aspect ratio is also helpful for capturing more of the background, such as scenic landscapes.

  - **9:16** : Also called portrait, vertical, or rotated widescreen. 9:16 is essential for mobile-first platforms like TikTok, Instagram Reels, and YouTube Shorts. The 9:16 aspect ratio is also helpful for portraits or tall objects with strong vertical orientations, such as buildings, trees, or waterfalls.

## Focus short videos on a single scene

For short videos, dedicate each prompt to a single, focused moment. Trying to chain multiple distinct events (A then B then C) in one prompt for a short video often leads to muddled or incomplete videos.

  - **Not recommended** : "A detective finds a clue in a library, then drives across the city at night, and then confronts a suspect in a warehouse"

  - **Recommended** : Generate each part as a separate clip:
    
      - **Clip 1** : "close-up on a detective's gloved hand brushing dust off an old book in a dark library, revealing a hidden symbol"
    
      - **Clip 2** : "a car driving through a neon-lit city at night, with rain streaking across the windshield, in a film noir style"
    
      - **Clip 3** : "inside a shadowy warehouse, a detective stands opposite a silhouetted figure, creating a tense atmosphere"

## Enhance your workflow with Gemini Omni

Gemini Omni can be a powerful partner throughout your entire video creation process, from ideation to evaluation.

**Before video creation: use Gemini Omni as an expert prompter**

Instead of starting from scratch, you can ask Gemini Omni to act as an expert prompter. Have it refine your basic ideas into detailed, prompts. For example, you can give it an instruction such as the following:

    "Act as an expert prompter for a generative AI video generation model. Look at
    this image, and write a prompt that INSTRUCTION. Ensure your
    prompt is comprehensive and detailed."

Replace `  INSTRUCTION  ` with further instructions to the model.

**After video creation: use Gemini Omni as a "second pair of eyes"**

After your video is generated, Gemini Omni can evaluate the final output, check it against company or brand guidelines, and flag any potentially problematic areas that may require human review.

## Achieve character and voice consistency

**Create a detailed character description** : Your character description is the foundation for consistency. To ensure reusability and voice consistency, give your character a name and a specific voice style. Then, build out the description with a rich set of unchangeable features: physical build and age, hair color and style, facial structure, eye color and shape, and any defining marks. You can use Gemini Omni to generate an exhaustive verbal description of your character's facial features.

**Apply the description consistently** : Copy and paste the entire, unchanged character description into your prompt for every new scene or action. Only modify the parts that describe the new action or setting. To improve your workflow, you can also use Gemini Omni as a scene generator. Provide Gemini Omni with your final character description and ask it to generate multiple scene prompts for you.

**Use the same seed parameter** : To ensure consistent visual, stylistic, and voice output across multiple scenes, use the same seed parameter.

**Example:** The following video was generated using the same seed parameter and the following prompts. The repeated character and voice descriptions are bolded in each of the following prompts:

[Video](https://www.youtube.com/watch?v=TZ8go3Q7Sqo)

**Prompt for Scene 1** :

    "A medium shot, with the camera slowly dollying forward in a dimly lit, grand
    Parisian archive. Dust motes dance in a single beam of light from a high window.
    Clara, a historian in her early 30s, with observant, dark brown
    eyes that hold a quiet intensity. She has chin-length, black hair styled in a
    classic bob. She is dressed in a sophisticated, dark navy-blue
    wool coat, with a silk scarf patterned with subtle gold and cream designs tied
    around her neck. She stands before a large, ancient wooden table, carefully
    turning the fragile, yellowed page of a massive, leather-bound book. Her
    expression is one of deep concentration. In a voice that is crisp
    and clear, with a thoughtful, analytical tone and a standard American
    accent, Clara says: It has to be here"

**Prompt for Scene 2** :

    "A wide shot of the Pont des Arts in Paris at twilight, the sky a mix of deep
    blue and soft orange. The lights of the city are beginning to twinkle on along
    the Seine. Clara, a historian in her early 30s, with observant,
    dark brown eyes that hold a quiet intensity. She has chin-length, black hair
    styled in a classic bob. She is dressed in a sophisticated, dark
    navy-blue wool coat, with a silk scarf patterned with subtle gold and cream
    designs tied around her neck. She leans against the railing, looking out at the
    water, a small, triumphant smile on her face. She pulls a folded, old map from
    her coat pocket and looks down at it. In a voice that is crisp and
    clear, with a thoughtful, analytical tone and a standard American
    accent, Clara says: I knew it. The path starts from here"

**Prompt for Scene 3** :

    "An eye-level shot in a small, hidden Parisian courtyard, overgrown with ivy and
    lit by a single, warm gas lamp. Clara, a historian in her early
    30s, with observant, dark brown eyes that hold a quiet intensity. She has
    chin-length, black hair styled in a classic bob. She is dressed
    in a sophisticated, dark navy-blue wool coat, with a silk scarf patterned with
    subtle gold and cream designs tied around her neck. She kneels down and runs her
    fingers over an ancient, carved symbol on a stone paver, almost completely
    obscured by moss. Her eyes light up with discovery. In a voice
    that is crisp and clear, with a thoughtful, analytical tone and a standard
    American accent, Clara says: After all these years, I've found
    it"

## Image-to-video

The following sections are best practices that are important when using image-to-video.

### Use a high-quality source image

When using the image-to-video feature, the quality of your source image is important. Gemini Omni and Veo use the source image as the basis for everything that follows, including character detail, lighting, and overall artistic style.

A sharp, clear, and well-composed photograph yields a more coherent and higher-quality video. Think of your source image as the first frame of your film: the stronger the start, the better the finish.

### Prompt for motion only

Your source image already provides the subject, scene, and style. Focus your prompt on the motion you want to see.

  - **Not recommended** : Re-describe the character, the background, or the lighting depicted in the image. Redundant prompts confuse the model and lead to poor results.

  - **Recommended** : Prompt for camera movement, subject animation, and environmental changes.

### Use general terms for characters in the source image

In your motion prompt, refer to the character with general terms like "the subject", "the woman", "he", "she", or "they".

### Direct the camera's movement

You can direct three types of movement, either alone or in combination.

  - **Camera Motion** : The camera moves, but the scene is static. This is the simplest and most reliable way to add dynamism.
    
      - Example: "Slow dolly in on the subject."

  - **Subject Animation** : The main character or object moves. Best for subtle, lifelike actions.
    
      - Example: "The character's hair and clothes flutter gently in the wind."

  - **Environmental Animation** : The background or atmosphere comes alive.
    
      - Example: "Fog rolls in slowly across the landscape."

**Example** : The following video and prompt demonstrate subject animation using the following image:

![An old, somewhat beat-up blue pickup truck in front of a field of sunflowers](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/models/video/images/veo-subject-animation-sample-image.webp)

[Video](https://www.youtube.com/watch?v=McOgmOGs6N0)

    "A sweeping drone-like aerial view starting from ground level and rising to
    reveal the entire landscape in epic proportions"

## Summary of best practices

The following table summarizes the best practices recommended in this document:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topic</th>
<th>Task</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prompts</td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#use-clear-and-specific-prompts">Use clear and specific prompts</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#avoid-quotation-marks">Avoid quotation marks</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#focus-short-videos-on-a-single-scene">Focus short videos on a single scene</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#enhance-workflow-with-gemini">Enhance your workflow with Gemini Omni</a></li>
</ul></td>
</tr>
<tr class="even">
<td>Video generation</td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#use-multiple-aspect-ratios">Use multiple aspect ratios</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#achieve-character-and-voice-consistency">Achieve character and voice consistency</a></li>
</ul></td>
</tr>
<tr class="odd">
<td>Image-to-video</td>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#use-high-quality-source-image">Use a high-quality source image</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#prompt-for-motion-only">Prompt for motion only</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#use-general-terms">Use general terms for characters in the source image</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice#direct-camera-movement">Direct the camera's movement</a></li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

  - [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide)

  - [Generate videos from text prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)

  - [Generate videos from an image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)

  - [Generate videos using first and last video frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)

  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)

  - [Understand responsible AI and usage guidelines for video generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines)
