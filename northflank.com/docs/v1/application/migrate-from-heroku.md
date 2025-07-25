---
source_url: https://northflank.com/docs/v1/application/migrate-from-heroku
title: Migrate from Heroku |  Northflank Application docs
crawl_date: 2025-07-25T12:06:49.218732
watsonmd_version: 0.1.0
---

# Migrate from Heroku

Northflank supports all your applications you've been deploying to Heroku, and migrating is straightforward and easy. You can use our automated import tool, or move your applications over manually.

You can also manage your account and projects through the Northflank API, CLI, and JavaScript client, helping you develop your applications locally using forwarding and command execute, and programmatically manage your entire devops workflow.

Our [pricing ](https://northflank.com/pricing) is straightforward and transparent, and you only pay for the resources you use.

Get started on Northflank

  1. [Create an account ](https://app.northflank.com/signup)
  2. If you're working with others, [create a team](collaborate/create-a-team) and invite your colleagues
  3. [Link an account](getting-started/link-your-git-account) from a supported Git service to Northflank to build from your repositories



If you have been using Heroku Git

If you've been using the Heroku Git service to deploy your applications, Northflank can clone your Heroku repositories to the Git service of your choice using the automated migration tool.  
  
If you want to migrate manually, just push your Heroku repositories to a Git service such as GitHub, GitLab, or Bitbucket.

Automatically import your Heroku applications and pipelines

To run an automated import, navigate to your account dashboard and select the `Heroku import` option from the settings page.

[Click here ](https://app.northflank.com/s/account/import/heroku) to link your Heroku account and start an automated import.

Link your Heroku account to view your applications and pipelines in the Northflank importer, and select the ones you want to import. Northflank will automatically select a project to import to, change this if you'd like the resource to be imported somewhere else. You can import your Heroku project to an account using the free Developer Sandbox plan, providing the [limits are not exceeded](billing/pricing-on-northflank#deploy-for-free).

Most options will be automatically configured from your Heroku settings, however you should check each field before importing, and complete or update where required.

  * Resource names: as there is not always a 1-to-1 relation between Northflank and Heroku resources, some names will be automatically generated for your new resources
  * Buildpack stack: Northflank will detect and use your buildpack configuration for each of your applications as a custom buildpack stack. You should check this is done correctly under `advanced build options`, especially if you are using legacy or custom buildpack stacks.
  * Branch: the main branch will be automatically selected if you're using Heroku Git, or if your repository only has one branch. If your application is built from a repository with multiple branches you must select one.
  * Environment variables: your secrets, including those provided by linked Heroku addons, will be copied to build and deployment services directly, or into secret groups. Northflank handles build arguments and runtime variables separately. Check the guides below to learn more about specific migration scenarios.



Database connections and secrets

Your Heroku database connections and other secrets will be imported so your deployments can still access them. You can then manage the migration of your data to Northflank.

You cannot import Heroku applications with no dyno formations, apps from pipelines that span multiple regions (e.g. one app deployed in US, one in Europe), and you cannot import apps running images from the Heroku container registry.

### Import guides for specific Heroku scenarios

[Import your single-dyno application from HerokuMigrate your Heroku application with a single dyno to Northflank.](/docs/v1/application/migrate-from-heroku#import-a-heroku-application-with-a-single-dyno-to-northflank)[Import your multi-dyno application from HerokuMigrate your Heroku application running multiple types of dynos to Northflank.](/docs/v1/application/migrate-from-heroku#import-a-heroku-application-with-multiple-dynos-to-northflank)[Import your pipeline from HerokuMigrate your Heroku pipeline to Northflank.](/docs/v1/application/migrate-from-heroku#import-a-heroku-pipeline-to-northflank)

Import a Heroku application with a single dyno to Northflank

### Automated import

Northflank will import your single-dyno application as a combined service. The combined service will build your application, deploy the built image, and contain your environment variables.

Your secrets will be copied to the [build arguments](secure/inject-secrets#build-arguments) and [runtime variables](secure/inject-secrets#runtime-variables) in the combined service. These secrets are separate, so if you edit the value of a build argument it will not affect the value of the runtime variable, and vice versa.

[Click here ](https://app.northflank.com/s/account/import/heroku) to link your Heroku account and start an automated import.

### Manual import

To import a Heroku application with a single dyno formation (an application that contains dynos of only one process type, e.g. web or worker dynos), you can create a combined service.

All aspects of a combined service can be configured after creation - except the name.

  1. Choose `service` from the `create new` menu in the top right corner of the dashboard
  2. Basic information: select combined service and enter a name
  3. Repository: select the Git repository from the drop-down list and choose the branch you want to build from
  4. Build options: choose [buildpack](build/build-code-from-a-git-repository#build-with-buildpacks) to automatically build your application. Northflank uses the Heroku 20 stack by default. You can select another buildpack stack, or add custom buildpacks, in `advanced build settings`.
  5. Environment variables (optional): you can set [build arguments](build/build-code-from-a-git-repository#specify-build-arguments) and [runtime variables](secure/inject-secrets#runtime-variables), or add [secret files](secure/upload-secret-files) in `advanced`. You can add your connection details for hosted databases or API keys for other services here to make them available within your application.
  6. Networking (optional): Northflank will add a public port for buildpacks, you can redefine this port and add more if required. You can also create a service with no public ports that means it can only be accessed by other resources within your project.
  7. Resources: choose a plan with more CPU and memory available to your builds and instances, and increase the number of instances to deploy, if required
  8. Advanced (optional): you can configure health checks and manage other advanced features



### Learn more about combined services

A combined service is a self-contained pipeline that builds and deploys commits to a branch in a Git repository.

Combined services are highly configurable: you can manage how they build your application, CI/CD, networking and domains, health checks, and more.

You can also scale your combined services to meet your needs, increasing the CPU power and memory available to each running instance and increasing the overall number of running instances.

You can learn more about [managing combined services](getting-started/build-and-deploy-your-code#create-a-combined-service) in our getting started guide, or check the documentation for specific tasks you want to achieve.

Networking and DNS on Northflank

Northflank allows flexible and secure private and public networking for services, jobs, databases and other addons. You can create secure, private connections within your project, or expose ports publicly to access your applications online.

You can expose multiple ports on every deployment, public and private, and HTTP, HTTP/2, Websockets, gRPC, TCP and UDP are all supported networking protocols.

Northflank uses scalable and highly performant load balancers to securely distribute external traffic to your applications.

Networking settings are accessed on the ports & DNS page on deployment and combined services, and on the settings page in the network section for databases and other addons.

### Domains

Public ports can use either a free `code.run` domain, generated by Northflank, or your own custom domains. All domains are secured with a free, auto-generated TLS certificate.

You can add your own domains in your account dashboard, then link them to specific ports in your services. You can quickly and easily change what port or service they are linked with, without needing to re-verify or restart your services.

  1. [Add a domain](domains/add-a-domain-to-your-account).

  2. [Add a subdomain](domains/add-a-domain-to-your-account#add-a-subdomain).

  3. [Link a domain to a port](domains/link-a-domain-to-a-port).




### Learn more about networking on Northflank, or follow a step-by-step guide to add and link a domain to a port

[Networking on NorthflankConfigure ports and security for your deployments.](/docs/v1/application/network/networking-on-northflank)[Add and verify domainAdd your domain name to your Northflank account and link it to a public port.](/docs/v1/application/getting-started/add-a-and-verify-domain)

Import your data to Northflank

To get started on Northflank you can use your existing databases and other service integrations by including their API keys, connection strings, or other secrets as environment variables. These will be included with the automated importer, or you can [add them manually yourself](secure/inject-secrets).

Northflank offers [several managed databases](databases-and-persistence/deploy-a-database), including [PostgreSQL](databases-and-persistence/deploy-databases-on-northflank/deploy-postgresql-on-northflank), [Redis](databases-and-persistence/deploy-databases-on-northflank/deploy-redis-on-northflank), [MongoDB](databases-and-persistence/deploy-databases-on-northflank/deploy-mongodb-on-northflank), [MySQL](databases-and-persistence/deploy-databases-on-northflank/deploy-mysql-on-northflank), and [MinIO](databases-and-persistence/deploy-databases-on-northflank/deploy-minio-on-northflank), that can be deployed with a click.

Select `addon` from the `create new` and choose a database to deploy.

After deploying a database you can import your data from the [backups page](databases-and-persistence/backup-restore-and-import-data) by uploading a text dump or specifying the connection string of the database you wish to import from. You have several options to automatically or manually manage [runtime migrations](release/handle-runtime-migrations) on Northflank.

You can also create [persistent volumes](databases-and-persistence/add-a-volume) to attach to your deployments, for any use cases not covered by our managed addons.

### Find guides to deploy and use databases and volumes on Northflank

[Deploy a databaseCreate a database to use with your Northflank deployments.](/docs/v1/application/databases-and-persistence/deploy-a-database)[Use a database with your applicationsSecurely access your database in your project's applications and services.](/docs/v1/application/databases-and-persistence/connect-database-secrets-to-workloads)[Backup, restore, and import your dataCreate and import backups of your database, or restore from an existing backup.](/docs/v1/application/databases-and-persistence/backup-restore-and-import-data)[Run migrationsRun database migrations and update your deployments simultaneously when you update your schema.](/docs/v1/application/release/run-migrations)

Schedule jobs on Northflank

If you're using Heroku scheduler you can create [cron jobs](run/run-an-image-once-or-on-a-schedule) on Northflank that will run your applications at specific times, before shutting down.

You can deploy from a repository, which allows you to automatically build any new commits to the tracked branch and so always run the latest version of your job, or deploy an image from a Northflank build service or an external container registry.

You can run the job on a cron schedule, or if a new image is available.

You can create and configure a new job from the `create new` menu.

### Learn more about jobs on Northflank

[Run an image once or on a scheduleRun an image manually or on a cron schedule.](/docs/v1/application/run/run-an-image-once-or-on-a-schedule)

Use the Northflank API, CLI, or JavaScript client

You can create and manage projects, builds, and deployments programmatically using [the API](../../api/use-the-api), interact with Northflank using [the CLI](../../api/use-the-cli), and integrate the [JavaScript client](../../api/use-the-javascript-client) into your applications to create solutions for any use-case you can imagine.

You can use the CLI to [forward resources](../../api/forwarding) for local development, and to [execute commands](../../api/execute-command) in your running containers.

To get started, create an [API token](secure/grant-api-access#generate-an-api-token), or create an [API role](secure/grant-api-access) for your team to use if you don't have one available.

### Learn more about using Northflank programmatically

[Forward deployments and databasesForward deployments and databases to your local machine for development.](/docs/v1/api/forwarding)[Execute commands in your workloadsAccess the shell for your running workloads or send commands to execute using the UI, CLI, API, or JavaScript client.](/docs/v1/api/execute-command)[Grant API accessCreate API roles to grant access to the Northflank API, with granular permissions.](/docs/v1/application/secure/grant-api-access)[Generate API tokensGenerate an API token to access your team and project.](/docs/v1/application/secure/grant-api-access#generate-an-api-token)[Use the Northflank APILearn how to create and manage projects on Northflank programmatically using the REST API.](/docs/v1/api/use-the-api)[Use the Northflank CLILearn how to create and manage projects on Northflank using the command line client.](/docs/v1/api/use-the-cli)[Use the Northflank JavaScript clientLearn how to create and manage projects on Northflank programmatically using the JavaScript client.](/docs/v1/api/use-the-javascript-client)

Import a Heroku application with multiple dynos to Northflank

### Automated import

Northflank will import your application with multiple dyno formations as a build service and multiple deployment services with an associated secret group. If your Heroku application contains dynos of different process types (e.g. web and worker dynos), a deployment service for each dyno type will be created. Your Heroku application's secrets will be copied to your build service as [build arguments](build/build-code-from-a-git-repository#specify-build-arguments) and to a secret group as [runtime variables](secure/inject-secrets#runtime-variables), to be inherited by your deployment services.

[Click here ](https://app.northflank.com/s/account/import/heroku) to link your Heroku account and start an automated import.

### Manual import

To import a Heroku application with multiple dyno formations (an application that contains dynos with more than one process type, e.g. web and workers dynos), you are recommended to create a build service, multiple deployment services, and a secret group (if required).

#### Build service

You can create a build service linked to the Git repository for your application, and build commits to specific branches and pull request branches by adding [build rules](build/build-code-from-a-git-repository#build-specific-branches-or-pull-requests).

All aspects of a build service can be configured after creation - except the name.

  1. Choose `service` from the `create new` menu in the top right corner of the dashboard
  2. Basic information: select build service and enter a name
  3. Repository: select the Git repository from the drop-down list and choose the branch you want to build from. You can also set [build rules](build/build-code-from-a-git-repository#build-specific-branches-or-pull-requests) to build specific branches or pull request branches.
  4. Build options: choose [buildpack](build/build-code-from-a-git-repository#build-with-buildpacks) to automatically build your application. Northflank uses the Heroku 20 stack by default. You can select another buildpack stack, or add custom buildpacks, in `advanced build settings`. You can also set the [build context](build/build-code-from-a-git-repository#build-a-specific-repository-directory), if it's not the root directory.
  5. Environment variables (optional): you can set [build arguments](build/build-code-from-a-git-repository#specify-build-arguments) or add [secret files](secure/upload-secret-files) in `advanced`
  6. Resources: choose a plan with more CPU and memory available to your builds, if required



[Learn more about building on Northflank](build/build-code-from-a-git-repository).

#### Deployment services

The deployment services will run containers from the images provided by your build service. You can create separate deployment services for each type of dyno in your Heroku application. For example, you would create one deployment service for your web dynos, and one deployment service for your worker dynos. These can then be configured and scaled separately.

For web dynos you can add the required HTTP ports and publicly expose them to the internet. For worker dynos you can add any required HTTP, TCP, or UDP ports and they will only be accessible to resources within your project.

You can either add variables required at runtime directly in the deployment services on the environment page, or create a [secret group](secure/manage-secret-groups) that can be inherited by multiple services.

  1. Choose `service` from the `create new` menu in the top right corner of the dashboard
  2. Basic information: select deployment service and enter a name
  3. Deployment: select Northflank and link your build service, selecting a branch to deploy builds from
  4. Environment variables (optional): you can set [runtime variables](secure/inject-secrets#runtime-variables) or add [secret files](secure/upload-secret-files) in `advanced`
  5. Networking (optional): add public ports to make the service accessible on the internet, or private ports for it to only be accessed by other resources within your project
  6. Resources: choose a plan with more CPU and memory available to your instances and increase the number of instances to deploy, if required
  7. Advanced (optional): you can configure health checks and manage other advanced features



[Learn more about deploying on Northflank](run/run-containers-and-micro-services).

#### Secret group

Rather than adding secrets to each of your services individually, you can create secret groups that can be inherited by multiple services. On Northflank environment variables for build arguments and runtime variables are normally separate, however your can create a secret group containing both. Variables in secret groups are inherited by all your services by default, but you can restrict them to specific services if required.

  1. Choose `secret group` from the `create new` menu in the top right corner of the dashboard
  2. Basic information: enter a name and select the type of secrets the group will contain: runtime variables, build arguments, or both
  3. Secrets: enter your secret keys and values using the key-value table `edit` view, as `JSON`, or upload or enter in `ENV` format. You can also add secret files in `advanced`.
  4. Linked addons: you can link addons to your secret group to make them easily accessible in your services and jobs
  5. Advanced: by default secret groups will be inherited by all your services and jobs in the project. You can choose to apply the secret group to specific services and jobs only.



[Learn more about secrets on Northflank](secure/security-on-northflank).

Import a Heroku pipeline to Northflank

### Automated import

Northflank will import each pipeline application as a build service and deployment services with associated secret groups. If your Heroku application contains dynos of different process types (e.g. web and worker dynos), a deployment service for each dyno type will be created.

The deployment services will be placed in staging and production stages in the pipeline, which you can then modify and configure release flows to suit your workflow.

The commits currently deployed to your Heroku apps, regardless of their stage in a pipeline, are built and deployed to your deployment services for that app during the import. See the guides on pipelines and CI/CD below for more information on managing your releases.

Each application's secrets will be copied to a build service as [build arguments](build/build-code-from-a-git-repository#specify-build-arguments) and to a secret group as [runtime variables](secure/inject-secrets#runtime-variables), to be inherited by your deployment services.

[Click here ](https://app.northflank.com/s/account/import/heroku) to link your Heroku account and start an automated import.

### Manual import

To import your pipeline to Northflank manually you can create a build service for each repository you wish to build from, and set [rules](build/build-code-from-a-git-repository#build-specific-branches-or-pull-requests) to build specific branches or pull requests.

You can then create deployment services, one for each type of dyno per application, to populate a pipeline.

You can add secrets as build arguments directly to build services, and runtime variables directly to deployment services, or create secret groups to contain environment variables that can be inherited by multiple services.

You can follow the steps in import a Heroku application with multiple dynos to Northflank to create build services, deployment services, and secret groups.

### Pipelines on Northflank

You can add your Northflank resources to a pipeline, and control them using release flows. Release flows allow you to deploy builds, promote images from one stage to another, and to perform many other tasks such as starting a build, backing up a database, and running a job. The guide below will explain the basics of creating a pipeline and deploying and promoting built images.

For your first pipeline stage (`development`) you will need to deploy an image from a build service. Your subsequent stages, `staging` and `production`, can promote images from the previous stage, or deploy images from a build service.

#### Create a pipeline

  1. Choose `pipeline` from the create new drop-down menu in the top right corner of the dashboard
  2. Enter a name
  3. Click `create pipeline`



#### Add resources to a pipeline

  1. Click ` add items to [stage]`, for each stage you want to use
  2. Select each resource to add to the stage (deployment services, jobs, and addons) and click `add items`



#### Create a release flow for your development stage

  1. Click ` add release flow` in the header for the development stage
  2. Select ` get started with visual editor`
  3. Click and drag a `deploy build` node into the workflow. Click on it to configure the node.
  4. Select the `build service` linked to the repository you want to use, select the `build` by selecting the branch or PR you want to deploy from, and either `latest` or a specific build. Select your deployment service as the `target` and `save node`.
  5. Exit the release flow editor by clicking the `` close button in the top-right corner



Note: if CI is not enabled on your build service, you can add a [build node](getting-started/set-up-a-pipeline#add-a-release-flow) before the deploy build node to start a new build to deploy.

#### Create release flows for your staging and production stages

  1. Click ` add release flow` in the header for the staging or production stage
  2. Select ` get started with visual editor`
  3. Click and drag a `promote build` node and drop it into the workflow. Click on it to configure the node.
  4. Select the deployment in the previous stage as the `origin`, the service or job you want to promote as the `target`, and `save node`.
  5. Exit the release flow editor by clicking the `` close button in the top-right corner



You can now deploy and promote built images on Northflank by running the release flows for your pipeline stages.

### Learn more about pipelines, release flows, and CI/CD on Northflank

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Manage CI/CDConfigure continuous integration and continuous delivery on your Northflank services.](/docs/v1/application/release/manage-ci-cd)

Next steps

[Add public portsConfigure ports to expose your services on the internet.](/docs/v1/application/network/configure-ports#public-ports)[Link a domain to a portHow to link and unlink domains and subdomains with specific ports on your deployments.](/docs/v1/application/domains/link-a-domain-to-a-port)[Run an image once or on a scheduleRun an image manually or on a cron schedule.](/docs/v1/application/run/run-an-image-once-or-on-a-schedule)[Configure health checksMonitor the uptime and success of your deployed services and builds to ensure your code runs correctly and is always available.](/docs/v1/application/observe/configure-health-checks)[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Manage CI/CDConfigure continuous integration and continuous delivery on your Northflank services.](/docs/v1/application/release/manage-ci-cd)[Deploy a databaseCreate a database to use with your Northflank deployments.](/docs/v1/application/databases-and-persistence/deploy-a-database)[Use the Northflank APILearn how to create and manage projects on Northflank programmatically using the REST API.](/docs/v1/api/use-the-api)[Use the Northflank CLILearn how to create and manage projects on Northflank using the command line client.](/docs/v1/api/use-the-cli)[Use the Northflank JavaScript clientLearn how to create and manage projects on Northflank programmatically using the JavaScript client.](/docs/v1/api/use-the-javascript-client)