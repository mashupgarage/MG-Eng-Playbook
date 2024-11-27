# Postgres Backup and Restore Steps

Creating backups and restoring db is always a part of the development process.
There are a lot of ways to backup data in Posgtres. Below are some of the few use cases that we encountered
in different projects that we had over the years.

## Anatomy of an AWS database connection string
```bash
postgres://postgres:2002A140316e@mashup-client-staging.c6tldzinifr8.us-east-1.rds.amazonaws.com:5432/staging_db
```
The above connection string can be dissected into parts that we could understand

```bash
postgres://<db-user-name>:<db-user-password>@<aws-rds-hostname>:<port>/<database-name>

db-user-name = postgres
db-user-password = 2002A140316e
aws-rds-hostname = mashup-client-staging.c6tldzinifr8.us-east-1.rds.amazonaws.com
port = 5432
database-name = staging_db
```


## Backing up data
One can pull db dumps at the comforts of their local machines; with the exception of you already have the
necessary credentials


### Basic
A very basic script that you can use is:
```bash
pg_dump -h <aws-rds-hostname> -U <db-user-name> -d <database-name> -f <dump-filename.sql>
```

But there are instances where you want to separate schema and data

### Schema only
For schema only kind of dump, one can use:
```bash
pg_dump <database-name> -h <aws-rds-hostname> -U <db-user-name> -f <dump-schema-filename.sql> -s -x
```

### Data only
For data only kind of dump, one can use:
```bash
pg_dump <database-name> -h <aws-rds-hostname> -U <db-user-name> -f <dump-schema-filename.sql> -a -x
```
For the data and schema only dumps, use case was for large database that has inconsistent data, its better
to restore the structure first then the data second as this ensures the integrity of the indexes first.


### Table exemption
For scenarios that you just want to dump all data except for some table.
For that we use the argument `-t` and the table name to be excepted from the dump
```
pg_dump -t 'some-table' <database-name> -h <aws-rds-hostname> -U <db-user-name> -f <dump-data-filename.sql> -a -x
```

### Restoring data
```bash
psql -h <aws-rds-hostname> -U <db-user-name> -d <database-name> < <dump-filename.sql>
```

## Inspecting database table sizes
Normally, before backing databases for staging restoration purposes, it is important to know how big the source data is
as per usual, staging databases are hosted in small sizes only

The SQL query below displays a tables in the database of choice along side its size in bytes
```sql
select
  table_schema,
  table_name,
  pg_relation_size('"'||table_schema||'"."'||table_name||'"')
from information_schema.tables
order by 3
```
