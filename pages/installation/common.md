---
layout: default
title: Common installation and configuration
---

# {{ page.title }}

Do this operation with **root** user.

## Apt-get

```bash
$ apt-get install vim
$ apt-get install wget
$ apt-get install git
$ apt-get install backup-manager
$ apt-get install fail2ban
```

## SMTP server

If you have application that want to send mail follow this else go next.  

```bash
$ sudo dpkg-reconfigure postfix
```
And enter this informations step by step:

```bash
Internet Site
NONE
server1.exemple.com
server1.exemple.com, localhost.exemple.com, localhost
No
127.0.0.0/8
0
+
```


## Configure Backup manager

To configure backup manager `vi /etc/backup-manager.conf`

```bash
BM_ARCHIVE_METHOD: add mysql (and svn if you have svn installed)
```
```bash
BM_TARBALL_DIRECTORIES: list of directories to backup (separated by space)
BM_TARBALL_BLACKLIST: list of ignored directories to backup (separated by space)
```

### BM_UPLOAD: upload to remote server/ftp
```bash
BM_UPLOAD_METHOD = "ftp"
BM_UPLOAD_FTP_USER = "ftp_user"
BM_UPLOAD_FTP_PASSWORD = "ftp_password"
BM_UPLOAD_FTP_HOSTS = "fpt.host.tld"
BM_UPLOAD_FTP_PURGE = "true"
BM_UPLOAD_FTP_TTL = "2" (One more is used during the archives trasfert)
BM_UPLOAD_FTP_DESTINATION = "/" (Do not leave blank)
````

### Crontab configuration
```bash
$ cp /usr/share/backup-manager/backup-manager.cron.tpl /etc/cron.daily/backup-manager
$ chmod a+x /etc/cron.daily/backup-manager
```

## Crontab

Use file `/etc/crontab` or add file into `/etc/cron.d/`.


## SSH

Disable ssh connection for `root` user and enable just for precise users or group.


## To continue

You can now install a [PHP server]({{ site.baseurl }}/pages/installation/php-prod) or a [Ruby server]({{ site.baseurl }}/pages/installation/ruby-prod) (or both).