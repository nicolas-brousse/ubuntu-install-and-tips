---
layout: page
title: Common installation and configuration
---

Do this operation with **root** user. You can also use _sudo_ before all commands.


## Apt-get

```bash
$ apt-get update
$ apt-get dist-upgrade
```

Packages for motd (optionals):

```bash
$ apt-get install update-notifier-common
$ apt-get install landscape-common
```

```bash
$ apt-get install vim
$ apt-get install curl
$ apt-get install wget
$ apt-get install git
$ apt-get install backup-manager
$ apt-get install fail2ban
```

## SMTP server

If you have application that want to send mail follow this else go next.

```bash
$ apt-get install postfix
```
And enter this informations step by step:

```bash
Internet Site
server1.exemple.com
```


## Crontab

Use file `/etc/crontab` or add file into `/etc/cron.d/`.


## SSH

Disable ssh connection for `root` user and enable just for precise users or group.


## To continue

You can now install a [PHP server]({{ site.baseurl }}/pages/installation/php-prod) or a [Ruby server]({{ site.baseurl }}/pages/installation/ruby-prod) (or both).
