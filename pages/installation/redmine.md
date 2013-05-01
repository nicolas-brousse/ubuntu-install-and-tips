---
layout: page
title: Redmine
---

## Installation

Create a new user

```bash
$ adduser --disabled-password --ingroup rvm --shell /bin/bash --gecos 'Redmine' --home /home/redmine redmine
```


Install dependencies for postgresql and rmagick

```bash
$ apt-get install libpq-dev
$ apt-get install imagemagick libmagickcore-dev libmagickwand-dev
```


If you want you can compile named ruby version:

```bash
$ rvm install 2.0.0 -n "redmine"
```


Install correct rubygems version (<= 1.8 needed)

```bash
$ rvm install rubygems <version>
# OR
$ gem update --system 1.8.25
```


Create a new gemset

```bash
rvm use 2.0.0@redmine --ruby-version --create
```


Clone the sources

```bash
$ git clone https://github.com/redmine/redmine.git app/
```


Create `Gemfile.local` file with this content:

```bash
source 'https://rubygems.org'

gem 'puma'
```


Install the dependencies

```bash
$ bundle install --without development test
```


For the rest of the installation just follow the [official procedure](http://www.redmine.org/projects/redmine/wiki/RedmineInstall#Installation-procedure).



## Configuration

`config/puma.rb`

```bash
#!/usr/bin/env puma

environment 'production'
# daemonize false
pidfile 'tmp/pids/puma.pid'
state_path 'tmp/pids/puma.state'
stdout_redirect 'log/puma.log', 'log/puma_err.log'
bind 'unix://tmp/sockets/puma.sock'
workers 2
activate_control_app 'unix://tmp/sockets/pumactl.sock'
```
