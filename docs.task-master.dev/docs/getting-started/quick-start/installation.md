---
source_url: https://docs.task-master.dev/docs/getting-started/quick-start/installation
title: Installation - Task Master
crawl_date: 2025-08-07T10:57:02.382973
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Quick Start

Installation

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

  * Installation Options



Quick Start

# Installation

Now that you have Node.js and your first API Key, you are ready to begin installing Task Master in one of three ways.

Cursor Users Can Use the One Click Install Below

Quick Install for Cursor 1.0+ (One-Click)

[![Add Task Master MCP server to Cursor](https://cursor.com/deeplink/mcp-install-light.png)![Add Task Master MCP server to Cursor](https://cursor.com/deeplink/mcp-install-dark.png)](cursor://anysphere.cursor-deeplink/mcp/install?name=task-master-ai&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIi0tcGFja2FnZT10YXNrLW1hc3Rlci1haSIsInRhc2stbWFzdGVyLWFpIl0sImVudiI6eyJBTlRIUk9QSUNfQVBJX0tFWSI6IllPVVJfQU5USFJPUElDX0FQSV9LRVlfSEVSRSIsIlBFUlBMRVhJVFlfQVBJX0tFWSI6IllPVVJfUEVSUExFWElUWV9BUElfS0VZX0hFUkUiLCJPUEVOQUlfQVBJX0tFWSI6IllPVVJfT1BFTkFJX0tFWV9IRVJFIiwiR09PR0xFX0FQSV9LRVkiOiJZT1VSX0dPT0dMRV9LRVlfSEVSRSIsIk1JU1RSQUxfQVBJX0tFWSI6IllPVVJfTUlTVFJBTF9LRVlfSEVSRSIsIk9QRU5ST1VURVJfQVBJX0tFWSI6IllPVVJfT1BFTlJPVVRFUl9LRVlfSEVSRSIsIlhBSV9BUElfS0VZIjoiWU9VUl9YQUlfS0VZX0hFUkUiLCJBWlVSRV9PUEVOQUJFX0FQSV9LRVkiOiJZT1VSX0FaVVJFX0tFWV9IRVJFIiwiT0xMQU1BX0FQSV9LRVkiOiJZT1VSX09MTEFNQV9BUElfS0VZX0hFUkUifX0%3D)Or click the copy button (top-right of code block) then paste into your browser:

Copy

Ask AI
    
    
    cursor://anysphere.cursor-deeplink/mcp/install?name=taskmaster-ai&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIi0tcGFja2FnZT10YXNrLW1hc3Rlci1haSIsInRhc2stbWFzdGVyLWFpIl0sImVudiI6eyJBTlRIUk9QSUNfQVBJX0tFWSI6IllPVVJfQU5USFJPUElDX0FQSV9LRVlfSEVSRSIsIlBFUlBMRVhJVFlfQVBJX0tFWSI6IllPVVJfUEVSUExFWElUWV9BUElfS0VZX0hFUkUiLCJPUEVOQUlfQVBJX0tFWSI6IllPVVJfT1BFTkFJX0tFWV9IRVJFIiwiR09PR0xFX0FQSV9LRVkiOiJZT1VSX0dPT0dMRV9LRVlfSEVSRSIsIk1JU1RSQUxfQVBJX0tFWSI6IllPVVJfTUlTVFJBTF9LRVlfSEVSRSIsIk9QRU5ST1VURVJfQVBJX0tFWSI6IllPVVJfT1BFTlJPVVRFUl9LRVlfSEVSRSIsIlhBSV9BUElfS0VZIjoiWU9VUl9YQUlfS0VZX0hFUkUiLCJBWlVSRV9PUEVOQUlfQVBJX0tFWSI6IllPVVJfQVpVUkVfS0VZX0hFUkUiLCJPTExBTUFfQVBJX0tFWSI6IllPVVJfT0xMQU1BX0FQSV9LRVlfSEVSRSJ9fQo=
    

> **Note:** After clicking the link, you’ll still need to add your API keys to the configuration. The link installs the MCP server with placeholder keys that you’ll need to replace with your actual API keys.

## 

​

Installation Options

Option 1: MCP (Recommended)

MCP (Model Control Protocol) lets you run Task Master directly from your editor.

## 

​

1\. Add your MCP config at the following path depending on your editor

Editor| Scope| Linux/macOS Path| Windows Path| Key  
---|---|---|---|---  
**Cursor**|  Global| `~/.cursor/mcp.json`| `%USERPROFILE%\.cursor\mcp.json`| `mcpServers`  
| Project| `<project_folder>/.cursor/mcp.json`| `<project_folder>\.cursor\mcp.json`| `mcpServers`  
**Windsurf**|  Global| `~/.codeium/windsurf/mcp_config.json`| `%USERPROFILE%\.codeium\windsurf\mcp_config.json`| `mcpServers`  
**VS Code**|  Project| `<project_folder>/.vscode/mcp.json`| `<project_folder>\.vscode\mcp.json`| `servers`  
  
## 

​

Manual Configuration

### 

​

Cursor & Windsurf (`mcpServers`)

Copy

Ask AI
    
    
    {
      "mcpServers": {
        "taskmaster-ai": {
          "command": "npx",
          "args": ["-y", "--package=task-master-ai", "task-master-ai"],
          "env": {
            "ANTHROPIC_API_KEY": "YOUR_ANTHROPIC_API_KEY_HERE",
            "PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
            "OPENAI_API_KEY": "YOUR_OPENAI_KEY_HERE",
            "GOOGLE_API_KEY": "YOUR_GOOGLE_KEY_HERE",
            "MISTRAL_API_KEY": "YOUR_MISTRAL_KEY_HERE",
            "OPENROUTER_API_KEY": "YOUR_OPENROUTER_KEY_HERE",
            "XAI_API_KEY": "YOUR_XAI_KEY_HERE",
            "AZURE_OPENAI_API_KEY": "YOUR_AZURE_KEY_HERE",
            "OLLAMA_API_KEY": "YOUR_OLLAMA_API_KEY_HERE"
          }
        }
      }
    }
    

> 🔑 Replace `YOUR_…_KEY_HERE` with your real API keys. You can remove keys you don’t use.

> **Note** : If you see `0 tools enabled` in the MCP settings, try removing the `--package=task-master-ai` flag from `args`.

### 

​

VS Code (`servers` \+ `type`)

Copy

Ask AI
    
    
    {
      "servers": {
        "taskmaster-ai": {
          "command": "npx",
          "args": ["-y", "--package=task-master-ai", "task-master-ai"],
          "env": {
            "ANTHROPIC_API_KEY": "YOUR_ANTHROPIC_API_KEY_HERE",
            "PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
            "OPENAI_API_KEY": "YOUR_OPENAI_KEY_HERE",
            "GOOGLE_API_KEY": "YOUR_GOOGLE_KEY_HERE",
            "MISTRAL_API_KEY": "YOUR_MISTRAL_KEY_HERE",
            "OPENROUTER_API_KEY": "YOUR_OPENROUTER_KEY_HERE",
            "XAI_API_KEY": "YOUR_XAI_KEY_HERE",
            "AZURE_OPENAI_API_KEY": "YOUR_AZURE_KEY_HERE"
          },
          "type": "stdio"
        }
      }
    }
    

> 🔑 Replace `YOUR_…_KEY_HERE` with your real API keys. You can remove keys you don’t use.

#### 

​

2\. (Cursor-only) Enable Taskmaster MCP

Open Cursor Settings (Ctrl+Shift+J) ➡ Click on MCP tab on the left ➡ Enable task-master-ai with the toggle

#### 

​

3\. (Optional) Configure the models you want to use

In your editor’s AI chat pane, say:

Copy

Ask AI
    
    
    Change the main, research and fallback models to <model_name>, <model_name> and <model_name> respectively.
    

For example, to use Claude Code (no API key required):

Copy

Ask AI
    
    
    Change the main model to claude-code/sonnet
    

#### 

​

4\. Initialize Task Master

In your editor’s AI chat pane, say:

Copy

Ask AI
    
    
    Initialize taskmaster-ai in my project
    

Option 2: Using Command Line

## 

​

CLI Installation

Copy

Ask AI
    
    
    # Install globally
    npm install -g task-master-ai
    
    # OR install locally within your project
    npm install task-master-ai
    

## 

​

Initialize a new project

Copy

Ask AI
    
    
    # If installed globally
    task-master init
    
    # If installed locally
    npx task-master init
    
    # Initialize project with specific rules
    task-master init --rules cursor,windsurf,vscode
    

This will prompt you for project details and set up a new project with the necessary files and structure.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/getting-started/quick-start/installation.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/getting-started/quick-start/installation)

[Requirements](/docs/getting-started/quick-start/requirements)[Configuration](/docs/getting-started/quick-start/configuration-quick)

Assistant

Responses are generated using AI and may contain mistakes.