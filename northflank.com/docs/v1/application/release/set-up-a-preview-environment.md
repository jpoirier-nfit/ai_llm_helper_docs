---
source_url: https://northflank.com/docs/v1/application/release/set-up-a-preview-environment
title: Set up a preview environment | Release | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.549585
watsonmd_version: 0.1.0
---

Release / 

# Set up a preview environment

You can preview your changes on your Git branches and pull requests with ephemeral environments, configured in your [pipelines](create-a-pipeline-and-release-flow).

Preview environments can automatically build your latest changes and deploy them, either in an entirely self-contained environment, or one that shares resources with your existing development environment.

A new preview environment will be created automatically when you push a commit to a branch or open a pull request that matches your Git triggers. If the branch already has a preview environment, the existing preview environment will be updated. You can also use a webhook to create a new preview environment, or create one manually.

![Creating a new preview environment template using the visual editor in the Northflank application.](https://assets.northflank.com/documentation/v1/application/release/create-a-preview-environment/create-preview-template-form.png)

Preview environments are defined using [Northflank templates](../infrastructure-as-code/infrastructure-as-code) to provision resources and to build and deploy your commits. They use existing [build services](../build/build-code-from-a-git-repository) from your project to build the branch or PR for preview.

You can use trigger references, node references, and arguments to programmatically provision resources for your preview environment, and resources created by the preview environment are tagged for easy identification and teardown.

### Preview environment scope

You can define previews as entirely separate environments from your existing project resources, or share existing configuration values and resources from your project.

To provision preview environments faster and with less resource consumption you could share an existing development database and any services in your project that aren't under development. Alternatively, to completely isolate your existing environments you could replicate your project in its entirety, fork your development database and provision a new addon, and create new secret groups and configuration details for it.

Learn more in inject secrets securely and share environment resources.

Create a preview environment template

To create a preview environment, open a new or existing pipeline in your project and click the configure button ` add preview template`. When you create a new preview environment template it will guide you through selecting a naming convention and a Git trigger, and automatically create a build on trigger node in your template.

You can also create and manage a preview environment using a [pipeline node in the template editor](../infrastructure-as-code/write-a-template#include-release-flows-and-preview-environment-templates).

[Click here ](https://app.northflank.com/s/project/v2-pipelines) to select a pipeline and create a preview environment in it.

You can edit an existing preview environment configuration with the `` settings button in a pipeline, or run a template that updates the preview environment template.

Choose a naming convention

When you create a new preview environment you will be prompted to choose a naming convention. You can change the naming convention in the preview environment template settings.

The naming convention for a preview environment will determine the name of the preview environment and resources within it, to distinguish the preview environment from your permanent project resources.

Convention| Description  
---|---  
Pull request ID| Uses the ID of the pull request that triggered the preview environment, for example `pr-1234`  
Branch name| Uses the name of the branch that the preview environment is based on, for example `feature-new-ui`. Branch names will be slugified, removing any slashes and other non-alphanumeric characters  
Timestamp| Uses the current date and time in the format `yy-mm-dd-hhmm`, for example `24-01-31-1301`  
Random words| Uses the Northflank name generator to provide two random words, for example `general-question`  
  
You can then choose whether the generated portion of the name will be attached to the start (prefix) or the end (suffix) of the names for your resources.

The name of a preview environment is available within the preview environment template as the argument `name`, accessible in the format `${args.name}`.

Any names you assign to resources in the preview environment template (using the visual editor) will automatically have the naming convention applied when the template is run.

Naming convention| Preview environment name| Resource name| Resource name template value| Resulting name  
---|---|---|---|---  
Pull request ID (suffix)| `pr-439`| `database`| `database-${args.name}`| `database-pr-439`  
  
If a run is triggered by an event that does not match your selected convention the preview will use a randomly-generated name instead.

note

Resource names are limited to 39 characters, you must ensure your naming convention combined with your resource names do not exceed this limit.

Add a Git trigger

You can add Git triggers that will create a new preview environment when a commit is pushed to a branch or pull request that matches the trigger. If a preview environment already exists for the branch or pull request, the template will re-run to build and deploy the new commit and update the environment's resources.

You will be prompted to add one or more Git triggers when you create your preview environment template. You can also add `` or remove `` Git triggers in the visual editor, and click on an existing trigger to edit it.

To configure a Git trigger, select the repository you want to trigger preview environments for. The trigger will be given a reference based on the repository name to access it in the template.

You can choose to create new preview environments based on `all pull requests`, which will trigger when a new PR is opened or a commit is pushed to a branch with an open PR. You can also trigger on `all branches`, which will create a preview environment for any branch in your repository when a commit is pushed to it. Preview environments will be created for draft pull requests, unless you choose to ignore them.

The values from the triggers can be used in your template to build and deploy the desired commit using build on trigger nodes. Northflank will automatically add build on trigger nodes for each trigger you add when you create a new preview environment.

### Custom rules

You can define custom [pull request and branch rules](../build/build-code-from-a-git-repository#build-specific-branches-or-pull-requests) instead of creating a new preview environment for all branches or pull requests. Branch rules will run the template when a commit is pushed to a branch matching the given rules. Pull request rules will run the template whenever a pull request is opened for a branch matching the given rules, or a commit is pushed to a branch matching the given rules with an open pull request.

You can also add [path rules](../build/build-code-from-a-git-repository#trigger-a-build-on-changes-to-specific-files-or-directories) and [ignore flags](../build/build-code-from-a-git-repository#skip-ci-with-commit-messages) to only create a preview when changes are made to specific files, or to skip runs when a certain commit message is included.

### Reference triggers in your template

Git trigger references take the format `${refs.<git-trigger-name>.<key>}` and can return the following values:

Key| Value  
---|---  
`branch`| The name of the branch  
`sha`| The SHA of the specific commit  
`pullRequestId`| The ID of the pull request, if triggered by PR  
`repoUrl`| The repository URL  
  
You can also override Git trigger values [using a webhook trigger](create-and-manage-previews#create-a-preview-environment-using-a-webhook).

Build on trigger

The build on trigger node uses an existing build service to build a commit when it is triggered by the selected Git trigger. You can add multiple build on trigger nodes to handle multiple repositories. For most use cases the repository for the build service and the repository for the trigger should be the same.

The node will use the branch and commit passed by the trigger. You can specify a default branch and commit to use if your template has multiple triggers and build on trigger nodes, or for [manually created previews](create-and-manage-previews#create-a-preview-environment-manually) or [webhook triggers](create-and-manage-previews#create-a-preview-environment-using-a-webhook) with no `branch` or `sha` arguments provided. You can also select the branch and commit for each node when manually creating a new preview environment.

![Editing a build on trigger node in a preview environment template using the visual editor in the Northflank application.](https://assets.northflank.com/documentation/v1/application/release/create-a-preview-environment/build-on-trigger-node.png)

After adding a build on trigger node you can use the ` deploy to service` or ` deploy to job` to create a deployment service or job that uses the build from the build on trigger node.

note

The build on trigger node will not override the repository of the chosen build service. The build service will attempt to build the branch specified by the provided trigger, if it does not exist on the build service repository the build will fail.

The node has the following configurable settings:

Option| Description  
---|---  
Build service (required)| The build service to use to build the image  
Trigger (required)| A Git trigger specified in the preview environment settings  
Reference| A reference to refer to the node and its outputs later in the template, generated automatically from the repository name  
Default branch (advanced)| Select a Git repository branch to build from by default if the template is run is caused by a different trigger  
Default commit (advanced)| Select a Git commit to build by default, if the template is run is caused by a different trigger. If left blank, the latest commit to the branch will be built  
Build configuration (advanced)| Preview and override build arguments to be used  
Reuse existing builds| Use an existing build for the commit if one is available, otherwise a new build will be triggered  
Wait for completion| If selected, the next node or workflow will not run until the build has completed  
Skip node execution| Use references, functions, or arguments that resolve to a boolean to conditionally [skip the node](../infrastructure-as-code/write-a-template#control-node-execution)  
  
Build on trigger node specification and example

  * {object}

BuildSource node

    * ref

string

An identifier that can used to reference the output of this node later in the PreviewEnvTemplate.

    * kind

string required

The kind of node.

one of

BuildSource

    * spec

{object} required

The specification for the BuildSource node.

    * condition

string

one of

success

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




An example of a build on trigger node specification, which obtains the `branch` and `sha` to build from a trigger called `application`. It will use the `main` branch by default, it will use an existing build of the commit if one is available, and will wait until the build has completed before allowing the template to progress. It does not pass any build overrides, so the build service will use the default configuration.
    
    
    {
      "kind": "BuildSource",
      "ref": "build",
      "spec": {
        "type": "service",
        "id": "<build service>",
        "branch": "${refs.application.branch}",
        "sha": "${refs.application.sha}",
        "defaults": {
          "branch": "main"
        },
        "reuseExistingBuilds": true,
        "buildOverrides": {
          "buildArguments": {}
        }
      },
      "condition": "success"
    }
    

Configure a preview environment template

Your preview environment should have one or more triggers, with one or more corresponding build on trigger nodes. Alternatively, you can use a [webhook trigger](create-and-manage-previews#create-a-preview-environment-using-a-webhook) or create the environment [manually](create-and-manage-previews#create-a-preview-environment-manually), passing in the required `branch` and `sha` values as arguments.

You can then deploy the new builds from the build on trigger nodes in deployment service nodes, or using job nodes.

You can add nodes for the other resources required in your environment, such as addons, secret groups. You can base these on existing resources in your project by [copying their specification](../infrastructure-as-code/create-a-template#create-from-an-existing-project-or-resource) and pasting the code into a new node.

Depending on your requirements you may want to duplicate your entire development environment, including databases, services, and jobs, or deploy some resources for the preview environment and share databases and jobs with your permanent environment.

When you saved your preview environment template Northflank will create a preview environment for each branch that matches your Git triggers when they receive a new commit.

You can choose how a template will behave if it receives more than one request to run at the same time, or receives a request to run while a run is still in progress. You can set the run concurrency on the template's settings page.

  * Allow (default): multiple template runs can be executed in parallel, with no restrictions
  * Queue: each time a template run is triggered it will be added to a queue, and runs will be executed sequentially in order of creation
  * Forbid: if a template is currently pending or running any run requests will be ignored



You may want to queue or forbid simultaneous runs to ensure that resources are not updated with conflicting configurations.

Manage your preview environment template with GitOps

You can create and update preview environment templates as part of a template using the [pipeline node](../infrastructure-as-code/write-a-template#include-release-flows-and-preview-environment-templates). You can use the visual editor to configure the preview environment template for the pipeline, and refer to resources and arguments contained in the parent template.

You can then manage the parent template [using GitOps](../infrastructure-as-code/gitops-on-northflank), and the preview environment template will be updated whenever the parent template is run.

### Use GitOps to manage a preview environment template

You can enable GitOps to sync the preview environment template with a Git repository. You can make changes to your preview environment template by committing changes to it in the repository or by editing it on Northflank, and the changes will be propagated to Northflank or Git respectively. This allows you to maintain your preview environment templates alongside your codebase, or in a separate infrastructure repository.

Enable GitOps and select the repository and branch that contains, or will contain, the preview environment template. Enter the path to the preview environment template file relative to the repository root. For example `/release-development.json` will look for a file called `release-development.json` in the repository root, while `/release/development.json` will look for a file called `development.json` in the directory `release`.

If a preview environment template already exists at the path, it will be loaded into the editor. If no template exists, one will be created with the specification defined in the editor.

It is not necessary, but it is recommended, to save the preview environment template with the format `json` so it can be recognised by IDEs and text editors.

Inject secrets securely and share environment resources

You can provide secrets to preview environment resources by creating a [secret group](../secure/manage-secret-groups) in the template. It will be automatically [restricted](../secure/manage-secret-groups#restrict-secrets) by the preview environment's [tag](../release/tag-workloads-and-resources) so that only resources in the environment inherit variables from it.

You should not include any secrets, such as API keys, passwords, or other sensitive data directly in your template. To add configuration details or secret values you should include them as [arguments](../infrastructure-as-code/make-a-template-dynamic#add-arguments) and [set them as overrides in the settings](../infrastructure-as-code/make-a-template-dynamic#supply-secrets-with-argument-overrides). This stores them securely on Northflank, and they are only injected when the template is run.

![Adding secrets to a group via arguments and functions in a preview environment template in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/create-a-preview-environment/preview-arguments.png)

### Share secrets

You can share secrets from a development or staging environment with your preview environment by using [secret groups](../secure/manage-secret-groups) that are restricted by [tag](../release/tag-workloads-and-resources). Add the relevant tag to preview environment resources so that they can also inherit secrets from the restricted group.

You can create a new secret group in your preview environment and link it to an existing addon to share connection details. The new secret group will be restricted to resources tagged with the preview environment ID by default.

Preview environments will also inherit from any [unrestricted](../secure/manage-secret-groups#restrict-secrets) secret groups in your project.

### Share resources

You can use existing permanent resources from your project in your preview environments, such as build services, databases, and jobs.

For example, build on trigger nodes use existing build services, you can run a [job with overrides](../run/run-an-image-once-or-on-a-schedule#override-a-job-configuration), or execute a command in a running service.

You can provide the connection details for an existing database via an existing secret group, so that your preview environment can use the database in your development environment, for example. Alternatively, create a new secret group in your template and link the existing addon. The secret group will be restricted to resources tagged with the preview environment ID by default.

You can back up and create a fork of an existing database, so that the original database in your permanent environment is unaffected by any changes (for example migrations) in the preview branch. You can use `latest` to attempt to use the most recent backup, but if no backup exists the preview environment creation will fail. The backup must be for the same major version.

Generate dynamic domains for preview environments

You can generate dynamic subdomains and subdomain paths to assign to deployments in preview environments. Subdomains and subdomain paths created in the template will be deleted when the preview environment is deleted or expires.

You can include template [arguments, references, and functions](../infrastructure-as-code/make-a-template-dynamic), such as the preview environment name, when creating your subdomain or subdomain paths.

You can create a new subdomain and paths for the new subdomain by using the reference to the subdomain node in the subdomain path node.

### Generate a subdomain

You can configure a domain to use [wildcard redirect routing and certificate generation](../domains/wildcard-domains-and-certificates) to dynamically create subdomains in preview environment templates. This approach does not require certificates to be generated, and will not impact certificate generation rate limits.

If you need to generate dynamic domains in multiple regions you will need to add a wildcard domain for each region, for example `us-east.previews.acme.com`.

Add a subdomain node to your template and select the wildcard domain to use. The name will be the new subdomain created for the domain.

For example, creating a subdomain and selecting `previews.acme.com` as the domain and using the reference `${args.name}` for the name will result in a new subdomain of `<preview-name>.previews.acme.com` (where the preview name is the name of the preview environment). Assigning the subdomain directly to a port will use the root path.

  * {object}

Subdomain node

    * ref

string

An identifier that can used to reference the output of this node later in the PreviewEnvTemplate.

    * kind

string required

The kind of node.

one of

Subdomain

    * spec

{object} required

The specification for the Subdomain node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Generate a subdomain path

You can use [path-based routing](../domains/use-path-based-routing) to create or update a path for an existing subdomain, or select a reference to a subdomain node in the preview template to use a subdomain created by the template.

For example, creating a subdomain and selecting `previews.acme.com` as the domain and entering `${args.API_PATH}` for the URI will result in a new path of `previews.acme.com/<API_PATH>` (provided the `API_PATH` argument is supplied to the preview environment template).

  * {object}

SubdomainPath node

    * ref

string

An identifier that can used to reference the output of this node later in the PreviewEnvTemplate.

    * kind

string required

The kind of node.

one of

SubdomainPath

    * spec

{object} required

The specification for the SubdomainPath node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Assign a dynamic subdomain or subdomain path to a port

You can select a subdomain or subdomain path in the port configuration options of a deployment or combined service node. After you [add a port](../network/configure-ports) to the service, `expand custom domains & security rules`. `Add custom domain`, and select the reference to the subdomain or subdomain path node you wish to assign to the port.

Example template

This example template shows the creation of a new subdomain (for the domain `preview.example.com`), the creation of a path for that subdomain, and assigns the subdomain path to a deployment service's port.
    
    
    {
      "apiVersion": "v1.2",
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "Subdomain",
              "spec": {
                "name": "${args.name}",
                "domain": "preview.example.com"
              },
              "ref": "previewexamplecom"
            },
            {
              "kind": "SubdomainPath",
              "spec": {
                "subdomain": "${refs.previewexamplecom.id}",
                "uri": "/${args.API_PATH}",
                "mode": "prefix"
              },
              "ref": "subdomainpath"
            },
            {
              "kind": "DeploymentService",
              "spec": {
                "deployment": {
                  "instances": 1,
                  "storage": {
                    "ephemeralStorage": {
                      "storageSize": 1024
                    },
                    "shmSize": 64
                  },
                  "docker": {
                    "configType": "default"
                  },
                  "external": {
                    "imagePath": "nginx:latest"
                  }
                },
                "name": "nginx-${args.name}",
                "tags": [
                  "${args.previewId}"
                ],
                "runtimeEnvironment": {},
                "runtimeFiles": {},
                "billing": {
                  "deploymentPlan": "nf-compute-20"
                },
                "ports": [
                  {
                    "internalPort": 80,
                    "protocol": "HTTP",
                    "public": true,
                    "name": "web",
                    "domains": [
                      "${refs.subdomainpath.name}"
                    ],
                    "security": {
                      "policies": [],
                      "credentials": []
                    },
                    "disableNfDomain": true
                  }
                ]
              },
              "ref": "nginx"
            }
          ]
        }
      }
    }
    

![Selecting a dynamic subdomain to assign to a port in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/create-a-preview-environment/dynamic-subdomain-path.png)

Set preview environment duration and creation times

You can configure a preview environment to be torn down after a certain amount of time, and set preview environments to only be created automatically during certain hours. This allows you to limit preview environment creation and existence to your working hours to reduce spend on resources. Both of these options are configurable in a preview environment template's settings.

### Preview environment duration

Set the hours and minutes for a preview environment's resources to persist before the environment is torn down. You can allow this duration to be reset if the environment is updated. For example, if a new commit is pushed to the branch of the preview environment the duration timer will start again.

### Active hours

Configure the days and hours during which preview environments should be created by Git triggers. Outside of these hours you can still create preview environments manually, or using a webhook trigger, but committing to a branch or opening a pull request will not create or update a preview environment.

You can create a schedule with start and end times for each selected day, or select a start time for one day and an end time on another day to enable previews across multiple days. For example, you could create a schedule that's active from 09:00 to 18:00 each week day, or from 09:00 on Monday through to 18:00 Friday to enable previews for the whole work week.

This feature is only available for [projects deployed to your own cloud account](../bring-your-own-cloud/use-other-cloud-providers-with-northflank).

![Configuring a preview environment's lifetime and active hours in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/create-a-preview-environment/preview-duration-and-active-hours.png)

Example preview environment template

This example preview environment template has two Git triggers configured to build on any pull request to the selected repositories, configured in the `triggers` array.

The template starts with a parallel workflow containing two build on trigger nodes and a backup node, which triggers a snapshot of an existing addon (`postgres-demo`).

After the backup has completed a new addon is deployed as a fork of the existing addon, using the addon ID and the latest backup. A secret group is then created with connection details for the ephemeral preview environment addon. These secrets are restricted to resources that have the preview environment tag.

Finally, two deployment services are deploying the builds created by the build on trigger nodes. The Redis deployment includes the existing tag `devel-redis`, so that it can inherit the secrets for a permanent resource in the project and share the addon with the development environment, rather than creating a new one for each preview environment.

Example preview environment template
    
    
    {
      "apiVersion": "v1.2",
      "triggers": [
        {
          "accountLogin": "northflank-platform",
          "vcsService": "github",
          "repoUrl": "https://github.com/northflank-platform/postgres-demo",
          "branchRestrictions": [],
          "prRestrictions": [
            "*"
          ],
          "pathIgnoreRules": [],
          "isAllowList": false,
          "ciIgnoreFlagsEnabled": true,
          "ciIgnoreFlags": [
            "[skip ci]",
            "[ci skip]",
            "[no ci]",
            "[skip nf]",
            "[nf skip]",
            "[northflank skip]",
            "[skip northflank]"
          ],
          "ref": "postgres-demo",
          "manualOnly": false,
          "id": "<trigger-ID>"
        },
        {
          "accountLogin": "northflank-platform",
          "vcsService": "github",
          "repoUrl": "https://github.com/northflank-platform/redis-demo",
          "branchRestrictions": [],
          "prRestrictions": [
            "*"
          ],
          "pathIgnoreRules": [],
          "isAllowList": false,
          "ciIgnoreFlagsEnabled": true,
          "ciIgnoreFlags": [
            "[skip ci]",
            "[ci skip]",
            "[no ci]",
            "[skip nf]",
            "[nf skip]",
            "[northflank skip]",
            "[skip northflank]"
          ],
          "ref": "redis-demo",
          "manualOnly": false,
          "id": "<trigger_ID>"
        }
      ],
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "Workflow",
              "spec": {
                "type": "parallel",
                "steps": [
                  {
                    "kind": "BuildSource",
                    "ref": "build-source-1",
                    "spec": {
                      "defaults": {},
                      "reuseExistingBuilds": true,
                      "branch": "${refs.postgres-demo.branch}",
                      "id": "build-postgres-demo",
                      "type": "service",
                      "sha": "${refs.postgres-demo.sha}"
                    },
                    "condition": "success"
                  },
                  {
                    "kind": "BuildSource",
                    "ref": "build-source-2",
                    "spec": {
                      "defaults": {},
                      "reuseExistingBuilds": true,
                      "branch": "${refs.redis-demo.branch}",
                      "id": "build-redis-demo",
                      "type": "service",
                      "sha": "${refs.redis-demo.sha}"
                    },
                    "condition": "success"
                  },
                  {
                    "kind": "AddonBackup",
                    "spec": {
                      "addonId": "postgres-demo",
                      "backupType": "snapshot"
                    },
                    "condition": "success"
                  }
                ]
              }
            },
            {
              "kind": "Addon",
              "spec": {
                "name": "${args.name}-postgres",
                "tags": [
                  "${args.previewId}"
                ],
                "externalAccessEnabled": false,
                "type": "postgresql",
                "billing": {
                  "replicas": 1,
                  "storage": 4096,
                  "storageClass": "ssd",
                  "deploymentPlan": "nf-compute-200"
                },
                "typeSpecificSettings": {
                  "postgresqlConnectionPoolerReplicas": 2,
                  "postgresqlReadConnectionPoolerReplicas": 2
                },
                "tlsEnabled": true,
                "version": "16",
                "source": {
                  "addonId": "postgres-demo",
                  "backupId": "latest"
                }
              },
              "ref": "postgres-addon"
            },
            {
              "kind": "SecretGroup",
              "spec": {
                "type": "secret",
                "secretType": "environment-arguments",
                "priority": 10,
                "name": "${args.name}-secrets",
                "tags": [
                  "${args.previewId}"
                ],
                "secrets": {
                  "variables": {},
                  "files": {}
                },
                "restrictions": {
                  "restricted": true,
                  "tags": [
                    "${args.previewId}"
                  ],
                  "nfObjects": []
                },
                "addonDependencies": [
                  {
                    "addonId": "${refs.postgres-addon.id}",
                    "keys": [
                      {
                        "keyName": "HOST",
                        "aliases": []
                      },
                      {
                        "keyName": "POSTGRES_URI",
                        "aliases": [
                          "POSTGRES_URL"
                        ]
                      },
                      {
                        "keyName": "USERNAME",
                        "aliases": []
                      },
                      {
                        "keyName": "PASSWORD",
                        "aliases": []
                      },
                      {
                        "keyName": "DATABASE",
                        "aliases": []
                      }
                    ]
                  }
                ]
              },
              "ref": "secrets"
            },
            {
              "kind": "Workflow",
              "spec": {
                "type": "parallel",
                "steps": [
                  {
                    "kind": "DeploymentService",
                    "spec": {
                      "deployment": {
                        "instances": 1,
                        "storage": {
                          "ephemeralStorage": {
                            "storageSize": 1024
                          },
                          "shmSize": 64
                        },
                        "docker": {
                          "configType": "default"
                        },
                        "internal": {
                          "id": "${refs.build-source-1.nfObjectId}",
                          "branch": "${refs.build-source-1.branch}"
                        }
                      },
                      "name": "${args.name}-demo",
                      "tags": [
                        "${args.previewId}"
                      ],
                      "runtimeEnvironment": {},
                      "runtimeFiles": {},
                      "billing": {
                        "deploymentPlan": "nf-compute-20"
                      },
                      "ports": []
                    },
                    "ref": "demo"
                  },
                  {
                    "kind": "DeploymentService",
                    "spec": {
                      "deployment": {
                        "instances": 1,
                        "storage": {
                          "ephemeralStorage": {
                            "storageSize": 1024
                          },
                          "shmSize": 64
                        },
                        "docker": {
                          "configType": "default"
                        },
                        "internal": {
                          "id": "${refs.build-source-2.nfObjectId}",
                          "branch": "${refs.build-source-2.branch}"
                        }
                      },
                      "name": "${args.name}-redis",
                      "tags": [
                        "${args.previewId}",
                        "devel-redis"
                      ],
                      "runtimeEnvironment": {},
                      "runtimeFiles": {},
                      "billing": {
                        "deploymentPlan": "nf-compute-20"
                      },
                      "ports": []
                    },
                    "ref": "redis-demo"
                  }
                ]
              }
            }
          ]
        }
      },
      "options": {
        "concurrencyPolicy": "allow"
      }
    }
    

![A preview environment template in the visual editor in the Northflank application.](https://assets.northflank.com/documentation/v1/application/release/create-a-preview-environment/preview-environment-template.png)

Next steps

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Write a templateLearn how to structure a Northflank template, define workflows, create resources, and perform actions.](/docs/v1/application/infrastructure-as-code/write-a-template)[Run migrationsRun database migrations and update your deployments simultaneously when you update your schema.](/docs/v1/application/release/run-migrations)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)