#ubuntu配置java环境变量
1.备份环境变量配置文件
```
sudo cp /etc/profile /etc/profile.bakup
```
2.编辑配置文件
```
sudo vi /etc/profile 
```
3.在配置文件末尾追加
```
#JDK PATH
export JAVA_HOME=/opt/jdk1.8.0_101
export JRE_HOME=/opt/jdk1. 8.0_101/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH
```
4.加载环境变量
```
source /etc/ profile
```