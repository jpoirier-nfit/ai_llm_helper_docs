---
source_url: https://docs.task-master.dev/docs/capabilities/task-structure#best-practices-for-ai-driven-development
title: Task Structure - Task Master
crawl_date: 2025-08-07T10:57:02.311858
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Technical Capabilities

Task Structure

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

  * Task Fields in tasks.json
  * Task File Format
  * Features in Detail
  * Best Practices for AI-Driven Development



Technical Capabilities

# Task Structure

Tasks in Task Master follow a specific format designed to provide comprehensive information for both humans and AI assistants.

## 

​

Task Fields in tasks.json

Tasks in tasks.json have the following structure: Field| Description| Example  
---|---|---  
`id`| Unique identifier for the task.| `1`  
`title`| Brief, descriptive title.| `"Initialize Repo"`  
`description`| What the task involves.| `"Create a new repository, set up initial structure."`  
`status`| Current state.| `"pending"`, `"done"`, `"deferred"`  
`dependencies`| Prerequisite task IDs. ✅ Completed, ⏱️ Pending| `[1, 2]`  
`priority`| Task importance.| `"high"`, `"medium"`, `"low"`  
`details`| Implementation instructions.| `"Use GitHub client ID/secret, handle callback..."`  
`testStrategy`| How to verify success.| `"Deploy and confirm 'Hello World' response."`  
`subtasks`| Nested subtasks related to the main task.| `[{"id": 1, "title": "Configure OAuth", ...}]`  
  
## 

​

Task File Format

Individual task files follow this format:

Copy

Ask AI
    
    
    # Task ID: <id>
    # Title: <title>
    # Status: <status>
    # Dependencies: <comma-separated list of dependency IDs>
    # Priority: <priority>
    # Description: <brief description>
    # Details:
    <detailed implementation notes>
    
    # Test Strategy:
    <verification approach>
    

## 

​

Features in Detail

Analyzing Task Complexity

The `analyze-complexity` command:

  * Analyzes each task using AI to assess its complexity on a scale of 1-10
  * Recommends optimal number of subtasks based on configured DEFAULT_SUBTASKS
  * Generates tailored prompts for expanding each task
  * Creates a comprehensive JSON report with ready-to-use commands
  * Saves the report to scripts/task-complexity-report.json by default

The generated report contains:

  * Complexity analysis for each task (scored 1-10)
  * Recommended number of subtasks based on complexity
  * AI-generated expansion prompts customized for each task
  * Ready-to-run expansion commands directly within each task analysis



Viewing Complexity Report

The `complexity-report` command:

  * Displays a formatted, easy-to-read version of the complexity analysis report
  * Shows tasks organized by complexity score (highest to lowest)
  * Provides complexity distribution statistics (low, medium, high)
  * Highlights tasks recommended for expansion based on threshold score
  * Includes ready-to-use expansion commands for each complex task
  * If no report exists, offers to generate one on the spot



Smart Task Expansion

The `expand` command automatically checks for and uses the complexity report:When a complexity report exists:

  * Tasks are automatically expanded using the recommended subtask count and prompts
  * When expanding all tasks, they’re processed in order of complexity (highest first)
  * Research-backed generation is preserved from the complexity analysis
  * You can still override recommendations with explicit command-line options

Example workflow:

Copy

Ask AI
    
    
    # Generate the complexity analysis report with research capabilities
    task-master analyze-complexity --research
    
    # Review the report in a readable format
    task-master complexity-report
    
    # Expand tasks using the optimized recommendations
    task-master expand --id=8
    # or expand all tasks
    task-master expand --all
    

Finding the Next Task

The `next` command:

  * Identifies tasks that are pending/in-progress and have all dependencies satisfied
  * Prioritizes tasks by priority level, dependency count, and task ID
  * Displays comprehensive information about the selected task:
    * Basic task details (ID, title, priority, dependencies)
    * Implementation details
    * Subtasks (if they exist)
  * Provides contextual suggested actions:
    * Command to mark the task as in-progress
    * Command to mark the task as done
    * Commands for working with subtasks



Viewing Specific Task Details

The `show` command:

  * Displays comprehensive details about a specific task or subtask
  * Shows task status, priority, dependencies, and detailed implementation notes
  * For parent tasks, displays all subtasks and their status
  * For subtasks, shows parent task relationship
  * Provides contextual action suggestions based on the task’s state
  * Works with both regular tasks and subtasks (using the format taskId.subtaskId)



## 

​

Best Practices for AI-Driven Development

## 📝 Detailed PRD

The more detailed your PRD, the better the generated tasks will be.

## 👀 Review Tasks

After parsing the PRD, review the tasks to ensure they make sense and have appropriate dependencies.

## 📊 Analyze Complexity

Use the complexity analysis feature to identify which tasks should be broken down further.

## ⛓️ Follow Dependencies

Always respect task dependencies - the Cursor agent will help with this.

## 🔄 Update As You Go

If your implementation diverges from the plan, use the update command to keep future tasks aligned.

## 📦 Break Down Tasks

Use the expand command to break down complex tasks into manageable subtasks.

## 🔄 Regenerate Files

After any updates to tasks.json, regenerate the task files to keep them in sync.

## 💬 Provide Context

When asking the Cursor agent to help with a task, provide context about what you’re trying to achieve.

## ✅ Validate Dependencies

Periodically run the validate-dependencies command to check for invalid or circular dependencies.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/capabilities/task-structure.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/capabilities/task-structure)

[CLI Commands](/docs/capabilities/cli-root-commands)

Assistant

Responses are generated using AI and may contain mistakes.