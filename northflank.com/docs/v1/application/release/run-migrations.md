---
source_url: https://northflank.com/docs/v1/application/release/run-migrations
title: Run migrations | Release | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.576215
watsonmd_version: 0.1.0
---

Release / 

# Run migrations

When you make changes to your database schema you may need to update your application and change your production database simultaneously.

You can handle database schema migrations on Northflank in various ways:

  * By configuring a release flow, which automatically runs a migration and then promotes the deployment only when the migration is successful (recommended)
  * Using a job triggered by CI
  * Restarting your deployment with command overrides
  * Executing commands in a container's shell



We recommend using release flows to automate your migration process, especially for production deployments, as this makes the process easy and ensures the migration has run before deploying your updated application.

To release a new version of your application with a migration it is recommended you follow the workflow:

  1. Back up your database, in case you need to restore it
  2. Run your migration
  3. If the migration is successful, deploy the new release to the deployment service



If your updated application is deployed before the migration has completed it may crash or not function as expected, and you may need to redeploy it.

Migrate using a release flow

You can handle a migration with a release flow by [creating and populating a pipeline](create-a-pipeline-and-release-flow) with your relevant deployments and database addons.

You can then [configure a release flow](configure-a-release-flow) to automate the various steps of your release workflow.

You could create, for example, a sequential workflow that backs up the database, executes your migration, and then promotes the deployment. The migration could be executed by using a job node to run a job with your migration code, or by using an action node to execute a command in a running container.

![An example release flow to run a migration in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/run-migrations/release-flow-migration.png)

Migrate using a job triggered by CI

You can run a migration automatically by configuring a job to run whenever a new build is completed.

You can:

  * build directly from the same repository and branch as the deployment that requires migration, with CI and CD enabled on the job
  * deploy an image from a [build service](../build/build-code-from-a-git-repository) that also builds the image for your deployment service, with CD enabled



Create a new manual job with the source for your migration code, either from a repository or a build service. Enable `run on image change` on your job, select `CD & pipeline promotion` or `always`, depending on your desired workflow.

Enter any necessary configuration details to run your migration, for example a [command override](../run/override-command-entrypoint) if your migration code needs to be called with a command other than the default.

Your job will now execute when your latest commit to the repository is built, so your migration should occur at the same time as your new deployment. You can check the [logs](../observe/view-logs) for the job run to ensure it has executed successfully.

![Configuration settings for a job in the Northflank application to run a migration when a new build is available](https://assets.northflank.com/documentation/v1/application/release/run-migrations/ci-job-migrate.png)

Migrate using command override

You can run a migration using [command override](../run/override-command-entrypoint#override-command) to execute the migration code when deploying your latest commit. This allows you to chain commands to run a migration and then start your application whenever it is redeployed.

Your deployment will begin redeploying as soon as you save the custom command.

### Enter command manually

    
    
    ## Run migration, then start the server
    bin/sh -c "node migrate/migration-code.js; node built/server.js"
    
    ## Run migration, then start the server if it is successful (migration process returns exit code 0)
    bin/sh -c "node migrate/migration-code.js && node built/server.js"
    

### Use a script or process

If you have added a script containing your migration command, for example in `package.json` for node-based applications or `Pipfile` for Python applications using Pipenv, you can include this in the command override. If you are building your application with buildpacks you can [add a process to your Procfile](../run/override-command-entrypoint#buildpack-processes) and select `custom process` in the runtime mode.
    
    
    yarn migrate-and-run
    

![An example command override in the Northflank application for a service to run a migration for Rails in a deployment service](https://assets.northflank.com/documentation/v1/application/release/run-migrations/cmd-override-migrate.png)

Migrate by executing a shell command

You can manually [execute commands](../run/access-running-containers-locally#execute-commands-in-a-container) in a running workload by accessing the shell from the Northflank application, or by using the [Northflank CLI or JS client](../../api/execute-command).

Navigate to your deployment and ensure the commit with your migration is deployed. Open a shell for a running container and enter the command to run your migration.

![An example command in a container shell in the Northflank application for a service to run a migration for Django in a deployment service](https://assets.northflank.com/documentation/v1/application/release/run-migrations/shell-migrate.png)

Common migration commands

You can write your own migrations and run them either embedded in your application, or as separate processes using command override or via a container shell.

### Node

You can run migrations on Node using tools like [Knex ](https://knexjs.org/guide/migrations.html), [Prisma ](https://www.prisma.io/docs/concepts/components/prisma-migrate/migrate-development-production), [db-migrate ](https://db-migrate.readthedocs.io/en/latest/), and [Sequelize ](https://sequelize.org/docs/v6/other-topics/migrations/).
    
    
    ## Knex
    knex migrate:latest
    
    ## Prisma (in production)
    npx prisma migrate deploy
    
    ## db-migrate
    db-migrate up
    
    ## Sequelize
    npx sequelize-cli db:migrate
    

### Ruby on Rails

You can use the following commands to run a migration, either as a command in a running container, as a command override to start a deployment or job, or as a process (for example in a Procfile):
    
    
    bin/rails db:migrate
    ## or
    bundle exec rails db:migrate
    

While `bin/rails` will work in both running deployments and as a runtime command or command override, `bundle exec rails` may be more reliable as a command for starting jobs. You can specify the migration to run as a command argument (`VERSION=<version-number>`), or as an environment variable with the key `VERSION`.

[Learn more about creating and running migrations in Rails ](https://guides.rubyonrails.org/active_record_migrations.html).

### Flask

You can run migrations using Flask extensions such as [Flask-Alembic ](https://flask-alembic.readthedocs.io/) or [Flask-Migrate ](https://flask-migrate.readthedocs.io/en/latest/).

Migrations can be run for these extensions using:
    
    
    ## flask-alembic
    alembic upgrade head
    
    ## flask-migrate
    flask db upgrade
    

### Django

Django has built-in support for [creating and running migrations. ](https://docs.djangoproject.com/en/4.1/topics/migrations/)
    
    
    python manage.py migrate
    

### Laravel

You can run [migrations in Laravel ](https://laravel.com/docs/11.x/migrations) using artisan:
    
    
    php artisan migrate
    

### Rust

You can run migrations in Rust via the command line with Crates for toolkits such as [SQLx ](https://crates.io/crates/sqlx-cli), [Refinery ](https://crates.io/crates/refinery_cli), and [Diesel ](https://crates.io/crates/diesel_cli).
    
    
    ## sqlx
    sqlx migrate run
    
    ## refinery
    refinery migrate -e ${DB_URI} -p ./sql_migrations
    
    ## diesel
    diesel migration run
    

Learn more

[Configure a release flowLearn how to use the visual editor or code to configure a release flow.](/docs/v1/application/release/configure-a-release-flow)[Run an image once or on a scheduleRun an image manually or on a cron schedule.](/docs/v1/application/run/run-an-image-once-or-on-a-schedule)[Override command or entrypointOverride the default command or entrypoint instructions for your application.](/docs/v1/application/run/override-command-entrypoint)[Execute commands in your workloadsAccess the shell for your running workloads or send commands to execute using the UI, CLI, API, or JavaScript client.](/docs/v1/api/execute-command)