# mysql-sqoop-hdfs

start mysql in docker :
`docker-compose up -d`

stop container :
`docker-compose stop`

---

Need to :
- start __hdfs__
- start __yarn__

---

sqoop dependencies (add to sqoop/lib) :
- mysql-connector-java
- common-lang-2.6

---

## mysql to hdfs

database : dbtest  
table : tabletest  
hdfs target directory : /sqoop_out  

To import data from __mysql__ to __hdfs__ using __sqoop__ :  
`sqoop import --connect jdbc:mysql://localhost:3306/dbtest --table tabletest --username root --password root --target-dir /sqoop_out -m 1`

Verify data :  
`hdfs dfs -cat /sqoop_out/part-m-00000`


## mysql to hive

lib :
- hive-common

__mysql__
```sql
create database dbhive;

create table dbhive.tablehive(name varchar(50), age int, city varchar(50));

INSERT INTO tablehive VALUES ('Alice','27','New York')
```
__hive__
```
create database db_hive;

use db_hive;

create table table_hive(name string, age int, city string);
```

To import data from __mysql__ to __hive__ using __sqoop__ :  
`sqoop import --connect jdbc:mysql://localhost:3306/dbhive --username root --password root --table tablehive --hive-import --hive-table db_hive.table_hive --m 1`

Verification :
```
select * from db_hive.table_hive;
```
