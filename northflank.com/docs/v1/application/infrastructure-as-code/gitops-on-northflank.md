---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/gitops-on-northflank
title: GitOps on Northflank | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.805880
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# GitOps on Northflank

GitOps on Northflank allows you to manage infrastructure, run releases, update deployments, and automate complex tasks using templates in a Git repository.

Bidirectional sync means that any changes to your template in your repository are automatically reflected on Northflank, and any changes you make in Northflank are committed to your repository on save, enforcing a single source of truth.

You can use GitOps with Northflank templates, release flows, and preview environments. You can [include release flows and preview environment templates](write-a-template#include-release-flows-and-preview-environment-templates) in a single template, or enable GitOps on each of your templates separately.

If `run automatically when updated` is also enabled you can run releases, scale up deployments, run backups, and manage almost anything else on Northflank simply by pushing a commit to a Git repository.

You can store templates in the same directory as your codebase, or you can store them in separate infrastructure repositories.

Enable GitOps

You can `enable GitOps` from a template's settings page to begin syncing your release flow or template with a Git repository.

Northflank must have access to the repository to be able to create and update templates in it. If the repository is not accessible, navigate to Git integrations in your Northflank account and edit the installation for the Git account to enable access.

It is recommended, but not required, that you save templates with the `.json` file extension, so your IDE knows how to handle the file. When you save a template that has GitOps enabled you will be prompted to provide a commit message.

### Save a new template in a repository

You can create a template in the Northflank application and save it to a repository and branch of your choice. Select the repository and branch, and enter the path (relative to the repository root) you want to save the file to.

Click `fetch` and continue editing your template. When you save your template Northflank will create the file in your repository and link it with the template on Northflank.

warning

When you enable GitOps and fetch a template, if a template already exists at the specified path it will overwrite any template content on Northflank.

### Use an existing template

You can use a template that already exists in a Git repository on Northflank. Select the repository and branch that contains the template file you want to use in the GitOps section.

Enter the path to your file (relative to the repository root, e.g. `/Northflank.json` or `/release-flows/development.json`) and click `fetch` to retrieve the existing template or release flow.

Northflank will load the file into the editor, and the file in the repository will be linked with the template or release flow in the Northflank application.

Use GitOps

Any changes you make to a release flow or template with GitOps enabled in the Northflank application will be pushed to your linked repository on the configured branch on save.

Likewise, any commit pushed to the linked branch in your repository will update the template or release flow in Northflank.

### Run a template on change

You can enable `run automatically when the template is updated` so that any changes to the template pushed to your repository will trigger a run of the template. You may want to configure your template's [concurrency settings](create-a-template#configure-template-run-concurrency), so that multiple updates in a short time period are handled as desired.

### Run a release flow on change

You can run a release flow when changes are pushed to your repository, by configuring [Git triggers](../release/create-a-pipeline-and-release-flow#release-flow-settings).

You can configure Git triggers to run a release only on commits to specific branches or pull requests with branch and pull request rules. You can also only run a release flow when either specific files or directories are changed, or ignore certain files or directories so releases are not triggered by, for example, documentation files.

You can also add commit message ignore flags, so that releases will not be triggered when commits with certain strings are pushed to your repository.

note

If you have configured your template or release flow to run on change, your modified template or release flow will run as soon as it's updated. Make sure your changes are as intended before saving or pushing to the repository, especially if the template affects your production environment.

Create multiple Northflank templates from one source

You can use a single template file in a Git repository as the source for multiple Northflank templates. To use the same template file for multiple Northflank templates you can use [arguments](make-a-template-dynamic#add-arguments), as well as [references](make-a-template-dynamic#get-node-outputs-from-references) and [functions](make-a-template-dynamic#use-northflank-functions) to make it programmatic, and not tied to specific projects or regions.

You can then create multiple Northflank templates from the template file. Create a new template in Northflank, enable GitOps and enter the repository, branch, and path of your template. Give the template a distinct name and provide the necessary configuration values and secrets using argument overrides, which can be [added in the template's settings](make-a-template-dynamic#supply-secrets-with-argument-overrides). You can then repeat this process, adding different argument overrides for each template. Argument overrides are stored securely on Northflank, and not saved to your Git repository.

note

If you have `run automatically when the template is updated` enabled while GitOps is enabled, all templates linked to the template file in the same Git repository and branch will run when the template is updated on Northflank or via Git.

The example below shows a template that creates a new project with a combined service. Most of the configuration fields are given as arguments, some of which are set as defaults in the arguments object, which can be overridden. Other arguments have no defaults, and must be provided as overrides for a successful template run.

Example template

### Argument overrides

    
    
    {
      "argumentOverrides": {
        "PROJECT_NAME": "Demo in Europe West",
        "PROJECT_REGION": "europe-west",
        "API_KEY": "123xyz"
      }
    }
    

### Example template

    
    
    {
      "apiVersion": "v1.2",
      "arguments": {
        "PROJECT_NAME": "",
        "PROJECT_REGION": "",
        "SERVICE_INSTANCES": "1",
        "SERVICE_PLAN": "nf-compute-100-1",
        "GIT_ACCOUNT": "acme_corp",
        "GIT_REPO": "https://vcs.example.com/acme-corp/demo-service",
        "GIT_BRANCH": "main"
        "API_KEY": ""
      },
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "Project",
              "ref": "project",
              "spec": {
                "name": "${args.PROJECT_NAME}",
                "color": "#7FD1B9",
                "region": "${args.PROJECT_REGION}",
                "networking": {
                  "allowedIngressProjects": []
                }
              }
            },
            {
              "kind": "Workflow",
              "spec": {
                "type": "sequential",
                "context": {
                  "projectId": "${refs.project.id}"
                },
                "steps": [
                  {
                    "kind": "CombinedService",
                    "spec": {
                      "deployment": {
                        "instances": "${args.SERVICE_INSTANCES}",
                        "storage": {
                          "ephemeralStorage": {
                            "storageSize": 1024
                          },
                          "shmSize": 64
                        },
                        "docker": {
                          "configType": "default"
                        }
                      },
                      "runtimeEnvironment": {
                        "API_KEY": "${args.API_KEY}"
                      },
                      "runtimeFiles": {},
                      "buildArguments": {},
                      "buildFiles": {},
                      "billing": {
                        "deploymentPlan": "${args.SERVICE_PLAN}",
                        "buildPlan": "nf-compute-400-16"
                      },
                      "name": "Demo",
                      "vcsData": {
                        "projectType": "github",
                        "accountLogin": "${args.GIT_ACCOUNT}",
                        "projectUrl": "${args.GIT_REPO}",
                        "projectBranch": "${args.GIT_BRANCH}"
                      },
                      "ports": [
                        {
                          "internalPort": 80,
                          "protocol": "HTTP",
                          "name": "web",
                          "public": true,
                          "domains": [
                            "${args.PROJECT_REGION}.example.com"
                          ],
                          "security": {
                            "policies": [],
                            "credentials": []
                          },
                          "disableNfDomain": true
                        }
                      ],
                      "buildSettings": {
                        "dockerfile": {
                          "buildEngine": "kaniko",
                          "useCache": false,
                          "dockerWorkDir": "/",
                          "dockerFilePath": "/Dockerfile"
                        }
                      },
                      "disabledCI": false,
                      "buildConfiguration": {
                        "pathIgnoreRules": [],
                        "isAllowList": false,
                        "ciIgnoreFlagsEnabled": false
                      }
                    },
                    "ref": "demo"
                  }
                ]
              }
            }
          ]
        }
      }
    }
    

