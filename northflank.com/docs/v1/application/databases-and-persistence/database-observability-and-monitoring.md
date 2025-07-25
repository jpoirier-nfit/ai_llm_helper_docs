---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/database-observability-and-monitoring
title: Database observability and monitoring | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.292546
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Database observability and monitoring

You can monitor the health and see the logs of your running and terminated database containers as you can with services and jobs.

You can also monitor the status and review the logs of imports, backups, and restores.

Containers

You can view a list of running and terminated containers, which can be filtered by state, from the containers page in an addon.

Only the 10 most recently terminated containers are displayed.

You can click through on each container to view live, detailed logs and metrics.

![A list of containers for an addon in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/database-observability-and-monitoring/addon-containers.png)

Backups, imports, and restores

At a glance the backups list will show you the status of each backup, the time and date it was completed (if successful), and the status of the most recently attempted restore.

Logs are available for native backups, but not disk snapshots.

### Backup logs and metrics

You can click through on each backup to view more detailed logs and metrics.

Native backups created on Northflank will display a live tail log containing information about the success or failure of the attempted backup.

### Restore logs and metrics

Each backup includes a list of restores from that backup, with the date, current status, and whether the backup has been completed. Click on a native backup to view live tail logs of the attempted restore.

![A list of backups for an addon in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/database-observability-and-monitoring/addon-backups-list.png)

Learn more

[Monitor containersMonitor the health and resource usage of deployments, and view detailed logs and metrics for individual container.](/docs/v1/application/observe/monitor-containers)[View logsView detailed, real-time logs from builds, deployments, and more.](/docs/v1/application/observe/view-logs)