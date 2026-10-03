---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction
title: System instructions
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> To see an example of system instructions, run the "Intro to Gemini 3.5 Flash" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_3_5_flash.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_gemini_3_5_flash.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_gemini_3_5_flash.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_3_5_flash.ipynb)

This document describes what system instructions are and best practices for writing effective system instructions. To learn how to add system instructions to your prompts, see [Use system instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instructions) instead.

System instructions are a set of instructions that the model processes before it processes prompts. We recommend that you use system instructions to tell the model how you want it to behave and respond to prompts. For example, you can include things like a persona to adopt, contextual information, and formatting instructions.

System instructions are especially useful in cases when you want to provide the model with information that an end user can't see or change, which can help you give the model additional context to understand the task, provide more customized responses, adhere to specific guidelines over the full user interaction with the model. Additionally, system instructions are beneficial when you want to run multiple prompts with the same set of instructions.

When system instructions are set, they apply to the entire request. System instructions work across multiple user and model turns when included in the prompt. Though system instructions are separate from the contents of the prompt, they're still part of your overall prompts and therefore subject to standard data use policies.

> **Note:** System instructions can help guide the model to follow instructions, but they don't fully prevent jailbreaks or leaks. We recommend exercising caution around putting any sensitive information in system instructions.

## Use cases

Generally, we recommend using system instructions to do one or more of the following:

- Define a persona or role

- Define output format

- Define output style and tone

- Define goals or rules for the task

- Provide additional context for the prompt

### Persona or role

You can influence how a model responds to prompts by defining a persona or role in system instructions.

For example, suppose you want to use a model to help teach students about writing papers. Compare the difference in the model's responses when you define the following roles:

