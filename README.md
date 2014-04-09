# Database Backup Manager

[![Latest Stable Version](https://poser.pugx.org/mccool/database-backup/version.png)](https://packagist.org/packages/mccool/database-backup)
[![License](https://poser.pugx.org/mccool/database-backup/license.png)](https://packagist.org/packages/mccool/database-backup)
[![Build Status](https://travis-ci.org/heybigname/database-backup-manager.svg?branch=master)](https://travis-ci.org/heybigname/database-backup-manager)
[![Coverage Status](https://coveralls.io/repos/heybigname/database-backup-manager/badge.png?branch=master)](https://coveralls.io/r/heybigname/database-backup-manager?branch=master)
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/5e507053-58d7-4cff-b757-4202b021f9b0/mini.png)](https://insight.sensiolabs.com/projects/5e507053-58d7-4cff-b757-4202b021f9b0)
[![Total Downloads](https://poser.pugx.org/mccool/database-backup/downloads.png)](https://packagist.org/packages/mccool/database-backup)

- supports MySQL and PostgreSQL
- backup to or restore databases from AWS S3, Dropbox, FTP, SFTP, Rackspace Cloud, and WebDAV
- compress with Gzip
- framework-agnostic
- dead simple configuration
- optional integrations for MVC framework [Laravel](http://laravel.com) and team-communication software [Slack](http://slack.com)

### Quick and Dirty

Configure your databases.

```php
'development' => [
    'type' => 'mysql',
    'host' => 'localhost',
    'port' => '3306',
    'user' => 'root',
    'pass' => 'password',
    'database' => 'test',
],
'production' => [
    'type' => 'postgresql',
    'host' => 'localhost',
    'port' => '5432',
    'user' => 'postgres',
    'pass' => 'password',
    'database' => 'test',
],
```

Configure your filesystems.

```php
'local' => [
    'type' => 'Local',
    'working-path' => '/',
],
's3' => [
    'type' => 'AwsS3',
    'key'    => '',
    'secret' => '',
    'region' => Aws\Common\Enum\Region::US_EAST_1,
    'bucket' => '',
],
'rackspace' => [
    'type' => 'Rackspace',
    'username' => '',
    'password' => '',
    'container' => '',
],
'dropbox' => [
    'type' => 'Dropbox',
    'key' => '',
    'secret' => '',
    'app' => '',
    'root' => '',
],
```

Want to back up a database?

```php
use BigName\DatabaseBackup\Manager;
$manager = new Manager('storage.php', 'database.php');
$manager->backup('development', 's3', 'test/backup.sql', 'gzip');
```

Want to restore a database?

```php
use BigName\DatabaseBackup\Manager;
$manager = new Manager('storage.php', 'database.php');
$manager->restore('s3', 'test/backup.sql.gz', 'production', 'gzip');
```

### Requirements

- PHP 5.4
- MySQL support requires `mysqldump` and `mysql` command-line binaries
- PostgreSQL support requires `pg_dump` and `psql` command-line binaries
- Gzip support requires `gzip` and `gunzip` command-line binaries

### License

MIT
