+ 使用linux命令查找出lib文件夹重定向到analyzeJar.py

```shell
find /opt/ylbs -path *WEB-INF/lib |grep mobile-api | python3 analyzeJar.py 
```
+ analyzeJar.py源代码如下

```python
#################################################################
# 程序用来分析多个目录中文件(jar)差异
# 并用共有jar和独有jar的形式展示
# 输入参数要求是多行的目录，可以是重定向内容
# 使用实例：
# find /opt/ylbs -path *WEB-INF/lib | python3 analyzeJar.py 
#################################################################
import sys,os

def showList(list):
    for l in list:
        print(l)
HR="=+"*40
jarDirs=sys.stdin.readlines()
print("对下面的目录进行jar包分析:")
baseJar=[]
for d in jarDirs:
    if len(baseJar)!=0:
        baseJar=set(os.listdir(d.strip())) & baseJar
    else:
        baseJar=set(os.listdir(d.strip()))
    print(d.strip())
print(HR)
print("共有的jar有"+str(len(baseJar))+"个")
showList(baseJar)
print(HR)
for d in jarDirs:
    jars=set(os.listdir(d.strip()))-baseJar
    print(d.strip()+"独有的jar"+str(len(jars))+"个")
    showList(jars)

```