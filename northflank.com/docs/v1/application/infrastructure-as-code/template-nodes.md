---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/template-nodes
title: Template nodes | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.779348
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Template nodes

The sections below contain information on the types of node that you can include in your template, how they are used, and their schema.

The nodes are divided into the following categories:

  * Flow control  contains nodes that are to be run in sequence or parallel
  * Team resources  specifies team-level resources, such as projects and cloud integrations
  * Project resources  specifies a service, job, addon, or other resource to be created or updated
  * Actions  specifies an action to run on a resources, such as starting a build, running a job, or executing a command
  * Conditions  hold the template run while until the status of a resource or action is returned



Flow control nodes

Flow control nodes contain resource and action nodes, and determine in what order they are executed. You can click the switch button `` in the workflow node to change to a parallel or sequential flow.

Sequential workflows will execute nodes from first to last, and will wait until a node has succeeded before executing the next. Parallel workflows will execute all the nodes contained within in them at the same time.

Workflows can be nested. For example, you can run two sequential workflows simultaneously within a parallel workflow, within another sequential workflow.

If a node contained in a workflow fails, the entire workflow will be marked as failed.

### Project context

You can specify the [project context](write-a-template#set-project-context) for a workflow which will be inherited by all the nodes contained within the workflow. This context can be overridden by setting the context directly on nodes or other workflows nested within this workflow.

  * {object}

Workflow node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Workflow

    * spec

{object} required

The specification for the workflow node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




Team resource nodes

Team nodes create and update resources and integrations on the team level. They do not require a project context to run.

Kind| Description  
---|---  
Project| Create or update a project  
BYOC integration| Create or update a cloud provider integration  
BYOC cluster| Create or update a cluster and node pools  
Subdomain path| Create a path for routing on a subdomain  
Tag| Create a new tag in the team for tagging resources  
Custom plan| Create a custom resource plan in the team  
  
### Project

  * {object}

Project node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Project

    * spec

(multiple options: oneOf) required

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### BYOC integration

  * {object}

BYOCIntegration node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

BYOCIntegration

    * spec

{object} required

The specification for the BYOCIntegration node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### BYOC cluster

  * {object}

BYOCCluster node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

BYOCCluster

    * spec

{object} required

The specification for the BYOCCluster node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Subdomain path

  * {object}

SubdomainPath node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

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




### Tag

  * {object}

ResourceTag node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

ResourceTag

    * spec

{object} required

The specification for the ResourceTag node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Custom plan

  * {object}

CustomPlan node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

CustomPlan

    * spec

{object} required

The specification for the CustomPlan node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




Project resource nodes

Project resource nodes can be used to create or update services, jobs, addons, and other resources on the Northflank platform. They can also be used to trigger builds, run jobs, and schedule addon backups.

Project resource nodes require a [project context](create-a-template#set-project-context) to run. The context can be set directly on the node or inherited from a parent workflow.

Kind| Description  
---|---  
Combined service| Create or update a combined service  
Build service| Create or update a build service  
Deployment service| Create or update a deployment service  
Cron job| Create or update a cron job  
Manual job| Creates or update a manual job  
Addon| Creates or updates an addon  
Secret group| Creates or updates a secret group  
Pipeline| Creates or updates a pipeline  
Volume| Creates or updates a volume  
  
To enable CI/CD and build from private Git repositories you must have a [Git account linked to your Northflank team](../getting-started/link-your-git-account). To deploy images from a private container registry you must add your [registry credentials to your team](../run/save-registry-credentials).

### Combined service

A combined service will automatically build and deploy the latest commit for the selected branch when it is created.

  * {object}

CombinedService node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

CombinedService

    * spec

{object} required

The specification for the CombinedService node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Build service

You must trigger a build using a start build node to deploy from a build service later in the template. Otherwise, a build will only be triggered when a commit matching the [build rules](../build/build-code-from-a-git-repository#build-from-a-repository) is pushed.

  * {object}

BuildService node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

BuildService

    * spec

{object} required

The specification for the BuildService node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Deployment service

You can link a deployment service to a build service or deploy an image from a container registry.

If you are deploying from a Northflank build service you can toggle between deploying the latest build or the latest commit from the build service.

Latest build will deploy whatever the service has build most recently, regardless of the commit age. Latest commit will deploy the most recent commit to the branch that has been built by the service.

  * {object}

DeploymentService node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

DeploymentService

    * spec

{object} required

The specification for the DeploymentService node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Cron job

You can deploy a job using an image from a container registry or one built by a Northflank build service.

You can also build and deploy an image in a job by linking it to a Git repository, and create a build to deploy using a start build node.

  * {object}

CronJob node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

CronJob

    * spec

{object} required

The specification for the CronJob node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Manual job

You can deploy a job using an image from a container registry or one built by a Northflank build service.

You can also build and deploy an image in a job by linking it to a Git repository, and create a build to deploy using a start build node.

  * {object}

ManualJob node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

ManualJob

    * spec

{object} required

The specification for the ManualJob node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Addon

You can make an addon's connection details available by linking them in a secret group node. An addon must be running to execute a backup or restore, you can use a condition node to check before performing actions on an addon.

#### Fork an addon

You can fork an addon from an existing project, or one created earlier in the template using a reference. The addon must have a backup available created from the same major version.

You can use `latest` to use the most recent backup, but if no backup exists the template run will fail.

#### Upgrade an addon

You can enable `upgrade on version mismatch` to allow a template to trigger an upgrade for an existing addon (disabled by default). If the addon version specified in the template is greater than the version of the existing addon, the addon will be upgraded. Addons must follow the upgrade path and cannot skip major versions. For example, to upgrade an addon from version 14 to version 16, you must first run the template with version 15 specified before updating to version 16.

  * {object}

Addon node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Addon

    * spec

(multiple options: anyOf) required

The provisioner type of the addon

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Secret group

  * {object}

SecretGroup node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

SecretGroup

    * spec

{object} required

The specification for the SecretGroup node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Volume

A running service will be restarted when a volume is attached to it.

  * {object}

Volume node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Volume

    * spec

{object} required

The specification for the Volume node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




Pipeline node

Pipeline nodes are used to create a pipeline in a project and populate the stages of the pipeline with deployment services, jobs, and addons.

You can also define a [preview environment and release flow templates](write-a-template#include-release-flows-and-preview-environment-templates) for each stage of the pipeline using the visual editor within the pipeline node.

### References, arguments, and functions in nested templates

Normally composed references, arguments, and functions will not be resolved in release flow or preview environment templates in pipeline nodes when the template is executed. This is to preserve their functionality in the release flow and preview templates when they are created.

If you want to include references, arguments, or functions that will be executed when the template runs, so that the values are resolved in the release flow and preview environment templates when they are created, you can prefix them with `template`.

For example:

  * `"${refs.build.branch}"` would become `"${template.refs.build.branch}"`
  * `"${args.SECRET}"` would become `"${template.args.SECRET}"`
  * `"${fn.randomString(64)}"` would become `"${template.fn.randomString(64)}"`



  * {object}

Pipeline node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Pipeline

    * spec

{object} required

The specification for the Pipeline node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




### Preview environment

The pipeline specification can include `preview`, a node with the kind `PreviewEnv`. The spec for the `PreviewEnv` node includes `apiVersion` and `spec`, where `spec` is the content of the preview environment template.

  * {object}

preview

    * kind

string

The kind of node.

one of

PreviewEnv

    * spec

{object} required

The preview environment template specification.




### Release flow

Release flow template specifications can be included in pipeline stages.

  * {object}

releaseFlow

    * kind

string required

The kind of node.

one of

ReleaseFlow

    * spec

{object} required

The release flow template specification.




Action nodes

You can define actions to take on existing services, addons, or Git services.

Kind| Description  
---|---  
Run backup| Performs a backup on an addon  
Job run| Runs a job with the specified configuration  
Start build| Triggers a build in a service or job, from a branch or a specific commit  
Run action| Performs the action contained within the node  
  
### Run backup

An addon must be in a running state to [run a backup](../databases-and-persistence/backup-restore-and-import-data) successfully. You can use a condition node to ensure an addon is ready before the backup node runs.

  * {object}

AddonBackup node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

AddonBackup

    * spec

{object} required

The specification for the AddonBackup node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*

    * condition

string

one of

success




### Run job

Start a [job run](../run/run-an-image-once-or-on-a-schedule). The job must have a build or image available.

  * {object}

JobRun node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

JobRun

    * spec

{object} required

The specification for the JobRun node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*

    * condition

string

one of

success




### Start build

You can trigger builds in build and combined services, and jobs that deploy from version control.

  * {object}

Build node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Build

    * spec

{object} required

The specification for the Build node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*

    * condition

string

one of

success




### Run action

The run action node can be used to perform actions in services, jobs, addons, and VCS (version control system) accounts.

Kind| On resource  
---|---  
Restart| Service or addon  
Execute command| Service or job  
Restore addon from backup| Addon (with available backup)  
Clone repository| Linked VCS account  
  
Commands in action nodes do not invoke a shell by default. Learn more about [executing commands in action nodes](../run/access-running-containers-locally#execute-commands-in-an-action-node).

  * {object}

Action node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Action

    * spec

(multiple options: oneOf) required

The specification for the Action node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




Condition nodes

You can use condition nodes to check the status of a resource or action in a template or in an individual workflow. The workflow or template will continue to run until the condition is met, or until it times out.

In a sequential workflow the condition will stop following steps from running until the condition is met. In a parallel workflow all the steps will run, but the workflow will not be marked as completed unless the condition is met.

Below is a list of checks you can include in your template.

Kind| Description  
---|---  
Running| Check a service, addon, or BYOC cluster is running  
Success| Check a job, build, or addon backup has completed successfully  
VCS| Check that a repository has been created  
Kind| Description  
---|---  
Service| Check a service is running  
Addon| Check an addon is running  
Addon backup| Check an addon backup has completed successfully  
BYOC cluster| Check a BYOC cluster is running  
VCS| Check a Git repository has been cloned successfully  
Build| Check a build has completed successfully  
Job run| Check a job run has completed successfully  
  
  * {object}

Condition node

    * ref

string

An identifier that can used to reference the output of this node later in the template.

    * kind

string required

The kind of node.

one of

Condition

    * spec

(multiple options: oneOf) required

The specification for the Condition node.

    * skipNodeExecution

(multiple options: oneOf)

      * string

one of

true, false

OR

      * string

pattern

.*\${.*}.*




Next steps

[Run a templateRun templates manually or automatically.](/docs/v1/application/infrastructure-as-code/run-a-template)[Update a templateUpdate a template and resources within a project.](/docs/v1/application/infrastructure-as-code/run-a-template#update-a-template)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)[Share a templateShare templates with your team or the public.](/docs/v1/application/infrastructure-as-code/share-a-template)[Manage template versions on NorthflankUse the template drafts system to review, accept, or reject proposed changes to your team's Northflank templates.](/docs/v1/application/infrastructure-as-code/manage-template-versions)