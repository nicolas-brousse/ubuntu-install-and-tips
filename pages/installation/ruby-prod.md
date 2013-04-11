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


## Installation of Passenger + Nginx

Switch to `rvm` user

```bash
$ su - rvm
```

Create `passenger` repository and `gemset`

```bash
$ mkdir ~/passenger
$ rvm --create --ruby-version use ruby-2.0.0@passenger
```

You can use `ree` instead of `ruby-2.0.0`

Now install passenger.

```bash
$ cd ~/passenger
$ gem install passenger
```

To find out where the Phusion Passenger gem directory is, run:

```bash
$ passenger-config --root
```

Install Passenger Nginx module:

```bash
$ passenger-install-nginx-module
```

Restart web server and verifying that Phusion Passenger is running

```bash
$ passenger-memory-stats
```


## Nginx configuration

Edit Nginx config `/opt/nginx/conf/nginx.conf`. (Create symlink into `/etc`?)

```nginx
...
server {
    listen 80;
    server_name my_app.tld www.my_app.tld;
    root /home/my_app/public;
    passenger_enabled on;
}
...
```
_Other [example](https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf)._

```bash
$ restart nginx

$ curl localhost
```


## Other

For a better configuration you can create a user by application:

```bash
$ adduser app_user
$ adduser app_user rvm
```

-------------------------------
sources:

- [http://www.modrails.com/documentation/Users%20guide%20Nginx.html#_installing_or_upgrading_on_red_hat_fedora_centos_or_scientificlinux](http://www.modrails.com/documentation/Users%20guide%20Nginx.html#_installing_or_upgrading_on_red_hat_fedora_centos_or_scientificlinux)
- [https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf](https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf)
- [http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/](http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/)
- [http://www.modrails.com/documentation/Users%20guide%20Nginx.html#rubygems_generic_install](http://www.modrails.com/documentation/Users%20guide%20Nginx.html#rubygems_generic_install)
- [https://gist.github.com/2499900](https://gist.github.com/2499900)
