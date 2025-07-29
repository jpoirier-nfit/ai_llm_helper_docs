---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability
title: Configure addons for high availability | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.293927
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Configure addons for high availability

Northflank implements several features to ensure high availability (HA) of your [addons](stateful-workloads-on-northflank) in the event a replica becomes unavailable. You can configure both your addon and your application to maximise your uptime.

### Multiple replicas

You can scale addons on Northflank to deploy multiple replicas. Deploying multiple replicas helps you ensure that your data will be accessible even if the primary replica is inaccessible.

An addon with multiple replicas either consists of:

  * a primary read-write replica with secondary read replicas that maintain a copy of the data on the primary replica. Primary replicas can handle any read-write connections, while read-only replicas can only handle read connections.
  * a sharded distribution, where data is replicated across multiple replicas, but each replica may not contain the full dataset



How an addon manages additional replicas, and replica failures, depends on the type of addon deployed. With automated failover, a secondary replica will be promoted to a primary using a failure detection mechanism. This means that after a primary failure, writes are typically available again within less than 30 seconds. For addons which don’t support automated failover, it can take several minutes until the primary replica is restarted and available again. In the severe case of a complete failure of the primary replica (such as disk failure) write downtime can be longer as the primary needs to be recovered manually.

Addon| Replication strategy| Failover strategy  
---|---|---  
PostgreSQL| Primary-secondary| Automated failover: a read replica is promoted to primary  
MongoDB®| Primary-secondary| Automated failover: a read replica is promoted to primary  
MySQL| Primary-secondary| Read-only: writes unavailable until primary replica is replaced  
Redis®| Primary-secondary| Read-only: writes unavailable until primary replica is replaced OR Automated failover if deployed with Sentinel  
MinIO®| Sharding| Damaged data is restored using healthy shards, failing replicas will be replaced  
RabbitMQ (quorum queue)| Primary-secondary| Automated failover: a queue follower is promoted to leader  
RabbitMQ (streams)| Sharding| Streams are available as long as a quorum of replicas is available, failing replicas will be replaced  
  
### Read-only connection strings

Some addons provide separate read-only connection strings. You can configure your application to use separate connection strings for read operations, which will allow your application to still read data when write requests cannot be processed.

Methods to set up your application to use an addon with high-availability vary depending on which client you use in your application. You could, for example, implement separate read and write clients and select the appropriate client depending on your query. Alternatively, you could use the connection string containing both primary and read replicas, and fall back to a read-only client if a read fails. Consider the importance of write operations for your application and plan how to gracefully handle unavailability.

If your application is read-intensive, it is best to use read-only connection strings to keep the primary replica free for write operations.

You can read specific information below on how to use read-only connection strings for each type of addon.

### Upgrades and maintenance

[Major upgrades](upgrade-a-database) can cause some downtime for an addon, but can also potentially introduce breaking changes between your addon and your application.

For major upgrades we recommend [forking your addon](fork-an-addon), upgrade the forked addon, and then connecting a development version of your application to the upgraded addon. This allows you to test and verify proper functionality before running the upgrade on your production addon.

