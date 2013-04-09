---
layout: page
title: Fresh install RUBY/RAILS PROD server
---

__See [common installation]({{ site.baseurl }}/pages/installation/common) and configuration before.__  
Do this operation with **root** user.

## Apt-get

Install **PosgreSQL** and **Nginx**

```bash
$ apt-get install postgresql
$ apt-get isntall nginx
```

## Backup-manager configurations for PostgreSQL

Add this code at the end of `/etc/backup-manager.conf`

See: [Backup manager]({{ site.baseurl }}/pages/configuration/backup-manager)

## RVM

Create user and group:

```bash
$ adduser
  --system \
  --disabled-password \
  --group \
  --shell /bin/sh \
  --gecos 'RVM' \
  --home /home/rvm \
  rvm
```  

See [rvm.io](http://rvm.io). (install into a ruby or rails unix user).  
Add install the rvm requirments for ubuntu.  

Define a ruby version as default.

```bash
$ rvm use x.x.x --default
```

Update rubygems?

```bash
$ rvm rubygems current
```


## Passenger



## Nginx




## Other

For a better configuration you can create a user by application:

```bash
$ adduser app_user
$ adduser app_user rvm
```

-------------------------------
sources:

- [https://gist.github.com/2499900](https://gist.github.com/2499900)
