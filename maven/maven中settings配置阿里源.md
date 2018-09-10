* mirrors更换central

```xml
    <mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
```

* 配置公司自己的profile
  ```xml
    <profile>
        <id>unionx</id>
        <properties>
            <maven.compiler.source>1.7</maven.compiler.source>
            <maven.compiler.target>1.7</maven.compiler.target>
            <maven.compiler.compilerVersion>1.7</maven.compiler.compilerVersion>
        </properties>
        <repositories>
            <repository>
                <id>unionxMvnRepo</id>
                <name>unionx maven Repository</name>
                <url>http://maven.yilingboshi.com/repository/maven-public</url>
                <releases>
                    <enabled>true</enabled>
                </releases>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
        </repositories>
    </profile>
  ```
* 记录公司自己的profile
  ```xml
  <activeProfiles>
    <activeProfile>unionx</activeProfile>
  </activeProfiles>
  ```



