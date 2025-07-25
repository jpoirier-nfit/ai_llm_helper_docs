---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/scale-a-database
title: Scale a database | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.271519
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Scale a database

You can increase the resources available to a database, including CPU and memory, storage space, and number of replicas. You should [monitor your addon](database-observability-and-monitoring) to identify bottlenecks.

You can also make use of [high-availability strategies](configure-addons-for-high-availability) for many addons, to ensure availability and enable automatic fail-over.

![An addon's resources page in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/scale-a-database/addon-resources-page.png)

See [Northflank pricing plans ](https://northflank.com/pricing) for compute plans available on Northflank's managed cloud, as well as storage and network egress costs.

Scale compute

You can increase the vCPU and memory dedicated to an addon on the resources page. Some databases have higher requirements than others, meaning lower compute plans will be unavailable for them.

Scale storage

You can increase the storage space dedicated to a database on the resources page.

You should increase the storage space for your database once it is over 50% full.

You cannot reduce the storage space assigned to a database after increasing it.

Scale replicas

You can increase the number of replica sets your database will use to improve availability, each replica set contains a copy of the database.

Database replicas can be scaled up from the resources page, but cannot be scaled down. Any increase will be permanent.

Next steps

[Upgrade a databaseUpgrade your database to a newer version with one click.](/docs/v1/application/databases-and-persistence/upgrade-a-database)[Backup, restore, and import your dataCreate and import backups of your database, or restore from an existing backup.](/docs/v1/application/databases-and-persistence/backup-restore-and-import-data)[Configure addons for high availabilityConfigure your addons to maximise availability.](/docs/v1/application/databases-and-persistence/configure-addons-for-high-availability)