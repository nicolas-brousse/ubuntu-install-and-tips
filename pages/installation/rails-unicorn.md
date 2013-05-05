---
layout: page
title: Rails app with Unicron
---


To start switch to your user app

```bash
$ su - app_user
```

## Configuration files

Create `Gemfile.local`

```ruby
source 'https://rubygems.org'

gem 'unicorn'
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
web: bundle exec
```


Create `config/nginx.conf` file and change that is necessary

```nginx
upstream rails_app {
  server unix:///home/rails/app_user/tmp/sockets/unicorn.sock fail_timeout=0;
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

Create `public/502.html` with [this page]({{ site.baseurl }}/resources/errors/unicorn/502.html).  
Create `public/503.html` with [this page]({{ site.baseurl }}/resources/errors/unicorn/503.html).


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
