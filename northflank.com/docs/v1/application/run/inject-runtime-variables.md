---
source_url: https://northflank.com/docs/v1/application/run/inject-runtime-variables
title: Inject runtime variables | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.372560
watsonmd_version: 0.1.0
---

Run / 

# Inject runtime variables

You can set [runtime variables (ENV) ](https://docs.docker.com/engine/reference/builder/#env) to be passed to the Docker container at runtime. You can set runtime variables in individual resources, or [create a secret group](../secure/manage-secret-groups) so that multiple resources in a project can inherit the same secrets.

You can also upload secret files to make certificates, configuration files, and other data available in your containers.

![Editing runtime variables in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/inject-runtime-variables/environment-variables.png)

Runtime variables can be set as key-value pairs, or as JSON in the following format:
    
    
    {
        "KEY_1": "value1",
        "KEY_2": "value2"
    }
    

An `.env` file can also be uploaded and edited using the following format:
    
    
    KEY_1=value1
    KEY_2=value2
    

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
  
Add a secret file to a deployment

You can include secret files which can be accessed in your container's file system. This can be useful to provide certificates, secrets, or configuration files that must are required by your application, but which should not be included in your repository.

To add a secret file, paste or upload the content in the secret file editor on the environment page of a deployment service, combined service, or a job. You can also upload secret files to [secret groups](../secure/manage-secret-groups) to make them available to multiple resources in the same project.

Next steps

[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)[Manage groups of secretsCreate and manage groups of secrets that can be inherited throughout an entire project or by specific services and jobs.](/docs/v1/application/secure/manage-secret-groups)[Upload a secret fileAdd secret files that will be mounted in your container.](/docs/v1/application/secure/upload-secret-files)