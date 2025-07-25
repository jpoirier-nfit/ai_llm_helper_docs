---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-postgresql-on-northflank
title: Deploy PostgreSQL on Northflank | Deploy Databases On Northflank | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.377408
watsonmd_version: 0.1.0
---

Databases And Persistence / Deploy Databases On Northflank / 

# Deploy PostgreSQL on Northflank

This guide explains how to quickly and easily deploy and use [PostgreSQL ](https://www.postgresql.org/) on Northflank.

Available versions| Description| Backups| TLS  
---|---|---|---  
17, 16, 15, 14, 13, 12| PostgreSQL is a free and open-source relational database management system. High availability with Patroni| Native or disk| Yes  
  
Deploy PostgreSQL

  1. [Click here to create an addon ](https://app.northflank.com/s/project/create/addon), or choose `addon` from the create new menu in the top right corner of the dashboard
  2. Select `PostgreSQL` and enter a name

  3. Choose a `version` or leave as default (most recent version)

  4. Choose whether to [deploy with TLS](../connect-database-secrets-to-workloads#enable-tls). This can be changed later.

  5. Choose whether to make the database `publicly accessible`. This will give your addon a URL and make it available online. TLS must be enabled to select this.

  6. If you have [secret groups](../../secure/manage-secret-groups) in your project, choose ones to [link to the addon](../connect-database-secrets-to-workloads#link-database-secrets-to-a-secret-group) so that the database can be used in services and jobs that inherit variables from the secret group. To link the database to a secret group:

     * `Show secret groups` and `configure` the secret groups you wish to use
     * `Select suggested` secrets from the database to link, or `select all`
     * Set any required `aliases` for specific secrets to make them accessible by that name within your application
  7. Select the required [resources](../scale-a-database) for your database. You can scale the database after creation, but available storage and replicas cannot be decreased once increased.

  8. `Create addon` and PostgreSQL will begin provisioning, this may take a few minutes.



Advanced options

PostgreSQL has the following advanced options available when creating your addon.

### Fork existing addon

You can create your new addon as a [fork from an existing addon](../fork-an-addon).

This will copy all data, including database names and users, from the selected backup of the source addon to your new addon during creation.

The newly forked addon may have a newer minor version than the source backup, but must have the same major version.

### Custom database name

The default database name is a randomly-generated string, and is used in connection details to access the addon. If your application expects a specific database name it can be useful to change it.

You can set a custom name for the default database created in your addon by entering one in advanced options. The name cannot be changed after creation.

If you are [forking from an existing addon](../fork-an-addon), it will use the name of the default database from the source addon.

### Write-Ahead Logging (WAL)

You can set the [wal_level ](https://www.postgresql.org/docs/current/runtime-config-wal.html#GUC-WAL-LEVEL) to either `replica` (default) or `logical`. This cannot be changed after creation. Setting the WAL to `Logical` will incur more usage for vCPU, networking, and disk space compared to `replica`.

### Deploy with zonal redundancy

Your addon will be deployed to your [project's region](../../run/deploy-to-a-region). Each region may have multiple availability zones, which are data centers with independent infrastructure such as networking, power supply and cooling within the region. Some regions, however, do not have more than one availability zone.

Normally your addon replicas will be provisioned in the same availability zone, but you can enable zonal redundancy to provision replicas across multiple availability zones.

This will ensure that your addon remains available in the event that one zone fails, however networking between replicas in different zones will be slightly slower compared to replicas provisioned in the same availability zone. Replicas will be bound to the zone they are deployed in.

### Backup schedules

You can [add backup schedules](../backup-restore-and-import-data#schedule-backups) when creating your addon. Backups of the addon will be taken according to the schedules.

Connect to PostgreSQL

You can manually copy the connection secrets for your PostgreSQL database from the connection details page into runtime variables or build arguments of your workloads on Northflank.

However, it is much easier to link your database's connection details to a new or existing [secret group](../connect-database-secrets-to-workloads#link-database-secrets-to-a-secret-group).

The necessary secrets to connect your workload will vary depending on the application in your workload.

Some clients may use a [connection string ](https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING), while some clients may not support the connection string URI format.

The connection string takes the format `postgresql://[username:password@][host][:port][/database][...options]`. The `POSTGRES_URI` and `JDBC_POSTGRES_URI` (for Java applications using JDBC) connection strings will be automatically configured for your database.

You can supply connections details and secrets such as `host`, `username`, `password`, and `port` to your workload if your application is configured to use these instead of a connection string.

### Available ports

Internal port| External port| Protocol| URI prefix  
---|---|---|---  
5432| Dynamically generated| PostgreSQL| `postgresql://`  
  
If you create more than one replica, read replicas will have the `read` prefixes in place of the `primary` prefix for the primary replica.

### Automatically inherit database connection details into your workload

  1. Create a new [secret group](../../secure/manage-secret-groups) of `runtime` variables to connect in the running workload
  2. `Show addons` and `configure` your addon with either the `POSTGRES_URI` or `JDBC_POSTGRES_URI` connection string, or select connection details and secrets
  3. Set the aliases required in your workload to access the secrets
  4. Enable `apply secrets to specific services/jobs` and select the workloads you want to access the database
  5. `Create secret group`
  6. Go to one of the workloads that inherits from the group and check the environment page, you should see the inherited variables from the secret group



The connection string or secrets will now be available in your workload under the configured aliases, and your application will be able to connect to the database using them.

Access PostgreSQL

You can access your PostgreSQL addon using the relevant connection string, or by using the `HOST`, `PORT`, `USERNAME` and `PASSWORD` secrets found in the connection details page of the addon.

You can connect using the [psql interactive terminal ](https://www.postgresql.org/docs/current/app-psql.html), or via a GUI such as [pgAdmin ](https://www.pgadmin.org/).

### Secure local access

To forward your PostgreSQL database for local access using the [Northflank CLI](../../../api/use-the-cli), copy and execute the forward addon command from the local access section of the overview.

You can then use the connection details to access your PostgreSQL deployment in your local development environment.

### External access

To access your PostgreSQL database externally, ensure `deploy with TLS` and `publicly accessible` are enabled on the settings page under networking. External connection strings will appear in the addon's connection details page, and the host will now resolve externally.

### Administration

You can connect to your PostgreSQL database as administrator using the connection strings that end in `_ADMIN`, or log in using `ADMIN_USERNAME` and `ADMIN_PASSWORD`. You should only use this account for necessary maintenance, and otherwise access the database using the standard user credentials.

PostgreSQL specifications

### Connection limits

The maximum concurrent connections allowed on a PostgreSQL is 750. You can add [connection poolers](../configure-addons-for-high-availability#postgresql) on the resources page if you need to manage high numbers of connections.

### Extensions

The PostgreSQL addon offers a number of available extensions which include:

  * `PostGIS`
  * `earthdistance`
  * `timescaledb`
  * `vector`
  * `pg_stat_statements`
  * `pg_cron`



For a complete list connect to your PostgreSQL addon and run `SELECT pg_available_extensions();`.

You can install an extension by running the `CREATE EXTENSION <extension-name>;` SQL command on your addon.

Next steps

[Configure PostgreSQL for high availabilityNorthflank's PostgreSQL addon offers automated failover and connection poolers.](/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability#postgresql)[Use the Northflank CLILearn how to create and manage projects on Northflank using the command line client.](/docs/v1/api/use-the-cli)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)