- You are a bot, tasked with teaching college students about how to write a paper about a given subject.
- You are a bot, tasked with helping primary school students about how to write a paper about a given subject.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>System instructions</th>
<th>Bot for college students</th>
<th>Bot for primary school students</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th><strong>You are a bot, tasked with teaching college students</strong> about how to write a paper about a given subject.</th>
<td><strong>You are a bot, tasked with helping primary school students</strong> about how to write a paper about a given subject.</td>
<td></td>
</tr>
<tr class="even">
<th>Prompt</th>
<td>Subject: Photosynthesis</td>
<td>Subject: Photosynthesis</td>
</tr>
<tr class="odd">
<th>Response</th>
<td><p>Writing a Paper on Photosynthesis: A Guide for College Students</p>
<p>Photosynthesis is a fascinating and complex process that forms the basis of life on Earth. Writing a paper on it can be a rewarding experience, allowing you to delve deeper into its intricacies and understand its significance. Here's a breakdown of how to approach this task:</p>
<ol>
<li>Choosing a Focus:
<ul>
<li>Broad Overview: You could provide a comprehensive overview of photosynthesis, covering its stages, requirements, byproducts, and its role in the ecosystem.</li>
<li>Specific Aspect: Choose a specific aspect of photosynthesis to explore in detail, like:
<ul>
<li>The role of light in photosynthesis.</li>
<li>The different types of photosynthesis (C3, C4, CAM).</li>
<li>The impact of environmental factors on photosynthesis.</li>
<li>The evolution of photosynthesis.</li>
<li>The applications of photosynthesis in biotechnology.</li>
</ul></li>
<li>Comparative Study: Compare and contrast different aspects of photosynthesis in different organisms (plants, algae, bacteria).</li>
</ul></li>
<li>Research and Gathering Information:
<ul>
<li>Reliable Sources: Use academic journals, reputable online sources, and textbooks. Avoid relying solely on Wikipedia or general websites.</li>
<li>Keyword Search: Use keywords like "photosynthesis," "chloroplasts," "chlorophyll," "light-dependent reactions," "Calvin cycle," etc.</li>
<li>Note-taking: Organize your research by taking thorough notes and summarizing key points, ensuring to cite sources properly.</li>
</ul></li>
<li>Outlining and Structuring your Paper:
<ul>
<li>Introduction:
<ul>
<li>Briefly introduce photosynthesis and its significance.</li>
<li>State your thesis statement, clearly outlining the main argument of your paper.</li>
</ul></li>
<li>Body Paragraphs:
<ul>
<li>Develop your points in a logical sequence, using evidence from your research.</li>
<li>Use headings and subheadings to organize your paper and make it easier to read.</li>
<li>Each paragraph should focus on a single idea and provide supporting evidence.</li>
</ul></li>
<li>Conclusion:
<ul>
<li>Summarize your main points and restate your thesis.</li>
<li>Discuss the implications of your findings and suggest future research directions.</li>
</ul></li>
</ul></li>
<li>Writing and Editing:
<ul>
<li>Clear and Concise Language: Use clear and concise language, avoiding jargon unless it is necessary.</li>
<li>Evidence-based Arguments: Support your claims with evidence from your research.</li>
<li>Proper Citation: Use a consistent citation style (MLA, APA, Chicago) throughout your paper.</li>
<li>Proofreading and Editing: Carefully proofread and edit your paper for grammar, spelling, and punctuation errors.</li>
</ul></li>
<li>Additional Tips:
<ul>
<li>Visual Aids: Use diagrams, graphs, or charts to illustrate complex concepts.</li>
<li>Case Studies: If applicable, include relevant case studies to demonstrate the real-world applications of photosynthesis.</li>
<li>Personal Connection: Find a way to connect your topic to your own interests or experiences.</li>
</ul></li>
</ol>
<p>Example Paper Titles:</p>
<ul>
<li>The Role of Light Intensity in Photosynthesis: A Comparative Study</li>
<li>The Evolution of Photosynthesis: From Early Life to Modern Plants</li>
<li>Harnessing Photosynthesis: The Potential of Biotechnology</li>
<li>The Impact of Climate Change on Photosynthesis: A Global Perspective</li>
</ul>
<p>Remember: A well-written paper on photosynthesis should be clear, informative, and engaging. By following these steps and utilizing a strong foundation of research, you can produce a successful paper that demonstrates your understanding of this essential biological process.</p>
(gemini-flash)</td>
<td><p>That's a great subject! Photosynthesis is super important for life on Earth. Here's how you can write a paper about it:</p>
<ol>
<li>Think about what you already know:
<ul>
<li>What is photosynthesis?</li>
<li>What does a plant need to do photosynthesis?</li>
<li>What does a plant make during photosynthesis?</li>
<li>Do you know any interesting facts about photosynthesis?</li>
</ul></li>
<li>Research and learn more:
<ul>
<li>Books: Check out your library for books about plants, nature, or science.</li>
<li>Websites: Look for websites for kids that explain photosynthesis in a simple way. Make sure the websites are reliable (like ones from National Geographic or NASA).</li>
<li>Ask a grown-up: Ask your teacher, parent, or librarian for help finding information.</li>
</ul></li>
<li>Organize your thoughts:
<ul>
<li>Title: Think of a catchy title for your paper, like "The Amazing Process of Photosynthesis" or "How Plants Make Their Own Food."</li>
<li>Introduction: Start with a sentence that grabs the reader's attention. Explain what photosynthesis is in simple terms.</li>
<li>Main Body: Divide your paper into paragraphs. Each paragraph should focus on one key idea about photosynthesis:
<ul>
<li>What plants need: Sunlight, water, carbon dioxide.</li>
<li>What plants make: Sugar (for food) and oxygen.</li>
<li>Why photosynthesis is important: It provides food for us and animals, and it cleans the air.</li>
</ul></li>
<li>Conclusion: Sum up what you learned about photosynthesis. You can also share your favorite fact or a question you still have.</li>
</ul></li>
<li>Write your paper:
<ul>
<li>Use clear and simple language.</li>
<li>Don't be afraid to use pictures or drawings to help explain things.</li>
<li>Check your work for spelling and grammar mistakes.</li>
</ul></li>
<li>Make it your own!
<ul>
<li>Add a personal touch to your paper.</li>
<li>Share an experience or observation you've had about plants.</li>
<li>Draw a diagram to show how photosynthesis works.</li>
</ul></li>
</ol>
<p>Remember: You're the expert on your paper! Have fun learning and writing about photosynthesis.</p>
(gemini-flash)</td>
</tr>
</tbody>
</table>

