---
layout: default
title: Fresh install RUBY/RAILS PROD server
---

# {{ page.title }}

__See [common installation]({{ site.baseurl }}/pages/installation/common) and configuration before.__  
Do this operation with **root** user.

## Apt-get
```bash
$ apt-get install postgresql
$ apt-get isntall nginx
```

## Backup-manager configurations for PostgreSQL

http://tcweb.org/wiki/Backup-manager_et_debian#Postgresql

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

See http://rvm.io. (install into a ruby or rails unix user).  
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

Interesting Gist: https://gist.github.com/2499900.
