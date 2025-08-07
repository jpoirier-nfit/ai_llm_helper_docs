---
source_url: https://docs.task-master.dev/docs/getting-started/quick-start/execute-quick#review-and-test
title: Executing Tasks - Task Master
crawl_date: 2025-08-07T10:57:02.901778
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Quick Start

Executing Tasks

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

  * Select the Task to Work on: Next Task
  * Discuss Task
  * Agent Task execution
  * Review and Test
  * Update Task Status
  * Rules and Context
  * On to the Next Task!



Quick Start

# Executing Tasks

Now that your tasks are generated and reviewed you are ready to begin executing.

## 

​

Select the Task to Work on: Next Task

Task Master has the “next” command to find the next task to work on. You can access it with the following request:

Copy

Ask AI
    
    
    What's the next task I should work on? Please consider dependencies and priorities.
    

Alternatively you can use the CLI to show the next task

Copy

Ask AI
    
    
    task-master next
    

## 

​

Discuss Task

When you know what task to work on next you can then start chatting with the agent to make sure it understands the plan of action. You can tag relevant files and folders so it knows what context to pull up as it generates its plan. For example:

Copy

Ask AI
    
    
    Please review Task 5 and confirm you understand how to execute before beginning. Refer to @models @api and @schema 
    

The agent will begin analyzing the task and files and respond with the steps to complete the task.

## 

​

Agent Task execution

If you agree with the plan of action, tell the agent to get started.

Copy

Ask AI
    
    
    You may begin. I believe in you.
    

## 

​

Review and Test

Once the agent is finished with the task you can refer to the task testing strategy to make sure it was completed correctly.

## 

​

Update Task Status

If the task was completed correctly you can update the status to done

Copy

Ask AI
    
    
    Please mark Task 5 as done
    

The agent will execute

Copy

Ask AI
    
    
    task-master set-status --id=5 --status=done
    

## 

​

Rules and Context

If you ran into problems and had to debug errors you can create new rules as you go. This helps build context on your codebase that helps the creation and execution of future tasks.

## 

​

On to the Next Task!

By now you have all you need to get started executing code faster and smarter with Task Master. If you have any questions please check out [Frequently Asked Questions](/docs/getting-started/faq)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/getting-started/quick-start/execute-quick.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/getting-started/quick-start/execute-quick)

[Tasks Setup](/docs/getting-started/quick-start/tasks-quick)[FAQ](/docs/getting-started/faq)

Assistant

Responses are generated using AI and may contain mistakes.