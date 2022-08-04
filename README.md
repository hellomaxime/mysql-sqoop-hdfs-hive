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
- my-sql-connector
- common-lang-2.6

---

database : dbtest  
table : tabletest  
hdfs target directory : /sqoop_out  

To import data from mysql to hdfs using sqoop :  
`sqoop import --connect jdbc:mysql://localhost:3306/dbtest --table tabletest --username root --password root --target-dir /sqoop_out -m 1`

Verify data :  
`hdfs dfs -cat /sqoop_out/part-m-00000`
