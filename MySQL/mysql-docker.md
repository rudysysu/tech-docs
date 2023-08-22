
## my.cnf 
```
[root@control-plane confluence]# cat /data/mysql/conf/my.cnf 
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql

# confluence special setting begin
character-set-server=utf8mb4
collation-server=utf8mb4_bin
default-storage-engine=INNODB
max_allowed_packet=256M
innodb_log_file_size=2GB
#sql_mode = NO_AUTO_VALUE_ON_ZERO
transaction-isolation=READ-COMMITTED
binlog_format=row
# confluence special setting end
```

## docker run
```
docker run -d --name mysql -p 3306:3306 -v /data/mysql/conf:/etc/mysql/conf.d -v /data/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:5.7.43
docker exec -it mysql mysql -uroot -p
grant all on *.* to 'root'@'%' identified by 'root';
```
