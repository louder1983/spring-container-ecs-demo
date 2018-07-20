# Spring-boot-container-ECS-demo

## Requirements

1. Java - 1.8.x

2. Maven - 3.x.x

## Steps to Setup

**1. Clone the application**

```bash
git clone https://github.cicd.pearl.local/yzhu/Spring-boot-container-ECS-demo.git

```

**2. Build and run the app using maven**

```bash
cd Spring-boot-container-ECS-demo
mvn package
java -jar target/websocket-demo-0.0.1-SNAPSHOT.jar
```

Alternatively, you can run the app directly without packaging it like so -

```bash
mvn spring-boot:run
```

**3. Defining a docker image with Dockerfile**

```bash
cd spring-boot-websocket-chat-demo
touch Dockerfile
```

Following is the Dockerfile for our spring boot application -

```bash
# Start with a base image containing Java runtime
FROM openjdk:8-jdk-alpine

# Add a volume pointing to /tmp
VOLUME /tmp

# Make port 8080 available to the world outside this container
EXPOSE 8080

# The application's jar file
ARG JAR_FILE=target/websocket-demo-0.0.1-SNAPSHOT.jar

# Add the application's jar to the container
ADD ${JAR_FILE} websocket-demo.jar

# Run the jar file 
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/websocket-demo.jar"]
```

**4. Building the Docker image**

```bash
$ docker build -t spring-boot-container-ECS-demo .

$ docker image ls

$ docker run -p 80:8080 spring-boot-container-ECS-demo
```

Once the application is started, you should be able to access it at http://localhost

You can use the -d option in docker run command to run the container in the background -

```bash
$ docker run -d -p 80:8080 spring-boot-container-ECS-demo
```

You can see the list of all containers running in your system using the following command -

```bash
$ docker container ls
```

**Reference**

https://github.com/callicoder/spring-boot-websocket-chat-demo
https://www.callicoder.com/spring-boot-docker-example/