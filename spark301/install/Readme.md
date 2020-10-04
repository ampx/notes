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