### Output format

You can influence how a model formats its response by defining an output format, such as Markdown or JSON, in system instructions.

For example, suppose you want to use a model to summarize customer reviews for your business. Compare the difference in the model's responses when you define the following output formats:

- Output your response in JSON. At the very end, outside the JSON object, write 3-5 sentences of advice to the business on how to improve.
- No formatting requirements.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>System instructions</th>
<th>JSON</th>
<th>No formatting requirements</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th><p>You are a PR professional for high-end businesses. Follow these instructions, and base your response on the provided User Input.</p>
<p>Instructions:</p>
<ul>
<li>Read through reviews submitted to you.</li>
<li>Summarize the pros and cons of the business based on reviews.</li>
</ul>
<strong></strong>
Output your response in JSON.
At the very end, outside the JSON object, write 3 to 5 sentences of advice to the business on how to improve.
<ul>
<li>Keep it concise.</li>
<li>Stick to the facts.</li>
<li>Do not hallucinate.</li>
<li>If there are conflicting opinions, only include the opinion that is recorded the most.</li>
<li>Do not include any irrelevant information.</li>
<li>Do not mention any reviewers by name.</li>
</ul></th>
<td><p>You are a PR professional for high-end businesses. Follow these instructions, and base your response on the provided User Input.</p>
<p>Instructions:</p>
<ul>
<li>Read through reviews submitted to you.</li>
<li>Summarize the pros and cons of the business based on reviews.</li>
<li>Keep it concise.</li>
<li>Stick to the facts.</li>
<li>Do not hallucinate.</li>
<li>If there are conflicting opinions, only include the opinion that is recorded the most.</li>
<li>Do not include any irrelevant information.</li>
<li>Do not mention any reviewers by name.</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Prompt</th>
<td><p>Chad Brocker: 4 stars</p>
<p>This spa was delightful! The entire atmosphere as soon as you walk in relaxes you. It almost feels like you're in a trance. You don't have to worry about ANYTHING. The workers have your schedule and guide you through your experience. Everything I got was amazing. The massage, the facial, the mud bath. Plus, they have a 0 cell phone policy, so it really does feel like you're in a whole different world. It is a bit pricey though.</p>
View full prompt
<p>Lisa Simmens: 5 stars</p>
<p>We had a wonderful time! My best friend and I treated ourselves to a spa day for our birthdays. When I tell you, our lives are changed. The employees go above and beyond to make sure you're getting the best experience possible. From asking you questions to high quality services and ensuring you get to each of your appointments on time, they were truly the best. We will be back soon! P.S. get the full body exfoliation treatment!</p>
<p>Allie Wood: 2 stars</p>
<p>While the workers were amazing in their customer services, my massage HURT and my facial BURNED. Plus, they didn't let you have your cellphone, which causes extra stress. The atmosphere was tranquil and calming, but not having my cell phone made me unable to relax. Plus, it was expensive.</p>
<p>Suzy Michaels: 3 stars</p>
<p>The environment of this space was out of this world. It's seriously like stepping into Heaven. My services were the best I've ever had. BUT, they didn't offer any sort of refreshments. I mean, come on, you at least should offer water?!</p>
<p>Martin Wong: 4 stars</p>
<p>Amazing experience. My only complaint is not being able to check my phone.</p>
<p>Debbie Ruiz: 5 stars</p>
<p>Amazing environment. Amazing workers. Amazing services. Plus, it's a cell phone free environment, which was SO freeing and adding = to the peaceful atmosphere. I definitely recommend it to everyone!!!</p>
<p>Lucy Mantel: 1 stars</p>
<p>No refreshments. No cellphones. Bad massage. Not a great experience. Do not recommend.</p></td>
<td></td>
</tr>
<tr class="odd">
<th>Response</th>
<td><pre class="json"><code>    {
      &quot;&quot;pros&quot;&quot;: [
        &quot;&quot;relaxing atmosphere&quot;&quot;,
        &quot;&quot;attentive and efficient staff&quot;&quot;,
        &quot;&quot;high-quality services&quot;&quot;
      ],
      &quot;&quot;cons&quot;&quot;: [
        &quot;&quot;pricey&quot;&quot;,
        &quot;&quot;no cell phone policy&quot;&quot;,
        &quot;&quot;no refreshments&quot;&quot;
      ]
    }
    </code></pre>
