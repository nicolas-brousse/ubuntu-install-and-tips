---
layout: page
title: Convert MySQL database to PostgreSQL
---



OR

```bash
# To install mysql2psql (under ubuntu 11.10): No need to get from github, just:
$ gem install mysql pg mysql2psql
# To get info about the mysql socket:
$ netstat -l | grep mysql

# creates a .yml template
$ mysql2psql
# edit the template
$ vi mysql2psql.yml
# connects to mysql database and write into postgres database
$ mysql2psql
```

---------
Sources:

- http://wiki.postgresql.org/wiki/Converting_from_other_Databases_to_PostgreSQL#MySQL
- https://github.com/maxlapshin/mysql2postgres
