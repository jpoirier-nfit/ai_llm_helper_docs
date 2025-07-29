---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/make-a-template-dynamic
title: Make a template dynamic | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.686757
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Make a template dynamic

You can include variables and functions that are evaluated and resolved when a template is run. Rather than manually updating the same value across a template, such as changing the number of instances on a service or editing configuration values in a secret group, you can provide these values dynamically using references, arguments, and functions.

This means you can create one template as the source of truth for your infrastructure, and deploy the same projects in different regions or cloud providers, or using different configuration values and secrets.

Node references allow you to access the outputs from previous nodes in the workflow. You can use these, for example, to specify a build to deploy, a subdomain path to assign to a port, or a database or deployment status to check in a condition.

You can use arguments to provide configuration values to the template or your resources, argument overrides to supply secrets such as API tokens, and functions to manipulate data and provide different values based on arguments or node outputs.

You can include dynamic values in [release flow and preview environment templates](template-nodes#pipeline-node) within a pipeline node that will resolve on a template run, and specify dynamic values that will persist into the created pipeline templates that will then resolve when the release flow or preview environment template is run.

Northflank will dry-run a template before any template nodes are executed to ensure any references, arguments, and functions in the template can be resolved.

### Use dynamic values in the visual editor

You can include dynamic values in node forms by entering them in text fields as you would any other value. For example `${args.PROJECT_NAME}` can be directly inserted into the `Project name` field of a project node.

Where node forms have non-text fields you can switch to references mode `` to enter a variable or function.

Get node outputs from references

When you add a node to your template and save it, it will be given a reference property (`ref`) generated from the resource name.

You can use this reference to refer to the output of that node later in the template. This is useful if you have steps in your workflow that require confirmation that previous steps have been completed successfully, or need values from resources created earlier. When you add a node to your template you will be given the option, where relevant, to select resources from your template, allowing you to specify resources that have not yet been created.

For example, a start build node will include references to any build services in your template when you select the resource to start a build in, as well as any that are in the project context if the project currently exists in your team.

![Getting a build service by reference in a template build node in the Northflank application](https://assets.northflank.com/documentation/v1/application/infrastructure-as-code/make-a-template-dynamic/build-service-reference.png)

You can see the available properties for a reference by expanding `output variables` on the relevant node.

References to a node return a promise, which resolves to the relevant response from the node. References are accessed as code using the `refs` object, in the format `${refs.<reference-name>.<property>}`.

Reference code example

The example below shows a node to create a build service, and later a node to start a build. In this case the reference will resolve to `my-build-service`, which will be the Northflank ID generated from the build service's name. By using the reference to get `id` you can change the name of the build service without the need to update the value in the rest of the template.
    
    
    "steps": [
      {
        "kind": "BuildService",
        "ref": "builder"
        "spec": {
          "name": "My build service",
          ...
        }
      },
      {
        "kind": "Build",
        "spec": {
          "id": "${refs.builder.id}",
          "type": "service",
          "branch": "main",
          "reuseExistingBuilds": true,
        },
        "condition": "success"
      },
    ]
    

### Northflank DNS references

You can obtain the public DNS for a service from a reference in the following format: `${refs.<service-name>.ports.<array-number>.dns}`. Ports are an array of objects, you must provide the array position of the port you want to get the DNS for. For example if the first port on your service is a public HTTP port, you would obtain the DNS with the following: `${refs.<service-name>.ports.0.dns}`.

If you are using references to obtain the Northflank-generated DNS for a service, or connection details for an addon, you should include a [condition node](template-nodes#condition-nodes) to make sure the service or addon is running. This will ensure the service or addon has obtained a subdomain before using the reference to obtain the DNS or connection details.

### Dynamic domains

You can dynamically create subdomains in templates by configuring your domain to use [wildcard redirect routing and certificate generation](../domains/wildcard-domains-and-certificates) when you add it to Northflank.

You can then use the values from references and arguments to assign subdomains to your services, for example `"${args.<argument-name>}.example.com"` or `"${refs.<reference-name>.<property>}.example.com"`.

You can also accept requests to any subdomain of the parent domain using [wildcard subdomains](../domains/wildcard-domains-and-certificates#redirect-all-subdomains).

Add arguments

Arguments can be used to store template configuration values, dynamic values that you want to change, or build and environment variables for services and secret groups. This allows you to change one value passed to your template, rather than potentially multiple values throughout your template code.

You can include arguments in your template, referenced in the format `${args.<argument-name>}`, replacing `<argument-name>` with your key.

They are also useful if you have a value which is used repeatedly throughout the template that you want to change on subsequent template runs, or a value you wish to dynamically generate using a function.

Arguments are stored in the [argument object at the top-level of the template](write-a-template#template-specification) as key-value pairs. If you enable [GitOps](gitops-on-northflank) the arguments object will be saved in your template file. Similarly, [sharing a template](share-a-template) will also share the arguments object.

It can be useful to include the keys for sensitive data in your arguments object for reference, but you should use placeholder values and not include the actual secrets. Secrets should only be provided to a template securely using argument overrides.

Supply secrets with argument overrides

Argument overrides can be used to inject secure values into your template, or override existing argument values. Argument overrides are stored securely on Northflank, separately from your template. If you are [using GitOps](gitops-on-northflank) these will not be saved in your repository if you add the argument overrides in the Northflank UI using the template form. You should not commit argument overrides in your template.

You can configure argument overrides for a template on its settings page, which will override arguments with the same key in the `arguments` object. If the key specified in the overrides object does not exist in the arguments object, it will be inserted.

You can supply argument overrides using [the API](../../api/templates/create-template) by including an `argumentOverrides` object containing the key-value pairs of arguments to override.

### Run on creation overrides

If you are creating a template using the API you can also specify `runOnCreationArgumentOverrides` in `options`, which will only be used when the template is created if `runOnCreation` is set to `true`.

Example template arguments
    
    
    {
      "name": "Example template arguments",
      "description": "This is a sample template.",
      "apiVersion": "v1",
      "arguments": {
        "ARGUMENT_1": "default_1",
        "ARGUMENT_2": "default_2",
        "ARGUMENT_3": ""
      },
      "argumentOverrides": {
        "ARGUMENT_1": "hello",
        "ARGUMENT_2": "world",
        "ARGUMENT_3": ""
      },
      "options": {
        "runOnCreation": true,
        "runOnCreationArgumentOverrides": {
          "ARGUMENT_1": "goodnight",
          "ARGUMENT_2": "moon",
          "ARGUMENT_3": ""
        },
        "autorun": false
      },
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            ...
          ]
        }
      }
    }
    

Use Northflank functions

You can include functions in your template. Functions are called in the format: `"${fn.<function-name>(<arguments>)}"`, for example `"${fn.randomSecret(32, 'hex')}"`.

Functions are deterministic and will be evaluated on every template run, excluding the `randomSecret` function.

Functions can include references and arguments that do not resolve to a value, unlike the top-level of a template where references and arguments must resolve. Unresolved references and arguments will be treated as `false` if used as boolean arguments.

Functions are listed below, consisting of the function name, arguments and their types, and the purpose of the function.

### General

Function| Arguments| Description  
---|---|---  
randomSecret| length: `number`, encoding: `string: 'base64' or 'hex'`| Returns a random secret of the specified length in either base64 (default) or hex. This secret will be securely stored in the target resource and remain unchanged during subsequent executions of the template, unless it is manually removed.  
date| format: `string`| Returns the current UTC date and time in ISO 8601, for example `2025-05-14T22:00:00.000Z`. You can optionally provide [Moment.js ](https://momentjs.com/) formatting options such as `'YYYYMMDD'` or `'llll'`.  
  
### String manipulation

Function| Arguments| Description  
---|---|---  
toBase64| string: `string`| Converts a UTF-8 encoded string to a base64-encoded string  
fromBase64| base64: `base64`| Converts a base64-encoded string to a UTF-8 encoded string  
slug| string: `string`| Converts a string to a slug (lowercase string with hyphens instead of spaces)  
indexOf| string: `string`, match: `string`| Returns the index of the first instance of the substring in the string, or `-1` if not found  
search| string: `string`, match: `string or regex`| Returns the index of the first pattern match in the string, or `-1` for no match  
replace| original: `string`, match: `string or regex`, replacement: `string`| Replace the first match in the original string with the replacement string  
replaceAll| original: `string`, match: `string or regex`, replacement: `string`| Replace all instances of the match in the original string with the replacement string  
slice| original: `string`, startIndex: `integer`, endIndex: `integer`| Returns the string between the indices of the original string  
length| string: `string`| Returns the length of the string as an integer  
toUpper| string: `string`| Returns the string as uppercase characters  
toLower| string: `string`| Returns the string as lowercase characters  
  
### Boolean functions

Boolean arguments can be provided as truthy and falsy values similar to JavaScript. They can accept booleans, strings, and numbers, and if a reference or argument does not resolve, it will be regarded as false.

Function| Arguments| Description  
---|---|---  
not| boolean: `boolean`| Not  
or| boolean1: `boolean`, boolean2: `boolean`, ...| Or, accepts any number of arguments  
and| boolean1: `boolean`, boolean2: `boolean`, ...| And, accepts any number of arguments  
if| boolean: `boolean`, then: `any`, else: `any` (optional)| If, returns `then` argument if true, otherwise returns `else` argument if provided  
eq| equal1: `any`, equal2: `any`, ...| Equals, accepts any number of arguments  
neq| not1: `any`, not2: `any`, ...| Not equals, accepts any number of arguments  
gt| num1: `number`, num2: `number`| Greater than  
lt| num1: `number`, num2: `number`| Lesser than  
gte| num1: `number`, num2: `number`| Greater than or equal to  
lte| num1: `number`, num2: `number`| Lesser than or equal to  
  
### Maths

Function| Arguments| Description  
---|---|---  
add| a: `number`, b: `number`, ...| Add all arguments, accepts any number of arguments  
subtract| a: `number`, b: `number`, ...| Subtract all arguments, accepts any number of arguments  
multiply| a: `number`, b: `number`, ...| Multiply all arguments, accepts any number of arguments  
divide| a: `number`, b: `number`| Divide `a` by `b`  
remainder| a: `number`, b: `number`| The remainder of `a` divided by `b`  
exp| a: `number`, b: `number`| `a` to the power of `b`  
floor| a: `number`| The floor of `a`  
ceil| a: `number`| The ceiling of `a`  
  
Functions example

This example template uses references, arguments, and functions to programmatically build and deploy from a Git repository. The Git account, repository, and branch are given as arguments to define the service names and retrieve the Git account and repository URL. References are then used to trigger a build and deploy it in the deployment service. The resources assigned to the deployment service depend on the name of the branch, combining `if` and `eq` functions, as well as passing different runtime variables to the deployment.
    
    
    {
      "apiVersion": "v1",
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "BuildService",
              "ref": "builder",
              "spec": {
                "name": "${args.repository}-builder",
                "billing": {
                  "deploymentPlan": "nf-compute-50"
                },
                "vcsData": {
                  "projectUrl": "https://github.com/${args.account}/${args.repository}",
                  "projectType": "github"
                },
                "buildSettings": {
                  "dockerfile": {
                    "buildEngine": "kaniko",
                    "dockerFilePath": "/Dockerfile",
                    "dockerWorkDir": "/"
                  }
                },
                "buildConfiguration": {
                  "prRestrictions": [
                    "*"
                  ],
                  "branchRestrictions": [
                    "main"
                  ]
                }
              }
            },
            {
              "kind": "Build",
              "ref": "build",
              "spec": {
                "id": "${refs.builder.id}",
                "type": "service",
                "branch": "${args.branch}"
              }
            },
            {
              "kind": "Condition",
              "spec": {
                "kind": "Build",
                "spec": {
                  "type": "success",
                  "data": {
                    "buildId": "${refs.build.id}"
                  }
                }
              }
            },
            {
              "kind": "DeploymentService",
              "spec": {
                "name": "${args.branch}-deployment",
                "billing": {
                  "deploymentPlan": "${fn.if(fn.eq(args.branch, 'main'), 'nf-compute-100', 'nf-compute-50')}"
                },
                "deployment": {
                  "instances": "${fn.if(fn.eq(args.branch, 'main'), 3, 1)}",
                  "docker": {
                    "configType": "default"
                  },
                  "storage": {
                    "ephemeralStorage": {
                      "storageSize": 1024
                    }
                  },
                  "internal": {
                    "id": "${refs.builder.id}",
                    "branch": "${args.branch}",
                    "buildId": "${refs.build.id}"
                  }
                },
                "runtimeEnvironment": {
                  "ENVIRONMENT": "${fn.if(fn.eq(args.branch, 'main'), 'production', 'development')}"
                }
              }
            }
          ]
        }
      }
    }
    

