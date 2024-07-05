## Steps: 

- In order to deploy the application to other machine, we often need to compile it as a .jar (Java Archive).
- Default compilation in java only included the code you write in the .jar file, without the dependencies. 
- Maven has a plugin to allow us to package all our code + dependenices into one jar, simply called a fat jar.
- Demo: 
  - Package application as a fat jar
  - Run application from the fat jar.
  ```
  java -jar .\target\streams-starter-project-1.0-SNAPSHOT-jar-with-dependencies.jar
  ```

```xml
<!--package as one fat jar -->
<plugin>
    <groupid>org.apache.maven.plugins</groupid>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>3.6.0</version>
    <configuration>
        <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
        <archive>
            <manifest>
                <addClasspath>true</addClasspath>
                <mainClass>com.github.kesharir.kafka.streams.StreamsStarterApp</mainClass>
            </manifest>
        </archive>
    </configuration>
    <executions>
        <execution>
            <id>assemble-all</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>

```