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


Edit or create `/etc/gemrc` file:

```bash
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
gem: --no-rdoc --no-ri
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

Add the user to the `rvm` group

```bash
$ adduser app_user rvm
```

Now switch to the application user

```bash
$ su - app_user
```

Create a gemset if the application doesn't contain

```bash
$ rvm use 2.0.0@rails_app --ruby-version --create
```

Deploy the app and chose the web server you want

- [Rails app with Puma]({{ site.baseurl }}/pages/installation/rails-puma)
- [Rails app with Unicorn]({{ site.baseurl }}/pages/installation/rails-unicorn)

-------------------------------
sources:

- [http://www.modrails.com/documentation/Users%20guide%20Nginx.html#_installing_or_upgrading_on_red_hat_fedora_centos_or_scientificlinux](http://www.modrails.com/documentation/Users%20guide%20Nginx.html#_installing_or_upgrading_on_red_hat_fedora_centos_or_scientificlinux)
- [https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf](https://github.com/defunkt/unicorn/blob/master/examples/nginx.conf)
- [http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/](http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/)
- [http://www.modrails.com/documentation/Users%20guide%20Nginx.html#rubygems_generic_install](http://www.modrails.com/documentation/Users%20guide%20Nginx.html#rubygems_generic_install)
- [https://gist.github.com/2499900](https://gist.github.com/2499900)
