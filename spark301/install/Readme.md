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
ExecStart=/opt/spark/sbin/start-all.sh
ExecStop=/opt/spark/sbin/stop-all.sh
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


