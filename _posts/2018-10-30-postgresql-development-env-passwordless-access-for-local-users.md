---
ID: 531
post_title: >
  PostgreSQL. Development env.
  Passwordless access for local users
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/postgresql-development-env-passwordless-access-for-local-users/
published: true
post_date: 2018-10-30 11:27:08
---
Edit config file
<code>
 vim /etc/postgresql/10/main/pg_hba.conf
</code>
And specify <strong>trust</strong> as an auth method for local users
<code>
# Database administrative login by Unix domain socket
local   all             postgres                                trust

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust
</code>