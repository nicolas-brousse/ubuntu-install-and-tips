---
layout: page
title: Rails app with Puma
---


To start switch to your user app

```bash
$ su - app_user
```

## Configuration files

Create `Gemfile.local`

```ruby
source 'https://rubygems.org'

gem 'puma'
gem 'foreman'
# gem 'newrelic_rpm'
# gem 'rpm_contrib'
```

Install the dependencies

```bash
$ bundle install --without development test
```


Create `Procfile`

```
web: bundle exec puma --config config/puma.rb
```


Create `config/puma.rb` file

```ruby
#!/usr/bin/env puma

# app do |env|
#   puts env
#
#   body = 'Hello, World!'
#
#   [200, { 'Content-Type' => 'text/plain', 'Content-Length' => body.length.to_s }, [body]]
# end

environment 'production'
daemonize false

pidfile 'tmp/pids/puma.pid'
state_path 'tmp/pids/puma.state'

# stdout_redirect 'log/puma.log', 'log/puma_err.log'

# quiet
threads 0, 16
bind 'unix://tmp/sockets/puma.sock'

# ssl_bind '127.0.0.1', '9292', { key: path_to_key, cert: path_to_cert }

# on_restart do
#   puts 'On restart...'
# end

# restart_command '/u/app/lolcat/bin/restart_puma'


# === Cluster mode ===

# workers 2

# on_worker_boot do
#   puts 'On worker boot...'
# end

# === Puma control rack application ===

activate_control_app 'unix://tmp/sockets/pumactl.sock'
```

Create `config/nginx.conf` file and change that is necessary

```nginx
upstream rails_app {
  server unix:///home/rails/app_user/tmp/sockets/puma.sock fail_timeout=0;
}

server {
  # listen 80 deferred;
  server_name domain.tld www.domain.tld;
  root /home/rails/app_user/public;

  try_files $uri/index.html $uri @rails_app;

  location @rails_app {
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_redirect off;

    proxy_pass http://rails_app;
  }

  error_page 500 504 /500.html;
  error_page 502 /502.html;
  error_page 503 /503.html;

  client_max_body_size 4G;
  keepalive_timeout 10;
}
```


## Custom error pages

Create `public/502.html` with [this page]({{ site.baseurl }}/resources/errors/puma/502.html).
Create `public/503.html` with [this page]({{ site.baseurl }}/resources/errors/puma/503.html).


## Add the app into Nginx

```bash
$ cd /etc/nginx/sites-available/
$ ln -s /home/rails/app_user/config/nginx.conf domain.app
$ cd /etc/nginx/sites-enable/
$ ln -s ../sites-available/domain.app
```

## Foreman export

```bash
$ foreman export upstart /etc/init -a rails_app -u app_user -l /var/log/rails/rails_app
```

## Start the application

```bash
$ start rails_app
```

You can also `stop` or `restart` the app.
