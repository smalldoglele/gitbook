关闭tomcat备份系统后，将jar包从jekens的指定目录中，复制到开发环境中
```shell
#!/bin/bash
export JAVA_HOME=/opt/jdk1.8.0_101
date=$(date +%Y%m%d%H%M)
tomcat=/opt/ylbs/mobile-api-server/app-server
jenkins=/opt/ylbs/warfromjenkins
bak=/opt/ylbs/warfromjenkins/bak/app
sh $tomcat/stop.sh
sleep 2
pid=`ps -ef |grep  $tomcat |grep -v grep  |awk '{print $2}'`
if [ -n "$pid" ]; then
        echo " 强制杀掉: $pid";
        kill -9 $pid ;
else
        echo “ 正常关闭~” 
fi
cd  $tomcat/webapps
echo "正在备份ROOT"  
tar -zcvf  ROOT_$date.tar.gz  ROOT/
rm -rf ROOT
mv   ROOT*.tar.gz   $bak
cp  $jenkins/mobile-app.war   $tomcat/webapps/
mv  mobile-app.war ROOT.war
rm -rf $tomcat/work/Catalina/
sleep 1
cd ../
./start.sh

```