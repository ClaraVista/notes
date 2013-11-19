Spark EC2 Deployment
===================

## Local
ec2 (launch/start)/login clarabox-<postfix>
(to change the cluster config, check ~/development/scripts/ec2cmd.sh)

need to know that: slaveNB * ebs-size > 3 * data-vol * 2

## EC2

### First launch

+ config cluster using toolbox	
```
git clone https://claravista@github.com/ClaraVista/toolbox.git
```
passwd = topcoder2013	
```
$ cd ~/toolbox/scripts/
$ ./init.sh 
$ cd
$ . .bashrc
```
(TODO: change init.sh which will download the lastest stable hbase version: see http://mirrors.linsrv.net/apache/hbase/stable/)


+ compile spark
```
vim ~/spark/project/SparkBuild.scala
val HBASE_VERSION = "0.94.12"
```
(can be changed, always pick a stable [version](http://mirrors.linsrv.net/apache/hbase/stable/))
```
cd ~/spark/
sbt/sbt assembly
```
** N.B. ***
sbt assembly generates a new spark-assemly jar, make sure that there is only one valid spark-assembly jar in the directory: /root/spark/assembly/target/scala-2.9.3/ and then
```
cpydir /root/spark/assembly/target/scala-2.9.3
```

+ auto load .bashrc (this part can be merged into init.sh)
add following code to /root/.bash_profile
```
vim /root/.bash_profile
```
```
if [ -f ~/.bashrc ]; then
      source ~/.bashrc
fi
```

+ move data via hdfs-over-ftp
```
$ cd
$ cd $FTP
./hdfs-over-ftp.sh_HDFS
```
Enable port 20-21 for the master's security group from AWS console<br>
Start FTPClaravista on ec2, associated an elastic IP<br>
On local pc, log on the FTPClaravista<br>
```
$ ec2ftp
```
On FTPClaravista
```
$ ftp <master of cluter>
```
login = pwd = root

### Daily startup cmd

+ enable hbase
```
$ startcfg
```
It will do all the necessary configueration

+ table-relocation
Enter a directory with meta-store in it
```
tblreloc
```