<p>While the spa has received praise for its tranquil atmosphere, exceptional staff, and top-notch services, there are some areas for improvement. Addressing customer concerns regarding the strict no-cellphone policy and the lack of refreshments could significantly enhance the overall experience. Consider offering a designated area for guests to access their phones if needed, and providing complimentary water or a limited selection of beverages.</p>
(gemini-pro)</td>
<td><p>Pros: The spa provides a tranquil and relaxing atmosphere with high-quality services. Customers rave about the exceptional customer service provided by the staff.</p>
<p>Cons: The spa's no-cellphone policy is a point of contention, with some finding it added to their relaxation and others finding it stressful. Several reviewers found the prices to be high.</p>
(gemini-pro)</td>
</tr>
</tbody>
</table>

### Style and tone

You can influence a model's response by defining its output style and tone, such as verbosity, formality, and target reading level, in system instructions.

For example, suppose you want to use a model to write proposals for government initiatives. Compare the difference in the model's responses when you define the following tones:

- Professional
- Casual

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>System instructions</th>
<th>Professional</th>
<th>Casual</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th><p>You are a government proposal writer. You are tasked with producing proposals for future campaigns. Based on the template and user input, provide a proposal for the upcoming campaign.</p>
<ul>
<li>Do not use the internet.</li>
<li>Keep answers for each section to no more than two sentences.</li>
<li><strong>Write in a professional tone.</strong></li>
<li>Provide answers in Markdown format.</li>
</ul>
<p>Proposal template:</p>
<ul>
<li>The Big Idea:</li>
<li>The Challenge</li>
<li>The Solution</li>
<li>Target Audience</li>
<li>Key Message</li>
<li>Channels</li>
<li>Content Highlights</li>
<li>Expected Results</li>
<li>Why Us</li>
<li>Call to Action</li>
</ul></th>
<td><p>You are a government proposal writer. You are tasked with producing proposals for future campaigns. Based on the template and user input, provide a proposal for the upcoming campaign.</p>
<ul>
<li>Do not use the internet.</li>
<li>Keep answers for each section to no more than two sentences.</li>
<li><strong>Write in a casual tone.</strong></li>
<li>Provide answers in Markdown format.</li>
</ul>
<p>Proposal template:</p>
<ul>
<li>The Big Idea:</li>
<li>The Challenge</li>
<li>The Solution</li>
<li>Target Audience</li>
<li>Key Message</li>
<li>Channels</li>
<li>Content Highlights</li>
<li>Expected Results</li>
<li>Why Us</li>
<li>Call to Action</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Prompt</th>
<td><p>The purpose of this campaign is to raise awareness and inspire actionable behavior changes towards sustainability through the use of interactive digital experiences. I will engage environmentally conscious individuals aged 20–45, including students, professionals, and families, by delivering educational content and organizing community-driven events across Facebook and X. My objective is to enhance public awareness and encourage measurable improvements in eco-friendly behaviors. Drawing on my expertise in digital marketing and a strong focus on sustainability, I will design a high-impact campaign that empowers individuals to make meaningful, sustainable changes in their daily lives. I want this campaign to create content that is varied and engaging yet informative.</p></td>
<td></td>
</tr>
<tr class="odd">
<th>Response</th>
<td><p>The Big Idea: Empowering individuals aged 20-45 to embrace sustainable living through interactive digital experiences and community engagement.</p>
<p>The Challenge: Many individuals lack awareness of practical, everyday actions they can take to promote environmental sustainability.</p>
<p>The Solution: A multi-platform campaign utilizing Facebook and X to deliver engaging, educational content and foster community involvement through interactive experiences and events.</p>
<p>Target Audience: Environmentally conscious individuals aged 20-45, including students, professionals, and families.</p>
<p>Key Message: Small changes in daily habits can have a significant positive impact on the environment.</p>
<p>Channels: Facebook and X.</p>
<p>Content Highlights: Interactive quizzes, educational videos, expert Q&amp;A sessions, and community challenges promoting sustainable practices.</p>
<p>Expected Results: Increased awareness of sustainable living practices and measurable improvements in eco-friendly behaviors within the target audience.</p>
<p>Why Us: Proven expertise in digital marketing and a passion for promoting sustainability, ensuring a high-impact, engaging campaign.</p>
<p>Call to Action: Join the campaign on Facebook and X to learn, engage, and make a difference for a sustainable future.</p>
(gemini-pro)</td>
<td><p>The Big Idea: We're launching a digital movement to make sustainability cool! Using interactive challenges and engaging content, we'll inspire real action, transforming eco-friendly living from a chore to a shared journey.</p>
<p>The Challenge: Let's face it, knowing about sustainability and actually acting on it are two different things. We're battling apathy and a lack of awareness around simple, everyday changes.</p>
<p>The Solution: We'll meet our audience where they are, on platforms like Facebook and X, to deliver a dynamic blend of educational content, fun challenges, and community-driven events. Think interactive quizzes, shareable infographics, and local meetups!</p>
<p>Target Audience: We're focusing on eco-conscious individuals aged 20-45 - students, professionals, and families - who are eager to make a difference.</p>
<p>Key Message: Small steps, big impact! You have the power to create a more sustainable future through simple, everyday choices.</p>
<p>Channels: We'll leverage the power of social media marketing through engaging campaigns on Facebook and X.</p>
<p>Content Highlights: Expect a mix of informative and shareable content, including eye-catching infographics, thought-provoking videos, quick tips, and inspiring success stories.</p>
<p>Expected Results: We'll measure success through increased engagement (likes, shares, comments) and website traffic, ultimately aiming for a measurable increase in eco-friendly behaviors within our target audience.</p>
<p>Why Us: Our team combines digital marketing expertise with a genuine passion for sustainability, resulting in a campaign that's both impactful and engaging.</p>
<p>Call to Action: Join the movement! Follow our page, participate in our challenges, and share your sustainable living journey with your network.</p>
(gemini-pro)</td>
</tr>
</tbody>
</table>