GitOps security

In order to use GitOps securely with release flows and templates you should avoid including any sensitive data in the file committed to the repository, even if it is private.

You can save secrets for a template as [argument overrides](create-a-template#provide-secrets-securely-to-a-template) in the template settings, or pass them in [using the API, CLI, or client](../../api/templates/run-template) when triggering a template run.

These arguments will be securely stored on the Northflank platform so you can save any sensitive information, or information you do not want to include in the template, as argument overrides. They can then be [used in your template](write-a-template#create-from-an-existing-project-or-resource) by referring to them using the format `${args.argumentName}`, replacing `argumentName` with the key saved in argument overrides.

Remove a GitOps integration

You can remove the integration with your infrastructure file by disabling GitOps for the template or release flow in the Northflank application.

This will leave the file in your repository, but changes pushed to the file in your repository will no longer update the relevant release flow or template on Northflank. Similarly, changes made on Northflank will not be pushed to the file in your repository.

warning

It is not recommended that you delete the file from the repository before disabling GitOps, as your file will become inaccessible on Northflank.

Next steps

[Create a templateLearn how to create and configure a Northflank template.](/docs/v1/application/infrastructure-as-code/create-a-template)[Write a templateLearn how to structure a Northflank template, define workflows, create resources, and perform actions.](/docs/v1/application/infrastructure-as-code/write-a-template)[Run a templateRun templates manually or automatically.](/docs/v1/application/infrastructure-as-code/run-a-template)[Share a templateShare templates with your team or the public.](/docs/v1/application/infrastructure-as-code/share-a-template)