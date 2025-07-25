---
source_url: https://northflank.com/docs/v1/application/release/configure-a-release-flow
title: Configure a release flow | Release | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.490992
watsonmd_version: 0.1.0
---

Release / 

# Configure a release flow

Release flows are templates that can automate your release process for a pipeline stage. Release flows consist of workflows that contain nodes to perform specific actions, such as triggering a build, backing up a database, or promoting a deployed image.

To configure a release flow you will need a pipeline with the services, jobs, and addons you want to manage added to it. You can create a release flow for each stage of your pipeline. You can only manage resources that exist in the same pipeline stage as the release flow, which you can refer to in the ` stage resources` view of a release flow template.

You can refer to the documentation in [create a pipeline and release flow](create-a-pipeline-and-release-flow#create-a-release-flow) to learn more about creating and configuring a release flow's settings.

Release flows can be created using the visual editor in the Northflank application, or configured as code, in the same way as [Northflank templates](../infrastructure-as-code/create-a-template#use-the-visual-editor). Similarly, release flows are [structured with workflows](../infrastructure-as-code/write-a-template#structure-a-template) and run in the same way as Northflank templates.

This documentation also includes examples for a simple release flow that deploys builds to deployment services, and a more complex example that performs a database migration before promoting deployments to the current stage.

![The release flow visual editor in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/configure-a-release-flow/backup-migrate-promote-visual.png)

Release flow nodes

Release flow templates have a release node specific to them with different types to deploy from a build service, from a container registry, or to promote an image from another deployment service. The remaining nodes are the same as [template nodes](../infrastructure-as-code/template-nodes).

Some nodes have a `wait for completion` option. You can enable this so that the next steps in the workflow will only run when the node has finished and was successful. This can be useful for ensuring, for example, a job run has completed before promoting a deployment with related changes. You can also use a separate [await condition](../infrastructure-as-code/template-nodes#condition-nodes) node to pause the workflow.

Release node specification

  * {object}

Release node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string

The kind of node.

one of

Release

    * spec

{object} required

The specification for the Release node.

    * condition

string

one of

running

    * timeoutDuration

(multiple options: oneOf)

Timeout for the condition in seconds. This will fail the condition after the timeout has elapsed.

      * integer

Timeout for the condition in seconds. This will fail the condition after the timeout has elapsed.

min

30

max

14400

OR

      * string

A string containing one or more references that resolve to timeout for the condition in seconds. This will fail the condition after the timeout has elapsed.

pattern

.*\${.*}.*

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Deploy build

Deploys an [image from a build service](../build/build-code-from-a-git-repository) to a target deployment service or job.

To configure the node, select the build service you want to deploy from. Open the build menu to select a branch or pull request. From here you can select a specific commit to deploy, or choose to always deploy the latest build. You can filter results for branches, pull requests, or commits by typing in the dropdown.

Finally, select a job or service from the pipeline stage to deploy the built image to.

When you run the release flow you can optionally change the branch, pull request, or select a specific commit to deploy instead of the configured option.

### Promote deployment

Deploys images from the preceding stage to the stage that the release flow is in.

To configure the node select the source service or job from the previous stage which contains the deployed image you want to promote, then select the target service or job to promote the image to. Arrows will appear in the pipeline to indicate which deployments will be promoted when a release flow is run.

When the release flow is run, the current image deployed on the source will be deployed on the target. The image can either be built on Northflank, or deployed from a container registry.

### Deploy image

Deploys an image from an [external container registry](../run/run-an-image-from-a-container-registry) to a target deployment service or job.

To configure the node, [enter the URL](../run/run-an-image-from-a-container-registry#image-paths) of the image you want to deploy. Northflank will try to confirm the image is accessible at the given path. If the image is private, select or create the relevant [registry credentials](../run/save-registry-credentials).

Finally, select a job or service from the pipeline stage to deploy the built image to.

When you run the release flow you can optionally change the image to deploy (and associated credentials) instead of the configured option.

Use Git triggers in a release flow

You can use [Git triggers](create-a-pipeline-and-release-flow#automatically-run-a-release-flow) in your release flow to build the triggering commit. You can also pass the data in to a job or services as environment variables, or use them as part of a command override or shell command.

You can select trigger values in a start build node by selecting a build service that builds from the same repository that the trigger monitors. You can then set the branch and commit using the trigger reference.

Git trigger references take the format `${refs.<git-trigger-name>.<key>}` and return the following values:

Key| Value  
---|---  
`branch`| The name of the branch that triggered the preview environment  
`sha`| The SHA to identify the specific commit to be built  
`repoUrl`| The URL of the repository specified in the Git trigger  
  
You can also override Git trigger values [using a webhook trigger](run-and-manage-releases#run-a-release-flow-using-a-webhook).

Enable webhook for a release flow

You can use a webhook trigger to run release flows. Enable the webhook trigger in the template settings and trigger it by making either a `GET` or `POST` request. This can be used to quickly integrate with third-party services such as GitHub Actions or your own tools.

You can [use query parameters](run-and-manage-releases#run-a-release-flow-using-a-webhook) to override Git trigger values and supply other arguments to the template.

Create a dynamic release flow

You can use references, arguments, and functions in a release flow the same as you would in any Northflank [template](../infrastructure-as-code/make-a-template-dynamic).

### References

All nodes are automatically given a unique reference, and you can change this reference if desired.

You can access references in the release flow using the `refs` object, in the format `${refs.<reference-name>.<property>}`.

This can be useful if you need to access details from resources created earlier, such as the status of a build in an await condition node.

![The release flow visual editor in the Northflank application showing node configuration](https://assets.northflank.com/documentation/v1/application/release/configure-a-release-flow/edit-deploy-build-node.png)

### Arguments

You can include arguments in your release flow, referenced in the format `${args.<argument-name>}`, replacing `<argument-name>` with your key. Arguments are stored in the [argument object at the top-level of the template](../infrastructure-as-code/write-a-template#template-specification) as key-value pairs.

You can set argument overrides on the settings page of a release flow to pass [configuration values and secrets](create-a-pipeline-and-release-flow#provide-secrets-securely-to-a-template) securely to your release flow.

### Functions

You can include [template functions](../infrastructure-as-code/make-a-template-dynamic#use-northflank-functions) in your release flow, which will be evaluated when the release flow is run.

Manually select a commit or build to release

You can add your own components to the release flow run UI to select specific branches, commits, or builds for all relevant template nodes when you run a release. This makes it possible to select a specific commit or build to deploy to multiple resources at once, instead of overriding each node individually.

Rich input components can be used to populate the values of argument overrides, and you can use these arguments to start and deploy builds. You can add these components to your release flow template, as an array of objects at the top level of the template object.

You can give each component a `title` and a `description`, which will be displayed when you run the release flow via the Northflank application.

Each component requires a `source` in the `inputs` object, which is the ID of the build service you want to select a commit or build from.

The `outputs` object maps your selection in the run modal to argument overrides. You can use these argument overrides in start build and deploy build nodes.

There are two available rich input components: `BranchCommitSelector` and `BuildSelector`, which can be added to an array called `richInputs` at the top-level of your release flow template.

![Selecting a commit using a rich input component in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/configure-a-release-flow/rich-inputs-branch-commit.png)

### Branch commit selector

The branch commit selector rich input allows you to select a branch or a specific commit to build and deploy. You can map the `branch` and `buildSha` outputs to arguments to start builds, and then deploy the resulting build to a deployment service or job.

    * kind

string required

`BranchCommitSelector`

    * spec

{object} required




Branch and commit rich input example
    
    
    {
      "apiVersion": "v1.2",
      "richInputs": [
        {
          "kind": "BranchCommitSelector",
          "spec": {
            "inputs": {
              "source": "build-service"
            },
            "outputs": {
              "branch": "RELEASE_BRANCH",
              "buildSha": "RELEASE_SHA"
            },
            "title": "Select branch & commit",
            "description": "Use this to set the branch and commit for all deployment and job nodes."
          }
        }
      ],
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "Build",
              "ref": "start-build",
              "spec": {
                "reuseExistingBuilds": true,
                "buildRuleFallThroughHandling": "fail",
                "buildOverrides": {
                  "buildArguments": {}
                },
                "id": "build-service",
                "type": "service",
                "branch": "${args.RELEASE_BRANCH}",
                "sha": "${args.RELEASE_SHA}"
              },
              "condition": "success"
            },
            {
              "kind": "Release",
              "spec": {
                "type": "build",
                "origin": {
                  "branch": "${refs.start-build.branch}",
                  "build": "${refs.start-build.id}"
                },
                "target": {
                  "id": "deployment-service",
                  "type": "service"
                }
              }
            }
          ]
        }
      }
    }
    

### Build selector

The build selector rich input allows you to select a specific build from a build service to deploy in your release flow. You can map the `branch` and `buildId` outputs to arguments to deploy builds to deployment services and jobs.

    * kind

string required

`BuildSelector`

    * spec

{object} required




Build selector rich input example
    
    
    {
      "apiVersion": "v1.2",
      "richInputs": [
        {
          "kind": "BuildSelector",
          "spec": {
            "inputs": {
              "source": "build-service"
            },
            "outputs": {
              "branch": "DEPLOY_BRANCH",
              "buildSha": "DEPLOY_SHA",
              "buildId": "DEPLOY_BUILD_ID"
            },
            "title": "Select build",
            "description": "Use this to select a build for all deployment and job nodes."
          }
        }
      ],
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "Release",
              "spec": {
                "type": "build",
                "origin": {
                  "id": "build-service",
                  "branch": "${args.DEPLOY_SHA}",
                  "build": "${args.DEPLOY_BUILD_ID}"
                },
                "target": {
                  "id": "deployment-service",
                  "type": "service"
                }
              }
            }
          ]
        }
      }
    }
    

Example build deployment

This is an example of a release flow that deploys the latest build of the branch `main` from a build service to a deployment service and a job. This is executed in a parallel workflow, so both deployments roll out at the same time.

![An example of a release flow in the Northflank application to deploy builds](https://assets.northflank.com/documentation/v1/application/release/configure-a-release-flow/deploy-build-parallel.png)

Example release flow
    
    
    {
      "apiVersion": "v1.2",
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "parallel",
          "steps": [
            {
              "kind": "Release",
              "spec": {
                "type": "build",
                "origin": {
                  "id": "builder",
                  "branch": "main",
                  "build": "latest"
                },
                "target": {
                  "id": "job-prod",
                  "type": "job"
                }
              }
            },
            {
              "kind": "Release",
              "spec": {
                "type": "build",
                "origin": {
                  "id": "builder",
                  "branch": "main",
                  "build": "latest"
                },
                "target": {
                  "id": "deployment-prod",
                  "type": "service"
                }
              }
            }
          ]
        }
      },
      "triggers": []
    }
    

Example build promotion with database migration

This is an example of a release flow that runs a database migration before promoting a deployment. The workflow is executed sequentially, as each node needs to complete successfully before the next node is executed.

The individual steps are:

  1. Run backup: backs up a database and waits for this to be completed successfully
  2. Promote deployment: promotes the image from the staging job to the production job
  3. Run job: runs the production job and waits for it to complete successfully
  4. Promote deployment: promotes the image from the staging deployment to the production deployment



![An example of a release flow in the Northflank application to promote deployments](https://assets.northflank.com/documentation/v1/application/release/configure-a-release-flow/backup-migrate-release-flow.png)

Example release flow
    
    
    {
      "apiVersion": "v1.2",
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "AddonBackup",
              "spec": {
                "addonId": "postgres-prod",
                "backupType": "snapshot"
              },
              "condition": "success"
            },
            {
              "kind": "Release",
              "spec": {
                "type": "deployment",
                "origin": {
                  "id": "job-staging",
                  "type": "job"
                },
                "target": {
                  "id": "job-prod",
                  "type": "job"
                }
              },
              "condition": "running"
            },
            {
              "kind": "JobRun",
              "spec": {
                "jobId": "job-prod"
              },
              "condition": "success"
            },
            {
              "kind": "Release",
              "spec": {
                "type": "deployment",
                "origin": {
                  "id": "deployment-staging",
                  "type": "service"
                },
                "target": {
                  "id": "deployment-prod",
                  "type": "service"
                }
              }
            }
          ]
        }
      },
      "triggers": []
    }
    

Next steps

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Run a release flowRun a release flow and manage releases for your different environments.](/docs/v1/application/release/run-and-manage-releases)[Roll back a releaseRoll back a release to a previous version.](/docs/v1/application/release/run-and-manage-releases#roll-back-a-release)[Run migrationsRun database migrations and update your deployments simultaneously when you update your schema.](/docs/v1/application/release/run-migrations)