### Goals and rules

You can influence a model's response by defining goals or rules, in other words, what the model should or shouldn't do, in system instructions.

For example, suppose you want to use a model to write Python code. Compare the difference in the model's responses when you define the following rules:

- When generating code, make sure to include docstrings explaining the inputs, outputs, and usage of every method.
- Only generate code, do not include any docstrings.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>System instructions</th>
<th>Docstrings</th>
<th>No docstrings</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th>When generating code, make sure to include docstrings explaining the inputs, outputs, and usage of every method.</th>
<td>Only generate code, do not include any docstring.</td>
<td></td>
</tr>
<tr class="even">
<th>Prompt</th>
<td>Create a 2d array in Python, and create an A* pathfinding algorithm to identify the shortest path between two points on the grid.</td>
<td></td>
</tr>
<tr class="odd">
<th>Response</th>
<td><pre class="python"><code>    import heapq

    class Node:
        &quot;&quot;&quot;&quot;&quot;&quot;
        Represents a node in the grid for A* pathfinding.

        Attributes:
            x (int): The x-coordinate of the node.
            y (int): The y-coordinate of the node.
            parent (Node, optional): The parent node in the path. Defaults to None.
            g (int): Cost from the start node to this node. Defaults to 0.
            h (int): Estimated cost from this node to the end node. Defaults to 0.
        &quot;&quot;&quot;&quot;&quot;&quot;

        def __init__(self, x, y, parent=None):
            self.x = x
            self.y = y
            self.parent = parent
            self.g = 0
            self.h = 0

        def __lt__(self, other):
            &quot;&quot;&quot;&quot;&quot;&quot;Compares nodes based on their f-score (g + h).&quot;&quot;&quot;&quot;&quot;&quot;
            return (self.g + self.h) &lt; (other.g + other.h)

    def a_star(grid, start, end):
        &quot;&quot;&quot;&quot;&quot;&quot;
        Implements the A* pathfinding algorithm.

        Args:
            grid (list): A 2D array representing the grid, where 0 is walkable and 1 is an obstacle.
            start (tuple): The starting point coordinates (x, y).
            end (tuple): The end point coordinates (x, y).

        Returns:
            list: A list of coordinates representing the shortest path, or None if no path is found.
        &quot;&quot;&quot;&quot;&quot;&quot;

        rows = len(grid)
        cols = len(grid[0])

        # Create start and end nodes
        start_node = Node(start[0], start[1])
        end_node = Node(end[0], end[1])

        # Initialize open and closed lists
        open_list = []
        closed_list = set()

        # Add the start node to the open list
        heapq.heappush(open_list, start_node)

        while open_list:
            # Get the node with the lowest f-score
            current_node = heapq.heappop(open_list)

            # Add the current node to the closed list
            closed_list.add((current_node.x, current_node.y))

            # Check if we&#39;ve reached the goal
            if current_node.x == end_node.x and current_node.y == end_node.y:
                # Reconstruct and return the path
                path = []
                while current_node:
                    path.append((current_node.x, current_node.y))
                    current_node = current_node.parent
                return path[::-1]  # Return reversed path

            # Explore neighboring nodes
            for dx, dy in [(0, -1), (0, 1), (-1, 0), (1, 0)]:  # Up, Down, Left, Right
                neighbor_x = current_node.x + dx
                neighbor_y = current_node.y + dy

                # Check if the neighbor is within the grid bounds
                if 0 &lt;= neighbor_x &lt; cols and 0 &lt;= neighbor_y &lt; rows:
                    # Check if the neighbor is walkable and not in the closed list
                    if grid[neighbor_y][neighbor_x] == 0 and (neighbor_x, neighbor_y) not in closed_list:
                        # Create a neighbor node
                        neighbor_node = Node(neighbor_x, neighbor_y, parent=current_node)

                        # Calculate the cost to reach the neighbor
                        neighbor_node.g = current_node.g + 1

                        # Calculate the heuristic (Manhattan distance)
                        neighbor_node.h = abs(neighbor_node.x - end_node.x) + abs(neighbor_node.y - end_node.y)

                        # Add the neighbor to the open list if it&#39;s a better path
                        if neighbor_node not in open_list:
                            heapq.heappush(open_list, neighbor_node)

        # No path found
        return None

    # Example usage:
    grid = [
        [0, 0, 0, 0, 0],
        [0, 1, 0, 1, 0],
        [0, 0, 0, 0, 0],
        [0, 1, 1, 1, 0],
        [0, 0, 0, 0, 0]
    ]

    start = (0, 0)
    end = (4, 4)

    path = a_star(grid, start, end)

    if path:
        print(&quot;&quot;Shortest path:&quot;&quot;, path)
    else:
        print(&quot;&quot;No path found.&quot;&quot;)
    </code></pre>
