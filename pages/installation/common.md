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

After this installation you can configure [**backup-manager**]({{ site.baseurl }}/pages/configuration/backup-manager) and [**fail2ban**]({{ site.baseurl }}/pages/configuration/fail2ban).

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
For this open `/etc/ssh/sshd_config` file and change this option:

```bash
PermitRootLogin no
```

You can also add an other parameter to precise a groups they are authorized to loggin with ssh:

```bash
AllowGroups ssh-login
```

Save and close `/etc/ssh/sshd_config` and **don't reboot ssh server now!**

Now you must create this group:

```bash
$ addgroup ssh-login --system
```

Add user you want authorized into **ssh-login** group (do this command for each user):

```bash
$ adduser username ssh-login
```

You can now restart ssh:

```bash
$ service ssh restart
```

**Before close your current ssh term open an another an try to log to your server to be sure that works.**

## .profile

To enable color for a user, just add this line into the user **.profile** file and add this line:

```bash
TERM="xterm-color"
```

## To continue

You can now install a [PHP server]({{ site.baseurl }}/pages/installation/php-prod) or a [Ruby server]({{ site.baseurl }}/pages/installation/ruby-prod) (or both).
