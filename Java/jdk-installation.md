```bash
tar zxvf jdk-8u121-linux-x64.tar.gz 
mv jdk1.8.0_121/ /opt/
ln -s /opt/jdk1.8.0_121/ /opt/java
vi /etc/profile
    export JAVA_HOME=/opt/java
    export PATH=$JAVA_HOME/bin:$PATH
source /etc/profile
```
