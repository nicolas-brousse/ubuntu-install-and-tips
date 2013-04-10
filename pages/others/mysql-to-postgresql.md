---
layout: page
title: Convert MySQL database to PostgreSQL
---



OR

```bash
# To install mysql2psql (under ubuntu 11.10): No need to get from github, just:
apt-get install ruby gems libmysqlclient-dev libpq-dev
gem install mysql pg mysql2psql
# To get info about the mysql socket:
netstat -l | grep mysql
mysql2psql # creates a .yml templae
vi mysql2psql.yml # edit the template
mysql2psql # connects to mysql database and write into postgres database
```

---------
Sources:

- http://wiki.postgresql.org/wiki/Converting_from_other_Databases_to_PostgreSQL#MySQL
- https://github.com/maxlapshin/mysql2postgres
