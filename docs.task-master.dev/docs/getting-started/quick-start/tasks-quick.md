---
source_url: https://docs.task-master.dev/docs/getting-started/quick-start/tasks-quick
title: Tasks Setup - Task Master
crawl_date: 2025-08-07T10:57:02.483179
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Quick Start

Tasks Setup

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

  * Expand Tasks
  * List/Show Tasks
  * Update Tasks
  * Analyze complexity



Quick Start

# Tasks Setup

Now that your tasks are generated you can review the plan and prepare for execution.

Not all of the setup steps are required but they are recommended in order to ensure your coding agents work on accurate tasks.

## 

​

Expand Tasks

Used to add detail to tasks and create subtasks. We recommend expanding all tasks using the MCP request below:

Copy

Ask AI
    
    
    Expand all tasks into subtasks.
    

The agent will execute

Copy

Ask AI
    
    
    task-master expand --all
    

## 

​

List/Show Tasks

Used to view task details. It is important to review the plan and ensure it makes sense in your project. Check for correct folder structures, dependencies, out of scope subtasks, etc. To see a list of tasks and descriptions use the following command:

Copy

Ask AI
    
    
    List all pending tasks so I can review.
    

To see all tasks in the CLI you can use:

Copy

Ask AI
    
    
    task-master list
    

To see all implementation details of an individual task, including subtasks and testing strategy, you can use Show Task:

Copy

Ask AI
    
    
    Show task 2 so I can review.
    

Copy

Ask AI
    
    
    task-master show --id=<##>
    

## 

​

Update Tasks

If the task details need to be edited you can update the task using this request:

Copy

Ask AI
    
    
    Update Task 2 to use Postgres instead of MongoDB and remove the sharding subtask
    

Or this CLI command:

Copy

Ask AI
    
    
    task-master update-task --id=2 --prompt="use Postgres instead of MongoDB and remove the sharding subtask"
    

## 

​

Analyze complexity

Task Master can provide a complexity report which can be helpful to read before you begin. If you didn’t already expand all your tasks, it could help identify which could be broken down further with subtasks.

Copy

Ask AI
    
    
    Can you analyze the complexity of our tasks to help me understand which ones need to be broken down further?
    

You can view the report in a friendly table using:

Copy

Ask AI
    
    
    Can you show me the complexity report in a more readable format?
    

Now you are ready to begin [executing tasks](/docs/getting-started/quick-start/execute-quick)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/getting-started/quick-start/tasks-quick.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/getting-started/quick-start/tasks-quick)

[PRD Creation and Parsing](/docs/getting-started/quick-start/prd-quick)[Executing Tasks](/docs/getting-started/quick-start/execute-quick)

Assistant

Responses are generated using AI and may contain mistakes.