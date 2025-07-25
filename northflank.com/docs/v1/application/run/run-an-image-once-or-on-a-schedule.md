---
source_url: https://northflank.com/docs/v1/application/run/run-an-image-once-or-on-a-schedule
title: Run an image once or on a schedule | Run | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.326549
watsonmd_version: 0.1.0
---

Run / 

# Run an image once or on a schedule

You can run code from a Git registry or an image from a container registry as a job that will terminate after the container has finished running. You can create either a manual job, to run once whenever you trigger it, or a cron job to run on a schedule.

You can create a job from the following sources:

  * Version control: build from a specific branch in a repository [on a linked git account](../getting-started/link-your-git-account) and run the resulting image
  * External image: deploy an image from a [container registry](../run/run-an-image-from-a-container-registry)
  * Northflank: deploy an image built by a [Northflank build service](../build/build-code-from-a-git-repository)



From the job overview you can run manual jobs, or pause and resume scheduled jobs.

[Click here ](https://app.northflank.com/s/project/create/job) to create a job.

Configure CI/CD for a job

Continuous integration (CI) is available to your jobs created with version control as their source. When CI is active on your job, every new commit to the tracked branch of the linked repository will automatically result in a new build. You can change the repository and branch from the build options page.

Continuous delivery (CD) is available on your jobs that have version control or a Northflank build service as their source. When CD is active new job runs will automatically use the latest available build.

The schedule for cron jobs can be toggled between inactive and active. If a job is inactive it will still build the latest commits (if CI is enabled), but it will not run the build.

Pausing a job will disable CI/CD and, for scheduled jobs, stop it from running on a schedule.

Run a job on image change

You can configure a job to run automatically when the source image is changed, if the job uses version control or a Northflank build service as the source. You can set this when creating the job, and change it from the job settings page. The following options are available:

  * Never: the job will not automatically run when the image changes. The job will continue to run on a schedule, or when run manually, and the image deployed will be according to the CI/CD configuration
  * CD & pipeline promotion: the job will be triggered to run if a build finishes and CD is enabled, or if an image is promoted to the job [via a pipeline](../release/create-a-pipeline-and-release-flow)
  * Always: the job will run every time the image is deployed via the UI, if a build finishes and CD is enabled, or if an image is promoted via a pipeline



Set the cron schedule and concurrency policy

For scheduled cron jobs you must set a schedule and concurrency policy to dictate when the job will run.

![Cron job settings in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/run-an-image-once-or-on-a-schedule/cron-job-settings.png)

#### Job schedule

The job schedule is a cron expression. It consists of five fields representing the time at which to execute a specified command.
    
    
    * * * * *
    | | | | |
    | | | | |___ day of week (0-6) (Sunday is 0)
    | | | |_____ month (1-12)
    | | |_______ day of month (1-31)
    | |_________ hour (0-23)
    |___________ minute (0-59)
    

For simple cron expressions you have option to use the following variables: `@yearly`, `@annually`, `@monthly`, `@weekly`, `@daily` or `@hourly`.

#### Concurrency policy

Choose whether to allow this job to run while another instance of the job is running, or to replace the currently running instance.

  * `Allow` will enable multiple instances of this job to run.
  * `Forbid` will keep the current instance of the job running and stop a new instance from being run.
  * `Replace` will terminate any currently running instance of the job and start a new one.



The concurrency policy does not apply when initiating a job run manually.

Set the retry and time limit

#### Retry limit

You can specify the maximum number of attempts to run a job before it is marked as failed.

#### Time limit

You can specify (in seconds) the maximum amount of time for a job to run, whether it has failed or not. This will take precedence over the Retry Limit.

For example, if you set a Retry Limit of 6 and a Time Limit of 480, the job will terminate after 8 minutes regardless of how many times it attempted to run.

Override a job configuration

You can preview and override a job's configuration when manually triggering a job run. This allows you to quickly change a job's configuration for the current run only. The configuration override section also includes a button to copy a shareable URL. You can send this URL to colleagues with access to the job, and it will open the job run modal with the configuration overrides you have set.

You can also configure job run overrides in a [job run node in a release flow](../release/configure-a-release-flow#run-job).

You can override the following settings:

### Deployment

Overriding the deployment depends on the job source:

  * From a Northflank build service: choose the [build service and build](../build/build-code-from-a-git-repository)
  * From a Git repository: choose the build service and build
  * From a container registry: choose the [external image to deploy](../run/run-an-image-from-a-container-registry)



### Environment variables

You can add new environment variables for the run, or override values by providing the same key as existing environment variables.

### Advanced options

You can configure the entrypoint, set a custom command, or select a process to run for [Docker or buildpack runtime modes](../run/override-command-entrypoint.

### Resources

You can dedicate more or less resources to a job run. For example, if your job normally runs with a minimal compute plan but you want the job to complete quickly for this run, you could use a plan with more CPU and memory.

View job runs

You can view job runs on the runs page of a job. Each run is listed with a randomly-generated name, the date and time of when the job run was started, and the status of the run: how many runs are active, how many runs have failed, and the duration of the run.

Clicking through to a job run shows more details about the status of the run, including the time limit for the run and when the run was last updated (for example when a new container was created, or when a container exited successfully).

![A job run page in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/run-an-image-once-or-on-a-schedule/manual-job-runs.png)

You can click on a container to view [logs](../observe/view-logs), [metrics](../observe/view-metrics), [health checks](../observe/configure-health-checks), and [access the shell](access-running-containers-locally) for running containers.

Next steps

[Scale your servicesIncrease the resources available to your services, and the number of instances to deploy.](/docs/v1/application/scale/scale-on-northflank)[Configure health checksMonitor the uptime and success of your deployed services and builds to ensure your code runs correctly and is always available.](/docs/v1/application/observe/configure-health-checks)[View logsView detailed, real-time logs from builds, deployments, and more.](/docs/v1/application/observe/view-logs)[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)