# DGshell
Deploy goedge Prelude based on docker in debian10.

## Runbase
```
wget -N https://raw.githubusercontent.com/Toyoui/DGshell/main/Dgshell.sh && bash Dgshell.sh
```

## Edit my.cnf
```
cd /home/data/mysql/config vi my.cnf
```
### Fill in the following
```
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
secure-file-priv= NULL
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0

# Custom config should go here
!includedir /etc/mysql/conf.d/

default_authentication_plugin= mysql_native_password
```
