---
source_url: https://northflank.com/docs/v1/api/use-the-cli
title: Use the CLI |  Northflank API docs
crawl_date: 2025-07-29T09:57:19.488025
watsonmd_version: 0.1.0
---

# Use the CLI

The [Northflank CLI client ](https://npmjs.com/@northflank/cli) allows you to interact with Northflank via the command line.

Requirements

You will need the following to get started:

  * [Node.js ](https://nodejs.org/en) (version 12 or greater)
  * [npm ](https://www.npmjs.com/)



The CLI client can be installed using either NPM or Yarn:

  * `npm i -g @northflank/cli`, or
  * `yarn global add @northflank/cli`



Once installed, authenticate yourself using the `northflank login` command. You will need to [create an API token](../application/secure/manage-api-tokens) in your account/team settings in the [Northflank application ](https://app.northflank.com). If you are a member of a team an [API token template](../application/secure/grant-api-access) must have been created by a member with permissions.

The CLI client is fully interactive, meaning that it will ask for any parameters needed along the way. However, you always have the option to pass in any required parameters in your commands. For example, after entering the command `northflank get service details` you will be prompted to enter a project ID and a service ID. You can achieve the same result in a single step by using the command `northflank get service details --project <PROJECT_ID> --service <SERVICE_ID>` .

Authentication and contexts

Contexts allow you to separate different Northflank accounts and preferences when using the CLI client.

For example, you may have a context for your personal Northflank account, and a different context for a team account.

Contexts are created with the `northflank login` command. A browser window will open where you can select an API token from your Northflank account or team. Select one, or create a new token, and check it was successfully created in your terminal. You can enter `Y` to view the URL to open the login link manually in your browser.

See `northflank login --help` for the full list of options, including `-n` to name your context, and `-t` to manually provide a Northflank API token. Once logged in, the active context will be switched automatically.

Team members can generate an API token in that team's settings, provided an [API role](../application/secure/grant-api-access) has been created by a member with permissions.

[Grant API accessCreate API roles to grant access to the Northflank API, with granular permissions.](/docs/v1/application/secure/grant-api-access)[Generate API tokensGenerate an API token to access your team and project.](/docs/v1/application/secure/grant-api-access#generate-an-api-token)

Once created, contexts can be viewed with `northflank context ls` and switched to with `northflank context use`, where you can choose from a list of available contexts.

To set a default project or service within a context, you can use the command `northflank context use project|service|job` to choose from an available list (or `-i` to specify manually by internal ID) and you will no longer need to supply a project/service/job for the set resources in the context in your commands.

Creating resources

When creating resources on Northflank, you can do so interactively, or you can supply a resource definition. This can be done using the `--input` or `-i` option followed by a JSON/YAML string, or by using the `--file` or `-f` option followed by the path to a JSON/YAML file containing the definition.

The resource definitions are equivalent to the API request bodies you will find in this documentation.

Help

You can get help at any time by using the `--help` flag. This includes getting help with specific commands, for example `northflank create project --help` will return helpful information about creating a project.

To see a handy tree view of all possible commands, you can run `northflank command-overview`.