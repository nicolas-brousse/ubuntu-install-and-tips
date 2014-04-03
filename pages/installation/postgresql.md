---
layout: page
title: PostgreSQL
---

config pgsql

Create user admin with superadmin role

su - postgres
psql
CREATE USER "admin";
ALTER USER "admin" WITH SUPERUSER;