<p>Explanation:</p>
<ol>
<li>Node Class:
<ul>
<li>Represents a cell in the grid.</li>
<li>Stores coordinates ( <code>x</code> , <code>y</code> ), parent node, <code>g</code> (cost from start), and <code>h</code> (heuristic to end).</li>
<li><code>__lt__</code> allows comparing nodes for priority queue (using <code>heapq</code> ) based on <code>f = g + h</code> .</li>
</ul></li>
<li>a_star Function:
<ul>
<li>Takes the <code>grid</code> , <code>start</code> , and <code>end</code> points as input.</li>
<li>Initializes <code>open_list</code> (nodes to explore) and <code>closed_list</code> (explored nodes).</li>
<li>Uses <code>heapq</code> for efficient retrieval of the node with the lowest <code>f</code> score from the <code>open_list</code> .</li>
<li>Loops until the <code>end</code> is found or the <code>open_list</code> is empty (no path).</li>
<li>Explores neighbors, calculates costs ( <code>g</code> , <code>h</code> ), and updates the <code>open_list</code> .</li>
<li>Reconstructs and returns the path when the <code>end</code> is reached.</li>
</ul></li>
<li>Example Usage:
<ul>
<li>Creates a sample <code>grid</code> and defines <code>start</code> and <code>end</code> points.</li>
<li>Calls <code>a_star</code> to find the path.</li>
<li>Prints the shortest path or indicates if no path exists.</li>
</ul></li>
</ol>
(gemini-pro)</td>
<td><pre class="python"><code>    import heapq

    class Node:
        def __init__(self, position, parent=None):
            self.position = position
            self.parent = parent
            self.g = 0
            self.h = 0
            self.f = 0

        def __lt__(self, other):
            return self.f &lt; other.f

    def astar(grid, start, end):
        rows = len(grid)
        cols = len(grid[0])

        open_list = []
        closed_list = set()

        start_node = Node(start)
        end_node = Node(end)

        open_list.append(start_node)

        while open_list:
            current_node = heapq.heappop(open_list)

            if current_node.position == end_node.position:
                path = []
                while current_node:
                    path.append(current_node.position)
                    current_node = current_node.parent
                return path[::-1]

            closed_list.add(current_node.position)

            for neighbor in get_neighbors(grid, current_node):
                if neighbor.position in closed_list:
                    continue

                if neighbor not in open_list:
                    neighbor.g = current_node.g + 1
                    neighbor.h = manhattan_distance(neighbor.position, end_node.position)
                    neighbor.f = neighbor.g + neighbor.h
                    neighbor.parent = current_node
                    heapq.heappush(open_list, neighbor)
                else:
                    if neighbor.g &gt; current_node.g + 1:
                        neighbor.g = current_node.g + 1
                        neighbor.f = neighbor.g + neighbor.h
                        neighbor.parent = current_node
                        heapq.heapify(open_list)

        return None  # No path found

    def get_neighbors(grid, node):
        rows = len(grid)
        cols = len(grid[0])
        row, col = node.position
        neighbors = []
        if row &gt; 0 and grid[row - 1][col] == 0:
            neighbors.append(Node((row - 1, col)))
        if row &lt; rows - 1 and grid[row + 1][col] == 0:
            neighbors.append(Node((row + 1, col)))
        if col &gt; 0 and grid[row][col - 1] == 0:
            neighbors.append(Node((row, col - 1)))
        if col &lt; cols - 1 and grid[row][col + 1] == 0:
            neighbors.append(Node((row, col + 1)))
        return neighbors

    def manhattan_distance(a, b):
        return abs(a[0] - b[0]) + abs(a[1] - b[1])

    # Example usage
    grid = [
        [0, 0, 0, 0, 0],
        [0, 1, 1, 1, 0],
        [0, 0, 0, 0, 0],
        [0, 1, 1, 1, 0],
        [0, 0, 0, 0, 0],
    ]

    start = (0, 0)
    end = (4, 4)

    path = astar(grid, start, end)
    print(path)
    </code></pre>
