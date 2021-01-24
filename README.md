# SparkStandalone

<H1>System Overview</H1>

![Architecture Overview](https://github.com/ampx/SparkStandalone/blob/main/ArchOverview.PNG)
![Architecture Overview](https://github.com/ampx/SparkStandalone/blob/main/ArchOverview2.PNG)

* [download](https://drive.google.com/drive/folders/1HnkGb1gGYEP-X6EOwdHWeYhvxBD-yIUN?usp=sharing) prepared CentOS VM:

<H1>Included Tools</H1>

* [Spark 3.0.1 installation](https://github.com/ampx/SparkStandalone/tree/main/spark301/install)

* MongoDB 3.4.9 installation 

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

* MySql 8 installation 

```
yum install mysql
yum install  mysql-server*
systemctl start mysqld

sudo mysql_secure_installation
#root password was set to P3&!gH<m9I4Z
```

* Grafana 7.2.0 installation
```
wget https://dl.grafana.com/oss/release/grafana-7.2.0-1.x86_64.rpm
sudo yum install grafana-7.2.0-1.x86_64.rpm
```
