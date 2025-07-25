---
source_url: https://northflank.com/docs/v1/application/production-workloads/persistent-storage-in-production
title: Persistent storage in production | Production Workloads | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.090778
watsonmd_version: 0.1.0
---

Production Workloads / 

# Persistent storage in production

You can deploy many of the most popular databases on Northflank with one click, and enjoy a fully-managed experience for upgrading, scaling, and administering your persistent storage.

You can check the [available types of Northflank addon here](../databases-and-persistence/deploy-a-database#available-databases).

Using Northflank’s database as a service option allows you to easily:

  * Deploy in one click with minimal configuration
  * Dynamically import connection details to workloads
  * Access securely with TLS, private networking, or expose to the internet
  * Import data from a live database or dump file
  * Create a backup schedule or create manual backups
  * Restore from a backup
  * Scale vertically and horizontally
  * Upgrade version
  * Access metrics and receive alerts about your database



If you need to run a workload with persistent storage and have a use-case not covered by any available addons, you can create a persistent volume attached to a deployment. However, this comes with several limitations, and you are recommended to use Northflank addons wherever possible.

Import your production data

You can import your production data after creating an addon, the exact method depends on the type of addon.

For PostgreSQL, MongoDB, and MySQL you can import your data from either a dump backup of your database, or by providing a connection string to your live database.

You can only import one database by uploading a dump file, which will become the default database for the Northflank addon. Importing via connection string will allow you to import multiple databases.

Other addons have different methods to import data, such as command-line tools or web interfaces, which are detailed in their specific guides.

### Learn more

[Migrate PostgreSQL to NorthflankImport your PostgreSQL database to Northflank by uploading a dump, or providing a connection string to a running PostgreSQL instance.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-postgresql-database-to-northflank)[Migrate MongoDB® to NorthflankImport your MongoDB data to Northflank by uploading a dump, or providing a connection string to a running MongoDB instance.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-mongodb-database-to-northflank)[Migrate MySQL to NorthflankImport your MySQL database to Northflank by uploading a dump, or provide a connection string to a running MySQL instance.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-mysql-database-to-northflank)[Migrate S3 storage to NorthflankConfigure live replication of your existing MinIO® instance, or transfer files from S3-compatible storage to Northflank.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-minio-deployment-to-northflank)[Migrate Redis® to NorthflankImport a snapshot of your Redis keystore, or configure live replication to migrate without interruption.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-redis-deployment-to-northflank)[Migrate RabbitMQ to NorthflankImport your RabbitMQ definitions to run your message broker with the same configuration on Northflank.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-rabbitmq-deployment-to-northflank)

Configure networking for your database

You can configure network settings to change where you can access your addon: from within your project only, from within your project and your local machine only, or publicly available on the internet.

By default, your addon will have TLS enabled, and will only be accessible within your Northflank project.

You can enable or disable TLS for addons, depending on your application’s requirements. The TLS status will be reflected in the connection detail `TLS_ENABLED`.

## Forward your addon for local access

You can securely forward your addon to your local machine to access and administer your database while it remains otherwise inaccessible over the internet. Forwarding establishes a secure connection between your local machine and the addon via a Northflank proxy.

You can forward an addon, and other Northflank resources, using the Northflank CLI. You can copy the specific forward command from your addon’s overview, in the local access section.

## Publicly expose an addon

You may need to make an addon available over the public internet, for example to connect external services, where forwarding is insufficient.

You can make an addon publicly accessible from the network settings page, which requires TLS to be enabled. Making an addon publicly accessible will add new connection strings which can be used to connect to the addon over the public internet.

If you expose an addon in this method you are advised to add security rules to restrict external ingress traffic to the specified IP addresses.

### Learn more

[Access a databaseSecurely access your database locally or make it available online.](/docs/v1/application/databases-and-persistence/access-a-database)[NetworkingConfigure public and private ports for your Northflank workloads, and add security with IP policies and basic authentication.](/docs/v1/application/network/networking-on-northflank)

Connect your addon to production workloads

The best way to connect your addon is by providing the relevant connection details to your application via environment variables.

You can do this by linking the addon to a secret group, which will make the connection details available automatically throughout your project or the scoped resources. This also has the benefit of automatically updating any connection details that are passed to your application if they change, for example if you scale your addon to more replicas.

Alternatively you can manually add the relevant secrets to individual services or jobs on their environment variables page.

To access an addon in your build process, it must be [publicly exposed](../databases-and-persistence/connect-database-secrets-to-workloads#access-a-database-in-a-build).

### Learn more

[Use a database with your applicationsSecurely access your database in your project's applications and services.](/docs/v1/application/databases-and-persistence/connect-database-secrets-to-workloads)[Manage groups of secretsCreate and manage groups of secrets that can be inherited throughout an entire project or by specific services and jobs.](/docs/v1/application/secure/manage-secret-groups)

Configure your addon for high availability

You can configure your Northflank addons for high availability to remove or reduce downtime incurred from adding more replicas, updating your addon’s version, or from issues with replicas. Restoring data to an addon will always lead to some downtime, which depends on the size of the backup you are restoring from.

Each addon behaves differently when multiple replicas are added, but by configuring at least two replicas you can minimise the amount of downtime your production workloads will experience. By using the only read replicas to read data, you can also reduce the load on the primary replica and ensure it is always available to handle writes.

You may need to configure your application to make use of separate read replica connection details, or configure your addon to work with multiple replicas.

### Learn more

[Configure addons for high availabilityConfigure your addons to maximise availability.](/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability)[Configure your deployments for zero downtimeConfigure your production workloads to run with high availability.](/docs/v1/application/production-workloads/release-for-production#configure-your-deployments-for-zero-downtime)

Backup and restore your data

You can ensure that your data is securely backed up on Northflank by either running manual backups, or creating a backup schedule. You can create either native dump backups, which can also be downloaded, or take a disk snapshot of the addon storage. Native backups are not available for all types of addon.

Native backups will always back up the whole database which can require a large number of read operations for databases with more records, which can increase addon resource usage for some time. Native backup dumps can also be downloaded, so that you can back your data up to another location.

Disk snapshots initially save a copy of the entire addon storage, but subsequent backups only record changes since the last snapshot (changes will be propagated to the next backup if an older backup is deleted). This makes snapshots much faster than dump backups, and they can use less storage space than native backups. Snapshots can also be used to create new addons with the data pre-provisioned, but they cannot be downloaded.

## Schedule backups

Scheduled backups are the best way to ensure your data is regularly saved.

You can create hourly, daily, and weekly backup schedules with different configurations to suit your needs. You could create an hourly disk snapshot backup schedule with a short retention time to be able to restore your data if you encounter an issue, and a weekly native backup schedule with a longer retention period to store data for regulatory purposes.

The retention time you select determines how long the backup will be kept on Northflank. A shorter retention time for hourly and daily backup schedule would make sense, as it reduces storage costs, and longer retention times can be used for weekly backups to ensure data is available in the long term.

## Export backups

It is a good idea to export backups on a regular basis, whether that is to your own storage or a third-party storage service, for disaster recovery and to meet any legal and regulatory requirements you may be subject to.

You can manually download native backups from the backup page, or create a [job](../run/run-an-image-once-or-on-a-schedule) which uses the [Northflank API](../../api/introduction) to trigger a backup, and then automatically download the backup and transfer it to another storage service when it is completed.

## Restore data

You can restore from native dump backups or disk snapshots created in the addon, or import dump backups to restore from.

Importing a dump allows you to migrate your data from another database, restore data from a different Northflank addon, or restore from a backup that you downloaded but is no longer available on Northflank after the retention period has expired.

### Learn more

[Backup, restore, and import your dataCreate and import backups of your database, or restore from an existing backup.](/docs/v1/application/databases-and-persistence/backup-restore-and-import-data)

Run a migration

You can run a migration, or perform other jobs on a database, by connecting either in the build stage, or by running your migration as a job or service.

If you want to connect to an addon in your build stage, you must use external connection details and publicly expose your addon, as builds are run on separate, dedicated infrastructure.

### Learn more

[Run migrationsRun database migrations and update your deployments simultaneously when you update your schema.](/docs/v1/application/release/run-migrations)[Link connection details to groupUse your database in your application by linking it to a secret group.](/docs/v1/application/databases-and-persistence/connect-database-secrets-to-workloads)

Fork an addon

You can fork an existing addon to create a duplicate for development and testing purposes. For example, you may want to test a migration for a specific customer before running it in production, or test your application works with newer version of the addon.

You can create a fork of an addon that contains a disk snapshot backup when creating a new addon of the same type and version. Forking is only available for some addons.

### Learn more

[Fork an addonFork an addon to create an exact duplicate of your existing database.](/docs/v1/application/databases-and-persistence/fork-an-addon)

Upgrade an addon

Upgrades are fully managed by Northflank, and new versions of addons are regularly made available. You will receive a notification in the Northflank application if your addon can be upgraded, or if your current version is deprecated.

You should endeavour to keep your addon versions up to date as part of a regular maintenance schedule to make sure bugs and security vulnerabilities have been patched.

Northflank will always ensure there is a valid upgrade path from your current version to the latest available version, but addon versions cannot be downgraded. You can fork an addon before upgrading to ensure you can revert to a previous version.

### Learn more

[Upgrade a databaseUpgrade your database to a newer version with one click.](/docs/v1/application/databases-and-persistence/upgrade-a-database)

Connect to an external service

You may choose to use an external service to manage your data, such as [MongoDB Atlas ](https://www.mongodb.com/atlas), [Amazon RDS ](https://aws.amazon.com/rds/), or [Upstash ](https://upstash.com/), if you have existing relationships with these providers or require more features and database-specific support.

You can add the connection details for these external services to a secret group, or directly in the environment variable of your services and jobs, as you would for a Northflank addon.

You may be required to provide the IP address for your Northflank services to your external service provider. If you would like to discuss creating a static egress IP address for your team, contact [[support@northflank.com](mailto:support@northflank.com)](mailto:support@northflank.com).

Add a persistent volume

If no Northflank addons or external services are suitable for your needs you can create persistent volumes to attach to your service. Persistent volumes are not a recommended solution as they limit your service to 1 instance, meaning you cannot configure your application for zero downtime.

### Learn more

[Add a persistent volumeAdd persistent volumes to your deployments.](/docs/v1/application/databases-and-persistence/add-a-volume)