# gitswitch-drupal

This repository is a working Drupal project to use the agomezmoron/simple_git module.

## Install

Download the source code:
```bash
git clone [repository]
```

Change to the repository folder:
```bash
cd gitswitch-drupal
```

Fetch dependencies:
```bash
composer install
```

Change to the Drupal folder:
```bash
cd web
```

Install the Drupal (Replace with your own database user and password):
```bash
../vendor/bin/drush si minimal -y \
--account-pass=password \
--site-name=git-switch \
--db-url=mysql://dbuser:dbpassword@localhost/gitswitch \
--notify \
--config-dir=../config/sync
```

Restore the database dump:
```bash
../vendor/bin/drush sql-cli < ../dump.sql
```

Remove the given oauth client and add a new one with your own keys.

## Synchronize

From the project directory (under web), pull the changes:
```bash
git pull --rebase origin [branch]
```
or using PhpStorm VCS->Update Project->Rebase

Fetch dependencies:
```bash
composer update
```

Import Drupal configurations:
```bash
../vendor/bin/drush cim sync
```

Apply any database updates required:
```bash
../vendor/bin/drush updb --entity-updates
```
