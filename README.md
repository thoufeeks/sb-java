# sb-java
---------------
Spring Boot App from Scratch
------------------------------------
sudo apt update

sudo apt install openjdk-17-jdk maven -y

java -version
mvn -version

-----------------------------
Create Project Structure
------------------------------
mkdir spring-demo

cd spring-demo

mkdir -p src/main/java/com/demo
-----------------------------------
nano pom.xml

<project xmlns="http://maven.apache.org/POM/4.0.0">

    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.5.0</version>
    </parent>

    <groupId>com.demo</groupId>
    <artifactId>spring-demo</artifactId>
    <version>1.0</version>

    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
--------------------------------------------------------------------------

Create Java File
------------------------------
nano src/main/java/com/demo/Application.java

package com.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;

@SpringBootApplication
@RestController
public class Application {

    @GetMapping("/")
    public String home() {
        return "Hello from java Spring Boot!";
    }

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}


---------------------------------------------------------------
Build
----------
mvn clean package

run
------------
java -jar target/*.jar

curl localhost:8080


------------------------------------------
Next dockerization
----------------------------
nano Dockerfile

FROM eclipse-temurin:17-jre

COPY target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app.jar"]
-------------------

Build and run--------------------------------------------------------------