Having a [snapshot](backup-restore-and-import-data#types-of-backup) of your data before running a major upgrade also allows you to create a forked addon of the previous version, if you find that you need to revert to the older version.

### Deploy with zonal redundancy

Your addon will be deployed to your [project's region](../run/deploy-to-a-region). Each region may have multiple availability zones, which are data centers with independent infrastructure such as networking, power supply and cooling within the region. Some regions, however, do not have more than one availability zone.

Normally your addon replicas will be provisioned in the same availability zone, but you can enable zonal redundancy to provision replicas across multiple availability zones.

This will ensure that your addon remains available in the event that one zone fails, however networking between replicas in different zones will be slightly slower compared to replicas provisioned in the same availability zone. Replicas will be bound to the zone they are deployed in.

PostgreSQL

Northflank's PostgreSQL addon offers automated failover to replace failed primary replicas and the option to add connection poolers.

#### Automated failover

Northflank uses [Patroni ](https://github.com/zalando/patroni) for automated PostgreSQL failover. If a primary replica becomes unavailable due to a failure or scheduled maintenance, a read replica will be promoted to primary, allowing read-write operations to continue. The old primary replica will become a new read replica when it is restarted.

The addon provides two connection strings, a primary for read/write operations, and a secondary that directs to read replicas for read-only operations.

#### Connection pooler

Northflank uses [PgBouncer ](https://www.pgbouncer.org/) to provider connection poolers for PostgreSQL addons. You can enable connection poolers to improve performance for workloads which frequently create large numbers of database connections. Opening a connection is a relatively resource-intensive action and a pooler can reduce this overhead by keeping a pool of reusable connections open.

For high-availability applications you should deploy at least 2 connection pooler instances per type of connection to provide redundancy in the event that one pooler instance becomes unavailable.

You can add connection poolers to a PostgreSQL addon by configuring them under `advanced resource options` during creation, or on the resources page for an existing addon. You can configure primary and read connection poolers separately, so you can deploy more of one type depending on whether your application will be more read or write intensive.

![Connection poolers deployed for a PostgreSQL addon in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/configure-addons-for-high-availability/postgressql-connection-poolers.png)

Northflank will automatically begin routing connections through a pooler when they become available, using the same connection details as before.

Using the connection pooler also increases the maximum number of connections, limited by the amount of memory available:

Memory available| Maximum connections  
---|---  
256MB| 64  
512MB| 96  
1024MB| 124  
2048MB| 256  
4096MB| 1024  
8192MB| 2048  
16384MB| 4096  
32768MB| 8192  
65536MB| 16384  
  
MongoDB

You can scale MongoDB to multiple replicas. The primary replica will handle read/write operations, and secondary replicas will replicate all operations on the primary to maintain an identical data set. If a primary replica fails, a secondary replica will automatically be promoted to primary.

You can configure your [read preference ](https://www.mongodb.com/docs/manual/core/read-preference/) in your MongoDB client to favour the primary replica or secondary replicas for read operations. Setting your preference to `secondaryPreferred`, for example, would first attempt to read from secondary replicas and fall back to the primary, which would reduce load on the primary replica and free it up for write operations.

MySQL

When you scale a MySQL addon, new read replicas of the database are added. New read replica secrets are also added to the connection details for the addon. The read replica connection is added to each connection string, as well as a separate `HOST_READ` secret.

In the event a primary replica becomes unavailable writes will be blocked, and only read operations will be available. Write operations will be available when the primary replica becomes available again.

You can configure your application to make use of the read replica connections to ensure your application can still read data. You can, for example, implement handling in your application to use a separate read connection for read operations only, or fall back to a read-only connection if the primary becomes unavailable.

Redis

When you scale a Redis addon, new read replicas of the database are added. New read replica secrets are also added to the connection details for the addon.

A `REDIS_SLAVE_URL` is added to the connection details, to connect to the read replicas, and the `REDIS_MASTER_URL` remains unchanged.

In the event a primary replica becomes unavailable writes will be blocked, and only read operations will be available. Write operations will be available when the primary replica becomes available again, within 1-2 minutes.

### Redis Sentinel

#### Deploy Redis with Sentinel

When you create a Redis addon you can enable Sentinel, which will trigger automated failover in case of an instance failure.

An additional Sentinel process will be deployed with each of your Redis instances to monitor their health. This requires a minimum of 3 Redis replicas to be deployed in order to reach consensus. The Sentinel processes will also incur compute costs, which can be seen in the cost breakdown in resources.

Sentinel can only be enabled on addon creation, and cannot be disabled after creation. To use Sentinel with an existing Redis addon, you can [create a fork](fork-an-addon) from an existing Redis addon, or [use another migration strategy](migrate-data-to-northflank/migrate-your-redis-deployment-to-northflank) and configure your application to use the new addon.

#### Use Redis Sentinel

Deploying Redis with Sentinel will remove the `MASTER` and `SLAVE` connection details. You should use the `HOST_SENTINEL` and `PORT_SENTINEL` details to connect instead. The [client library ](https://redis.io/resources/libraries/) you use to access Redis in your application will need to support Sentinel.

If your application is read-heavy you can configure your Redis client to prioritise read replicas, or load-balance across all replicas, for read connections.

You can use [CLI commands and the Sentinel API ](https://redis.io/docs/management/sentinel/#sentinel-api) to monitor your Redis instances. The `SENTINEL_GET_MASTER_COMMAND` CLI command will fetch the current Redis master, and should be used if you require a write connection.

MinIO

To ensure high-availability access you must create your MinIO addon with multiple replicas, as it cannot be horizontally scaled afterwards. You do not need to configure any special handling in your application, and MinIO will use an [erasure coding algorithm ](https://min.io/docs/minio/linux/operations/concepts/erasure-coding.html) to continue read/write operations even when half the configured replicas are unavailable.

RabbitMQ

RabbitMQ addons have two options for configuring high-availability: quorum queues and streams.

#### Quorum queues

If you scale RabbitMQ to multiple replicas you can configure it to use a [quorum queue ](https://www.rabbitmq.com/quorum-queues.html), a durable, replicated, first-in-first-out queue, rather than the classic queue type. This ensures your RabbitMQ addon will be highly available and fault-tolerant.

You can create a quorum queue by creating a queue with the type `quorum`, which requires the RabbitMQ addon to be scaled to three or more replicas (odd numbers of replicas are best for quorum queues). One of the replicas will be the queue leader, and if the queue leader becomes unavailable, another replica will be selected as the leader. When a replica comes back online it will resynchronise with the leader, which does not affect the queue's availability.

#### Streams

[Streams ](https://www.rabbitmq.com/streams.html) are an alternative option to quorum queues, and are more suitable for use-cases which require replicated, persistent messages.

You can declare a stream by setting the queue type to `stream`, however you will need to contact [[support@northflank.com](mailto:support@northflank.com)](mailto:support@northflank.com) to enable the stream plugin first.

Next steps

[Upgrade a databaseUpgrade your database to a newer version with one click.](/docs/v1/application/databases-and-persistence/upgrade-a-database)[Backup, restore, and import your dataCreate and import backups of your database, or restore from an existing backup.](/docs/v1/application/databases-and-persistence/backup-restore-and-import-data)