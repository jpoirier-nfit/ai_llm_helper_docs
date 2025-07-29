---
source_url: https://northflank.com/docs/v1/application/secure/inject-secrets#next-steps
title: Inject secrets | Secure | Northflank Application docs
crawl_date: 2025-07-29T10:44:49.166595
watsonmd_version: 0.1.0
---

Secure / 

# Inject secrets

You can define build arguments and runtime variables to be injected at build or runtime respectively for services and jobs. You can set [build arguments](../build/inject-build-arguments) and [environment variables](../run/inject-runtime-variables) in individual resources, or [create a secret group](manage-secret-groups) so that multiple resources in a project can inherit the same secrets.

The editor for both allows you to view arguments and variables, edit them in a table as key-value pairs, or in JSON or ENV format.

If you are working in a team, or edit the variables in another tab, you will be notified that the values have changed and can either view a difference editor or discard your changes. The difference editor will update the remote values in real-time so you can be sure of any variables you may overwrite.

Priority

Build arguments and environment variables set directly in a service or job will always override variables with the same name inherited from secret groups.

To enter or edit environment variables using JSON use the following format:
    
    
    {
        "KEY_1": "value1",
        "KEY_2": "value2"
    }
    

To upload or edit a `.env` file use the following format:
    
    
    KEY_1=value1
    KEY_2=value2
    

Build arguments

You can set build arguments (`ARG`) to be passed to the Docker container at build-time in jobs, build services, and combined services.

Your build arguments will be passed to the Dockerfile on build via the `--build-arg` flag. They do not persist in the built image and are set as key-value pairs.

For example, a variable set as `PACKAGES=npm-cache` can be accessed in the Dockerfile by declaring the ARG. Variables must be declared in the Dockerfile with ARG before being accessed. Arguments will only be in scope for the build section where they are declared.
    
    
    FROM alpine as base
    ARG PACKAGES
    RUN echo "Using: ${PACKAGES}"
    # PACKAGES available
    
    FROM base as stage1
    RUN echo "Using: ${PACKAGES}"
    # PACKAGES not available
    
    FROM base as stage2
    ARG PACKAGES
    RUN echo "Using: ${PACKAGES}"
    # PACKAGES available
    

To set build arguments for a single resource, navigate to the build arguments page in your resource and select an editor mode. You may be prompted to enter your password.

### Persist build arguments in the runtime environment

If you want to access a build argument value in the runtime environment, declare it as an runtime variable (`ENV`) in the Dockerfile with the value of the build argument. You should not pass secrets to your runtime environment in this way, as it will be visible to anyone with the image.
    
    
    FROM alpine as production
    ARG PACKAGES
    ENV PACKAGES=${PACKAGES}
    # PACKAGES available in build and runtime
    

