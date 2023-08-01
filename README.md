So here’s kind of my setup:

Run the maven quickstart command:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=demo-simple  -Dversion=1.0-SNAPSHOT -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Gives a project dir like 

```
demo-simple
├── pom.xml
└── src
    ├── main
    │   └── java
    │       └── com
    │           └── example
    │               └── App.java
    └── test
        └── java
            └── com
                └── example
                    └── AppTest.java

9 directories, 3 files
```

Then I add the following to the pom.xml

```xml
  <properties>
    <!-- build -->
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

    <!-- dependencies -->
    <ngrok.version>0.1.0</ngrok.version>
    <slf4j.version>2.0.6</slf4j.version>
    <jetty.version>11.0.14</jetty.version>
  </properties>
```
Then the deps

```xml
    <dependency>
      <groupId>com.ngrok</groupId>
      <artifactId>ngrok-java</artifactId>
      <version>${ngrok.version}</version>
    </dependency>
    <dependency>
      <groupId>com.ngrok</groupId>
      <artifactId>ngrok-java-native</artifactId>
      <version>${ngrok.version}</version>
      <classifier>${os.detected.classifier}</classifier>
      <scope>runtime</scope>
    </dependency>
```

With a build like such

```xml
  <build>
    <extensions>
      <extension>
        <groupId>kr.motd.maven</groupId>
        <artifactId>os-maven-plugin</artifactId>
        <version>1.7.0</version>
      </extension>
    </extensions>
    <plugins>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.1.0</version>
        <executions>
          <execution>
            <id>demo</id>
            <goals>
              <goal>java</goal>
            </goals>
            <configuration>
              <mainClass>com.example.App</mainClass>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
```

Then in `App.java` I copy the `demo-simple` ’s `SimpleEcho.java` and rename the `SimpleEcho` to `App`  and the package to package `com.example`