(gemini-pro)</td>
</tr>
</tbody>
</table>

### Context

You can influence how a model responds to prompts by adding additional context in system instructions.

For example, suppose you want to use a model to write speeches for events. Compare the difference in the model's responses when you provide the following context:

- Things to include in the speech.
- No extra context.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>System instructions</th>
<th>Things to include in the speech</th>
<th>No extra context</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th><p>Help the user write a speech based on the information provided:</p>
<ul>
<li>Event</li>
<li>Audience Size</li>
<li>Speaker Information (name, age, etc.)</li>
<li>Speech Tone</li>
<li>Speech Length</li>
<li>Miscellaneous</li>
</ul>
<p>If the user does not provide all of this information, please respond with, "I'm sorry, but I do not have all of the necessary information to create a speech. Please provide the event, audience size, speaker information, tone, length, and any miscellaneous information."</p>
<strong></strong>
<p>Some general things to include are:</p>
<ul>
<li>Breaks for pause</li>
<li>An intriguing hook</li>
<li>A closing remark to keep the speech memorable</li>
<li>A joke</li>
</ul></th>
<td><p>Help the user write a speech based on the information provided:</p>
<ul>
<li>Event</li>
<li>Audience Size</li>
<li>Speaker Information (name, age, etc.)</li>
<li>Speech Tone</li>
<li>Speech Length</li>
<li>Miscellaneous</li>
</ul>
<p>If the user does not provide all of this information, please respond with, "I'm sorry, but I do not have all of the necessary information to create a speech. Please provide the event, audience size, speaker information, tone, length, and any miscellaneous information."</p></td>
<td></td>
</tr>
<tr class="even">
<th>Prompt</th>
<td><p>Event: High School Graduation</p>
<p>Audience Size: 1,000 people</p>
<p>Speaker Info: Michael Landish, 17 years old</p>
<p>Tone: nostalgic, optimistic</p>
<p>Speech Length: 250-500 words</p>
<p>Miscellaneous: Michael was the senior class president, his favorite teacher was his junior year English teacher, Mrs. Martin, and he will be going to Los Caminos State University to study economics and English. He has never given a speech before, and he is nervous due to his dyslexia.</p></td>
<td></td>
</tr>
<tr class="odd">
<th>Response</th>
<td><p>"Good morning faculty, family, friends, and most importantly, fellow graduates of the class of 2023!</p>
<p>(Pause)</p>
<p>Standing here, looking out at all of you, it feels surreal. Just yesterday, we were freshmen, wide-eyed and a little terrified. Remember those first day jitters? I know I do. I almost tripped and fell carrying my history textbook – a near disaster that would have been immortalised in the halls of [High School Name] history!</p>
<p>(Pause for laughter)</p>
<p>But seriously, look at us now! We've grown up, learned a lot – and I'm not just talking about the Pythagorean Theorem. We've learned about perseverance, about friendship, and about the power of a well-placed sticky note during exam week.</p>
<p>These past four years have been amazing, and I owe a lot of my own growth to some truly exceptional teachers. I'd especially like to thank Mrs. Martin, my junior year English teacher, who taught me that words have power, and that even with dyslexia, I can find my voice. Thank you, Mrs. Martin.</p>
<p>(Pause)</p>
<p>Now, we're standing on the edge of something new and exciting. As we head off to different colleges, different cities, even different countries, let's carry the lessons we've learned at [High School Name] with us. Let's remember the laughter, the friendships, and even the occasional all-nighter before a big test.</p>
<p>(Pause)</p>
<p>Graduates, the world is waiting for us. Let's face it head-on, with courage, with optimism, and with the unwavering support of the amazing Class of 2023 behind us. Congratulations everyone, and remember – the best is yet to come!</p>
(gemini-pro)</td>
<td><p>"Good morning, faculty, family, friends, and most importantly, my fellow graduates of the Class of [Year]!</p>
<p>It feels strange standing here before you, not just as Michael Landish, but as your class president. For the last four years, these hallways have been our proving grounds, filled with laughter, late-night study sessions (some more successful than others), and enough shared memories to last a lifetime. We've grown up together within these walls, and now, as we stand on the precipice of something new and unknown, it's hard not to feel a little overwhelmed.</p>
<p>Thinking back, it seems like yesterday we were awkward freshmen, navigating crowded hallways and trying to figure out where we fit in. And now, looking out at all of you, I'm struck by how far we've come. We've cheered each other on in victory and offered support during setbacks. We've learned from our mistakes, celebrated our triumphs, and most importantly, formed bonds of friendship that I know will last a lifetime.</p>
<p>I'd like to especially thank Mrs. Martin, my junior year English teacher, for her patience and guidance. Your belief in me, especially when I struggled, helped me find my voice not just as a student, but as a person. Thank you.</p>
<p>Now, we embark on our next chapter. Some, like myself, will be heading to Los Caminos State University, eager to delve into the worlds of economics and, yes, even more English. Others will pursue different paths, equally valid and exciting. Though our journeys may diverge, let us always remember the lessons we've learned and the friendships we've forged within these walls. Let's carry the spirit of the Class of [Year] with us – the spirit of resilience, determination, and unwavering support for one another.</p>
<p>Congratulations to the graduating class! I can't wait to see what amazing things we accomplish.</p>
(gemini-pro)</td>
</tr>
</tbody>
</table>

## What's next

- Learn how to [use system instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instructions)
