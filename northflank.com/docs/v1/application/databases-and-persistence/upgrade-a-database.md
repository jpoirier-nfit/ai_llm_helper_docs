---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/upgrade-a-database
title: Upgrade a database | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.325158
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Upgrade a database

Northflank regularly updates the available versions of databases on the platform to ensure security and compatibility.

If your database has an upgrade available you will see a notice in the database's header: 

Upgrade available

If your database version is deprecated you will see a warning in the database's header: 

Upgrade recommended

We strongly recommend that you upgrade a database to a newer version if it becomes deprecated. Northflank will always ensure a valid upgrade path from a deprecated version.

Upgrading

You can upgrade a database on the upgrade page in your addon.

If an upgrade is available you will be able to select the newer version to install. If multiple newer versions are available, you may need to upgrade to the next major release before upgrading to the latest minor version.

You should back up your data before upgrading. You will not be able to downgrade to an older version when it is complete.

Upgrading will incur some downtime as the addon will be restarted. Major upgrades usually take longer.

You will be able to see a list of previous upgrades and their statuses on the upgrade page.

![Upgrading an addon's version in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/upgrade-a-database/addon-upgrade.png)

Next steps

[Deploy a databaseCreate a database to use with your Northflank deployments.](/docs/v1/application/databases-and-persistence/deploy-a-database)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)