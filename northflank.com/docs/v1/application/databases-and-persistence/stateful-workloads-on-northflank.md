---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/stateful-workloads-on-northflank
title: Stateful workloads on Northflank | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.243635
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Stateful workloads on Northflank

You can add persistence to your services deployed on Northflank by creating database, storage, or message queue addons and connecting to them in your running services.

Persistent databases and storage allow your applications to restart or deploy new versions without losing important data, such as registered users or uploaded content.

You can back up your data and expose addons using TLS. Check the [features](./deploy-a-database#available-databases) for databases and storage addons to make sure they offer the features you require.

Deploy an addon

Learn how to deploy an addon, or read guides for specific addons on Northflank.

Managed addons offer backups, upgrades, and high-availability options.

[Deploy a databaseCreate a database to use with your Northflank deployments.](/docs/v1/application/databases-and-persistence/deploy-a-database)[Deploy MongoDB® on NorthflankMongoDB is a document-oriented database program that uses JSON-like documents with schema.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-mongodb-on-northflank)[Deploy PostgreSQL on NorthflankPostgreSQL, also known as Postgres, is a free and open-source relational database management system.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-postgresql-on-northflank)[Deploy MySQL on NorthflankMySQL is a fast, reliable, scalable, and easy to use open-source relational database system.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-mysql-on-northflank)[Deploy Redis® on NorthflankRedis implements a distributed, in-memory key-value database with optional durability.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-redis-on-northflank)[Deploy MinIO® on NorthflankMinIO is a High Performance Object Storage with an Amazon S3 cloud storage service compatible API.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-minio-on-northflank)[Deploy RabbitMQ on NorthflankRabbitMQ is a lightweight, easy to deploy, open-source message broker that supports multiple messaging protocols.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-rabbitmq-on-northflank)

Back up and migrate your data

Back up your data, fork addons with existing data, and migrate your data from other platforms to Northflank.

[Backup, restore, and import your dataCreate and import backups of your database, or restore from an existing backup.](/docs/v1/application/databases-and-persistence/backup-restore-and-import-data)[Fork an addonFork an addon to create an exact duplicate of your existing database.](/docs/v1/application/databases-and-persistence/fork-an-addon)[Migrate PostgreSQL to NorthflankImport your PostgreSQL database to Northflank by uploading a dump, or providing a connection string to a running PostgreSQL instance.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-postgresql-database-to-northflank)[Migrate MongoDB® to NorthflankImport your MongoDB data to Northflank by uploading a dump, or providing a connection string to a running MongoDB instance.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-mongodb-database-to-northflank)[Migrate MySQL to NorthflankImport your MySQL database to Northflank by uploading a dump, or provide a connection string to a running MySQL instance.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-mysql-database-to-northflank)[Migrate S3 storage to NorthflankConfigure live replication of your existing MinIO® instance, or transfer files from S3-compatible storage to Northflank.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-minio-deployment-to-northflank)[Migrate Redis® to NorthflankImport a snapshot of your Redis keystore, or configure live replication to migrate without interruption.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-redis-deployment-to-northflank)[Migrate RabbitMQ to NorthflankImport your RabbitMQ definitions to run your message broker with the same configuration on Northflank.](/docs/v1/application/databases-and-persistence/migrate-data-to-northflank/migrate-your-rabbitmq-deployment-to-northflank)

Use an addon

Connect your addon to your deployments on Northflank, and access your addon with management tools.

You can also securely forward an addon to your local machine for development and management.

[Use a database with your applicationsSecurely access your database in your project's applications and services.](/docs/v1/application/databases-and-persistence/connect-database-secrets-to-workloads)[Access a databaseSecurely access your database locally or make it available online.](/docs/v1/application/databases-and-persistence/access-a-database)[Connect to an Addon with TLSEnsure your service or job can connect to an addon using TLS.](/docs/v1/application/databases-and-persistence/access-a-database#access-tls-certificates-in-containers)

Monitor and manage an addon

Monitor your addons and scale them to meet demand. Add replicas and deploy features for high-availability applications. Upgrade your addons to access new features and remain secure.

[Observe a databaseMonitor the health and view logs of your running databases, and view the status of backups and upgrades.](/docs/v1/application/databases-and-persistence/database-observability-and-monitoring)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)[Configure addons for high availabilityConfigure your addons to maximise availability.](/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability)[Upgrade a databaseUpgrade your database to a newer version with one click.](/docs/v1/application/databases-and-persistence/upgrade-a-database)

Use persistent volumes and create custom addons

As well as Northflank's managed addons, you can add persistent volumes to services that require other storage solutions.

You can also create custom addons for your team to use in clusters hosted on your own cloud provider account.

[Add a persistent volumeAdd persistent volumes to your deployments.](/docs/v1/application/databases-and-persistence/add-a-volume)[Create a custom addon typeCreate your own addon types for your team to deploy using a Helm chart.](/docs/v1/application/databases-and-persistence/create-a-custom-addon-type)

Integrate with other providers

You can access data or storage hosted on another provider on Northflank by providing connection details. You can also access resources on your private network by adding Tailscale to your Northflank project.

[Use MongoDB® Atlas on NorthflankConnect your MongoDB® Atlas cluster to applications on Northflank.](/docs/v1/application/databases-and-persistence/integrate-with-a-database-provider/integrate-mongodb-atlas-with-northflank)[Use TailscaleAllow secure access to Tailscale devices to resources within your project.](/docs/v1/application/network/use-tailscale)