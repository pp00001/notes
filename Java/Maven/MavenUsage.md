# 创建项目

```shell
$ mvn archetype:generate
```

# 打包

```shell
$ mvn package
```

# 可执行jar

```xml
<build>
  <resources>
    <resource>
      <directory>
        ${project.basedir}/src/main/resources
      </directory>
      <filtering>true</filtering>
    </resource>
  </resources>

  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-assembly-plugin</artifactId>
      <executions>
        <execution>
          <goals>
            <goal>attached</goal>
          </goals>
          <phase>package</phase>
          <configuration>
            <descriptorRefs>
              <descriptorRef>jar-with-dependencies</descriptorRef>
            </descriptorRefs>
            <archive>
              <manifest>
                <mainClass>top.szhkai.mitest.TestZKFacade</mainClass>
              </manifest>
            </archive>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

# 搜索依赖包

```shell
 $ mvn dependency:tree | grep recommend-service-common
```

# 指定编译版本

```xml
</plugins>  
	  <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.5.1</version>
        <configuration>
            <source>1.8</source>
            <target>1.8</target>
        </configuration>
    </plugin>
	  ...
</plugins>
```

