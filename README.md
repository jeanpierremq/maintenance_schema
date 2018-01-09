# maintenance_schema

A DBA framework for postgres using views.

# INSTALL

Put both files in the extension folder.

Use `CREATE EXTENSION` in the wanted database(s).

## **WARNING**: log out and back in for the schema to be loaded in the current user path.

## **NOTE**: intended for postgres user or user with SUPER.

* `rpt_` views are meant as information 
* `audit_` views serve as warnings 
* `dba_` views contain DDL/DML statement (just \gexec it !)

## USAGE of full_report 
NOTE : use in shell to have a "nice" html report
`psql -d pgbench -c "select concat(sql_statement , ';') from maintenance_schema.full_report  " | psql -d pgbench -H  -o fullrpt.html`

or

~~~
postgres@pgbench=# \H
Output format is html.
postgres@pgbench=# \o fullrpt.html
postgres@pgbench=# select sql_statement from maintenance_schema.full_report \gexec
~~~

# **TODOs** :
- add `ALTER TABLE` statements for autovacuum and autoanalyze based on size
- add `ALTER TABLE... SET STATISTICS` if the need is confirmed, watch table/column special statistics in audit
- audit check : pg_hba.conf, listen_addresses, unix socket,...  security in general, (others?) -> On the way for version 0.0.2
- encoding : to perfect (add server side...)
- perfect row filtering on expect_av, foreign_fk (others?),
- add extensions pgstattuple, others ?
- Version compatibility handling for 9.3 and 9.4 (and 10 for replication)
- Handling of query type/lock type/state/wait event on long running queries dba view (restrictions needed)
- Need name of view for each table from full report

VERSION COMPATIBILITY
=====================

All views should be compatible from 9.5 and up.
Some views might be compatible starting with 9.4.