Conditionally skip node execution

You can execute nodes on a conditional basis, so that they can either be skipped or executed depending on your requirements. You can use this to include nodes or entire workflows in your template that you don't want to execute on every template run, for example a job to initialise your database that you can skip on subsequent runs to scale your existing resources.

You can set this on a node in the template section where applicable. You can check `skip node execution` to skip a node or workflow, or switch the mode `` to enter an argument or function.

If the provided value resolves to `true` then the node will not be executed during the template run, if the value resolves to `false` then the node will execute as normal.

You can use template arguments, functions, and references to programmatically execute or skip nodes.

Skip node execution example

In this example a function to check equality is used to see if the argument provided for `ENVIRONMENT` is `DEVELOPMENT`. If it is `DEVELOPMENT` then the function will resolve to `true` and the node will be skipped in the template run.
    
    
    {
        "kind": "workflow",
        "skipNodeExecution": "${fn.eq(args.ENVIRONMENT, 'DEVELOPMENT')}",
        "spec": {}
    }
    

Next steps

[Run a templateRun templates manually or automatically.](/docs/v1/application/infrastructure-as-code/run-a-template)[Update a templateUpdate a template and resources within a project.](/docs/v1/application/infrastructure-as-code/run-a-template#update-a-template)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)[Share a templateShare templates with your team or the public.](/docs/v1/application/infrastructure-as-code/share-a-template)[Manage template versions on NorthflankUse the template drafts system to review, accept, or reject proposed changes to your team's Northflank templates.](/docs/v1/application/infrastructure-as-code/manage-template-versions)