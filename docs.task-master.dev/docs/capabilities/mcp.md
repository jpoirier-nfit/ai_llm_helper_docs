---
source_url: https://docs.task-master.dev/docs/capabilities/mcp#6-tag-management
title: MCP Tools - Task Master
crawl_date: 2025-08-07T10:57:02.159377
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Technical Capabilities

MCP Tools

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

  * MCP Tools
  * Core Concepts
  * Tool Categories
  * 1\. Task and Subtask Management
  * 2\. Task Information and Status
  * 3\. Task Analysis and Expansion
  * 4\. Dependency Management
  * 5\. Project and Configuration
  * 6\. Tag Management



Technical Capabilities

# MCP Tools

# 

​

MCP Tools

This document provides an overview of the MCP (Machine-to-Machine Communication Protocol) interface for the Task Master application. The MCP interface is defined in the `mcp-server/` directory and exposes the application’s core functionalities as a set of tools that can be called remotely.

## 

​

Core Concepts

The MCP interface is built on top of the `fastmcp` library and registers a set of tools that correspond to the core functionalities of the Task Master application. These tools are defined in the `mcp-server/src/tools/` directory and are registered with the MCP server in `mcp-server/src/tools/index.js`. Each tool is defined with a name, a description, and a set of parameters that are validated using the `zod` library. The `execute` function of each tool calls the corresponding core logic function from `scripts/modules/task-manager.js`.

## 

​

Tool Categories

The MCP tools can be categorized in the same way as the core functionalities:

### 

​

1\. Task and Subtask Management

  * **`add_task`** : Creates a new task.
  * **`add_subtask`** : Adds a subtask to a parent task.
  * **`remove_task`** : Removes one or more tasks or subtasks.
  * **`remove_subtask`** : Removes a subtask from its parent.
  * **`update_task`** : Updates a single task.
  * **`update_subtask`** : Appends information to a subtask.
  * **`update`** : Updates multiple tasks.
  * **`move_task`** : Moves a task or subtask.
  * **`clear_subtasks`** : Clears all subtasks from one or more tasks.



### 

​

2\. Task Information and Status

  * **`get_tasks`** : Lists all tasks.
  * **`get_task`** : Shows the details of a specific task.
  * **`next_task`** : Shows the next task to work on.
  * **`set_task_status`** : Sets the status of a task or subtask.



### 

​

3\. Task Analysis and Expansion

  * **`parse_prd`** : Parses a PRD to generate tasks.
  * **`expand_task`** : Expands a task into subtasks.
  * **`expand_all`** : Expands all eligible tasks.
  * **`analyze_project_complexity`** : Analyzes task complexity.
  * **`complexity_report`** : Displays the complexity analysis report.



### 

​

4\. Dependency Management

  * **`add_dependency`** : Adds a dependency to a task.
  * **`remove_dependency`** : Removes a dependency from a task.
  * **`validate_dependencies`** : Validates the dependencies of all tasks.
  * **`fix_dependencies`** : Fixes any invalid dependencies.



### 

​

5\. Project and Configuration

  * **`initialize_project`** : Initializes a new project.
  * **`generate`** : Generates individual task files.
  * **`models`** : Manages AI model configurations.
  * **`research`** : Performs AI-powered research.



### 

​

6\. Tag Management

  * **`add_tag`** : Creates a new tag.
  * **`delete_tag`** : Deletes a tag.
  * **`list_tags`** : Lists all tags.
  * **`use_tag`** : Switches to a different tag.
  * **`rename_tag`** : Renames a tag.
  * **`copy_tag`** : Copies a tag.



Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/capabilities/mcp.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/capabilities/mcp)

[Advanced Tasks](/docs/best-practices/advanced-tasks)[CLI Commands](/docs/capabilities/cli-root-commands)

Assistant

Responses are generated using AI and may contain mistakes.