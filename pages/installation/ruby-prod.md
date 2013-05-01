---
layout: page
title: Fresh install RUBY/RAILS PROD server
---

__See [common installation]({{ site.baseurl }}/pages/installation/common) and configuration before.__

## Apt-get

Do this operation with **root** user.
Install **PosgreSQL** and **Nginx**

```bash
$ apt-get install postgresql libpq-dev
$ apt-get install nginx
```

## Backup-manager configurations for PostgreSQL

Add this code at the end of `/etc/backup-manager.conf`

See: [Backup manager]({{ site.baseurl }}/pages/configuration/backup-manager/#pgsql)

## RVM

See [rvm.io](http://rvm.io). (install into a ruby or rails unix user).
For production install for all user use `sudo`

```bash
$ \curl -#L https://get.rvm.io | sudo bash -s stable --autolibs=3 --ruby
```

Update rubygems if you want

```bash
$ rvm rubygems current
```



## New application

For a better configuration you can create a user by application:

Create user and group:

```bash
$ adduser \
  --disabled-password \
  --ingroup rvm \
  --shell /bin/bash \
  --gecos 'Application' \
  --home /home/app_user \
  app_user
```

```bash
$ adduser app_user
$ adduser app_user rvm
```

Log with `app_user` user and execute this command:

```bash
$ ln -s /home/rvm/.rvm .rvm
```

Edit or create `/etc/gemrc` file:

```bash
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
gem: --no-rdoc --no-ri
```



### Configuration of Puma + Nginx

To start switch to your user app

```bash
$ su - app_user
```

Install `gem puma`

```bash
$ gem install puma
```

Launch puma

```bash
$ bundle exec puma -b unix://tmp/sockets/puma.app_name.sock -d
```

Create config file `/etc/nginx/sites-available/app_name`.

```nginx
upstream app_name {
  server unix:///home/app_user/tmp/sockets/puma.app_name.sock fail_timeout=0;
}

server {
  # listen 80 default deferred;
  server_name my_app.tld www.my_app.tld;
  root /home/app_user/public;

  try_files $uri/index.html $uri @app_name;

  location @app_name {
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_redirect off;

    proxy_pass http://app_name;
  }

  error_page 500 502 503 504 /500.html;

  client_max_body_size 4G;
  keepalive_timeout 10;
}
```
_Other [example](https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf)._

```bash
$ restart nginx

$ curl localhost
```

-------------------------------
sources:

- [http://www.modrails.com/documentation/Users%20guide%20Nginx.html#_installing_or_upgrading_on_red_hat_fedora_centos_or_scientificlinux](http://www.modrails.com/documentation/Users%20guide%20Nginx.html#_installing_or_upgrading_on_red_hat_fedora_centos_or_scientificlinux)
- [https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf](https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf)
- [http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/](http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/)
- [http://www.modrails.com/documentation/Users%20guide%20Nginx.html#rubygems_generic_install](http://www.modrails.com/documentation/Users%20guide%20Nginx.html#rubygems_generic_install)
- [https://gist.github.com/2499900](https://gist.github.com/2499900)
