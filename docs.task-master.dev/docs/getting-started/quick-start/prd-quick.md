---
source_url: https://docs.task-master.dev/docs/getting-started/quick-start/prd-quick
title: PRD Creation and Parsing - Task Master
crawl_date: 2025-08-07T10:57:02.448061
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Quick Start

PRD Creation and Parsing

[Task Master Documentation](/docs/introduction)

* [Github](https://github.com/eyaltoledano/claude-task-master)
* [Discord](https://discord.gg/fWJkU7rf)

##### Welcome

  * [Introduction](/docs/introduction)



##### Getting Started

  * Quick Start

    * [Quick Start](/docs/getting-started/quick-start/quick-start)
    * [Requirements](/docs/getting-started/quick-start/requirements)
    * [Installation](/docs/getting-started/quick-start/installation)
    * [Configuration](/docs/getting-started/quick-start/configuration-quick)
    * [PRD Creation and Parsing](/docs/getting-started/quick-start/prd-quick)
    * [Tasks Setup](/docs/getting-started/quick-start/tasks-quick)
    * [Executing Tasks](/docs/getting-started/quick-start/execute-quick)
  * [FAQ](/docs/getting-started/faq)
  * [Contribute](/docs/getting-started/contribute)



##### Best Practices

  * [Advanced Usage](/docs/best-practices)
  * [Advanced Configuration](/docs/best-practices/configuration-advanced)
  * [Advanced Tasks](/docs/best-practices/advanced-tasks)



##### Technical Capabilities

  * [MCP Tools](/docs/capabilities/mcp)
  * [CLI Commands](/docs/capabilities/cli-root-commands)
  * [Task Structure](/docs/capabilities/task-structure)



On this page

  * Writing a PRD
  * What Makes a Good PRD?
  * Writing a PRD for Task Master
  * Where to Save Your PRD
  * Parse your PRD into Tasks



Quick Start

# PRD Creation and Parsing

# 

​

Writing a PRD

A PRD (Product Requirements Document) is the starting point of every task flow in Task Master. It defines what you’re building and why. A clear PRD dramatically improves the quality of your tasks, your model outputs, and your final product — so it’s worth taking the time to get it right.

You don’t need to define your whole app up front. You can write a focused PRD just for the next feature or module you’re working on.

You can start with an empty project or you can start with a feature PRD on an existing project.

You can add and parse multiple PRDs per project using the —append flag

## 

​

What Makes a Good PRD?

  * Clear objective — what’s the outcome or feature?
  * Context — what’s already in place or assumed?
  * Constraints — what limits or requirements need to be respected?
  * Reasoning — why are you building it this way?

The more context you give the model, the better the breakdown and results.

* * *

## 

​

Writing a PRD for Task Master

An example PRD can be found in .taskmaster/templates/example_prd.txt

You can co-write your PRD with an LLM model using the following workflow:

  1. **Chat about requirements** — explain what you want to build.
  2. **Show an example PRD** — share the example PRD so the model understands the expected format. The example uses formatting that work well with Task Master’s code. Following the example will yield better results.
  3. **Iterate and refine** — work with the model to shape the draft into a clear and well-structured PRD.

This approach works great in Cursor, or anywhere you use a chat-based LLM.

* * *

## 

​

Where to Save Your PRD

Place your PRD file in the `.taskmaster/docs` folder in your project.

  * You can have **multiple PRDs** per project.
  * Name your PRDs clearly so they’re easy to reference later.
    * Examples: `dashboard_redesign.txt`, `user_onboarding.txt`



* * *

# 

​

Parse your PRD into Tasks

This is where the Task Master magic begins. In Cursor’s AI chat, instruct the agent to generate tasks from your PRD:

Copy

Ask AI
    
    
    Please use the task-master parse-prd command to generate tasks from my PRD. The PRD is located at .taskmaster/docs/<prd-name>.txt.
    

The agent will execute the following command which you can alternatively paste into the CLI:

Copy

Ask AI
    
    
    task-master parse-prd .taskmaster/docs/<prd-name>.txt
    

This will:

  * Parse your PRD document
  * Generate a structured `tasks.json` file with tasks, dependencies, priorities, and test strategies

Now that you have written and parsed a PRD, you are ready to start setting up your tasks.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/getting-started/quick-start/prd-quick.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/getting-started/quick-start/prd-quick)

[Configuration](/docs/getting-started/quick-start/configuration-quick)[Tasks Setup](/docs/getting-started/quick-start/tasks-quick)

Assistant

Responses are generated using AI and may contain mistakes.