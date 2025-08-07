---
source_url: https://docs.task-master.dev/docs/capabilities/cli-root-commands
title: CLI Commands - Task Master
crawl_date: 2025-08-07T10:56:56.804057
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Technical Capabilities

CLI Commands

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



Technical Capabilities

# CLI Commands

Parse PRD

Copy

Ask AI
    
    
    # Parse a PRD file and generate tasks
    task-master parse-prd <prd-file.txt>
    
    # Limit the number of tasks generated
    task-master parse-prd <prd-file.txt> --num-tasks=10
    

List Tasks

Copy

Ask AI
    
    
    # List all tasks
    task-master list
    
    # List tasks with a specific status
    task-master list --status=<status>
    
    # List tasks with subtasks
    task-master list --with-subtasks
    
    # List tasks with a specific status and include subtasks
    task-master list --status=<status> --with-subtasks
    

Show Next Task

Copy

Ask AI
    
    
    # Show the next task to work on based on dependencies and status
    task-master next
    

Show Specific Task

Copy

Ask AI
    
    
    # Show details of a specific task
    task-master show <id>
    # or
    task-master show --id=<id>
    
    # View a specific subtask (e.g., subtask 2 of task 1)
    task-master show 1.2
    

Update Tasks

Copy

Ask AI
    
    
    # Update tasks from a specific ID and provide context
    task-master update --from=<id> --prompt="<prompt>"
    

Update a Specific Task

Copy

Ask AI
    
    
    # Update a single task by ID with new information
    task-master update-task --id=<id> --prompt="<prompt>"
    
    # Use research-backed updates with Perplexity AI
    task-master update-task --id=<id> --prompt="<prompt>" --research
    

Update a Subtask

Copy

Ask AI
    
    
    # Append additional information to a specific subtask
    task-master update-subtask --id=<parentId.subtaskId> --prompt="<prompt>"
    
    # Example: Add details about API rate limiting to subtask 2 of task 5
    task-master update-subtask --id=5.2 --prompt="Add rate limiting of 100 requests per minute"
    
    # Use research-backed updates with Perplexity AI
    task-master update-subtask --id=<parentId.subtaskId> --prompt="<prompt>" --research
    

Unlike the `update-task` command which replaces task information, the `update-subtask` command _appends_ new information to the existing subtask details, marking it with a timestamp. This is useful for iteratively enhancing subtasks while preserving the original content.

Generate Task Files

Copy

Ask AI
    
    
    # Generate individual task files from tasks.json
    task-master generate
    

Set Task Status

Copy

Ask AI
    
    
    # Set status of a single task
    task-master set-status --id=<id> --status=<status>
    
    # Set status for multiple tasks
    task-master set-status --id=1,2,3 --status=<status>
    
    # Set status for subtasks
    task-master set-status --id=1.1,1.2 --status=<status>
    

When marking a task as “done”, all of its subtasks will automatically be marked as “done” as well.

Expand Tasks

Copy

Ask AI
    
    
    # Expand a specific task with subtasks
    task-master expand --id=<id> --num=<number>
    
    # Expand with additional context
    task-master expand --id=<id> --prompt="<context>"
    
    # Expand all pending tasks
    task-master expand --all
    
    # Force regeneration of subtasks for tasks that already have them
    task-master expand --all --force
    
    # Research-backed subtask generation for a specific task
    task-master expand --id=<id> --research
    
    # Research-backed generation for all tasks
    task-master expand --all --research
    

Clear Subtasks

Copy

Ask AI
    
    
    # Clear subtasks from a specific task
    task-master clear-subtasks --id=<id>
    
    # Clear subtasks from multiple tasks
    task-master clear-subtasks --id=1,2,3
    
    # Clear subtasks from all tasks
    task-master clear-subtasks --all
    

Analyze Task Complexity

Copy

Ask AI
    
    
    # Analyze complexity of all tasks
    task-master analyze-complexity
    
    # Save report to a custom location
    task-master analyze-complexity --output=my-report.json
    
    # Use a specific LLM model
    task-master analyze-complexity --model=claude-3-opus-20240229
    
    # Set a custom complexity threshold (1-10)
    task-master analyze-complexity --threshold=6
    
    # Use an alternative tasks file
    task-master analyze-complexity --file=custom-tasks.json
    
    # Use Perplexity AI for research-backed complexity analysis
    task-master analyze-complexity --research
    

View Complexity Report

Copy

Ask AI
    
    
    # Display the task complexity analysis report
    task-master complexity-report
    
    # View a report at a custom location
    task-master complexity-report --file=my-report.json
    

Managing Task Dependencies

Copy

Ask AI
    
    
    # Add a dependency to a task
    task-master add-dependency --id=<id> --depends-on=<id>
    
    # Remove a dependency from a task
    task-master remove-dependency --id=<id> --depends-on=<id>
    
    # Validate dependencies without fixing them
    task-master validate-dependencies
    
    # Find and fix invalid dependencies automatically
    task-master fix-dependencies
    

Add a New Task

Copy

Ask AI
    
    
    # Add a new task using AI
    task-master add-task --prompt="Description of the new task"
    
    # Add a task with dependencies
    task-master add-task --prompt="Description" --dependencies=1,2,3
    
    # Add a task with priority
    task-master add-task --prompt="Description" --priority=high
    

Initialize a Project

Copy

Ask AI
    
    
    # Initialize a new project with Task Master structure
    task-master init
    

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/capabilities/cli-root-commands.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/capabilities/cli-root-commands)

[MCP Tools](/docs/capabilities/mcp)[Task Structure](/docs/capabilities/task-structure)

Assistant

Responses are generated using AI and may contain mistakes.