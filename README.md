# SparkStandalone
* download prepared CentOS VM:

```
https://drive.google.com/drive/folders/1HnkGb1gGYEP-X6EOwdHWeYhvxBD-yIUN?usp=sharing
```

<H1>Included Tools</H1>
[Spark 3.0.1](https://github.com/ampx/SparkStandalone/tree/main/spark301/install)
* includes MongoDB 3.4.9

```
su
wget repo.mongodb.org/yum/redhat/8/mongodb-org/3.4/x86_64/RPMS/mongodb-org-mongos-3.4.24-1.el8.x86_64.rpm
wget repo.mongodb.org/yum/redhat/8/mongodb-org/3.4/x86_64/RPMS/mongodb-org-server-3.4.24-1.el8.x86_64.rpm
wget repo.mongodb.org/yum/redhat/8/mongodb-org/3.4/x86_64/RPMS/mongodb-org-shell-3.4.24-1.el8.x86_64.rpm
wget repo.mongodb.org/yum/redhat/8/mongodb-org/3.4/x86_64/RPMS/mongodb-org-tools-3.4.24-1.el8.x86_64.rpm

rpm -i ./mongodb-org-server-3.4.24-1.el8.x86_64.rpm
rpm -i ./mongodb-org-shell-3.4.24-1.el8.x86_64.rpm 
rpm -i ./mongodb-org-tools-3.4.24-1.el8.x86_64.rpm 
rpm -i ./mongodb-org-mongos-3.4.24-1.el8.x86_64.rpm

#to test run
mongo
#should connect to locally installed mongodb
```

* includes MySql 8

```
yum install mysql
yum install  mysql-server*
systemctl start mysqld

sudo mysql_secure_installation
#root password was set to P3&!gH<m9I4Z
```

* includes Grafana 7.2.0
```
wget https://dl.grafana.com/oss/release/grafana-7.2.0-1.x86_64.rpm
sudo yum install grafana-7.2.0-1.x86_64.rpm
```
