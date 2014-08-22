---
layout: page
title: Backup manager configuration
---

To configure backup manager `vi /etc/backup-manager.conf`

```ini
; Add mysql if you have mysql-server installed 
; Add svn if you have svn installed
BM_ARCHIVE_METHOD=""
```
```ini
;list of directories to backup (separated by space)
BM_TARBALL_DIRECTORIES=""
;list of ignored directories to backup (separated by space)
BM_TARBALL_BLACKLIST=""
```

## BM_UPLOAD: upload to remote server/ftp

```ini
...
BM_UPLOAD_METHOD="ftp"
BM_UPLOAD_FTP_USER="ftp_user"
BM_UPLOAD_FTP_PASSWORD="ftp_password"
BM_UPLOAD_FTP_HOSTS="ftp.host.tld"
BM_UPLOAD_FTP_PURGE="true"
BM_UPLOAD_FTP_TTL="2" (One more is used during the archives trasfert)
BM_UPLOAD_FTP_DESTINATION="/" (Do not leave blank)
````

## BM_BURNING

```ini
BM_BURNING_METHOD="none"
```

## Crontab configuration

```bash
$ cp /usr/share/backup-manager/backup-manager.cron.tpl /etc/cron.daily/backup-manager
$ chmod a+x /etc/cron.daily/backup-manager
```


## <a id="pgsql"></a>Backup-manager configurations for PostgreSQL

Add this code at the end of `/etc/backup-manager.conf`

```ini
...
;  Add pipe
BM_TARBALL_DIRECTORIES="... pipe"
...
# Postgresql
BM_PIPE_COMMAND[0]="/usr/local/share/backups/bk_pgsql"
BM_PIPE_NAME[0]="pgsql_one_file_by_base"
BM_PIPE_FILETYPE[0]="tar"
BM_PIPE_COMPRESS[0]="gzip"
```

Create `/usr/local/share/backups/bk_pgsql` file (it's possible that `/usr/local/share/backups` dir doesn't exist):

```bash
#!/bin/bash
WORK_DIR=$(mktemp -d)
LST_BASES=$(su postgres -c "psql -l --no-align" | sed -e '1d' -e '2d' -e '$d' | cut -d '|' -f 1)
for base in $LST_BASES
do
    su postgres -c "/usr/bin/pg_dump $base" > $WORK_DIR/$base.sql
done
cd $WORK_DIR
tar -c *
cd /tmp/
rm -rf $WORK_DIR
```

Do this file executable:

```bash
$ chmod a+x /usr/local/share/backups/bk_pgsql
```


-------------------------------
sources:

- [http://tcweb.org/wiki/Backup-manager_et_debian#Postgresql](http://tcweb.org/wiki/Backup-manager_et_debian#Postgresql)
