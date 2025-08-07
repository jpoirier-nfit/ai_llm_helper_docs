---
source_url: https://docs.task-master.dev/docs/best-practices/advanced-tasks#8-breaking-down-complex-tasks
title: Advanced Tasks - Task Master
crawl_date: 2025-08-07T10:57:01.922273
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Best Practices

Advanced Tasks

[Task Master Documentation](/docs/introduction)

* [Github](https://github.com/eyaltoledano/claude-task-master)
* [Discord](https://discord.gg/fWJkU7rf)

##### Welcome

  * [Introduction](/docs/introduction)



##### Getting Started

  * Quick Start

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

  * AI-Driven Development Workflow
  * 1\. Task Discovery and Selection
  * 2\. Task Implementation
  * 2.1. Viewing Multiple Tasks
  * 3\. Task Verification
  * 4\. Task Completion
  * 5\. Handling Implementation Drift
  * 6\. Reorganizing Tasks
  * 7\. Resolving Merge Conflicts with Tasks
  * 8\. Breaking Down Complex Tasks



Best Practices

# Advanced Tasks

## 

​

AI-Driven Development Workflow

The Cursor agent is pre-configured (via the rules file) to follow this workflow:

### 

​

1\. Task Discovery and Selection

Ask the agent to list available tasks:

Copy

Ask AI
    
    
    What tasks are available to work on next?
    

Copy

Ask AI
    
    
    Can you show me tasks 1, 3, and 5 to understand their current status?
    

The agent will:

  * Run `task-master list` to see all tasks
  * Run `task-master next` to determine the next task to work on
  * Run `task-master show 1,3,5` to display multiple tasks with interactive options
  * Analyze dependencies to determine which tasks are ready to be worked on
  * Prioritize tasks based on priority level and ID order
  * Suggest the next task(s) to implement



### 

​

2\. Task Implementation

When implementing a task, the agent will:

  * Reference the task’s details section for implementation specifics
  * Consider dependencies on previous tasks
  * Follow the project’s coding standards
  * Create appropriate tests based on the task’s testStrategy

You can ask:

Copy

Ask AI
    
    
    Let's implement task 3. What does it involve?
    

### 

​

2.1. Viewing Multiple Tasks

For efficient context gathering and batch operations:

Copy

Ask AI
    
    
    Show me tasks 5, 7, and 9 so I can plan my implementation approach.
    

The agent will:

  * Run `task-master show 5,7,9` to display a compact summary table
  * Show task status, priority, and progress indicators
  * Provide an interactive action menu with batch operations
  * Allow you to perform group actions like marking multiple tasks as in-progress



### 

​

3\. Task Verification

Before marking a task as complete, verify it according to:

  * The task’s specified testStrategy
  * Any automated tests in the codebase
  * Manual verification if required



### 

​

4\. Task Completion

When a task is completed, tell the agent:

Copy

Ask AI
    
    
    Task 3 is now complete. Please update its status.
    

The agent will execute:

Copy

Ask AI
    
    
    task-master set-status --id=3 --status=done
    

### 

​

5\. Handling Implementation Drift

If during implementation, you discover that:

  * The current approach differs significantly from what was planned
  * Future tasks need to be modified due to current implementation choices
  * New dependencies or requirements have emerged

Tell the agent:

Copy

Ask AI
    
    
    We've decided to use MongoDB instead of PostgreSQL. Can you update all future tasks (from ID 4) to reflect this change?
    

The agent will execute:

Copy

Ask AI
    
    
    task-master update --from=4 --prompt="Now we are using MongoDB instead of PostgreSQL."
    
    # OR, if research is needed to find best practices for MongoDB:
    task-master update --from=4 --prompt="Update to use MongoDB, researching best practices" --research
    

This will rewrite or re-scope subsequent tasks in tasks.json while preserving completed work.

### 

​

6\. Reorganizing Tasks

If you need to reorganize your task structure:

Copy

Ask AI
    
    
    I think subtask 5.2 would fit better as part of task 7 instead. Can you move it there?
    

The agent will execute:

Copy

Ask AI
    
    
    task-master move --from=5.2 --to=7.3
    

You can reorganize tasks in various ways:

  * Moving a standalone task to become a subtask: `--from=5 --to=7`
  * Moving a subtask to become a standalone task: `--from=5.2 --to=7`
  * Moving a subtask to a different parent: `--from=5.2 --to=7.3`
  * Reordering subtasks within the same parent: `--from=5.2 --to=5.4`
  * Moving a task to a new ID position: `--from=5 --to=25` (even if task 25 doesn’t exist yet)
  * Moving multiple tasks at once: `--from=10,11,12 --to=16,17,18` (must have same number of IDs, Taskmaster will look through each position)

When moving tasks to new IDs:

  * The system automatically creates placeholder tasks for non-existent destination IDs
  * This prevents accidental data loss during reorganization
  * Any tasks that depend on moved tasks will have their dependencies updated
  * When moving a parent task, all its subtasks are automatically moved with it and renumbered

This is particularly useful as your project understanding evolves and you need to refine your task structure.

### 

​

7\. Resolving Merge Conflicts with Tasks

When working with a team, you might encounter merge conflicts in your tasks.json file if multiple team members create tasks on different branches. The move command makes resolving these conflicts straightforward:

Copy

Ask AI
    
    
    I just merged the main branch and there's a conflict with tasks.json. My teammates created tasks 10-15 while I created tasks 10-12 on my branch. Can you help me resolve this?
    

The agent will help you:

  1. Keep your teammates’ tasks (10-15)
  2. Move your tasks to new positions to avoid conflicts:



Copy

Ask AI
    
    
    # Move your tasks to new positions (e.g., 16-18)
    task-master move --from=10 --to=16
    task-master move --from=11 --to=17
    task-master move --from=12 --to=18
    

This approach preserves everyone’s work while maintaining a clean task structure, making it much easier to handle task conflicts than trying to manually merge JSON files.

### 

​

8\. Breaking Down Complex Tasks

For complex tasks that need more granularity:

Copy

Ask AI
    
    
    Task 5 seems complex. Can you break it down into subtasks?
    

The agent will execute:

Copy

Ask AI
    
    
    task-master expand --id=5 --num=3
    

You can provide additional context:

Copy

Ask AI
    
    
    Please break down task 5 with a focus on security considerations.
    

The agent will execute:

Copy

Ask AI
    
    
    task-master expand --id=5 --prompt="Focus on security aspects"
    

You can also expand all pending tasks:

Copy

Ask AI
    
    
    Please break down all pending tasks into subtasks.
    

The agent will execute:

Copy

Ask AI
    
    
    task-master expand --all
    

For research-backed subtask generation using the configured research model:

Copy

Ask AI
    
    
    Please break down task 5 using research-backed generation.
    

The agent will execute:

Copy

Ask AI
    
    
    task-master expand --id=5 --research
    

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/best-practices/advanced-tasks.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/best-practices/advanced-tasks)

[Advanced Configuration](/docs/best-practices/configuration-advanced)[MCP Tools](/docs/capabilities/mcp)

Assistant

Responses are generated using AI and may contain mistakes.