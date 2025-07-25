---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/backup-restore-and-import-data
title: Backup, restore, and import data | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.307194
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Backup, restore, and import data

You can create, import, and delete backups of your database or addon from the backups page, as well as restore your database or addon from an existing backup.

You can also use backups to [fork an existing addon]().

Types of backup

### Snapshot (disk backup)

Snapshots save the state of the whole volume. Each new snapshot you create will only store the differences from the previous snapshot.

Snapshots are the best method for regular backups as the incremental way of storing backup data is highly efficient and uses a minimal amount of storage space.

Snapshots cannot be downloaded and do not support logging.

### Dump (native backup)

Creates a text dump of the full existing database and stores it in a compressed file. Native backups are [not available for all databases](deploy-a-database).

You can select either [gzip ](https://www.gnu.org/software/gzip/) or [Zstandard ](https://facebook.github.io/zstd/) compression when creating the dump.

Dumps can be downloaded, and logs can be viewed for backups and restores.

![Logs for a dump backup of a MongoDB addon in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/backup-restore-and-import-data/addon-backup-logs.png)

Schedule backups

You can configure up to three separate backup schedules for each database or addon.

You can create one hourly, one daily, and one weekly schedule to meet your operational and legal requirements.

### Create a schedule

You can `add schedule` from the backups schedule page on an addon to begin configuring a new backup schedule. You can also add a backup schedule to a new addon on creation.

Choose the backup type, and how often to run the backup: hourly, daily, or weekly.

![Adding scheduled backups for an addon in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/backup-restore-and-import-data/addon-scheduled-backups.png)

You can configure each schedule by minute, hour, and day. Your schedule will then run the backup at the selected times, per the schedule frequency (hourly, daily, or weekly).

  * Retention time defines how many days a backup will be stored for.
  * If any backup schedules overlap, only one backup will be created at the overlapping time.
  * After creating a schedule you will only be able to edit the retention period. To change any other settings, delete the current schedule and create a new one.
  * Schedules can produce a maximum of 500 backups before any expire, you will be unable to create schedules that would produce more than this.



### Backups from schedule

Backups created by schedule are available on the backups page for the database or addon, and detail the schedule they were created by. You can click on an individual backup to see more details and select `` retain backup forever to override the schedule's retention policy.

Create a manual backup

You can manually create a new backup from the backups page on a running database or addon. Choose the backup type and it will be immediately scheduled for creation. Check the entry on the backups page to view its status.

Import a backup

You can import a backup from a file or directly from another running database. Once imported you can restore from the imported backup.

### URL or file upload

You can restore a database from a file by providing the URL to the hosted file, for example `https://yourdomain.com/backups/data.db.gz`, or uploading a file. If the file ends in `.gz` or `.zst` Northflank will attempt to unzip it, otherwise it will be treated as clear text. Northflank will copy the imported file, which will be used as a source when restoring the backup.

Please note that when you restore from this kind of import:

  * All existing user databases will be removed. The default admin and access users and system databases will not be affected.
  * All databases from the backup source will be imported
  * The default admin and access users will have full access to the imported database. If these users have been deleted they will be recreated before restoring.
  * If the source includes user manipulation commands (create user, grant permissions), they will be executed unless they grant too many rights



### Connection string

You can restore or import from another database by providing a connection string with relevant credentials and parameters. Northflank will create a dump from the source database which you can then restore from. You can choose the type of compression to use when Northflank creates a dump of the live database.

You can download the created dump after it has been imported, in whichever compression format you selected to create it.

Please note that when you restore from this kind of import:

  * All existing user databases will be removed. The default admin and access users and system databases will not be affected.
  * All databases, except users, from the backup source will be imported (depending on the access of the specified user when importing by connection string)
  * The default admin and access users will have full access to the imported database. If these users have been deleted they will be recreated before restoring.

Database| Connection string syntax example  
---|---  
MongoDB| `mongodb://user:password@mongodb0.yourdomain.com:port`  
MySQL (using JDBC)| `jdbc:mysql://user:password@yourdomain.com:port`  
PostgreSQL| `postgresql://user:password@yourdomain.com:port`  
  
Restore from a backup

You can restore your database or addon from a specific backup on the backups page. Select `` restore backup to immediately schedule a restoration.

Each listed backup displays the following information:

Column| Explanation  
---|---  
Name| Backup name, usually automatically generated  
Source| Indicates whether the backup was created on Northflank or imported, and if it's a disk or native backup  
Status| Displays the date the backup was completed, or the status if it is in-progress  
Schedule| Indicates which schedule created the backup, if any. If created by overlapping schedules, it will list all applicable.  
Size| The size of the backup. May not be displayed if the backup is too small.  
Restore status| Indicates if a restore has been scheduled from the backup, is in progress, or is complete  
Created| The date and time the backup was scheduled for creation  
  
You can click on the entry in the list to view the backup logs, restore history, and abort scheduled restorations. Each backup has the following available actions:

Button| Action  
---|---  
``| Download the backup as a gzip (`.gz`) or ZStandard (`.zst`) archive file. Only available for native (dump) backups.  
``| Restore from this backup. The restore will be immediately scheduled and executed as soon as possible.  
``| Override the retention policy of the schedule and keep the backup forever. Only available for backups created by a schedule  
``| Delete the backup from Northflank.  
  
Reset an addon

You can reset an addon from the billing page. Resetting an addon will erase all the data, and restore it to the state of a newly-provisioned addon. If you reset an addon that was created by [forking an existing addon](fork-an-addon), the backup must still be available to restore from.

This can be used to reset the addon's data while retaining the same [connection details](connect-database-secrets-to-workloads) used in any environment variables, secret groups, or to connect locally.

Next steps

[Upgrade a databaseUpgrade your database to a newer version with one click.](/docs/v1/application/databases-and-persistence/upgrade-a-database)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)