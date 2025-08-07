---
source_url: https://docs.task-master.dev/docs/getting-started/contribute#changeset-guidelines
title: Contribute - Task Master
crawl_date: 2025-08-07T10:57:00.492991
watsonmd_version: 0.1.0
---

[Task Master home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/taskmaster-49ce32d5/logo/task-master-logo.png)](/)

Search...

⌘KAsk AI

Search...

Navigation

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

  * Contributing to Task Master
  * 🤝 Our Collaborative Approach
  * 🚀 Quick Start for Contributors
  * 1\. Fork and Clone
  * 2\. Create a Feature Branch
  * 3\. Make Your Changes
  * 4\. Test Everything Yourself
  * 5\. Create a Changeset
  * 6\. Submit Your PR
  * 📋 Development Guidelines
  * Branch Strategy
  * Code Quality Standards
  * Testing Requirements
  * 📦 Changeset Guidelines
  * When to Create a Changeset
  * How to Create a Changeset
  * Changeset vs Git Commit Messages
  * 🔧 Development Setup
  * Prerequisites
  * Environment Setup
  * Running Tests
  * Code Formatting
  * 📝 PR Guidelines
  * Before Submitting
  * PR Description Template
  * What We Look For
  * 🏗️ Project Structure
  * Key Areas for Contribution
  * 🐛 Reporting Issues
  * Bug Reports
  * Feature Requests
  * 💬 Getting Help
  * 📄 License



Getting Started

# Contribute

# 

​

Contributing to Task Master

Thank you for your interest in contributing to Task Master! We’re excited to work with you and appreciate your help in making this project better. 🚀

## 

​

🤝 Our Collaborative Approach

We’re a **PR-friendly team** that values collaboration:

  * ✅ **We review PRs quickly** \- Usually within hours, not days
  * ✅ **We’re super reactive** \- Expect fast feedback and engagement
  * ✅ **We sometimes take over PRs** \- If your contribution is valuable but needs cleanup, we might jump in to help finish it
  * ✅ **We’re open to all contributions** \- From bug fixes to major features

**We don’t mind AI-generated code** , but we do expect you to:

  * ✅ **Review and understand** what the AI generated
  * ✅ **Test the code thoroughly** before submitting
  * ✅ **Ensure it’s well-written** and follows our patterns
  * ❌ **Don’t submit “AI slop”** \- untested, unreviewed AI output



> **Why this matters** : We spend significant time reviewing PRs. Help us help you by submitting quality contributions that save everyone time!

## 

​

🚀 Quick Start for Contributors

### 

​

1\. Fork and Clone

Copy

Ask AI
    
    
    git clone https://github.com/YOUR_USERNAME/claude-task-master.git
    cd claude-task-master
    npm install
    

### 

​

2\. Create a Feature Branch

**Important** : Always target the `next` branch, not `main`:

Copy

Ask AI
    
    
    git checkout next
    git pull origin next
    git checkout -b feature/your-feature-name
    

### 

​

3\. Make Your Changes

Follow our development guidelines below.

### 

​

4\. Test Everything Yourself

**Before submitting your PR** , ensure:

Copy

Ask AI
    
    
    # Run all tests
    npm test
    
    # Check formatting
    npm run format-check
    
    # Fix formatting if needed
    npm run format
    

### 

​

5\. Create a Changeset

**Required for most changes** :

Copy

Ask AI
    
    
    npm run changeset
    

See the Changeset Guidelines below for details.

### 

​

6\. Submit Your PR

  * Target the `next` branch
  * Write a clear description
  * Reference any related issues



## 

​

📋 Development Guidelines

### 

​

Branch Strategy

  * **`main`** : Production-ready code
  * **`next`** : Development branch - **target this for PRs**
  * **Feature branches** : `feature/description` or `fix/description`



### 

​

Code Quality Standards

  1. **Write tests** for new functionality
  2. **Follow existing patterns** in the codebase
  3. **Add JSDoc comments** for functions
  4. **Keep functions focused** and single-purpose



### 

​

Testing Requirements

Your PR **must pass all CI checks** :

  * ✅ **Unit tests** : `npm test`
  * ✅ **Format check** : `npm run format-check`

**Test your changes locally first** \- this saves review time and shows you care about quality.

## 

​

📦 Changeset Guidelines

