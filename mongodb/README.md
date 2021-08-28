### Installation notes MongoDB 3.4.9 for RHEL 8

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