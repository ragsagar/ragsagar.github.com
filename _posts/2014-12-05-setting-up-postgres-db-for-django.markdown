---
layout: post
title:  "Setting up postgres database for django development"
date:   2014-12-04 21:51:11
categories: django postgres
---

Install postgresql postgresql-client packages. Then start the
postgresql service.

{% highlight bash %}
# service start postgresql
{% endhighlight %}

Now run the psql shell as postgres user.

{% highlight bash %}
# su - postgres
postgres@localhost$ psql
{% endhighlight %}

Create an user that you want to use with django. Here I am going
to create database user `ragsagar` with password `s0mestr0ngPassw0rd`.
Permission to create database is also given to this user
by appending `CREATDB`. If this is not given django tests will fail when it
try to create test database while running tests.

{% highlight bash %}
postgres=# CREATE USER ragsagar WITH PASSWORD 's0mestr0ngPassw0rd' CREATEDB;
CREATE ROLE
{% endhighlight %}

Create a database with the created user as its owner. I am going to
create a database with name `djangodb` 

{% highlight bash %}
postgres=# CREATE DATABASE djangodb OWNER ragsagar;
CREATE DATABASE
{% endhighlight %}


By default postgres will only allow peer authentication for local
users. So we have to open the authentication configuration file
`/etc/postgresql/9.1/main/pg_hba.conf` and change the auth method
of local users from peer to md5.

Find the line which looks like following

{% highlight bash %}
local   all             all                                     peer
{% endhighlight %}

And change it to

{% highlight bash %}
local   all             all                                     md5
{% endhighlight %}

Restart the postgresql service and check if you are able to connect to
the database from the shell. It will ask for password and opens a psql
shell like shown below.

{% highlight bash %}
# service postgresql restart
$ psql -U ragsagar djangodb
Password for user ragsagar: 
psql (9.1.14)
Type "help" for help.

djangodb=> 
{% endhighlight %}

Open your django project settings.py file and add the
database name, user and password.

{% highlight python %}
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'djangodb',
        'USER': 'ragsagar',
        'PASSWORD': 's0mestr0ngPassw0rd',
    }
}
{% endhighlight %}

Make migrations and create tables with it.

{% highlight bash %}
$ python manage.py makemigrations
$ python manage.py migrate
{% endhighlight %}

Now go make awesome webapps with postgres datastore.

Happy Hacking :-)