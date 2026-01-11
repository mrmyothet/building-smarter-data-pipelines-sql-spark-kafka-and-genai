# Data Engineering: Pipelines, ETL, Hadoop

### Reading

- [Data Engineer Skills: Roles and Resposibilities](https://www.simplilearn.com/data-engineer-role-article)
- [ETL and Data Warehousing Explained: ETL Tool Basics](https://www.integrate.io/blog/etl-data-warehousing-explained-etl-tool-basics/)
- [Streamlining Business Solutions: The Role of Data Analysis and Visual Tools](https://analystanswers.com/solution-design-template-steps-definition/)

### Setting Up Hadoop

1. Update the system 
```bash 
sudo apt update
```

2. Install Java 
```bash 
sudo apt install openjdk-8-jdk -y
sudo apt install openjdk-17-jdk -y
```

3. Install OpenSSH on Ubuntu 
```bash 
sudo apt install openssh-server openssh-client -y
```

4. Create a Hadoop User 
```bash 
sudo adduser hadoop
sudo adduser hadoop sudo
```

5. Switch to the created user
```bash 
sudo su - hadoop
```

6. Generate public and private key pairs
```bash 
ssh-keygen -t rsa
sudo cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
sudo chmod 640 ~/.ssh/authorized_keys
```
- verify the password-less SSH is functional
```bash 
ssh localhost
```

7. Download and Extract Hadoop
```bash 
wget https://downloads.apache.org/hadoop/common/hadoop-3.4.2/hadoop-3.4.2.tar.gz
```

```bash 
tar -xvzf hadoop-3.4.2.tar.gz
```

8. Configure Hadoop Environment Variables (bashrc)
```bash 
sudo nano ~/.bashrc
```

```bash 
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_INSTALL=$HADOOP_HOME 
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME 
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native 
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```

```bash 
source ~/.bashrc
```

9.  Move Hadoop folder to a more appropriate location `/usr/local/`
```bash 
mv hadoop-3.4.2 /usr/local/hadoop
```

```bash
# Edit the Hadoop environment file:
nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh
```

```bash
# find the line 
# export JAVA_HOME=
# change it to 
# export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

10. Format Hadoop FileSystem and start the HDFS
```bash 
hdfs namenode -format

start-dfs.sh
start-yarn.sh

# verify the hadoop is running:
jps
```

11. Access Hadoop UI from the browser
```bash 
http://localhost:9870
```

### Uploading data to HDFS
```bash 
hdfs dis -copyFromLocal <local-source> <hdfs-destination>
hdfs dfs -put <local-source> <hdfs-destination>
```

### Reading data from HDFS
```bash 
hdfs dfs -copyToLocal <hdfs-source> <local-destination>
hdfs dfs get <hdfs-source> <local-destination>
```

### Delete data from HDFS
```bash 
hdfs dfs -rm <hdfs-path>
```