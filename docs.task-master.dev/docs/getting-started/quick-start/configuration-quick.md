---
source_url: https://docs.task-master.dev/docs/getting-started/quick-start/configuration-quick
title: Configuration - Task Master
crawl_date: 2025-08-07T10:57:02.420125
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

Quick Start

Configuration

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

  * API Key Setup
  * MCP Usage: mcp.json file
  * CLI Usage: .env File
  * What Else Can Be Configured?



Quick Start

# Configuration

Before getting started with Task Master, you’ll need to set up your API keys. There are a couple of ways to do this depending on whether you’re using the CLI or working inside MCP. It’s also a good time to start getting familiar with the other configuration options available — even if you don’t need to adjust them yet, knowing what’s possible will help down the line.

## 

​

API Key Setup

Task Master uses environment variables to securely store provider API keys and optional endpoint URLs.

### 

​

MCP Usage: mcp.json file

For MCP/Cursor usage: Configure keys in the env section of your .cursor/mcp.json file.

.env

Copy

Ask AI
    
    
    {
    	"mcpServers": {
    		"task-master-ai": {
    			"command": "node",
    			"args": ["./mcp-server/server.js"],
    			"env": {
    				"ANTHROPIC_API_KEY": "ANTHROPIC_API_KEY_HERE",
    				"PERPLEXITY_API_KEY": "PERPLEXITY_API_KEY_HERE",
    				"OPENAI_API_KEY": "OPENAI_API_KEY_HERE",
    				"GOOGLE_API_KEY": "GOOGLE_API_KEY_HERE",
    				"XAI_API_KEY": "XAI_API_KEY_HERE",
    				"OPENROUTER_API_KEY": "OPENROUTER_API_KEY_HERE",
    				"MISTRAL_API_KEY": "MISTRAL_API_KEY_HERE",
    				"AZURE_OPENAI_API_KEY": "AZURE_OPENAI_API_KEY_HERE",
    				"OLLAMA_API_KEY": "OLLAMA_API_KEY_HERE",
    				"GITHUB_API_KEY": "GITHUB_API_KEY_HERE"
    			}
    		}
    	}
    }
    

### 

​

CLI Usage: `.env` File

Create a `.env` file in your project root and include the keys for the providers you plan to use:

.env

Copy

Ask AI
    
    
    # Required API keys for providers configured in .taskmaster/config.json
    ANTHROPIC_API_KEY=sk-ant-api03-your-key-here
    PERPLEXITY_API_KEY=pplx-your-key-here
    # OPENAI_API_KEY=sk-your-key-here
    # GOOGLE_API_KEY=AIzaSy...
    # AZURE_OPENAI_API_KEY=your-azure-openai-api-key-here
    # etc.
    
    # Optional Endpoint Overrides
    # Use a specific provider's base URL, e.g., for an OpenAI-compatible API
    # OPENAI_BASE_URL=https://api.third-party.com/v1
    #
    # Azure OpenAI Configuration
    # AZURE_OPENAI_ENDPOINT=https://your-resource-name.openai.azure.com/ or https://your-endpoint-name.cognitiveservices.azure.com/openai/deployments
    # OLLAMA_BASE_URL=http://custom-ollama-host:11434/api
    
    # Google Vertex AI Configuration (Required if using 'vertex' provider)
    # VERTEX_PROJECT_ID=your-gcp-project-id
    

## 

​

What Else Can Be Configured?

The main configuration file (`.taskmaster/config.json`) allows you to control nearly every aspect of Task Master’s behavior. Here’s a high-level look at what you can customize:

You don’t need to configure everything up front. Most settings can be left as defaults or updated later as your workflow evolves.

View Configuration Options

### 

​

Models and Providers

  * Role-based model setup: `main`, `research`, `fallback`
  * Provider selection (Anthropic, OpenAI, Perplexity, etc.)
  * Model IDs per role
  * Temperature, max tokens, and other generation settings
  * Custom base URLs for OpenAI-compatible APIs



### 

​

Global Settings

  * `logLevel`: Logging verbosity
  * `debug`: Enable/disable debug mode
  * `projectName`: Optional name for your project
  * `defaultTag`: Default tag for task grouping
  * `defaultSubtasks`: Number of subtasks to auto-generate
  * `defaultPriority`: Priority level for new tasks



### 

​

API Endpoint Overrides

  * `ollamaBaseURL`: Custom Ollama server URL
  * `azureBaseURL`: Global Azure endpoint
  * `vertexProjectId`: Google Vertex AI project ID
  * `vertexLocation`: Region for Vertex AI models



### 

​

Tag and Git Integration

  * Default tag context per project
  * Support for task isolation by tag
  * Manual tag creation from Git branches



### 

​

State Management

  * Active tag tracking
  * Migration state
  * Last tag switch timestamp



For advanced configuration options and detailed customization, see our [Advanced Configuration Guide](/docs/best-practices/configuration-advanced) page.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/getting-started/quick-start/configuration-quick.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/getting-started/quick-start/configuration-quick)

[Installation](/docs/getting-started/quick-start/installation)[PRD Creation and Parsing](/docs/getting-started/quick-start/prd-quick)

Assistant

Responses are generated using AI and may contain mistakes.