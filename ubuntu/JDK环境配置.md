配置环境变量



#JDK PATH

export JAVA_HOME
=/
opt
/
jdk1
.
8.0
_101

export JRE_HOME
=/
opt
/
jdk1
.
8.0
_101
/
jre

export CLASSPATH
=.:
$JAVA_HOME
/
lib
:
$JRE_HOME
/
lib
:
$CLASSPATH

export PATH
=
$JAVA_HOME
/
bin
:
$JRE_HOME
/
bin
:
$PATH

加载环境变量



source 
/
etc
/
profile

