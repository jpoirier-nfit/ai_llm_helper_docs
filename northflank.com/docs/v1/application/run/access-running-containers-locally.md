---
source_url: https://northflank.com/docs/v1/application/run/access-running-containers-locally
title: Access running containers locally | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.389294
watsonmd_version: 0.1.0
---

Run / 

# Access running containers locally

You can forward your deployment and addons for local development, this allows you to access resources as if you were in your secure Northflank project network.

You can also open a shell in your running containers, giving you SSH-like access to the filesystem, environment, and processes.

Execute commands in a container

Shell access gives you access to everything inside your container, such as environment, filesystem, processes, and the ability to run commands like `top`, `npm`, `sed`, `vi`, `df`. It also provides command completion and command history where possible.

You can access the shell of running containers in deployment and combined services by navigating to the containers page for the specific service. You can open a shell for a specific container by clicking `` shell access button.

Running job containers can be accessed by navigating to the job runs page and selecting an active job run. Click `` shell access button on the specific container to open a shell.

![Accessing a container shell in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/access-running-containers-locally/shell-access-container.png)

Copy & paste

You can copy and paste in the browser shell with `control-shift-c` and `control-shift-v`. This may not work in Firefox, where you may need to use the right-click menu to copy and paste. `Command-c` and `command-v` works across all browsers on macOS.

Forward containers for local access

You can forward a deployment for local development and access using the [Northflank CLI](../../api/use-the-cli).

Your deployment must be running and have at least one port configured.

You can view and copy the command to connect to a deployment on the specific deployment's overview, in the local access section, or use the following commands:

  * To forward a specific service:

`sudo northflank forward service --projectId [project-name] --serviceId [service-name]`
  * To forward all ports in a project:

`sudo northflank forward all --projectId [project-name]`



You can now connect to your deployment locally on the available ports.

Execute commands in an action node

You can execute commands in a service in a [template](../infrastructure-as-code/template-nodes#action-nodes) or [release flow](../release/configure-a-release-flow#run-action) by using an action node.

Commands supplied in an action node will not be executed with a shell by default. This means commands executed without a shell will not be able to use any shell features, and will directly pass all strings after the specified executable as parameters without any evaluation.

If you require a shell you must explicitly invoke it first, for example `sh -c`. You can then include your command in the release flow or template after `sh -c` in quote marks escaped with a backslash (`\"`).

Below is an example of a command run with and without a shell in a template's action node. The commands are executed in a service container which has the environment variable `MESSAGE` with the value `Hello!`.

Command| Output| Description  
---|---|---  
`"command": "echo ${MESSAGE}"`| `${MESSAGE}`| Executes `echo` directly, fails to access the environment variable `MESSAGE` without a shell  
`"command": "sh -c \"echo ${MESSAGE}\""`| `Hello!`| Invokes a shell to execute `echo` and successfully reads the environment variable `MESSAGE`  
  
Next steps

[Forward deployments and databasesForward deployments and databases to your local machine for development.](/docs/v1/api/forwarding)[Add private portsConfigure ports to allow your services to communicate securely within your project.](/docs/v1/application/network/configure-ports#private-ports)[Add public portsConfigure ports to expose your services on the internet.](/docs/v1/application/network/configure-ports#public-ports)[Use Northflank generated DNS entriesLearn about Northflank-generated DNS entries for your private and public ports.](/docs/v1/application/network/configure-ports)[Run your application as a different userRun your Docker image as a different user, or execute commands as a different user in your container.](/docs/v1/application/run/run-as-a-different-user#run-a-command-as-a-different-user)