We use [Changesets](https://github.com/changesets/changesets) to manage versioning and generate changelogs.

### 

​

When to Create a Changeset

**Always create a changeset for** :

  * ✅ New features
  * ✅ Bug fixes
  * ✅ Breaking changes
  * ✅ Performance improvements
  * ✅ User-facing documentation updates
  * ✅ Dependency updates that affect functionality

**Skip changesets for** :

  * ❌ Internal documentation only
  * ❌ Test-only changes
  * ❌ Code formatting/linting
  * ❌ Development tooling that doesn’t affect users



### 

​

How to Create a Changeset

  1. **After making your changes** :

Copy

Ask AI
         
         npm run changeset
         

  2. **Choose the bump type** :
     * **Major** : Breaking changes
     * **Minor** : New features
     * **Patch** : Bug fixes, docs, performance improvements
  3. **Write a clear summary** :

Copy

Ask AI
         
         Add support for custom AI models in MCP configuration
         

  4. **Commit the changeset file** with your changes:

Copy

Ask AI
         
         git add .changeset/*.md
         git commit -m "feat: add custom AI model support"
         




### 

​

Changeset vs Git Commit Messages

  * **Changeset summary** : User-facing, goes in CHANGELOG.md
  * **Git commit** : Developer-facing, explains the technical change

Example:

Copy

Ask AI
    
    
    # Changeset summary (user-facing)
    "Add support for custom Ollama models"
    
    # Git commit message (developer-facing)
    "feat(models): implement custom Ollama model validation
    
    - Add model validation for custom Ollama endpoints
    - Update configuration schema to support custom models
    - Add tests for new validation logic"
    

## 

​

🔧 Development Setup

### 

​

Prerequisites

  * Node.js 18+
  * npm or yarn



### 

​

Environment Setup

  1. **Copy environment template** :

Copy

Ask AI
         
         cp .env.example .env
         

  2. **Add your API keys** (for testing AI features):

Copy

Ask AI
         
         ANTHROPIC_API_KEY=your_key_here
         OPENAI_API_KEY=your_key_here
         # Add others as needed
         




### 

​

Running Tests

Copy

Ask AI
    
    
    # Run all tests
    npm test
    
    # Run tests in watch mode
    npm run test:watch
    
    # Run with coverage
    npm run test:coverage
    
    # Run E2E tests
    npm run test:e2e
    

### 

​

Code Formatting

We use Prettier for consistent formatting:

Copy

Ask AI
    
    
    # Check formatting
    npm run format-check
    
    # Fix formatting
    npm run format
    

## 

​

📝 PR Guidelines

### 

​

Before Submitting

  * **Target the`next` branch**
  * **Test everything locally**
  * **Run the full test suite**
  * **Check code formatting**
  * **Create a changeset** (if needed)
  * **Re-read your changes** \- ensure they’re clean and well-thought-out



### 

​

PR Description Template

Copy

Ask AI
    
    
    ## Description
    
    Brief description of what this PR does.
    
    ## Type of Change
    
    - [ ] Bug fix
    - [ ] New feature
    - [ ] Breaking change
    - [ ] Documentation update
    
    ## Testing
    
    - [ ] I have tested this locally
    - [ ] All existing tests pass
    - [ ] I have added tests for new functionality
    
    ## Changeset
    
    - [ ] I have created a changeset (or this change doesn't need one)
    
    ## Additional Notes
    
    Any additional context or notes for reviewers.
    

### 

​

What We Look For

✅ **Good PRs** :

  * Clear, focused changes
  * Comprehensive testing
  * Good commit messages
  * Proper changeset (when needed)
  * Self-reviewed code

❌ **Avoid** :

  * Massive PRs that change everything
  * Untested code
  * Formatting issues
  * Missing changesets for user-facing changes
  * AI-generated code that wasn’t reviewed



## 

​

🏗️ Project Structure

Copy

Ask AI
    
    
    claude-task-master/
    ├── bin/                    # CLI executables
    ├── mcp-server/            # MCP server implementation
    ├── scripts/               # Core task management logic
    ├── src/                   # Shared utilities and providers and well refactored code (we are slowly moving everything here)
    ├── tests/                 # Test files
    ├── docs/                  # Documentation
    └── .cursor/               # Cursor IDE rules and configuration
    └── assets/							   # Assets like rules and configuration for all IDEs
    

### 

​

Key Areas for Contribution

  * **CLI Commands** : `scripts/modules/commands.js`
  * **MCP Tools** : `mcp-server/src/tools/`
  * **Core Logic** : `scripts/modules/task-manager/`
  * **AI Providers** : `src/ai-providers/`
  * **Tests** : `tests/`



## 

​

🐛 Reporting Issues

### 

​

Bug Reports

Include:

  * Task Master version
  * Node.js version
  * Operating system
  * Steps to reproduce
  * Expected vs actual behavior
  * Error messages/logs



### 

​

Feature Requests

Include:

  * Clear description of the feature
  * Use case/motivation
  * Proposed implementation (if you have ideas)
  * Willingness to contribute



## 

​

💬 Getting Help

  * **Discord** : [Join our community](https://discord.gg/taskmasterai)
  * **Issues** : [GitHub Issues](https://github.com/eyaltoledano/claude-task-master/issues)
  * **Discussions** : [GitHub Discussions](https://github.com/eyaltoledano/claude-task-master/discussions)



## 

​

📄 License

By contributing, you agree that your contributions will be licensed under the same license as the project (MIT with Commons Clause).

* * *

**Thank you for contributing to Task Master!** 🎉 Your contributions help make AI-driven development more accessible and efficient for everyone.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/taskmaster-ai/docs/edit/main/docs/getting-started/contribute.mdx)[Raise issue](https://github.com/taskmaster-ai/docs/issues/new?title=Issue on docs&body=Path: /docs/getting-started/contribute)

[FAQ](/docs/getting-started/faq)[Advanced Usage](/docs/best-practices)

Assistant

Responses are generated using AI and may contain mistakes.