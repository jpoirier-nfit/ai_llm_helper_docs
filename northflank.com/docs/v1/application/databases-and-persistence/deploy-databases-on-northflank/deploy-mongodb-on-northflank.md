---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-mongodb-on-northflank
title: Deploy MongoDB® on Northflank | Deploy Databases On Northflank | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.360510
watsonmd_version: 0.1.0
---

Databases And Persistence / Deploy Databases On Northflank / 

# Deploy MongoDB® on Northflank

This guide explains how to quickly and easily deploy and use [MongoDB® ](https://mongodb.com/docs/manual/) on Northflank.

Available versions| Description| Backups| TLS  
---|---|---|---  
8.0.10, 8.0.3, 7.0.21, 7.0.15, 6.0.24, 6.0.13, 5.0.31, 5.0.24, 4.4.15, 4.2.21| MongoDB® is a document-oriented database program that uses JSON-like documents with schema.| Native or disk| Yes  
  
Deploy MongoDB

  1. [Click here to create an addon ](https://app.northflank.com/s/project/create/addon), or choose `addon` from the create new menu in the top right corner of the dashboard
  2. Select `MongoDB` and enter a name

  3. Choose a `version` or leave as default (most recent version)

  4. Choose whether to [deploy with TLS](../connect-database-secrets-to-workloads#enable-tls). This can be changed later.

  5. Choose whether to make the database `publicly accessible`. This will give your database a URL and make it available online. TLS must be enabled to select this.

  6. If you have [secret groups](../../secure/manage-secret-groups) in your project, choose ones to [link to the addon](../connect-database-secrets-to-workloads#link-database-secrets-to-a-secret-group) so that the database can be used in services and jobs that inherit variables from the secret group. To link the database to a secret group:

     * `Show secret groups` and `configure` the secret groups you wish to use
     * `Select suggested` secrets from the database to link, or `select all`
     * Set any required `aliases` for specific secrets to make them accessible by that name within your application
  7. Select the required [resources](../scale-a-database) for your database. You can scale the database after creation, but available storage and replicas cannot be decreased once increased.

  8. `Create addon` and MongoDB will begin provisioning, this may take a few minutes.



Advanced options

MinIO has the following advanced options available when creating your addon.

### Fork existing addon

You can create your new addon as a [fork from an existing addon](../fork-an-addon).

This will copy all data, including database names and users, from the selected backup of the source addon to your new addon during creation.

The newly forked addon may have a newer minor version than the source backup, but must have the same major version.

### Custom database name

The default database name is a randomly-generated string, and is used in connection details to access the addon. If your application expects a specific database name it can be useful to change it.

You can set a custom name for the default database created in your addon by entering one in advanced options. The name cannot be changed after creation.

If you are [forking from an existing addon](../fork-an-addon), it will use the name of the default database from the source addon.

### Deploy with zonal redundancy

Your addon will be deployed to your [project's region](../../run/deploy-to-a-region). Each region may have multiple availability zones, which are data centers with independent infrastructure such as networking, power supply and cooling within the region. Some regions, however, do not have more than one availability zone.

Normally your addon replicas will be provisioned in the same availability zone, but you can enable zonal redundancy to provision replicas across multiple availability zones.

This will ensure that your addon remains available in the event that one zone fails, however networking between replicas in different zones will be slightly slower compared to replicas provisioned in the same availability zone. Replicas will be bound to the zone they are deployed in.

### Backup schedules

You can [add backup schedules](../backup-restore-and-import-data#schedule-backups) when creating your addon. Backups of the addon will be taken according to the schedules.

Connect to MongoDB

You can manually copy the connection secrets for your MongoDB database from the connection details page into environment variables or build arguments of your workloads on Northflank.

However, it is much easier to link your database's connection details to a new or existing [secret group](../connect-database-secrets-to-workloads#link-database-secrets-to-a-secret-group).

The necessary secrets to connect your workload will vary depending on the application in your workload.

Some clients may use the [MongoDB connection string ](https://www.mongodb.com/docs/manual/reference/connection-string/), while some clients may not support the connection string URI format.

The connection string takes the format `mongodb://[username:password@][host][:port][/database][...options]`, options include specifying the replica set, authentication source, and TLS requirement. The `mongoSrv` connection string will be automatically configured for your database.

You can supply connections details and secrets such as `host`, `database`, `username`, `password`, and `port` to your workload if your application is configured to use these instead of a connection string.

### Available ports

Port| Protocol| URI prefix  
---|---|---  
27017| MongoDB| `mongodb://`  
  
### Automatically inherit database connection details into your workload

  1. Create a new [secret group](../../secure/manage-secret-groups) of `runtime` variables to connect in the running workload
  2. `Show addons` and `configure` your addon with either the `mongoSrv` connection string, or select connection details and secrets
  3. Set the aliases required in your workload to access the secrets
  4. Enable `apply secrets to specific services/jobs` and select the workloads you want to access the database
  5. `Create secret group`
  6. Go to one of the workloads that inherits from the group and check the environment page, you should see the inherited variables from the secret group



The connection string or secrets will now be available in your workload under the configured aliases, and your application will be able to connect to the database using them.

Access MongoDB

You can access your MongoDB addon using the relevant [connection string ](https://www.mongodb.com/docs/manual/reference/connection-string/), or by using the `HOST`, `PORT`, `USERNAME` and `PASSWORD` secrets found in the connection details page of the addon.

You can connect using the [Mongo shell ](https://www.mongodb.com/docs/v4.4/mongo/#mongodb-instance-on-a-remote-host), or via a GUI such as [Compass ](https://www.mongodb.com/products/compass).

### Secure local access

To forward your MongoDB database for local access using the [Northflank CLI](../../../api/use-the-cli), copy and execute the `forward addon` command from the local access section of the overview in your terminal.

You can then use the connection details to access your MongoDB deployment in your local development environment.

### External access

To access your MongoDB database externally, ensure `deploy with TLS` and `publicly accessible` are enabled on the settings page under networking. External connection strings will appear in the addon's connection details page, and the host will now resolve externally.

### Administration

You can connect to your MongoDB database as administrator using the connection strings that end in `_ADMIN`, or log in using `ADMIN_USERNAME` and `ADMIN_PASSWORD`. You should only use this account for necessary maintenance, and otherwise access the database using the standard user credentials.

Scale MongoDB

You can scale your MongoDB database on the resources page. You can increase the CPU and memory, storage, and replicas available to your database.

### Compute plan

You can change the compute plan to improve performance for more intensive workloads.

### Storage

You can increase storage, but not decrease it. You should increase storage if your database uses over 50% of the available storage.

### Replica behaviour

You can increase the number of available replicas, but you cannot decrease them. If a primary node becomes unavailable one of the replica nodes will be promoted to primary, supporting read/write operations.

MongoDB specifications

### Connection limits

The [default connection limit ](https://www.mongodb.com/docs/manual/reference/configuration-options/#mongodb-setting-net.maxIncomingConnections) for MongoDB is 80% of the limit for the maximum number of open files on the system.

Your addon will be able to handle more concurrent connections by increasing the available CPU and memory. You can do this by selecting the compute plan on the [addon's resources page](../scale-a-database).

Next steps

[Configure MongoDB® for high availabilityTake advantage of automated failover and configure your client's read preference.](/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability#mongodb)[Use the Northflank CLILearn how to create and manage projects on Northflank using the command line client.](/docs/v1/api/use-the-cli)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)