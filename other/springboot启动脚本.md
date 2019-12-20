####Spring Boot Shell 启动/停止/状态/ 脚本
```shell
#!/bin/bash
#----------------------------------
# Spring Boot 服务器操作脚本
#----------------------------------

# resolve links - $0 may be a softlink
PRG="$0"
while [ -h "$PRG" ]; do
  ls=`ls -ld "$PRG"`
  link=`expr "$ls" : '.*-> \(.*\)$'`
  if expr "$link" : '/.*' > /dev/null; then
    PRG="$link"
  else
    PRG=`dirname "$PRG"`/"$link"
  fi
done

PRGDIR=`dirname "$PRG"`
BASEDIR=`cd "$PRGDIR/.." >/dev/null; pwd`

#程序名称
APP_NAME=${artifactId}
#程序主jar名称
JAR_NAME=${artifactId}-${version}.${packaging}
# 日志文件目录
LOGS="$BASEDIR"/logs
#如果logs目录不存在，就创建一个
if [ ! -d ${LOGS} ]; then
      mkdir ${LOGS}
fi
# 临时目录
TEMP="$BASEDIR"/temp
#如果temp目录不存在，就创建一个
if [ ! -d ${TEMP} ]; then
      mkdir ${TEMP}
fi
# 控制台输出文件
CONSOLE_LOG="$LOGS/$APP_NAME".out
#库文件目录
REPO="$BASEDIR"/lib
#配置文件目录
CONF="$BASEDIR"/conf

# 虚拟机参数,设置虚拟机内存等一些配置.
# JAVA_OPTS="-Xms128m -Xmx256m -XX:MaxPermSize=64m \
#              -Djava.awt.headless=true \
#              -XX:+HeapDumpOnOutOfMemoryError \
#              -XX:+HeapDumpOnCtrlBreak \ "
JAVA_OPTS=
# spring boot 参数设置
BOOT_OPTS=""
#接受第二个参数
OPTION="$2"

# 启动服务(判断服务是否启动,只有没有启动的情况下,才启动.)
function start(){

  # 正在运行的服务数量
  runNum=`ps -ef|tr -s ' '|sort -n |grep app.name=$APP_NAME |grep -v "grep" | awk '{print $2}' |wc -l`

  # 当前运行的服务数为 0 ,启动服务.
  if [ $runNum -eq 0 ] ; then
    # 启动命令
    command="java $JAVA_OPTS -Dapp.name=$APP_NAME \
            -Dapp.home=$BASEDIR \
            -Dloader.path=$REPO,$CONF \
            -Djava.io.tmpdir=$TEMP \
            -jar  $BASEDIR/$JAR_NAME $BOOT_OPTS"

    # 将服务挂到后台启动,并将控制台日志重定向到 CONSOLE_LOG.
    nohup $command > $CONSOLE_LOG 2>&1 &

    # 打开控制台日志.
    if [ $? -eq 0 ] ; then
      echo "服务$APP_NAME 启动成功!! 服务进程PID=$! ."
      if [ -n "$OPTION" -a "$OPTION" = "-f" ];then
        echo "正在打开控制台日志..."
        tail -f $CONSOLE_LOG
      fi
    else
      echo "服务启动失败,1秒钟后将打开控制台日志."
      sleep 1
    fi

  # 当前可能存在正在运行的服务,或者脚本判断服务数量有错误.
  else
    echo "服务已经启动,启动服务个数为 ${runNum} 个, 请先停止服务 $APP_NAME."
  fi

}


# 停止服务
function stop(){
  # 正在运行的服务数量
  runNum=`ps -ef|tr -s ' '|sort -n |grep app.name=$APP_NAME|grep -v "grep" | awk '{print $2}' |wc -l`

  # 如果正在运行的服务数量为1, 则停止服务
  if [ $runNum -eq 1 ] ; then
    PID=`ps -ef|tr -s ' '|sort -n |grep app.name=$APP_NAME|grep -v "grep" | awk '{print $2}'`
    if [ $PID -gt 1 ] ; then
      echo "服务 $APP_NAME 的PID为 $PID. 2秒钟之后将停止该服务."
      sleep 2
      kill $PID
      sleep 3
      if [ $? -eq 0 ] ; then
        echo "停止服务 $APP_NAME 成功!!"
        #清除临时目录
        if [ -d ${TEMP} ]; then
            rm -rf ${TEMP}
        fi
        return 0
      else
        echo "停止服务发生异常,请手工停止并检查原因."
      fi
    else
      echo "获取PID失败,获取PID为 $PID .请手工停止服务 $APP_NAME."
    fi

  # 停止服务数量不对,需要人工干预
  else
    if [ $runNum -eq 0 ] ; then
      echo "当前正在运行服务数量 $runNum 个.无正在运行的服务."
      return 0
    else
      echo "当前正在运行服务数量 $runNum 个,请手动选择停止!!"
    fi
  fi

  return 1
}
# 重启
function restart(){
   stop
   if [ $? -eq 0 ] ; then
     echo "正在启动服务..."
     sleep 5
     start
   else
     echo "停止服务失败,请检查原因!!"
   fi
}
#服务状态
function status(){
  # 正在运行的服务数量
  runNum=`ps -ef|tr -s ' '|sort -n |grep app.name=$APP_NAME|grep -v "grep" | awk '{print $2}' |wc -l`
  if [ $runNum -eq 0 ] ; then
      echo "当前正在运行服务数量 $runNum 个.无正在运行的服务."
      return 0
  else
    echo "当前正在运行服务数量 $runNum 个.服务运行情况如下:"
    echo -e  `ps -aux |grep -v 'grep' |grep "app.name=$APP_NAME"`
  fi
}
# 其他情况
function others(){
  echo " Usage: start|stop|restart|status [option]"
  echo "        start -f follow with log will be hold screen"
}

case "$1" in
  start)
    start
  ;;
  stop)
    stop
  ;;
  restart)
    restart
  ;;
    status)
    status
  ;;
  *)
    others
  ;;
esac

```