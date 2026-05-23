---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/compare-prompts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/compare-prompts
title: Compare prompts
description: Compare prompt engineering techniques, model outputs, and parameter settings using the Compare feature in Agent Platform.
data_source: docs.cloud.google.com
---

The Compare feature lets you see how a different prompt, model, or a parameter setting changes the model's output. You can view each of the prompts and their responses side by side to compare and analyze in the following ways:

  - With a new prompt.
  - With another saved prompt.
  - With a ground truth.

> **Note:** The Compare feature doesn't support prompts with media or chat prompts with more than one exchange.

## Before you begin

To access the Compare feature, follow these steps:

1.  In the Google Cloud console, go to the **Create prompt** page.

2.  Select **Compare** . The **Compare** page appears.

## Create a prompt in the Compare feature

On the **Compare** page, you can create a prompt before selecting another prompt to compare results.

To create a prompt, follow these steps:

1.  In the **New Prompt** field, enter your prompt.

2.  Click **Submit prompts** . The model's response appears below the prompt text that you entered.

3.  Click **Save as new** . A **Save prompt** dialog appears.

4.  Enter the name of your new prompt in the **Prompt name** field.

5.  Select your region in the **Region** field, or leave it as the default region.

6.  If a customer-managed encryption key (CMEK) applies, do the following:
    
    1.  Select the **Customer-managed encryption key (CMEK)** checkbox.
    2.  Select a key from the **Select a Cloud KMS key** field.

7.  Click **Save** , which saves your prompt in the list of prompts to use on the **Compare saved prompt** page.

8.  Click **Submit prompts** to compare the prompts and their responses.

You can update your prompts, and save updated versions as new prompts.

## Compare with a new prompt

To compare your saved prompt with a new prompt, follow these steps:

Click **Compare new prompt** . A **Compare** pane appears.

Optional: Click **Switch model** to use a different model from the default model.

Optional: Expand **Outputs** .

##### Outputs:

Optional: If you want the model to output in a specific format such as JSON, click the **Structured output** toggle. After you select **Structured output** , the Grounding options are turned off, because grounding isn't supported with structured output.

Optional: Change the **Thinking budget** to one of the following options:

  - **Auto** : The model only thinks when it needs to. The model adjusts how much it thinks or analyzes a situation based on what's needed at the time.
  - **Manual** : You can adjust the thinking budget tokens.
  - **Off** : No thinking or budgets are used.

Optional: Expand **Tools** .

##### Tools:

Select one of the following options:

**Grounding: Google** : Grounding with Google Search or Google Maps.

**Grounding: Your data** : Grounding with Vertex AI RAG Engine, Agent Search or Elasticsearch.

1.  If you select **Grounding: Your data** , select the data source that you want to use.

Optional: Expand **Advanced** :

##### Advanced:

Select **Region** .

Select **Safety Filter Settings** . A dialog appears. Keep the default of **Off** , or you can specify **Block few** , **Block some** , or **Block most** for each of the following options:

  - **Hate speech** : Negative or harmful comments targeting identity or protected attributes.
  - **Dangerous content** : Promotes or enables access to harmful goods, services, and activities.
  - **Sexually explicit content** : Contains references to sexual acts or other lewd content.
  - **Harassment content** : Malicious, intimidating, bullying, or abusive comments targeting another individual.

Click **Save** to save the settings and close the dialog.

Select the temperature from the **Temperature** field. The temperature controls the randomness in token selection. A lower temperature is good when you expect a true or correct response. A higher temperature can lead to diverse or unexpected results.

Select the output token limit from the **Output token limit** field. Output token limit determines the maximum amount of text output from one prompt. A token is approximately four characters.

Select the maximum responses from the **Max responses** field. If the maximum number of model responses generated per prompt. Because of safety filters or other policies, responses can still be blocked.

Select a value from the **Top-P** field. The Top-p changes how the model selects tokens for output.

Click toggle on the **Stream model responses** field. If selected, the responses are printed as they're generated.

Enter a stop sequence in the **Add stop sequence** field. Press **Enter** after each sequence.

6.  Click **Save** to save changes to your settings.
7.  Click **Apply** .
8.  Click **Submit prompts** to compare the prompts and their responses.

For more information on token limits for each model, see [Control the thinking budget](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#budget) .

## Compare with another saved prompt

To compare your saved prompt with another saved prompt, follow these steps:

1.  Click **Compare saved prompt** . The **Existing Prompt** pane appears.

2.  Choose up to two existing prompts to compare.
    
    1.  Select a **Prompt name** . If you have many prompts in your list, click in the **Filter** field, and select the property that you want to filter by. Enter a value, and press Enter .
    2.  Click **Apply** . The **Compare** page displays the prompt that you've selected alongside other prompts that you've created or selected for comparison.

3.  Click **Submit prompts** to compare the prompts and their responses.

## Compare with a ground truth

Ground truth is your preferred answer to the prompt. All other model responses are evaluated against the ground truth answer.

To compare your saved prompt with a ground truth, follow these steps:

1.  Click **Ground truth** . The **Ground truth** pane appears.
2.  Enter your ground truth to generate additional evaluation metrics.
3.  Click **Save** to save the ground truth.
4.  Click **Submit prompts** to compare the prompts and their responses.

The evaluation metrics that are generated when you compare a prompt with a ground truth aren't affected by the region that you select.

## What's next

  - Explore more examples of prompts in the [Prompt gallery](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/prompt-gallery) .
  - For more information about evaluating your models, see [Gen AI evaluation service overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/evaluation-overview) .
