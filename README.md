# MariaDB Galera Cluster - Trainining - Nördlingen

## Best Documentation for Galera Cluster 
https://galeracluster.com/documentation-webpages/

## Server System Variables 
https://mariadb.com/kb/en/server-system-variables/

## Show more than 10 lines of log in status systemctl 
systemctl status mariadb -l -n 50

## Galera status variables 
https://galeracluster.com/library/documentation/galera-status-variables.html#wsrep-apply-oooe

## Block firewall to simulate non-primary (drop out of cluster) 
```
for i in 3306 4567 4568 4444; do iptables -A INPUT -p tcp --destination-port $i -j DROP; iptables -A OUTPUT -p tcp --destination-port $i -j DROP; done
```

## Show row-based data in real from binlog
## if e.g. your executed an insert or update 
mysqlbinlog -vv noerd2-bin.000002

## pit - prep 
```
mysqldump --all-databases -uroot -p --master-data=2 --delete-master-logs > /usr/src/all.sql
mysqlbinlog noerd2-bin.000003 > /usr/src/recover.sql
# now recover
mysql -uroot -p < /usr/src/all.sql 
mysql -uroot -p < /usr/src/recover.sql 
```
## License MaxScale 

```
Version is going to be GPL on Change Data or after 4 years (whatever is earlier) 

https://mariadb.com/projects-using-bsl-11/

Change Date: 2020-01-01 (MaxScale 2.2), 2021-09-01 (MaxScale 2.4.2). For MaxScale 2.4.3 and above, change date is four years from release date.

Before that in BSL 1.1 and 1.0 (from MaxScale 2.0 on), may be used without License Coss
with LESS than 3 Servers 
```
