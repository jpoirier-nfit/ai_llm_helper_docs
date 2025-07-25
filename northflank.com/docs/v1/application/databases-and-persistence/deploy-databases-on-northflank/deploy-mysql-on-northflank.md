---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/deploy-databases-on-northflank/deploy-mysql-on-northflank
title: Deploy MySQL on Northflank | Deploy Databases On Northflank | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.393394
watsonmd_version: 0.1.0
---

Databases And Persistence / Deploy Databases On Northflank / 

# Deploy MySQL on Northflank

This guide explains how to quickly and easily deploy and use [MySQL ](https://www.mysql.com/) on Northflank.

Available versions| Description| Backups| TLS  
---|---|---|---  
9.0.1, 8.4.3, 8.0.40| MySQL is a fast, reliable, scalable, and easy to use open-source relational database system.| Native or disk| Yes (cannot be changed after creation)  
  
Deploy MySQL

  1. [Click here to create an addon ](https://app.northflank.com/s/project/create/addon), or choose `addon` from the create new menu in the top right corner of the dashboard
  2. Select `MySQL` and enter a name

  3. Choose a `version` or leave as default (most recent version)

  4. Choose whether to [deploy with TLS](../connect-database-secrets-to-workloads#enable-tls). This cannot be changed later.

  5. Choose whether to make the database `publicly accessible`. This will give your addon a URL and make it available online. TLS must be enabled to select this.

  6. If you have [secret groups](../../secure/manage-secret-groups) in your project, choose ones to [link to the addon](../connect-database-secrets-to-workloads#link-database-secrets-to-a-secret-group) so that the database can be used in services and jobs that inherit variables from the secret group. To link the database to a secret group:

     * `Show secret groups` and `configure` the secret groups you wish to use
     * `Select suggested` secrets from the database to link, or `select all`
     * Set any required `aliases` for specific secrets to make them accessible by that name within your application
  7. Select the required [resources](../scale-a-database) for your database. You can scale the database after creation, but available storage and replicas cannot be decreased once increased.

  8. `Create addon` and MySQL will begin provisioning, this may take a few minutes.



Advanced options

MySQL has the following advanced options available when creating your addon.

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

Connect to MySQL

You can manually copy the connection secrets for your MySQL database from the connection details page into runtime variables or build arguments of your workloads on Northflank.

However, it is much easier to link your database's connection details to a new or existing [secret group](../connect-database-secrets-to-workloads#link-database-secrets-to-a-secret-group).

The necessary secrets to connect your workload will vary depending on the application in your workload.

Some clients may use a URI-like [connection string ](https://dev.mysql.com/doc/refman/8.0/en/connecting-using-uri-or-key-value-pairs.html), while some clients may not support the connection string format.

The connection string takes the format `[scheme://][user:password@][host][:port][/schema][...options]`. The `MYSQL_CONNECTOR_URI` and `MYSQL_JDBC_URI` (for Java applications using JDBC) connection strings will be automatically configured for your database, as well as the `CONNECT_COMMAND` for command-line clients.

You can supply connections details and secrets such as `host`, `database`, `username`, `password`, and `port` to your workload if your application is configured to use these instead of a connection string.

### Available ports

Internal port| External port| Protocol  
---|---|---  
3306| Dynamically generated| MySQL  
  
If you create more than one replica, read replicas will have the `read` prefixes in place of the `primary` prefix for the primary replica.

### Automatically inherit database connection details into your workload

  1. Create a new [secret group](../../secure/manage-secret-groups) of `runtime` variables to connect in the running workload
  2. `Show addons` and `configure` your addon with either the `MYSQL_CONNECTOR_URI` or `MYSQL_JDBC_URI` connection string, or select connection details and secrets
  3. Set the aliases required in your workload to access the secrets
  4. Enable `apply secrets to specific services/jobs` and select the workloads you want to access the database
  5. `Create secret group`
  6. Go to one of the workloads that inherits from the group and check the environment page, you should see the inherited variables from the secret group



The connection string or secrets will now be available in your workload under the configured aliases, and your application will be able to connect to the database using them.

Access MySQL

You can access your MySQL addon using the relevant connection string, or by using the `HOST`, `PORT`, `USERNAME` and `PASSWORD` secrets found in the connection details page of the addon.

You can connect using the [MySQL shell ](https://dev.mysql.com/doc/mysql-shell/8.0/en/) using the connect command, or via a GUI such as [phpMyAdmin ](https://www.phpmyadmin.net/).

### Secure local access

To forward your MySQL database for local access using the [Northflank CLI](../../../api/use-the-cli), copy and execute the forward addon command from the local access section of the overview.

You can then use the `CONNECT_COMMAND` from the connection details page to access your MySQL deployment using the command-line client, or use the connection details in your local development environment.

### External access

To access your MySQL database externally it must have been created with TLS enabled. If so, you can enable `publicly accessible` on the settings page under networking. External connection strings will appear in the addon's connection details page, as well as an external port, and the host will now resolve externally.

### Administration

You can connect to your MySQL database as administrator using the connection strings that end in `_ADMIN`, or log in using `ADMIN_USERNAME` and `ADMIN_PASSWORD`. You should only use this account for necessary maintenance, and otherwise access the database using the standard user credentials.

MySQL specifications

### Connection limits

The maximum concurrent connections allowed on a MySQL addon depend on the amount of available memory. This can be configured by selecting the compute plan on the [addon's resources page](../scale-a-database).

Memory available| Maximum connections  
---|---  
512MB| 32  
1024MB| 96  
4096MB| 250  
8192MB| 350  
16384MB| 700  
32768MB| 1000  
> 32768MB| 2000  
  
Next steps

[Configure MySQL for high availabilityMake use of read replicas in your application for high availability MySQL databases.](/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability#mysql)[Use the Northflank CLILearn how to create and manage projects on Northflank using the command line client.](/docs/v1/api/use-the-cli)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)