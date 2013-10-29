part 1 - deployment
===================

local
-----
ec2 (launch/start)/login clarabox-<postfix>
(to change the cluster config, check ~/development/scripts/ec2cmd.sh)

ec2
---
1. first launch
+ compile spark
cd ~/spark/project/SparkBuild.scala
val HBASE_VERSION = "0.94.12" (can be changed, always pick a stable version[version](http://mirrors.linsrv.net/apache/hbase/stable/))

cd ~/spark/
sbt/sbt assembly

**N.B.**
sbt assembly generates a new spark-assemly jar, make sure that there is only one valid spark-assembly jar in the directory: /root/spark/assembly/target/scala-2.9.3/ and then 

	cpydir /root/spark/assembly/target/scala-2.9.3

+ auto load .bashrc (this part can be merged into init.sh)
add 

if [ -f ~/.bashrc ]; then
   source ~/.bashrc
fi

to /root/.bash_profile

+ config cluster using toolbox
git clone https://claraviste@github.com/ClaraVista/toolbox.git
passwd = topcoder2013

cd ~/toolbox/scripts/
./init.sh (TODO: change init.sh which will download the lastest stable hbase version: see http://mirrors.linsrv.net/apache/hbase/stable/)

2. daily routine
+  enable hbase
rm -rf /tmp/hbase-root*
(can be merged into startcfg)

+  run startup script
startcfg
hbase hbck -repair
(can be merged into startcfg)





