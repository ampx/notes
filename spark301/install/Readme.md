<H1>Installing Spark</H1>

```
su 
cd /opt
wget http://mirror.cc.columbia.edu/pub/software/apache/spark/spark-3.0.1/spark-3.0.1-bin-hadoop2.7.tgz
tar -xvzf ./spark-3.0.1-bin-hadoop2.7.tgz
ln -s spark-3.0.1-bin-hadoop2.7/ spark
```

<H5>configure paths for all the users</H5>
create file with following content /etc/profile.d/spark.sh

```
export JAVA_HOME=<path-of-Java-installation>
#example export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.252.b09-2.el8_1.x86_64/
export SPARK_HOME=/opt/spark/
export PATH=$PATH:$SPARK_HOME/bin
```

<H5>create spark service on master node</H5>
create file with following content /etc/systemd/system/spark_master.service

```
[Unit]
Description=Apache Spark Master and Slave Servers
After=network.target
After=systemd-user-sessions.service
After=network-online.target
 
[Service]
User=spark
Type=forking
ExecStart=/opt/spark/sbin/start-master.sh
ExecStop=/opt/spark/sbin/stop-master.sh
TimeoutSec=30
Restart= on-failure
RestartSec=30
StartLimitInterval=350
StartLimitBurst=10
 
[Install]
WantedBy=multi-user.target
```

<H5>create spark service on slave slave node</H5>
create file with following content /etc/systemd/system/spark_worker.service

```
[Unit]
Description=Apache Spark Slave Servers
After=network.target
After=systemd-user-sessions.service
After=network-online.target
 
[Service]
User=spark
Type=forking
ExecStart=/opt/spark/sbin/start-slave.sh
ExecStop=/opt/spark/sbin/stop-slave.sh
TimeoutSec=30
Restart= on-failure
RestartSec= 30
StartLimitInterval=350
StartLimitBurst=10
 
[Install]
WantedBy=multi-user.target
```

<H5>reload services</H5>
systemctl daemon-reload

<H5>add users</H5>

```
#add application  user
useradd -M spark
usermod -L spark
chown -R spark /opt/spark*
chgrp -R spark /opt/spark*

#add spark write user
useradd spark_writer

#add general excecution user
useradd spark_user
```

<H5>add data directories</H5>

```
su
mkdir /data/
mkdir /data/rawdata/
chown -R spark_user /data/archive/
chgrp -R spark_user /data/archive/

mkdir /data/archive/
chown -R spark_writer /data/archive/
chgrp -R spark_writer /data/archive/

mkdir /data/tmp/
chown -R spark_user /data/archive/
chgrp -R spark_user /data/archive/
```

<h5>Restrict file availability</H5>

* spark_users - group that has read access to archive data
* spark_writer - a sole user that can write archive data

<H5>HW restriction</H5>

<H5>Restrict Spark availability</H5>

* setup cluster secret key
