##Maven工具介绍

+ maven打war包的时候排除包含jar

所有包都排除`%regex[WEB-INF/lib/*.*jar]`

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-war-plugin</artifactId>
    <configuration>
        <!--排除除了community-core开头的所有jar包-->
        <packagingExcludes>
            %regex[WEB-INF/lib/(?!community-core).*jar]
        </packagingExcludes>
    </configuration>
</plugin>
```
	
