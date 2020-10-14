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

```
systemctl daemon-reload
```

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

#spark_writer should have privalages of spark_user
usermod -a -G spark_user spark_writer
```

<H5>add data directories</H5>

```
su
mkdir /data/
mkdir /data/rawdata/
chown -R spark_user /data/rawdata/
chgrp -R spark_user /data/rawdata/
chmod g+wx /data/rawdata/

mkdir /data/archive/
chown -R spark_writer /data/archive/
chgrp -R spark_writer /data/archive/

mkdir /data/tmp/
chown -R spark_user /data/tmp/
chgrp -R spark_user /data/tmp/
chmod g+wx /data/tmp/
```

<H5>HW restriction</H5>

* Restrict access to the VM to spark users only

<H5>Spark internal configurations</H5>

```
cp /opt/spark/conf/spark-defaults.conf.template /opt/spark/conf/spark-defaults.conf
vi /opt/spark/conf/spark-defaults.conf
```

* setup cluster secret key

```
spark.authenticate.secret someSecretKey
```
Note:this option will also needs to be set in application sparkcontext 

<H5>Spark environment variables configurations</H5>

```
cp /opt/spark/conf/spark-env.sh.template /opt/spark/conf/spark-env.sh
vi /opt/spark/conf/spark-env.sh
```

<H5>setup open ports</H5>

Port|Description
---|---
7077|Master
