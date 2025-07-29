---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/deploy-a-database#available-databases
title: Deploy a database | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-29T10:44:49.060374
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Deploy a database

To deploy a new database in your project, create a new addon and select the type and version you require. Please note that while you can increase the storage size or replica count of databases after creation, you cannot decrease them.

After creating your addon it may take a few minutes to provision resources and set up a default configuration, after which its status will change to running.

Your database will be accessible by workloads within the same project using the provided [connection details](./connect-database-secrets-to-workloads).

[Click here ](https://app.northflank.com/s/project/create/addon) to deploy an addon.

![Creating a MongoDB addon in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/deploy-a-database/create-addon.png)

Available databases

Addon| Versions| Description| Backups| TLS  
---|---|---|---|---  
[MongoDB ](https://www.mongodb.com/docs/manual/)| 8.0.10, 8.0.3, 7.0.21, 7.0.15, 6.0.24, 6.0.13, 5.0.31, 5.0.24, 4.4.15, 4.2.21| MongoDB® is a document-oriented database program that uses JSON-like documents with schema.| Native or disk| Yes  
[Redis ](https://redis.io/)| 7.2.4, 6.2.14| Redis® implements a distributed, in-memory key-value database with optional durability.| Disk| Yes  
[MySQL ](https://www.mysql.com/)| 9.0.1, 8.4.3, 8.0.40| MySQL is a fast, reliable, scalable, and easy to use open-source relational database system.| Native or disk| Yes (cannot be changed after creation)  
[PostgreSQL ](https://www.postgresql.org/)| 17, 16, 15, 14, 13, 12| PostgreSQL is a free and open-source relational database management system. High availability with Patroni| Native or disk| Yes  
[MinIO ](https://min.io/)| 2024.1.31| MinIO® is a High Performance Object Storage with an Amazon S3 cloud storage service compatible API.| Disk| Yes  
[RabbitMQ ](https://www.rabbitmq.com/)| 4.0.5, 3.13.7, 3.12.14| RabbitMQ is an open source message broker software that implements the Advanced Message Queuing Protocol (AMQP).| Disk| Yes  
  
Advanced configuration

You can configure advanced options for addons, such as [backup schedules](backup-restore-and-import-data#schedule-backups) and custom database names. You can also fork databases from addons with existing backups.

See the deployment guides for addon-specific configuration options.

Next steps

[Deploy MongoDB® on NorthflankMongoDB is a document-oriented database program that uses JSON-like documents with schema.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-mongodb-on-northflank)[Deploy PostgreSQL on NorthflankPostgreSQL, also known as Postgres, is a free and open-source relational database management system.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-postgresql-on-northflank)[Deploy MySQL on NorthflankMySQL is a fast, reliable, scalable, and easy to use open-source relational database system.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-mysql-on-northflank)[Deploy Redis® on NorthflankRedis implements a distributed, in-memory key-value database with optional durability.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-redis-on-northflank)[Deploy MinIO® on NorthflankMinIO is a High Performance Object Storage with an Amazon S3 cloud storage service compatible API.](/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-minio-on-northflank)