![Setting build arguments in the Northflank application](https://assets.northflank.com/documentation/v1/application/secure/inject-secrets/build-arguments.png)

Learn more about build arguments and the [Docker ARG command ](https://docs.docker.com/engine/reference/builder/#arg).

Runtime variables

You can set runtime variables (`ENV`) in to be passed to the Docker container at runtime. Secrets can be saved and used within a project in [secret groups](manage-secret-groups).

To set runtime variables for a single resource, navigate to the environment page in your resource and select an editor mode. You may be prompted to enter your password.

![Setting environment variables in the Northflank application](https://assets.northflank.com/documentation/v1/application/secure/inject-secrets/environment-variables.png)

Learn more about runtime variables and the [Docker ENV command ](https://docs.docker.com/engine/reference/builder/#env).

Access environment variables in your code

Your runtime variables can be accessed via the process environment, for example in a Node environment a variable set as `ENV_VALUE=Northflank` can be accessed within the container by referring to `process.env.ENV_VALUE`.

Runtime environment| Environment variable accessor| Required import  
---|---|---  
Node| `process.env.ENV_KEY`| none  
Deno| `Deno.env.get("ENV_KEY")`| none  
Bun| `Bun.env.ENV_KEY` OR `process.env.ENV_KEY`| none  
Python| `os.environ.get("ENV_KEY")`| `import os`  
Java| `System.getenv("ENV_KEY")`| none  
Kotlin| `System.getenv("ENV_KEY")`| none  
Ruby on Rails| `ENV["ENV_KEY"]`| none  
Rust| `env::var("ENV_KEY")`| `use std::env`  
Go| `os.Getenv("ENV_KEY")`| `import ( "os" )`  
C# / .NET| `Environment.GetEnvironmentVariable("ENV_KEY")`| `using System;`  
C++| `std::getenv("ENV_KEY")`| `#include <cstdlib>`  
C| `getenv("ENV_KEY")`| `#include <stdlib.h>`  
PHP| `getenv("ENV_KEY")`| none  
Lua| `os.getenv("ENV_KEY")`| none  
Shell / Bash| `${ENV_KEY}`| none  
PowerShell| `$Env:ENV_KEY` OR `[Environment]::GetEnvironmentVariable('ENV_KEY')`| none  
  
Access Northflank injected secrets

Northflank injects build arguments and runtime variables into build and runtime workloads by default. You can access these values (as strings) using their key via the environment in your build and runtime workloads, or in your Dockerfile by specifying the key as an `ARG`.

Build argument key| Values| Example  
---|---|---  
`NF_GIT_SHA`| The git commit hash that is being built| `c7d1f7f0e95116dce9cdfe126edcf782f6de8712`  
`NF_GIT_BRANCH`| The git branch of the current build| `main`  
`NF_PREVIOUS_BUILD_GIT_SHA`| The git commit hash of the previous build attempted by the build service| `f12a3fd2738de900f36c8043cf48c29242bff8fe`  
Environment variable key| Values| Example  
---|---|---  
`NF_HOSTS`| A comma-separated string of Northflank generated DNS entries from your public ports for the deployment, combined with any custom DNS entries assigned to your public ports| `port1--my-service--my-project--user-1bfg.code.run,port2--my-service--my-project--user-1bfg.code.run,testing.example.com`  
`NF_HOSTS_CUSTOM`| A comma-separated string of your custom DNS entries assigned to public ports on the deployment| `testing.example.com`  
`NF_OBJECT_ID`| The Northflank ID for the deployment, generated from your original deployment name| `my-service`  
`NF_PROJECT_ID`| The Northflank ID for the project, generated from your original project name| `my-project`  
`NF_DEPLOYMENT_SHA`| The git commit hash of the deployed build| `c7d1f7f0e95116dce9cdfe126edcf782f6de8712`  
`NF_DEPLOYMENT_REPO`| The git repo of the deployed build| `https://gitservice.com/my-username/my-code-repo`  
`NF_DEPLOYMENT_BRANCH`| The git branch of the deployed build| `main`  
  
Dynamic templating

Build arguments and runtime variables can be constructed using dynamic templating. This allows you to create new variables from multiple sources, including previously defined variables and inherited secrets from [addons](../databases-and-persistence/stateful-workloads-on-northflank).

You can create build arguments or runtime variables using template literals (`${VARIABLE_NAME}`) in all editors (table, JSON, and env). Autocomplete is available in every editor, simply begin typing the template literal syntax (`${`) and a list of available variables will be displayed in a tooltip. You can hover over a variable reference to check its value.

You cannot refer to build arguments in runtime variables, or runtime variables in build arguments. However, if a variable is inherited from a secret group set to `build & runtime`, you can refer to it in both.

For example if `VARIABLE_NAME` with a value of `hello` is previously defined, or inherited by a service from a group, a new variable defined as `${VARIABLE_NAME} world` will have the value `hello world`.

Functions

You can use the `randomSecret` function in your secrets as an argument, for example `${fn.randomSecret(32)}`.

If you use this function in a build argument, runtime variable, or when creating a secret group, the function will be evaluated when you save it. This means the result will be securely stored as a secret rather than the function call itself, and the generated value will remain the same unless it is manually changed.

Function| Arguments| Description  
---|---|---  
randomSecret| length: `number`, encoding: `string: 'base64' or 'hex'`| Returns a random base64 secret of the given `length`, and an optional `encoding` argument, either 'base64' (default) or 'hex'.  
  
Next steps

[Manage groups of secretsCreate and manage groups of secrets that can be inherited throughout an entire project or by specific services and jobs.](/docs/v1/application/secure/manage-secret-groups)[Upload a secret fileAdd secret files that will be mounted in your container.](/docs/v1/application/secure/upload-secret-files)[Grant API accessCreate API roles to grant access to the Northflank API, with granular permissions.](/docs/v1/application/secure/grant-api-access)