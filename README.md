# Liquibase

[Fork freshbooks/liquibase-mysql](https://hub.docker.com/r/freshbooks/liquibase-mysql)

## Default Configuration

Runs liquibase with mysql connector

## Usage

### linking to a mysql container

If you are linking to a mysql container, `entrypoint.sh` will pick up on the
correct configuration via environment variables provided by the mysql container.
The only additional things needed are

* to mount the migrations
* to specify the database against which the migrations will be run

```
docker run -it \
  --link db:mysql \
  --rm \
  -v /local/path/migrations:/changelogs \
  -e TARGET_DATABASE=foo \
  goruha/liquibase-mysql
```


### Specifying configuration via environment variables

`entrypoint.sh` allows setting of the following to configure the liquibase run:

* `MYSQL_HOST`
* `MYSQL_PORT`
* `MYSQL_USER`
* `MYSQL_PASSWORD`
* `TARGET_DATABASE`


### Specifying your own commandline options

You may also invoke liquibase with whatever options or command you like.
`--driver=com.mysql.jbc.Driver` is already specified.

```
docker run -it \
  --rm \
  -v /local/path/migrations:/changelogs \
  goruha/liquibase_mysql \
   --changeLogFile=/changelogs/migrations.xml \
   --username=foo
   --password=bar
   --url="jbc:mysql://baz:3306/my_table
   update
```
